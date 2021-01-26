---
title: Comando del paquete de la CLI de NuGet
description: Referencia del comando del paquete de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780040"
---
# <a name="pack-command-nuget-cli"></a>comando Pack (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** la creación de paquetes: 2.7 +

Crea un paquete de NuGet basado en el archivo [. nuspec](../nuspec.md) o el archivo de proyecto especificado. El `dotnet pack` comando (consulte los [comandos de dotnet](../dotnet-Commands.md)) y `msbuild -t:pack` (vea [destinos de MSBuild](../msbuild-targets.md)) se puede usar como alternativa.

> [!Important]
> Use [`dotnet pack`](../dotnet-Commands.md) o [`msbuild -t:pack`](../msbuild-targets.md) para proyectos basados en [PackageReference](../../consume-packages/package-references-in-project-files.md) .
> En mono, no se admite la creación de un paquete a partir de un archivo de proyecto. También debe ajustar las rutas de acceso no locales del `.nuspec` archivo a las rutas de acceso de estilo Unix, ya que nuget.exe no convierte los nombres de usuario de Windows.

## <a name="usage"></a>Uso

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

donde `<nuspecPath>` y `<projectPath>` especifican el `.nuspec` archivo de proyecto o, respectivamente.

## <a name="options"></a>Opciones
- **`-BasePath`**

   Establece la ruta de acceso base de los archivos definidos en el archivo [. nuspec](../nuspec.md) .

- **`-Build`**

  Especifica que el proyecto debe compilarse antes de compilar el paquete.

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Exclude`**

  Especifica uno o más patrones de caracteres comodín que se deben excluir al crear un paquete. Para especificar más de un patrón, repita la marca-exclude. Consulte el ejemplo siguiente.

- **`-ExcludeEmptyDirectories`**

  Impide la inclusión de directorios vacíos al compilar el paquete.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-IncludeReferencedProjects`**

  Indica que el paquete compilado debe incluir los proyectos a los que se hace referencia como dependencias o como parte del paquete. Si un proyecto al que se hace referencia tiene un archivo correspondiente con `.nuspec` el mismo nombre que el proyecto, el proyecto al que se hace referencia se agrega como una dependencia. De lo contrario, el proyecto al que se hace referencia se agrega como parte del paquete.

- **`-InstallPackageToOutputPath`**

  Especifique si el comando debe preparar el directorio de salida del paquete para admitir el recurso compartido como fuente.

- **`-MinClientVersion`**

  Establezca el atributo *minClientVersion* para el paquete creado. Este valor invalidará el valor del atributo *minClientVersion* existente (si existe) en el `.nuspec` archivo.

- **`-MSBuildPath`**

  *(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el comando, que tiene prioridad sobre `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando. Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild.

- **`-NoDefaultExcludes`**

  Evita la exclusión predeterminada de archivos y archivos de paquetes de NuGet y carpetas que empiezan con un punto, como `.svn` y `.gitignore` .

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-NoPackageAnalysis`**

  Especifica que el paquete no debe ejecutar el análisis de paquetes después de crear el paquete.

- **`-OutputDirectory`**

  Especifica la carpeta en la que se almacena el paquete creado. Si no se especifica ninguna carpeta, se usa la carpeta actual.

- **`-OutputFileNamesWithoutVersion`**

  Especifique si el comando debe preparar el nombre de salida del paquete sin la versión.

- **`-PackagesDirectory`**

  Especifica la carpeta packages.

- **`-p|-Properties`**

  Debe aparecer en último lugar en la línea de comandos después de otras opciones. Especifica una lista de propiedades que invalidan los valores del archivo de proyecto. vea [propiedades comunes del proyecto de MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nombres de propiedad. El argumento Properties aquí es una lista de pares token = valor, separados por punto y coma, donde cada aparición de `$token$` en el `.nuspec` archivo se reemplazará por el valor especificado. Los valores pueden ser cadenas entre comillas. Tenga en cuenta que para la propiedad "Configuration", el valor predeterminado es "debug". Para cambiar a una configuración de versión, use `-Properties Configuration=Release` . **En general**, las propiedades deben ser las mismas que se usaron durante la compilación del proyecto correspondiente, con el fin de evitar un comportamiento potencialmente extraño.

- **`-SolutionDirectory`**

  Especifica el directorio de la solución.

- **`-Suffix`**

  *(3.4.4 +)* Anexa un sufijo al número de versión generado internamente, que se usa normalmente para anexar los identificadores de compilación u otros identificadores de versión preliminar. Por ejemplo, si usa, `-suffix nightly` se creará un paquete con un número de versión como `1.2.3-nightly` . Los sufijos deben comenzar con una letra para evitar las advertencias, los errores y las posibles incompatibilidades con las distintas versiones de NuGet y el administrador de paquetes NuGet.

- **`-SymbolPackageFormat`**

  Al crear un paquete de símbolos, permite elegir entre el `snupkg` `symbols.nupkg` formato y.

- **`-Symbols`**

  Especifica que el paquete contiene orígenes y símbolos. Cuando se usa con un `.nuspec` archivo, crea un archivo de paquete NuGet normal y el paquete de símbolos correspondiente. De forma predeterminada, crea un [paquete de símbolos heredado](../../create-packages/Symbol-Packages.md). El nuevo formato recomendado para paquetes de símbolos es .snupkg. Vea [Crear paquetes de símbolos (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).

- **`-Tool`**

   Especifica que los archivos de salida del proyecto deben colocarse en la `tool` carpeta.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

- **`-Version`**

  Invalida el número de versión del `.nuspec` archivo.

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Exclusión de las dependencias de desarrollo

Algunos paquetes NuGet son útiles como dependencias de desarrollo, lo que le ayuda a crear su propia biblioteca, pero no se necesita necesariamente como dependencias reales de paquetes.

El `pack` comando omitirá las `package` entradas de `packages.config` que tengan el `developmentDependency` atributo establecido en `true` . Estas entradas no se incluirán como dependencias en el paquete creado.

Por ejemplo, considere el siguiente `packages.config` archivo en el proyecto de origen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Para este proyecto, el paquete creado por `nuget pack` tendrá una dependencia en `jQuery` y, `microsoft-web-helpers` pero no en `netfx-Guard` .

## <a name="suppressing-pack-warnings"></a>Suprimir advertencias del paquete

Aunque se recomienda que resuelva todas las advertencias de NuGet durante las operaciones del paquete, en determinadas situaciones se garantiza la supresión.

Puede lograrlo de la siguiente manera: 

> Paquete de nuget.exe Pack. nuspec-Properties nowarn = NU5104

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
