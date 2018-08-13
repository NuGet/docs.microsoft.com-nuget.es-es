---
title: Formato PackageReference de NuGet (referencias de paquete en archivos de proyecto)
description: Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0 y versiones posteriores, VS2017 y .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 48930701f1bb5f13718505b85b293f38d37d19fb
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508353"
---
# <a name="package-references-packagereference-in-project-files"></a>Referencias del paquete (PackageReference) en archivos de proyecto

Las referencias de paquetes, con el nodo `PackageReference`, administran las dependencias de NuGet directamente en los archivos de proyecto (a diferencia de un archivo `packages.config` independiente). El uso de PackageReference, como así se llama, no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.Config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en [Configuración del comportamiento de NuGet](configuring-nuget-behavior.md).

Con PackageReference, también puede usar las condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras agrupaciones. También le proporciona un control específico sobre las dependencias y el flujo de contenido. (Para saber más, vea [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) (Empaquetado y restauración de NuGet como destinos de MSBuild).

De forma predeterminada, PackageReference se usa para proyectos de .NET Core, proyectos de .NET Standard y proyectos de UWP que tengan como destino Windows 10 Build 15063 (Creators Update) y versiones posteriores, con la excepción de los proyectos de UWP en C++. Los proyectos completos de .NET Framework admiten PackageReference, pero actualmente tienen como valor predeterminado `packages.config`. Para usar PackageReference, migre las dependencias de `packages.config` al archivo de proyecto y luego quite packages.config.

## <a name="adding-a-packagereference"></a>Agregar una PackageReference

Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Controlar la versión de una dependencia

La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Uso de una PackageReference para un proyecto sin PackageReferences
Avanzado: Si no tiene paquetes instalados en un proyecto (ninguna PackageReference en el archivo de proyecto y ningún archivo packages.config), pero quiere que el proyecto se restaure como de estilo PackageReference, puede establecer una propiedad de proyecto RestoreProjectStyle en PackageReference en el archivo de proyecto.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
Esto puede resultar útil si hace referencia a proyectos de estilo PackageReference (csproj existente o proyectos de estilo SDK). Esto permitirá que el proyecto haga referencia "de manera transitiva" a los paquetes a los que hacen referencia dichos proyectos.

## <a name="floating-versions"></a>Versiones flotantes

Las [versiones flotantes](../consume-packages/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Controlar los recursos de dependencias

Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete. En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Las siguientes etiquetas de metadatos controlan los recursos de dependencia:

| Etiqueta | Descripción | Valor predeterminado |
| --- | --- | --- |
| IncludeAssets | Se consumirán estos recursos | todo |
| ExcludeAssets | No se consumirán estos recursos | ninguna |
| PrivateAssets | Estos recursos se consumirán, pero no irán al proyecto principal | archivos de contenido; analizadores; compilación |

A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:

| Valor | Descripción |
| --- | ---
| compile | Contenido de la carpeta `lib` y controla si el proyecto se puede compilar con los ensamblados dentro de la carpeta |
| motor en tiempo de ejecución | Contenido de las carpetas `lib` y `runtimes` y controla si estos ensamblados se copiarán en el directorio de salida de compilación |
| contentFiles | Contenido de la carpeta `contentfiles` |
| compilación | Propiedades y destinos de la carpeta `build` |
| analyzers | Analizadores de .NET |
| nativas | Contenido de la carpeta `native` |
| ninguna | No se usa ninguno de los anteriores. |
| todo | Todo lo anterior (excepto `none`) |

En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal. Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger. AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.

## <a name="adding-a-packagereference-condition"></a>Agregar una condición PackageReference

Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades. Pero actualmente solo se admite la variable `TargetFramework`.

Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`. En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria. Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Un paquete creado con este proyecto mostrará que Newtonsoft.Json se incluye como dependencia únicamente para un destino `net452`:

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
