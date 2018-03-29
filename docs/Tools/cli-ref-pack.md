---
title: Comando de paquete de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia del comando de módulo nuget.exe
keywords: referencia al módulo de NuGet, comando pack
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 14ecf724477f652275eb68a090bb57b8640d4a8a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="eb241-104">comando Pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="eb241-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="eb241-105">**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="eb241-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="eb241-106">Crea un paquete de NuGet basado en las clases `.nuspec` o archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="eb241-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="eb241-107">El `dotnet pack` comando (vea [comandos dotnet](dotnet-Commands.md)) y `msbuild /t:pack` (consulte [destinos de MSBuild](../reference/msbuild-targets.md)) que puede utilizarse como alternativas.</span><span class="sxs-lookup"><span data-stu-id="eb241-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="eb241-108">En blanco y negro, no se admite la creación de un paquete desde un archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="eb241-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="eb241-109">También debe ajustar las rutas de acceso no es local en el `.nuspec` del archivo a las rutas de acceso de estilo Unix, como nuget.exe no se convierten las rutas de acceso de Windows propio.</span><span class="sxs-lookup"><span data-stu-id="eb241-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="eb241-110">Uso</span><span class="sxs-lookup"><span data-stu-id="eb241-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="eb241-111">donde `<nuspecPath>` y `<projectPath>` especificar el `.nuspec` o un proyecto de archivo, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="eb241-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="eb241-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="eb241-112">Options</span></span>

| <span data-ttu-id="eb241-113">Opción</span><span class="sxs-lookup"><span data-stu-id="eb241-113">Option</span></span> | <span data-ttu-id="eb241-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="eb241-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eb241-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="eb241-115">BasePath</span></span> | <span data-ttu-id="eb241-116">Establece la ruta de acceso base de los archivos definidos en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="eb241-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="eb241-117">Compilar</span><span class="sxs-lookup"><span data-stu-id="eb241-117">Build</span></span> | <span data-ttu-id="eb241-118">Especifica que se debe generar el proyecto antes de crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="eb241-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="eb241-119">Excluir</span><span class="sxs-lookup"><span data-stu-id="eb241-119">Exclude</span></span> | <span data-ttu-id="eb241-120">Especifica uno o varios patrones de caracteres comodín para excluir al crear un paquete.</span><span class="sxs-lookup"><span data-stu-id="eb241-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="eb241-121">Para especificar más de un patrón, repita-marcador de exclusión.</span><span class="sxs-lookup"><span data-stu-id="eb241-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="eb241-122">Vea el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="eb241-122">See example below.</span></span> |
| <span data-ttu-id="eb241-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="eb241-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="eb241-124">Impide la inclusión de directorios vacíos cuando se crea el paquete.</span><span class="sxs-lookup"><span data-stu-id="eb241-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="eb241-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="eb241-125">ForceEnglishOutput</span></span> | <span data-ttu-id="eb241-126">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="eb241-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="eb241-127">Ayuda</span><span class="sxs-lookup"><span data-stu-id="eb241-127">Help</span></span> | <span data-ttu-id="eb241-128">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="eb241-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="eb241-129">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="eb241-129">IncludeReferencedProjects</span></span> | <span data-ttu-id="eb241-130">Indica que el paquete creado debe incluir los proyectos que se hace referencia como dependencias o como parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="eb241-130">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="eb241-131">Si un proyecto que se hace referencia tiene su correspondiente `.nuspec` archivo que tiene el mismo nombre que el proyecto y, a continuación, se agrega ese proyecto que se hace referencia como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="eb241-131">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="eb241-132">En caso contrario, se agrega el proyecto que se hace referencia como parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="eb241-132">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="eb241-133">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="eb241-133">MinClientVersion</span></span> | <span data-ttu-id="eb241-134">Establecer el *minClientVersion* atributo para el paquete creado.</span><span class="sxs-lookup"><span data-stu-id="eb241-134">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="eb241-135">Este valor invalida el valor de la existente *minClientVersion* atributo (si existe) en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="eb241-135">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="eb241-136">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="eb241-136">MSBuildPath</span></span> | <span data-ttu-id="eb241-137">*(4.0 +)*  Especifica la ruta de acceso de MSBuild para usar con el comando, tiene prioridad sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="eb241-137">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="eb241-138">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="eb241-138">MSBuildVersion</span></span> | <span data-ttu-id="eb241-139">*(3.2 +)*  Especifica la versión de MSBuild que se utilizará con este comando.</span><span class="sxs-lookup"><span data-stu-id="eb241-139">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="eb241-140">Valores admitidos son 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="eb241-140">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="eb241-141">De forma predeterminada, se seleccionará el MSBuild en la ruta de acceso, en caso contrario, valor predeterminado es la última versión instalada de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="eb241-141">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="eb241-142">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="eb241-142">NoDefaultExcludes</span></span> | <span data-ttu-id="eb241-143">Evita la exclusión predeterminada de NuGet empaquetar archivos y archivos y carpetas que comience con un punto, como `.svn` y `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="eb241-143">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="eb241-144">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="eb241-144">NoPackageAnalysis</span></span> | <span data-ttu-id="eb241-145">Especifica que el paquete no debe ejecutar el análisis de paquetes después de crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="eb241-145">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="eb241-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="eb241-146">OutputDirectory</span></span> | <span data-ttu-id="eb241-147">Especifica la carpeta en la que está almacenado el paquete creado.</span><span class="sxs-lookup"><span data-stu-id="eb241-147">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="eb241-148">Si no se especifica ninguna carpeta, se usa la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="eb241-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="eb241-149">Propiedades</span><span class="sxs-lookup"><span data-stu-id="eb241-149">Properties</span></span> | <span data-ttu-id="eb241-150">Especifica una lista de propiedades que invalidan los valores en el archivo de proyecto; vea [propiedades comunes de proyectos de MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para los nombres de propiedad.</span><span class="sxs-lookup"><span data-stu-id="eb241-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="eb241-151">Aquí el argumento de propiedades es una lista del token de pares de nombre-valor, separados por punto y coma, donde cada aparición de `$token$` en el `.nuspec` archivo se sustituirá con el valor dado.</span><span class="sxs-lookup"><span data-stu-id="eb241-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="eb241-152">Los valores pueden ser cadenas entre comillas.</span><span class="sxs-lookup"><span data-stu-id="eb241-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="eb241-153">Tenga en cuenta que para la propiedad "Configuration", el valor predeterminado es "Debug".</span><span class="sxs-lookup"><span data-stu-id="eb241-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="eb241-154">Para cambiar a una configuración de lanzamiento, utilice `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="eb241-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="eb241-155">Sufijo</span><span class="sxs-lookup"><span data-stu-id="eb241-155">Suffix</span></span> | <span data-ttu-id="eb241-156">*(3.4.4+)*  Anexa un sufijo para el número de versión generado internamente, se utiliza normalmente para anexar compilación u otros identificadores de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="eb241-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="eb241-157">Por ejemplo, si se usa `-suffix nightly` creará un paquete con un tipo de número de versión `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="eb241-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="eb241-158">Los sufijos deben empezar por una letra para evitar posibles incompatibilidades con distintas versiones de NuGet y el Administrador de paquetes de NuGet, errores y advertencias.</span><span class="sxs-lookup"><span data-stu-id="eb241-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="eb241-159">Símbolos</span><span class="sxs-lookup"><span data-stu-id="eb241-159">Symbols</span></span> | <span data-ttu-id="eb241-160">Especifica que el paquete contiene orígenes y símbolos.</span><span class="sxs-lookup"><span data-stu-id="eb241-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="eb241-161">Cuando se usa con un `.nuspec` archivos, esto crea un archivo de paquete de NuGet normal y el correspondiente paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="eb241-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="eb241-162">Herramienta</span><span class="sxs-lookup"><span data-stu-id="eb241-162">Tool</span></span> | <span data-ttu-id="eb241-163">Especifica que los archivos de salida del proyecto deben estar situados en el `tool` carpeta.</span><span class="sxs-lookup"><span data-stu-id="eb241-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="eb241-164">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="eb241-164">Verbosity</span></span> | <span data-ttu-id="eb241-165">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="eb241-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="eb241-166">Versión</span><span class="sxs-lookup"><span data-stu-id="eb241-166">Version</span></span> | <span data-ttu-id="eb241-167">Invalida el número de versión de la `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="eb241-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="eb241-168">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="eb241-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="eb241-169">Excluidas las dependencias de desarrollo</span><span class="sxs-lookup"><span data-stu-id="eb241-169">Excluding development dependencies</span></span>

<span data-ttu-id="eb241-170">Algunos paquetes de NuGet son útiles como las dependencias de desarrollo, que le ayudarán a crear su propia biblioteca, pero no son necesariamente necesarios como dependencias de paquete real.</span><span class="sxs-lookup"><span data-stu-id="eb241-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="eb241-171">El `pack` hará caso omiso de comando `package` entradas de `packages.config` que tienen la `developmentDependency` atributo establecido en `true`.</span><span class="sxs-lookup"><span data-stu-id="eb241-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="eb241-172">Estas entradas no se incluirá como un dependencias en el paquete creado.</span><span class="sxs-lookup"><span data-stu-id="eb241-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="eb241-173">Por ejemplo, considere la siguiente `packages.config` archivo en el proyecto de origen:</span><span class="sxs-lookup"><span data-stu-id="eb241-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="eb241-174">Para este proyecto, se crea el paquete por `nuget pack` tendrá una dependencia en `jQuery` y `microsoft-web-helpers` pero no `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="eb241-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="eb241-175">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="eb241-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
