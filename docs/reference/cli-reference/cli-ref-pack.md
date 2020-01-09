---
title: Comando del paquete de la CLI de NuGet
description: Referencia del comando del paquete Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 00e2ee760698afd8591909570d76e4bfe475a682
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384000"
---
# <a name="pack-command-nuget-cli"></a>Comando pack (CLI de NuGet)

**Se aplica a: creación de** paquetes &bullet; **versiones compatibles:** 2.7 +

Crea un paquete de NuGet basado en el archivo [. nuspec](../nuspec.md) o el archivo de proyecto especificado. El comando `dotnet pack` (consulte los [comandos dotnet](../dotnet-Commands.md)) y `msbuild -t:pack` (consulte [destinos de MSBuild](../msbuild-targets.md)) se pueden usar como alternativas.

> [!Important]
> Use [`dotnet pack`](../dotnet-Commands.md) o [`msbuild -t:pack`](../msbuild-targets.md) para proyectos basados en [PackageReference](../../consume-packages/package-references-in-project-files.md) .
> En mono, no se admite la creación de un paquete a partir de un archivo de proyecto. También debe ajustar las rutas de acceso no locales en el archivo `.nuspec` a las rutas de acceso de estilo Unix, ya que Nuget. exe no convierte los nombres de usuario de Windows.

## <a name="usage"></a>Usage

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

donde `<nuspecPath>` y `<projectPath>` especifican el `.nuspec` o el archivo de proyecto, respectivamente.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| BasePath | Establece la ruta de acceso base de los archivos definidos en el archivo [. nuspec](../nuspec.md) . |
| Compilar | Especifica que el proyecto debe compilarse antes de compilar el paquete. |
| Excluir | Especifica uno o más patrones de caracteres comodín que se deben excluir al crear un paquete. Para especificar más de un patrón, repita la marca-exclude. Consulte el ejemplo que aparece a continuación. |
| ExcludeEmptyDirectories | Impide la inclusión de directorios vacíos al compilar el paquete. |
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| ConfigFile | Especifique el archivo de configuración para el comando Pack. |
| Ayuda de | Muestra información de ayuda para el comando. |
| IncludeReferencedProjects | Indica que el paquete compilado debe incluir los proyectos a los que se hace referencia como dependencias o como parte del paquete. Si un proyecto al que se hace referencia tiene un archivo de `.nuspec` correspondiente con el mismo nombre que el proyecto, el proyecto al que se hace referencia se agrega como una dependencia. De lo contrario, el proyecto al que se hace referencia se agrega como parte del paquete. |
| MinClientVersion | Establezca el atributo *minClientVersion* para el paquete creado. Este valor invalidará el valor del atributo *minClientVersion* existente (si existe) en el archivo de `.nuspec`. |
| MSBuildPath | *(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el comando, que tiene prioridad sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando. Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild. |
| NoDefaultExcludes | Evita la exclusión predeterminada de archivos y archivos de paquetes de NuGet que comienzan con un punto, como `.svn` y `.gitignore`. |
| NoPackageAnalysis | Especifica que el paquete no debe ejecutar el análisis de paquetes después de crear el paquete. |
| OutputDirectory | Especifica la carpeta en la que se almacena el paquete creado. Si no se especifica ninguna carpeta, se usa la carpeta actual. |
| Propiedades | Debe aparecer en último lugar en la línea de comandos después de otras opciones. Especifica una lista de propiedades que invalidan los valores del archivo de proyecto. vea [propiedades comunes del proyecto de MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nombres de propiedad. El argumento Properties aquí es una lista de pares token = valor, separados por punto y coma, donde cada aparición de `$token$` en el archivo `.nuspec` se reemplazará por el valor especificado. Los valores pueden ser cadenas entre comillas. Tenga en cuenta que para la propiedad "Configuration", el valor predeterminado es "debug". Para cambiar a una configuración de versión, use `-Properties Configuration=Release`. |
| Sufijo | *(3.4.4 +)* Anexa un sufijo al número de versión generado internamente, que se usa normalmente para anexar los identificadores de compilación u otros identificadores de versión preliminar. Por ejemplo, el uso de `-suffix nightly` creará un paquete con un número de versión como `1.2.3-nightly`. Los sufijos deben comenzar con una letra para evitar las advertencias, los errores y las posibles incompatibilidades con las distintas versiones de NuGet y el administrador de paquetes NuGet. |
| Símbolos | Especifica que el paquete contiene orígenes y símbolos. Cuando se usa con un archivo de `.nuspec`, se crea un archivo de paquete NuGet normal y el paquete de símbolos correspondiente. De forma predeterminada, crea un [paquete de símbolos heredado](../../create-packages/Symbol-Packages.md). El nuevo formato recomendado para paquetes de símbolos es .snupkg. Vea [Crear paquetes de símbolos (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Herramienta | Especifica que los archivos de salida del proyecto deben colocarse en la carpeta `tool`. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |
| Version | Invalida el número de versión del archivo de `.nuspec`. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Exclusión de las dependencias de desarrollo

Algunos paquetes NuGet son útiles como dependencias de desarrollo, lo que le ayuda a crear su propia biblioteca, pero no se necesita necesariamente como dependencias reales de paquetes.

El comando `pack` omitirá `package` entradas de `packages.config` que tengan el atributo `developmentDependency` establecido en `true`. Estas entradas no se incluirán como dependencias en el paquete creado.

Por ejemplo, considere el siguiente archivo de `packages.config` en el proyecto de origen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Para este proyecto, el paquete creado por `nuget pack` tendrá una dependencia en `jQuery` y `microsoft-web-helpers`, pero no `netfx-Guard`.

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
