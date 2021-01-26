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
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="e00b1-103">comando Pack (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="e00b1-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="e00b1-104">**Se aplica a:** &bullet; **versiones compatibles con** la creación de paquetes: 2.7 +</span><span class="sxs-lookup"><span data-stu-id="e00b1-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="e00b1-105">Crea un paquete de NuGet basado en el archivo [. nuspec](../nuspec.md) o el archivo de proyecto especificado.</span><span class="sxs-lookup"><span data-stu-id="e00b1-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="e00b1-106">El `dotnet pack` comando (consulte los [comandos de dotnet](../dotnet-Commands.md)) y `msbuild -t:pack` (vea [destinos de MSBuild](../msbuild-targets.md)) se puede usar como alternativa.</span><span class="sxs-lookup"><span data-stu-id="e00b1-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="e00b1-107">Use [`dotnet pack`](../dotnet-Commands.md) o [`msbuild -t:pack`](../msbuild-targets.md) para proyectos basados en [PackageReference](../../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="e00b1-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="e00b1-108">En mono, no se admite la creación de un paquete a partir de un archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="e00b1-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="e00b1-109">También debe ajustar las rutas de acceso no locales del `.nuspec` archivo a las rutas de acceso de estilo Unix, ya que nuget.exe no convierte los nombres de usuario de Windows.</span><span class="sxs-lookup"><span data-stu-id="e00b1-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="e00b1-110">Uso</span><span class="sxs-lookup"><span data-stu-id="e00b1-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="e00b1-111">donde `<nuspecPath>` y `<projectPath>` especifican el `.nuspec` archivo de proyecto o, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e00b1-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="e00b1-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="e00b1-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="e00b1-113">Establece la ruta de acceso base de los archivos definidos en el archivo [. nuspec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="e00b1-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="e00b1-114">Especifica que el proyecto debe compilarse antes de compilar el paquete.</span><span class="sxs-lookup"><span data-stu-id="e00b1-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="e00b1-115">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="e00b1-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e00b1-116">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="e00b1-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="e00b1-117">Especifica uno o más patrones de caracteres comodín que se deben excluir al crear un paquete.</span><span class="sxs-lookup"><span data-stu-id="e00b1-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="e00b1-118">Para especificar más de un patrón, repita la marca-exclude.</span><span class="sxs-lookup"><span data-stu-id="e00b1-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="e00b1-119">Consulte el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e00b1-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="e00b1-120">Impide la inclusión de directorios vacíos al compilar el paquete.</span><span class="sxs-lookup"><span data-stu-id="e00b1-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="e00b1-121">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="e00b1-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="e00b1-122">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="e00b1-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="e00b1-123">Indica que el paquete compilado debe incluir los proyectos a los que se hace referencia como dependencias o como parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="e00b1-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="e00b1-124">Si un proyecto al que se hace referencia tiene un archivo correspondiente con `.nuspec` el mismo nombre que el proyecto, el proyecto al que se hace referencia se agrega como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="e00b1-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="e00b1-125">De lo contrario, el proyecto al que se hace referencia se agrega como parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="e00b1-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="e00b1-126">Especifique si el comando debe preparar el directorio de salida del paquete para admitir el recurso compartido como fuente.</span><span class="sxs-lookup"><span data-stu-id="e00b1-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="e00b1-127">Establezca el atributo *minClientVersion* para el paquete creado.</span><span class="sxs-lookup"><span data-stu-id="e00b1-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="e00b1-128">Este valor invalidará el valor del atributo *minClientVersion* existente (si existe) en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="e00b1-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="e00b1-129">*(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el comando, que tiene prioridad sobre `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="e00b1-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="e00b1-130">*(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando.</span><span class="sxs-lookup"><span data-stu-id="e00b1-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="e00b1-131">Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="e00b1-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="e00b1-132">De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e00b1-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="e00b1-133">Evita la exclusión predeterminada de archivos y archivos de paquetes de NuGet y carpetas que empiezan con un punto, como `.svn` y `.gitignore` .</span><span class="sxs-lookup"><span data-stu-id="e00b1-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="e00b1-134">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="e00b1-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="e00b1-135">Especifica que el paquete no debe ejecutar el análisis de paquetes después de crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="e00b1-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="e00b1-136">Especifica la carpeta en la que se almacena el paquete creado.</span><span class="sxs-lookup"><span data-stu-id="e00b1-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="e00b1-137">Si no se especifica ninguna carpeta, se usa la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="e00b1-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="e00b1-138">Especifique si el comando debe preparar el nombre de salida del paquete sin la versión.</span><span class="sxs-lookup"><span data-stu-id="e00b1-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="e00b1-139">Especifica la carpeta packages.</span><span class="sxs-lookup"><span data-stu-id="e00b1-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="e00b1-140">Debe aparecer en último lugar en la línea de comandos después de otras opciones.</span><span class="sxs-lookup"><span data-stu-id="e00b1-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="e00b1-141">Especifica una lista de propiedades que invalidan los valores del archivo de proyecto. vea [propiedades comunes del proyecto de MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nombres de propiedad.</span><span class="sxs-lookup"><span data-stu-id="e00b1-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="e00b1-142">El argumento Properties aquí es una lista de pares token = valor, separados por punto y coma, donde cada aparición de `$token$` en el `.nuspec` archivo se reemplazará por el valor especificado.</span><span class="sxs-lookup"><span data-stu-id="e00b1-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="e00b1-143">Los valores pueden ser cadenas entre comillas.</span><span class="sxs-lookup"><span data-stu-id="e00b1-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="e00b1-144">Tenga en cuenta que para la propiedad "Configuration", el valor predeterminado es "debug".</span><span class="sxs-lookup"><span data-stu-id="e00b1-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="e00b1-145">Para cambiar a una configuración de versión, use `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="e00b1-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="e00b1-146">**En general**, las propiedades deben ser las mismas que se usaron durante la compilación del proyecto correspondiente, con el fin de evitar un comportamiento potencialmente extraño.</span><span class="sxs-lookup"><span data-stu-id="e00b1-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="e00b1-147">Especifica el directorio de la solución.</span><span class="sxs-lookup"><span data-stu-id="e00b1-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="e00b1-148">*(3.4.4 +)* Anexa un sufijo al número de versión generado internamente, que se usa normalmente para anexar los identificadores de compilación u otros identificadores de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="e00b1-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="e00b1-149">Por ejemplo, si usa, `-suffix nightly` se creará un paquete con un número de versión como `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="e00b1-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="e00b1-150">Los sufijos deben comenzar con una letra para evitar las advertencias, los errores y las posibles incompatibilidades con las distintas versiones de NuGet y el administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="e00b1-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="e00b1-151">Al crear un paquete de símbolos, permite elegir entre el `snupkg` `symbols.nupkg` formato y.</span><span class="sxs-lookup"><span data-stu-id="e00b1-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="e00b1-152">Especifica que el paquete contiene orígenes y símbolos.</span><span class="sxs-lookup"><span data-stu-id="e00b1-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="e00b1-153">Cuando se usa con un `.nuspec` archivo, crea un archivo de paquete NuGet normal y el paquete de símbolos correspondiente.</span><span class="sxs-lookup"><span data-stu-id="e00b1-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="e00b1-154">De forma predeterminada, crea un [paquete de símbolos heredado](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="e00b1-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="e00b1-155">El nuevo formato recomendado para paquetes de símbolos es .snupkg.</span><span class="sxs-lookup"><span data-stu-id="e00b1-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="e00b1-156">Vea [Crear paquetes de símbolos (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="e00b1-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="e00b1-157">Especifica que los archivos de salida del proyecto deben colocarse en la `tool` carpeta.</span><span class="sxs-lookup"><span data-stu-id="e00b1-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="e00b1-158">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="e00b1-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="e00b1-159">Invalida el número de versión del `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="e00b1-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="e00b1-160">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e00b1-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="e00b1-161">Exclusión de las dependencias de desarrollo</span><span class="sxs-lookup"><span data-stu-id="e00b1-161">Excluding development dependencies</span></span>

<span data-ttu-id="e00b1-162">Algunos paquetes NuGet son útiles como dependencias de desarrollo, lo que le ayuda a crear su propia biblioteca, pero no se necesita necesariamente como dependencias reales de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e00b1-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="e00b1-163">El `pack` comando omitirá las `package` entradas de `packages.config` que tengan el `developmentDependency` atributo establecido en `true` .</span><span class="sxs-lookup"><span data-stu-id="e00b1-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="e00b1-164">Estas entradas no se incluirán como dependencias en el paquete creado.</span><span class="sxs-lookup"><span data-stu-id="e00b1-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="e00b1-165">Por ejemplo, considere el siguiente `packages.config` archivo en el proyecto de origen:</span><span class="sxs-lookup"><span data-stu-id="e00b1-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="e00b1-166">Para este proyecto, el paquete creado por `nuget pack` tendrá una dependencia en `jQuery` y, `microsoft-web-helpers` pero no en `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="e00b1-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="e00b1-167">Suprimir advertencias del paquete</span><span class="sxs-lookup"><span data-stu-id="e00b1-167">Suppressing pack warnings</span></span>

<span data-ttu-id="e00b1-168">Aunque se recomienda que resuelva todas las advertencias de NuGet durante las operaciones del paquete, en determinadas situaciones se garantiza la supresión.</span><span class="sxs-lookup"><span data-stu-id="e00b1-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="e00b1-169">Puede lograrlo de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="e00b1-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="e00b1-170">Paquete de nuget.exe Pack. nuspec-Properties nowarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="e00b1-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="e00b1-171">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="e00b1-171">Examples</span></span>

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
