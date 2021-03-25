---
title: Selección de ensamblados a los que hacen referencia proyectos
description: Haga que un subconjunto de ensamblados del paquete esté disponible para el compilador, mientras todos los ensamblados están disponibles en tiempo de ejecución.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859036"
---
# <a name="select-assemblies-referenced-by-projects"></a>Selección de ensamblados a los que hacen referencia proyectos

Las referencias de ensamblado explícitas permiten usar un subconjunto de ensamblados para IntelliSense y la compilación, mientras todos los ensamblados están disponibles en tiempo de ejecución. `PackageReference` y `packages.config` funcionan de manera diferente y, por lo tanto, los autores de paquetes deben tener cuidado al crear el paquete para que sea compatible con ambos tipos de proyecto.

> [!Note]
> Las referencias de ensamblado explícitas están relacionadas con ensamblados .NET. No son un método para distribuir ensamblados nativos invocados por un ensamblado administrado mediante P/Invoke.

## <a name="packagereference-support"></a>Compatibilidad con `PackageReference`

Cuando un proyecto usa un paquete con `PackageReference` y dicho paquete contiene un directorio `ref\<tfm>\`, NuGet clasifica estos ensamblados como recursos en tiempo de compilación, mientras que los ensamblados `lib\<tfm>\` se clasifican como recursos en tiempo de ejecución. Los ensamblados de `ref\<tfm>\` no se usan en tiempo de ejecución. Esto significa que todos los ensamblados de `ref\<tfm>\` deben tener un ensamblado coincidente en el directorio `lib\<tfm>\` o en un directorio `runtime\` pertinente. En caso contrario, probablemente se producirán errores en tiempo de ejecución. Dado que los ensamblados de `ref\<tfm>\` no se usan en tiempo de ejecución, podrían ser [ensamblados de solo metadatos](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) para reducir el tamaño del paquete.

> [!Important]
> Si un paquete contiene el elemento `<references>` nuspec (usado por `packages.config`, como verá más abajo) y no incluye ensamblados en `ref\<tfm>\`, NuGet anunciará los ensamblados que aparecen en el elemento `<references>` nuspec como recursos en tiempo de compilación y ejecución. Esto significa que habrá excepciones en tiempo de ejecución cuando los ensamblados a los que se hace referencia necesiten cargar otro ensamblado en el directorio `lib\<tfm>\`.

> [!Note]
> Si el paquete contiene un directorio `runtime\`, NuGet podría no usar los recursos del directorio `lib\`.

## <a name="packagesconfig-support"></a>Compatibilidad con `packages.config`

Los proyectos que usan `packages.config` para administrar paquetes NuGet suelen agregar referencias a todos los ensamblados del directorio `lib\<tfm>\`. El directorio `ref\` se ha agregado para admitir `PackageReference`, por lo que no se tiene en cuenta al usar `packages.config`. Para establecer explícitamente a qué ensamblados se hace referencia para los proyectos que usan `packages.config`, el paquete debe emplear el elemento [`<references>` en el archivo nuspec](../reference/nuspec.md#explicit-assembly-references). Por ejemplo:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> El proyecto `packages.config` usa un proceso denominado [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) para copiar los ensamblados en el directorio de salida `bin\<configuration>\`. Se copia el ensamblado del proyecto y, luego, el sistema de compilación examina el manifiesto del ensamblado en busca de los ensamblados a los que se hace referencia. Después, copia esos ensamblados y repite el proceso de forma recursiva para todos los ensamblados. Esto significa que si alguno de los ensamblados del directorio `lib\<tfm>\` no se muestra en el manifiesto de otro ensamblado como una dependencia (si el ensamblado se carga en tiempo de ejecución mediante `Assembly.Load`, MEF u otro marco de inserción de dependencias), puede que no se copie en el directorio de salida `bin\<configuration>\` del proyecto, a pesar de estar en `bin\<tfm>\`.

## <a name="example"></a>Ejemplo

Mi paquete contendrá tres ensamblados (`MyLib.dll`, `MyHelpers.dll` y `MyUtilities.dll`), que están destinados a .NET Framework 4.7.2. `MyUtilities.dll` contiene clases diseñadas para que las usen únicamente los otros dos ensamblados, por lo que no quiero que esas clases estén disponibles en IntelliSense o en tiempo de compilación para los proyectos que usen mi paquete. Mi archivo `nuspec` debe contener los siguientes elementos XML:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

Los archivos del paquete serán los siguientes:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
