---
title: Comando de restauración de la CLI de NuGet
description: Referencia del comando nuget.exe restore
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 108317aba2107948180ab0149c0c5ba5150cf9b8
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622835"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="6afa7-103">comando restore (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="6afa7-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="6afa7-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 2.7 +</span><span class="sxs-lookup"><span data-stu-id="6afa7-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="6afa7-105">Descarga e instala los paquetes que faltan en la `packages` carpeta.</span><span class="sxs-lookup"><span data-stu-id="6afa7-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="6afa7-106">Cuando se usa con NuGet 4.0 + y el formato PackageReference, genera un `<project>.nuget.props` archivo, si es necesario, en la `obj` carpeta.</span><span class="sxs-lookup"><span data-stu-id="6afa7-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="6afa7-107">(El archivo se puede omitir del control de código fuente).</span><span class="sxs-lookup"><span data-stu-id="6afa7-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="6afa7-108">En Mac OSX y Linux con la CLI en mono, la restauración de paquetes no es compatible con PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6afa7-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="6afa7-109">Uso</span><span class="sxs-lookup"><span data-stu-id="6afa7-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="6afa7-110">donde `<projectPath>` especifica la ubicación de una solución o un `packages.config` archivo.</span><span class="sxs-lookup"><span data-stu-id="6afa7-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="6afa7-111">Vea la [sección Comentarios](#remarks) a continuación para obtener información sobre el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="6afa7-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="6afa7-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="6afa7-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="6afa7-113">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="6afa7-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6afa7-114">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6afa7-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="6afa7-115">*(4.0 +)* Descarga paquetes directamente sin rellenar memorias caché con los archivos binarios o metadatos.</span><span class="sxs-lookup"><span data-stu-id="6afa7-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="6afa7-116">Deshabilita la restauración de varios paquetes en paralelo.</span><span class="sxs-lookup"><span data-stu-id="6afa7-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="6afa7-117">*(3,2 +)* Una lista de orígenes de paquetes que se usarán como reserva en caso de que el paquete no se encuentre en el origen principal o en el predeterminado.</span><span class="sxs-lookup"><span data-stu-id="6afa7-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="6afa7-118">Use un punto y coma para separar las entradas de la lista.</span><span class="sxs-lookup"><span data-stu-id="6afa7-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="6afa7-119">En los proyectos basados en PackageReference, fuerza la resolución de todas las dependencias, incluso si la última restauración se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="6afa7-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="6afa7-120">Especificar esta marca es similar a eliminar el `project.assets.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="6afa7-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="6afa7-121">Esto no omite la memoria caché http.</span><span class="sxs-lookup"><span data-stu-id="6afa7-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="6afa7-122">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="6afa7-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="6afa7-123">Fuerza la restauración para volver a evaluar todas las dependencias aunque ya exista un archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="6afa7-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="6afa7-124">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="6afa7-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="6afa7-125">Ubicación de salida donde se escribe el archivo de bloqueo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="6afa7-125">Output location where project lock file is written.</span></span> <span data-ttu-id="6afa7-126">De forma predeterminada, es `PROJECT_ROOT\packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="6afa7-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="6afa7-127">No permite actualizar el archivo de bloqueo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="6afa7-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="6afa7-128">*(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el comando, que tiene prioridad sobre `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="6afa7-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="6afa7-129">*(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando.</span><span class="sxs-lookup"><span data-stu-id="6afa7-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="6afa7-130">Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="6afa7-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="6afa7-131">De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6afa7-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="6afa7-132">Impide que NuGet use paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="6afa7-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="6afa7-133">Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="6afa7-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="6afa7-134">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="6afa7-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="6afa7-135">Especifica la carpeta en la que se instalan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="6afa7-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="6afa7-136">Si no se especifica ninguna carpeta, se usa la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="6afa7-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="6afa7-137">Obligatorio al restaurar con un `packages.config` archivo a menos `PackagesDirectory` que `SolutionDirectory` se use o.</span><span class="sxs-lookup"><span data-stu-id="6afa7-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="6afa7-138">Especifica los tipos de archivos que se van a guardar después de la instalación del paquete: uno de `nuspec` , `nupkg` o `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="6afa7-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="6afa7-139">Igual a `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="6afa7-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="6afa7-140">Obligatorio al restaurar con un `packages.config` archivo a menos `OutputDirectory` que `SolutionDirectory` se use o.</span><span class="sxs-lookup"><span data-stu-id="6afa7-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="6afa7-141">Tiempo de espera en segundos para resolver las referencias entre proyectos.</span><span class="sxs-lookup"><span data-stu-id="6afa7-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="6afa7-142">*(4.0 +)* Restaura todos los proyectos de referencias para los proyectos de UWP y .NET Core.</span><span class="sxs-lookup"><span data-stu-id="6afa7-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="6afa7-143">No se aplica a los proyectos que usan `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="6afa7-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="6afa7-144">Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="6afa7-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="6afa7-145">Para obtener más información, vea [restauración de paquetes](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="6afa7-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="6afa7-146">Especifica la carpeta de la solución.</span><span class="sxs-lookup"><span data-stu-id="6afa7-146">Specifies the solution folder.</span></span> <span data-ttu-id="6afa7-147">No es válido al restaurar los paquetes de una solución.</span><span class="sxs-lookup"><span data-stu-id="6afa7-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="6afa7-148">Obligatorio al restaurar con un `packages.config` archivo a menos `PackagesDirectory` que `OutputDirectory` se use o.</span><span class="sxs-lookup"><span data-stu-id="6afa7-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="6afa7-149">Especifica la lista de orígenes de paquetes (como direcciones URL) que se va a usar para la restauración.</span><span class="sxs-lookup"><span data-stu-id="6afa7-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="6afa7-150">Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, consulte [configuración del comportamiento de NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6afa7-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="6afa7-151">Use un punto y coma para separar las entradas de la lista.</span><span class="sxs-lookup"><span data-stu-id="6afa7-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="6afa7-152">Habilita la generación del archivo de bloqueo del proyecto y su uso con la restauración.</span><span class="sxs-lookup"><span data-stu-id="6afa7-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="6afa7-153">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="6afa7-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="6afa7-154">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6afa7-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="6afa7-155">Observaciones</span><span class="sxs-lookup"><span data-stu-id="6afa7-155">Remarks</span></span>

<span data-ttu-id="6afa7-156">El comando restore realiza los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6afa7-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="6afa7-157">Determine el modo de operación del comando restore.</span><span class="sxs-lookup"><span data-stu-id="6afa7-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="6afa7-158">tipo de archivo projectPath</span><span class="sxs-lookup"><span data-stu-id="6afa7-158">projectPath file type</span></span> | <span data-ttu-id="6afa7-159">Comportamiento</span><span class="sxs-lookup"><span data-stu-id="6afa7-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="6afa7-160">Solución (carpeta)</span><span class="sxs-lookup"><span data-stu-id="6afa7-160">Solution (folder)</span></span> | <span data-ttu-id="6afa7-161">NuGet busca un `.sln` archivo y lo utiliza si se encuentra; de lo contrario, produce un error.</span><span class="sxs-lookup"><span data-stu-id="6afa7-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="6afa7-162">`(SolutionDir)\.nuget` se utiliza como carpeta de inicio.</span><span class="sxs-lookup"><span data-stu-id="6afa7-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="6afa7-163">Archivo `.sln`</span><span class="sxs-lookup"><span data-stu-id="6afa7-163">`.sln` file</span></span> | <span data-ttu-id="6afa7-164">Restaure los paquetes identificados por la solución; proporciona un error si `-SolutionDirectory` se usa.</span><span class="sxs-lookup"><span data-stu-id="6afa7-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="6afa7-165">`$(SolutionDir)\.nuget` se utiliza como carpeta de inicio.</span><span class="sxs-lookup"><span data-stu-id="6afa7-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="6afa7-166">`packages.config` o archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="6afa7-166">`packages.config` or project file</span></span> | <span data-ttu-id="6afa7-167">Restaure los paquetes enumerados en el archivo, resolviendo e instalando las dependencias.</span><span class="sxs-lookup"><span data-stu-id="6afa7-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="6afa7-168">Otro tipo de archivo</span><span class="sxs-lookup"><span data-stu-id="6afa7-168">Other file type</span></span> | <span data-ttu-id="6afa7-169">Se supone que el archivo es un `.sln` archivo como el anterior; si no es una solución, NuGet genera un error.</span><span class="sxs-lookup"><span data-stu-id="6afa7-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="6afa7-170">(no se ha especificado projectPath)</span><span class="sxs-lookup"><span data-stu-id="6afa7-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="6afa7-171">NuGet busca archivos de solución en la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="6afa7-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="6afa7-172">Si se encuentra un solo archivo, se utilizará uno para restaurar los paquetes; Si se encuentran varias soluciones, NuGet genera un error.</span><span class="sxs-lookup"><span data-stu-id="6afa7-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="6afa7-173">Si no hay ningún archivo de solución, NuGet busca `packages.config` y lo usa para restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="6afa7-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="6afa7-174">Si no se encuentra ninguna solución o `packages.config` archivo, NuGet genera un error.</span><span class="sxs-lookup"><span data-stu-id="6afa7-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="6afa7-175">Determine la carpeta Packages con el siguiente orden de prioridad (NuGet genera un error si no se encuentra ninguna de estas carpetas):</span><span class="sxs-lookup"><span data-stu-id="6afa7-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="6afa7-176">La carpeta especificada con `-PackagesDirectory` .</span><span class="sxs-lookup"><span data-stu-id="6afa7-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="6afa7-177">El `repositoryPath` valor de `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="6afa7-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="6afa7-178">La carpeta especificada con `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="6afa7-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="6afa7-179">Al restaurar paquetes para una solución, NuGet hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6afa7-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="6afa7-180">Carga el archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="6afa7-180">Loads the solution file.</span></span>
    - <span data-ttu-id="6afa7-181">Restaura los paquetes de nivel de solución que aparecen en `$(SolutionDir)\.nuget\packages.config` la `packages` carpeta.</span><span class="sxs-lookup"><span data-stu-id="6afa7-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="6afa7-182">Restaure los paquetes `$(ProjectDir)\packages.config` que aparecen en la `packages` carpeta.</span><span class="sxs-lookup"><span data-stu-id="6afa7-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="6afa7-183">Para cada paquete especificado, restaure el paquete en paralelo, a menos que `-DisableParallelProcessing` se especifique.</span><span class="sxs-lookup"><span data-stu-id="6afa7-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="6afa7-184">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6afa7-184">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
