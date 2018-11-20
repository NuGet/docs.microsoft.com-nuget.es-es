---
title: Cómo publicar paquetes de símbolos de NuGet con el nuevo formato de paquete de símbolos ".snupkg" | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Cómo crear paquetes de símbolos de NuGet (snupkg).
keywords: Paquetes de símbolos de NuGet, depuración de paquetes de NuGet, compatibilidad con la depuración de NuGet, símbolos de paquetes, convenciones de paquetes de símbolos
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: a72b59a391ed25e9617ba3ba3656301a2ed90ddc
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580438"
---
# <a name="creating-symbol-packages-snupkg"></a>Crear paquetes de símbolos (.snupkg)

## <a name="prerequisites"></a>Requisitos previos

[nuget.exe v4.9.0 o una versión superior](https://www.nuget.org/downloads) o [dotnet.exe v2.2.0 o una versión superior](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementan los [protocolos de NuGet](../api/nuget-protocols.md) requeridos.

## <a name="creating-a-symbol-package"></a>Crear un paquete de símbolos

Un paquete de símbolos de snupkg se puede crear desde un archivo .nuspec o desde un archivo .csproj. Se admiten tanto NuGet.exe como dotnet.exe. Cuando se usen las opciones ```-Symbols -SymbolPackageFormat snupkg``` en el comando de paquete de nuget.exe, se creará un archivo .snupkg además del archivo .nupkg.

Comandos de ejemplo para crear archivos .snupkg
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild /t:pack MyPackage.csproj /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
```

Los archivos `.snupkgs` no se producen de forma predeterminada. Debe pasar la propiedad `SymbolsPackageFormat` junto con `-Symbols` en el caso de nuget.exe, `--include-symbols` en el caso de dotnet.exe o `/p:IncludeSymbols` en el caso de msbuild.

La propiedad SymbolsPackageFormat puede tener uno de estos dos valores: `symbols.nupkg` (predeterminado) o `snupkg`. Si no se especifica SymbolsPackageFormat, el valor predeterminado es `symbols.nupkg` y se creará un paquete de símbolos heredado.

> [!Note]
> El formato heredado `.symbols.nupkg` todavía se admite, pero solo por motivos de compatibilidad (vea [Paquetes de símbolos heredados](Symbol-Packages.md)). El servidor de símbolos de NuGet.org solo acepta el nuevo formato de paquete de símbolos, `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publicar un paquete de símbolos

1. Para su comodidad, guarde primero la clave de API con NuGet (vea [publicar un paquete](../create-packages/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Después de publicar el paquete principal en nuget.org, inserte el paquete de símbolos tal y como se describe a continuación.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. También puede insertar ambos paquetes al mismo tiempo con el comando siguiente. Tanto los archivos .nupkg como .snupkg deben estar presentes en la carpeta actual.

    ```cli
    nuget push MyPackage.nupkg
    ```

En este caso, NuGet publicará en nuget.org primero `MyPackage.nupkg` y, después, `MyPackage.snupkg`.

## <a name="nugetorg-symbol-server"></a>Servidor de símbolos de NuGet.org

NuGet.org admite su propio repositorio de servidor de símbolos y solo acepta el nuevo formato de paquete de símbolos, `.snupkg`. Los consumidores de paquetes pueden usar los símbolos publicados en el servidor de símbolos de nuget.org agregando `https://symbols.nuget.org/download/symbols` a sus orígenes de símbolos en Visual Studio, que permite entrar en el código del paquete en el depurador de Visual Studio. Vea [Especificar archivos de código fuente y símbolos (.pdb) en el depurador de Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) para obtener información detallada sobre ese proceso.

### <a name="nugetorg-symbol-package-constraints"></a>Restricciones de paquete de símbolos de Nuget.org

Los paquetes de símbolos admitidos en nuget.org tienen las siguientes restricciones:

- Solo se permite agregar las siguientes extensiones a un paquete de símbolos. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- En estos momentos, solo se admiten archivos [pdb portátiles](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) en el servidor de símbolos de nuget.
- Los archivos pdb y los dll de nupkg asociados deben compilarse con el compilador de la versión 15.9 de Visual Studio o una superior (vea [hash criptográfico de pdb](https://github.com/dotnet/roslyn/issues/24429)).

La publicación del paquete de símbolos en nuget.org producirá un error si cualquiera de los otros tipos de archivo se incluyen en el archivo .snupkg.

### <a name="symbol-package-validation-and-indexing"></a>Validación e indexación de paquetes de símbolos

Los paquetes de símbolos publicados en [NuGet.org](https://www.nuget.org/) se someten a varias validaciones, como comprobaciones de virus.

Cuando el paquete haya pasado todas las comprobaciones de validación, tardará un tiempo para que los símbolos se indexen y estén disponibles para su consumo desde los servidores de símbolos de NuGet.org. Si se produce un error de comprobación de validación en el paquete, la página de detalles del archivo .nupkg se actualizará y mostrará el error correspondiente. También recibirá un correo electrónico en el que se le notificará este extremo.

La validación y la indexación del paquete suelen tardar menos de 15 minutos. Si la publicación del paquete tarda más de lo esperado, visite [status.nuget.org](https://status.nuget.org/) para comprobar si nuget.org está experimentando alguna interrupción. Si todos los sistemas están operativos y el paquete no se ha publicado correctamente en una hora, inicie sesión en nuget.org y póngase en contacto con nosotros mediante el vínculo de contacto con el equipo de soporte técnico de la página de detalles del paquete.

## <a name="symbol-package-structure"></a>Estructura del paquete de símbolos

El archivo .nupkg debería ser exactamente el mismo que el de hoy, pero el archivo .snupkg debería tener las siguientes características:

1) El archivo .snupkg debe tener el mismo id. y la misma versión que el archivo .nupkg correspondiente.
2) El archivo .snupkg debe tener la misma estructura de carpetas exacta que el archivo .nupkg para cualquier archivo DLL o EXE con distinción de que, en vez de los archivos DLL o EXE, los archivos PDB correspondientes deben estar incluidos en la misma jerarquía de carpetas. El archivo .snupkg no debe incluir ningún archivos o carpetas con extensiones que no sean PDB.
3) El archivo .nuspec del archivo .snupkg también debe especificar un nuevo PackageType, tal y como se muestra a continuación. Este debería ser el único PackageType especificado. 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) Si un autor decide usar un archivo .nuspec personalizado para compilar sus archivos .nupkg y .snupkg, estos deben tener la misma jerarquía de carpetas y archivos mostrados en el punto 2.
5) Los campos ```authors``` y ```owners``` deben excluirse del archivo .nuspec del archivo .snupkg.

## <a name="see-also"></a>Vea también

[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
