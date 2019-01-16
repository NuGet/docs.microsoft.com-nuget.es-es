---
title: Comando de CLI de NuGet pack
description: Referencia del comando pack de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d39ec8caf94caa767b6c502cc475e278aa718b95
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324791"
---
# <a name="pack-command-nuget-cli"></a>Comando pack (CLI de NuGet)

**Se aplica a:** la creación del paquete &bullet; **versiones compatibles:** 2.7+

Crea un paquete de NuGet según lo especificado `.nuspec` o archivo de proyecto. El `dotnet pack` comando (vea [comandos dotnet](dotnet-Commands.md)) y `msbuild -t:pack` (consulte [destinos de MSBuild](../reference/msbuild-targets.md)) que puede utilizarse como alternativas.

> [!Important]
> En Mono, no se admite la creación de un paquete desde un archivo de proyecto. También deberá ajustar las rutas de acceso no local en el `.nuspec` de archivos para las rutas de acceso de estilo Unix, como nuget.exe no convierte las rutas de acceso de Windows sí.

## <a name="usage"></a>Uso

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

donde `<nuspecPath>` y `<projectPath>` especificar el `.nuspec` o archivo de proyecto, respectivamente.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| BasePath | Establece la ruta de acceso base de los archivos definidos en el `.nuspec` archivo. |
| Compilar | Especifica que el proyecto debe compilarse antes de crear el paquete. |
| Excluir | Especifica uno o varios patrones de caracteres comodín para excluir al crear un paquete. Para especificar más de un patrón, repita el - marcador de exclusión. Vea el ejemplo siguiente. |
| ExcludeEmptyDirectories | Impide la inclusión de directorios vacíos al crear el paquete. |
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| ConfigFile | Especifique el archivo de configuración para el comando pack. |
| Ayuda | Muestra información de ayuda para el comando. |
| IncludeReferencedProjects | Indica que el paquete generado debe incluir los proyectos que se hace referencia como dependencias o como parte del paquete. Si un proyecto que se hace referencia tiene un correspondiente `.nuspec` archivo que tiene el mismo nombre que el proyecto y, a continuación, ese proyecto se agrega como una dependencia. En caso contrario, se agrega el proyecto que se hace referencia como parte del paquete. |
| MinClientVersion | Establecer el *minClientVersion* atributo para el paquete creado. Este valor reemplazará el valor de la existente *minClientVersion* atributo (si existe) en el `.nuspec` archivo. |
| MSBuildPath | *(4.0 y versiones posteriores)*  Especifica la ruta de acceso de MSBuild que use con el comando, tiene prioridad sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 y versiones posteriores)*  Especifica la versión de MSBuild que se usará con este comando. Los valores admitidos son 4, 12, 14, 15. De forma predeterminada que se selecciona la versión de MSBuild en su ruta de acceso, en caso contrario, el valor predeterminado es la última versión instalada de MSBuild. |
| NoDefaultExcludes | Evita la exclusión predeterminada de NuGet empaquetar archivos y archivos y carpetas de inicio con un punto, como `.svn` y `.gitignore`. |
| NoPackageAnalysis | Especifica que el paquete no debe ejecutar el análisis de paquetes después de crear el paquete. |
| OutputDirectory | Especifica la carpeta donde se almacena el paquete creado. Si se especifica ninguna carpeta, se usa la carpeta actual. |
| Propiedades | Debe aparecer al final de la línea de comandos después de otras opciones. Especifica una lista de las propiedades que reemplazan los valores en el archivo de proyecto. consulte [propiedades comunes de proyectos de MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) nombres de propiedad. Aquí el argumento de propiedades es una lista de pares de nombre-valor, separados por punto y coma, donde cada aparición de `$token$` en el `.nuspec` archivo se sustituirá con el valor especificado. Los valores pueden ser cadenas entre comillas. Tenga en cuenta que para la propiedad "Configuration", el valor predeterminado es "Debug". Para cambiar a una configuración de lanzamiento, utilice `-Properties Configuration=Release`. |
| Sufijo | *(3.4.4+)*  Anexa un sufijo para el número de versión generada internamente, se utiliza normalmente para anexar las compilación u otros identificadores de versión preliminar. Por ejemplo, mediante `-suffix nightly` creará un paquete con un tipo de número de versión `1.2.3-nightly`. Sufijos deben empezar por una letra para evitar las advertencias, errores y las posibles incompatibilidades con distintas versiones de NuGet y el Administrador de paquetes de NuGet. |
| Símbolos | Especifica que el paquete contiene orígenes y símbolos. Cuando se usa con un `.nuspec` archivo, esto crea un archivo de paquete NuGet normal y el correspondiente paquete de símbolos. De forma predeterminada crea un [paquete de símbolos heredado](../create-packages/Symbol-Packages.md). El nuevo formato recomendado para paquetes de símbolos es .snupkg. Vea [Crear paquetes de símbolos (.snupkg)](../create-packages/Symbol-Packages-snupkg.md). |
| Herramienta | Especifica que se deben colocar los archivos de salida del proyecto en el `tool` carpeta. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |
| Versión | Invalida el número de versión desde el `.nuspec` archivo. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Exclusión de dependencias de desarrollo

Algunos paquetes de NuGet son útiles como las dependencias de desarrollo, que le ayudarán a crear su propia biblioteca, pero no son necesariamente necesarios como dependencias de paquete real.

El `pack` pasará por alto el comando `package` las entradas de `packages.config` que tienen el `developmentDependency` atributo establecido en `true`. Estas entradas no se incluirá como una dependencias en el paquete creado.

Por ejemplo, considere la siguiente `packages.config` archivo en el proyecto de origen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Para este proyecto, el paquete creado por `nuget pack` tiene una dependencia de `jQuery` y `microsoft-web-helpers` pero no `netfx-Guard`.

## <a name="examples"></a>Ejemplos

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
