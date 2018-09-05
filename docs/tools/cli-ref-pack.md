---
title: Comando de CLI de NuGet pack
description: Referencia del comando pack de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: db236b0eaac34ca9f6f67fd15ca3ad6884f6a18d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549101"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="c5003-103">Comando pack (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="c5003-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="c5003-104">**Se aplica a:** la creación del paquete &bullet; **versiones compatibles:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="c5003-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="c5003-105">Crea un paquete de NuGet según lo especificado `.nuspec` o archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="c5003-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="c5003-106">El `dotnet pack` comando (vea [comandos dotnet](dotnet-Commands.md)) y `msbuild /t:pack` (consulte [destinos de MSBuild](../reference/msbuild-targets.md)) que puede utilizarse como alternativas.</span><span class="sxs-lookup"><span data-stu-id="c5003-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="c5003-107">En Mono, no se admite la creación de un paquete desde un archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="c5003-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="c5003-108">También deberá ajustar las rutas de acceso no local en el `.nuspec` de archivos para las rutas de acceso de estilo Unix, como nuget.exe no convierte las rutas de acceso de Windows sí.</span><span class="sxs-lookup"><span data-stu-id="c5003-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="c5003-109">Uso</span><span class="sxs-lookup"><span data-stu-id="c5003-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="c5003-110">donde `<nuspecPath>` y `<projectPath>` especificar el `.nuspec` o archivo de proyecto, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c5003-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c5003-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="c5003-111">Options</span></span>

| <span data-ttu-id="c5003-112">Opción</span><span class="sxs-lookup"><span data-stu-id="c5003-112">Option</span></span> | <span data-ttu-id="c5003-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="c5003-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c5003-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="c5003-114">BasePath</span></span> | <span data-ttu-id="c5003-115">Establece la ruta de acceso base de los archivos definidos en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="c5003-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="c5003-116">Compilar</span><span class="sxs-lookup"><span data-stu-id="c5003-116">Build</span></span> | <span data-ttu-id="c5003-117">Especifica que el proyecto debe compilarse antes de crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="c5003-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="c5003-118">Excluir</span><span class="sxs-lookup"><span data-stu-id="c5003-118">Exclude</span></span> | <span data-ttu-id="c5003-119">Especifica uno o varios patrones de caracteres comodín para excluir al crear un paquete.</span><span class="sxs-lookup"><span data-stu-id="c5003-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="c5003-120">Para especificar más de un patrón, repita el - marcador de exclusión.</span><span class="sxs-lookup"><span data-stu-id="c5003-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="c5003-121">Vea el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="c5003-121">See example below.</span></span> |
| <span data-ttu-id="c5003-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="c5003-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="c5003-123">Impide la inclusión de directorios vacíos al crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="c5003-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="c5003-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c5003-124">ForceEnglishOutput</span></span> | <span data-ttu-id="c5003-125">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="c5003-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c5003-126">Ayuda</span><span class="sxs-lookup"><span data-stu-id="c5003-126">Help</span></span> | <span data-ttu-id="c5003-127">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="c5003-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="c5003-128">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="c5003-128">IncludeReferencedProjects</span></span> | <span data-ttu-id="c5003-129">Indica que el paquete generado debe incluir los proyectos que se hace referencia como dependencias o como parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="c5003-129">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="c5003-130">Si un proyecto que se hace referencia tiene un correspondiente `.nuspec` archivo que tiene el mismo nombre que el proyecto y, a continuación, ese proyecto se agrega como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="c5003-130">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="c5003-131">En caso contrario, se agrega el proyecto que se hace referencia como parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="c5003-131">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="c5003-132">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="c5003-132">MinClientVersion</span></span> | <span data-ttu-id="c5003-133">Establecer el *minClientVersion* atributo para el paquete creado.</span><span class="sxs-lookup"><span data-stu-id="c5003-133">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="c5003-134">Este valor reemplazará el valor de la existente *minClientVersion* atributo (si existe) en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="c5003-134">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="c5003-135">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="c5003-135">MSBuildPath</span></span> | <span data-ttu-id="c5003-136">*(4.0 y versiones posteriores)*  Especifica la ruta de acceso de MSBuild que use con el comando, tiene prioridad sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="c5003-136">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="c5003-137">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="c5003-137">MSBuildVersion</span></span> | <span data-ttu-id="c5003-138">*(3.2 y versiones posteriores)*  Especifica la versión de MSBuild que se usará con este comando.</span><span class="sxs-lookup"><span data-stu-id="c5003-138">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="c5003-139">Los valores admitidos son 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="c5003-139">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="c5003-140">De forma predeterminada que se selecciona la versión de MSBuild en su ruta de acceso, en caso contrario, el valor predeterminado es la última versión instalada de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c5003-140">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="c5003-141">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="c5003-141">NoDefaultExcludes</span></span> | <span data-ttu-id="c5003-142">Evita la exclusión predeterminada de NuGet empaquetar archivos y archivos y carpetas de inicio con un punto, como `.svn` y `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="c5003-142">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="c5003-143">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="c5003-143">NoPackageAnalysis</span></span> | <span data-ttu-id="c5003-144">Especifica que el paquete no debe ejecutar el análisis de paquetes después de crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="c5003-144">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="c5003-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="c5003-145">OutputDirectory</span></span> | <span data-ttu-id="c5003-146">Especifica la carpeta donde se almacena el paquete creado.</span><span class="sxs-lookup"><span data-stu-id="c5003-146">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="c5003-147">Si se especifica ninguna carpeta, se usa la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="c5003-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="c5003-148">Propiedades</span><span class="sxs-lookup"><span data-stu-id="c5003-148">Properties</span></span> | <span data-ttu-id="c5003-149">Debe aparecer al final de la línea de comandos después de otras opciones.</span><span class="sxs-lookup"><span data-stu-id="c5003-149">Should appear last on the command line after other options.</span></span> <span data-ttu-id="c5003-150">Especifica una lista de las propiedades que reemplazan los valores en el archivo de proyecto. consulte [propiedades comunes de proyectos de MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) nombres de propiedad.</span><span class="sxs-lookup"><span data-stu-id="c5003-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="c5003-151">Aquí el argumento de propiedades es una lista de pares de nombre-valor, separados por punto y coma, donde cada aparición de `$token$` en el `.nuspec` archivo se sustituirá con el valor especificado.</span><span class="sxs-lookup"><span data-stu-id="c5003-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="c5003-152">Los valores pueden ser cadenas entre comillas.</span><span class="sxs-lookup"><span data-stu-id="c5003-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="c5003-153">Tenga en cuenta que para la propiedad "Configuration", el valor predeterminado es "Debug".</span><span class="sxs-lookup"><span data-stu-id="c5003-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="c5003-154">Para cambiar a una configuración de lanzamiento, utilice `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="c5003-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="c5003-155">Sufijo</span><span class="sxs-lookup"><span data-stu-id="c5003-155">Suffix</span></span> | <span data-ttu-id="c5003-156">*(3.4.4+)*  Anexa un sufijo para el número de versión generada internamente, se utiliza normalmente para anexar las compilación u otros identificadores de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="c5003-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="c5003-157">Por ejemplo, mediante `-suffix nightly` creará un paquete con un tipo de número de versión `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="c5003-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="c5003-158">Sufijos deben empezar por una letra para evitar las advertencias, errores y las posibles incompatibilidades con distintas versiones de NuGet y el Administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5003-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="c5003-159">Símbolos</span><span class="sxs-lookup"><span data-stu-id="c5003-159">Symbols</span></span> | <span data-ttu-id="c5003-160">Especifica que el paquete contiene orígenes y símbolos.</span><span class="sxs-lookup"><span data-stu-id="c5003-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="c5003-161">Cuando se usa con un `.nuspec` archivo, esto crea un archivo de paquete NuGet normal y el correspondiente paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="c5003-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="c5003-162">Herramienta</span><span class="sxs-lookup"><span data-stu-id="c5003-162">Tool</span></span> | <span data-ttu-id="c5003-163">Especifica que se deben colocar los archivos de salida del proyecto en el `tool` carpeta.</span><span class="sxs-lookup"><span data-stu-id="c5003-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="c5003-164">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="c5003-164">Verbosity</span></span> | <span data-ttu-id="c5003-165">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="c5003-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="c5003-166">Versión</span><span class="sxs-lookup"><span data-stu-id="c5003-166">Version</span></span> | <span data-ttu-id="c5003-167">Invalida el número de versión desde el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="c5003-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="c5003-168">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c5003-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="c5003-169">Exclusión de dependencias de desarrollo</span><span class="sxs-lookup"><span data-stu-id="c5003-169">Excluding development dependencies</span></span>

<span data-ttu-id="c5003-170">Algunos paquetes de NuGet son útiles como las dependencias de desarrollo, que le ayudarán a crear su propia biblioteca, pero no son necesariamente necesarios como dependencias de paquete real.</span><span class="sxs-lookup"><span data-stu-id="c5003-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="c5003-171">El `pack` pasará por alto el comando `package` las entradas de `packages.config` que tienen el `developmentDependency` atributo establecido en `true`.</span><span class="sxs-lookup"><span data-stu-id="c5003-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="c5003-172">Estas entradas no se incluirá como una dependencias en el paquete creado.</span><span class="sxs-lookup"><span data-stu-id="c5003-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="c5003-173">Por ejemplo, considere la siguiente `packages.config` archivo en el proyecto de origen:</span><span class="sxs-lookup"><span data-stu-id="c5003-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="c5003-174">Para este proyecto, el paquete creado por `nuget pack` tiene una dependencia de `jQuery` y `microsoft-web-helpers` pero no `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="c5003-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="c5003-175">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c5003-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
