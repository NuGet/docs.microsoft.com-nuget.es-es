---
title: Comando del paquete de la CLI de NuGet
description: Referencia del comando del paquete Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e12944bdd5d43b8b9e84908be480a5249dd924f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327662"
---
# <a name="pack-command-nuget-cli"></a>Comando pack (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** la creación de paquetes: 2.7+

Crea un paquete de NuGet basado en el `.nuspec` archivo de proyecto o especificado. El `dotnet pack` comando (consulte los [comandos](../dotnet-Commands.md)de dotnet `msbuild -t:pack` ) y (vea [destinos de MSBuild](../msbuild-targets.md)) se puede usar como alternativa.

> [!Important]
> En mono, no se admite la creación de un paquete a partir de un archivo de proyecto. También debe ajustar las rutas de acceso no locales en el `.nuspec` archivo a las rutas de acceso de estilo Unix, ya que Nuget. exe no convierte los nombres de usuario de Windows.

## <a name="usage"></a>Uso

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

donde `<nuspecPath>` `.nuspec` y `<projectPath>` especifican el archivo de proyecto o, respectivamente.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| BasePath | Establece la ruta de acceso base de los archivos definidos `.nuspec` en el archivo. |
| Compilación | Especifica que el proyecto debe compilarse antes de compilar el paquete. |
| Excluir | Especifica uno o más patrones de caracteres comodín que se deben excluir al crear un paquete. Para especificar más de un patrón, repita la marca-exclude. Vea el ejemplo siguiente. |
| ExcludeEmptyDirectories | Impide la inclusión de directorios vacíos al compilar el paquete. |
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| ConfigFile | Especifique el archivo de configuración para el comando Pack. |
| Help | Muestra información de ayuda para el comando. |
| IncludeReferencedProjects | Indica que el paquete compilado debe incluir los proyectos a los que se hace referencia como dependencias o como parte del paquete. Si un proyecto al que se hace referencia `.nuspec` tiene un archivo correspondiente con el mismo nombre que el proyecto, el proyecto al que se hace referencia se agrega como una dependencia. De lo contrario, el proyecto al que se hace referencia se agrega como parte del paquete. |
| MinClientVersion | Establezca el atributo *minClientVersion* para el paquete creado. Este valor invalidará el valor del atributo *minClientVersion* existente (si existe) en el `.nuspec` archivo. |
| MSBuildPath | *(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el `-MSBuildVersion`comando, que tiene prioridad sobre. |
| MSBuildVersion | *(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando. Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild. |
| NoDefaultExcludes | Evita la exclusión predeterminada de archivos y archivos de paquetes de NuGet y carpetas que empiezan con un `.svn` punto `.gitignore`, como y. |
| NoPackageAnalysis | Especifica que el paquete no debe ejecutar el análisis de paquetes después de crear el paquete. |
| OutputDirectory | Especifica la carpeta en la que se almacena el paquete creado. Si no se especifica ninguna carpeta, se usa la carpeta actual. |
| Properties (Propiedades) | Debe aparecer en último lugar en la línea de comandos después de otras opciones. Especifica una lista de propiedades que invalidan los valores del archivo de proyecto. vea [propiedades comunes del proyecto de MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nombres de propiedad. El argumento Properties aquí es una lista de pares token = valor, separados por punto y coma, donde cada aparición de `$token$` en el `.nuspec` archivo se reemplazará por el valor especificado. Los valores pueden ser cadenas entre comillas. Tenga en cuenta que para la propiedad "Configuration", el valor predeterminado es "debug". Para cambiar a una configuración de versión, `-Properties Configuration=Release`use. |
| Sufijo | *(3.4.4 +)* Anexa un sufijo al número de versión generado internamente, que se usa normalmente para anexar los identificadores de compilación u otros identificadores de versión preliminar. Por ejemplo, si `-suffix nightly` usa, se creará un paquete con un `1.2.3-nightly`número de versión como. Los sufijos deben comenzar con una letra para evitar las advertencias, los errores y las posibles incompatibilidades con las distintas versiones de NuGet y el administrador de paquetes NuGet. |
| Símbolos | Especifica que el paquete contiene orígenes y símbolos. Cuando se usa con `.nuspec` un archivo, crea un archivo de paquete NuGet normal y el paquete de símbolos correspondiente. De forma predeterminada, crea un [paquete de símbolos heredado](../../create-packages/Symbol-Packages.md). El nuevo formato recomendado para paquetes de símbolos es .snupkg. Vea [Crear paquetes de símbolos (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Herramienta | Especifica que los archivos de salida del proyecto deben colocarse en la `tool` carpeta. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |
| `Version` | Invalida el número de versión del `.nuspec` archivo. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Exclusión de las dependencias de desarrollo

Algunos paquetes NuGet son útiles como dependencias de desarrollo, lo que le ayuda a crear su propia biblioteca, pero no se necesita necesariamente como dependencias reales de paquetes.

El `pack` comando omitirá `package` las entradas `packages.config` de que tengan `developmentDependency` el atributo establecido `true`en. Estas entradas no se incluirán como dependencias en el paquete creado.

Por ejemplo, considere el siguiente `packages.config` archivo en el proyecto de origen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Para este proyecto, el paquete creado por `nuget pack` tendrá una dependencia en y `jQuery` `microsoft-web-helpers` , pero no `netfx-Guard`en.

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
