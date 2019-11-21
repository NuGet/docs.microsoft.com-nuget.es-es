---
title: Cómo crear paquetes de símbolos de NuGet
description: Cómo crear paquetes de NuGet que solo contienen símbolos para admitir la depuración de otros paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 97a533171d698792d66a78550dacfe8eaf29a440
ms.sourcegitcommit: fc0f8c950829ee5c96e3f3f32184bc727714cfdb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2019
ms.locfileid: "74253916"
---
# <a name="creating-symbol-packages-legacy"></a>Crear paquetes de símbolos (heredado)

> [!Important]
> El nuevo formato recomendado para paquetes de símbolos es .snupkg. Vea [Crear paquetes de símbolos (.snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg todavía se admite, pero solo por motivos de compatibilidad.

Además de crear paquetes para nuget.org u otros orígenes, NuGet también admite la creación de paquetes de símbolos asociados y su publicación en el repositorio SymbolSource.

Los consumidores de paquetes pueden agregar `https://nuget.smbsrc.net` a sus orígenes de símbolos en Visual Studio, que permite entrar en el código del paquete en el depurador de Visual Studio. Vea [Especificar archivos de código fuente y símbolos (.pdb) en el depurador de Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obtener información detallada sobre ese proceso.

## <a name="creating-a-symbol-package"></a>Crear un paquete de símbolos

Para crear un paquete de símbolos, siga estas convenciones:

- Asigne al paquete principal (con el código) el nombre `{identifier}.nupkg` e incluya todos los archivos excepto los archivos `.pdb`.
- Asigne al paquete de símbolos el nombre `{identifier}.symbols.nupkg` e incluya los archivos DLL de ensamblado, los archivos `.pdb`, los archivos XMLDOC y los archivos de origen (vea las secciones siguientes).

Puede crear ambos paquetes con la opción `-Symbols`, ya sea desde un archivo `.nuspec` o desde un archivo de proyecto:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Tenga en cuenta que `pack` requiere Mono 4.4.2 en Mac OS X y no funciona en los sistemas Linux. En los equipos Mac, también debe convertir los nombres de las rutas de acceso de Windows del archivo `.nuspec` a las rutas de acceso de estilo Unix.

## <a name="symbol-package-structure"></a>Estructura del paquete de símbolos

Un paquete de símbolos puede tener como destino varias plataformas de destino de la misma manera que un paquete de bibliotecas, por lo que la estructura de la carpeta `lib` debe ser exactamente igual que el paquete principal, incluyendo solo los archivos `.pdb` junto con los archivos DLL.

Por ejemplo, un paquete de símbolos que tenga como destino .NET 4.0 y Silverlight 4 tendría este diseño:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Los archivos de código fuente se colocan en una carpeta especial independiente denominada `src`, que debe seguir la estructura relativa del repositorio de origen. Esto es así porque los archivos PDB contienen rutas de acceso absolutas a los archivos de código fuente que se usan para compilar los archivos DLL correspondientes y se deben buscar durante el proceso de publicación. Se puede quitar una ruta de acceso base (prefijo de ruta de acceso común). Por ejemplo, imagínese que tiene una biblioteca creada a partir de estos archivos:

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

Aparte de la carpeta `lib`, un paquete de símbolos tendría que tener este diseño:

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a>Hacer referencia a los archivos en el archivo nuspec

Se puede crear un paquete de símbolos mediante convenciones a partir de una estructura de carpetas, tal y como se describe en la sección anterior, o especificando su contenido en la sección `files` del manifiesto. Por ejemplo, para crear el paquete que se muestra en la sección anterior, use lo siguiente en el archivo `.nuspec`:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Publicar un paquete de símbolos

> [!Important]
> Para insertar paquetes en nuget.org debe usar [la versión 4.9.1 o una versión posterior de nuget.exe](https://www.nuget.org/downloads), que implementa los [protocolos de NuGet](../api/nuget-protocols.md) necesarios.

1. Para mayor comodidad, guarde primero la clave de API con NuGet (vea [Publish a package](../nuget-org/publish-a-package.md) [Publicar un paquete]), que se aplicará a nuget.org y a symbolsource.org, porque symbolsource.org comprobará con nuget.org que usted es el propietario del paquete.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Una vez publicado el paquete principal en nuget.org, inserte el paquete de símbolos del siguiente modo. El paquete usará automáticamente symbolsource.org como destino debido a la aparición de `.symbols` en el nombre de archivo:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Para publicar el paquete en otro repositorio de símbolos, o para insertar un paquete de símbolos que no sigue la convención de nomenclatura, use la opción `-Source`:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. También puede insertar el paquete principal y el paquete de símbolos en ambos repositorios a la vez usando lo siguiente:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Con la versión 4.5.0 o una versión posterior de nuget.exe, los paquetes de símbolos no se insertan automáticamente en symbolsource.org. Tendría que insertar los paquetes de símbolos por separado, tal como se describe en los pasos anteriores.
   
En este caso, NuGet publicará `MyPackage.symbols.nupkg`, si existe, en https://nuget.smbsrc.net/ (la dirección URL de inserción para symbolsource.org) después de que haya publicado el paquete principal en nuget.org.

## <a name="see-also"></a>Vea también

[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (Cambio al nuevo motor SymbolSource) (symbolsource.org)
