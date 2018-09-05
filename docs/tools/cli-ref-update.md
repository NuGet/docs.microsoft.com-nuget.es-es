---
title: Comando de actualización de la CLI de NuGet
description: Referencia del comando de actualización de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc34550b3669d83466318645987cfd3078bc3c18
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545105"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="142cc-103">Comando update (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="142cc-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="142cc-104">**Se aplica a:** consumo de paquetes &bullet; **versiones compatibles:** todas</span><span class="sxs-lookup"><span data-stu-id="142cc-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="142cc-105">Actualiza todos los paquetes en un proyecto (mediante `packages.config`) a sus versiones más recientes.</span><span class="sxs-lookup"><span data-stu-id="142cc-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="142cc-106">Se recomienda ejecutar ['restore'](cli-ref-restore.md) antes de ejecutar el `update`.</span><span class="sxs-lookup"><span data-stu-id="142cc-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="142cc-107">(Para actualizar un paquete individual, use [ `nuget install` ](cli-ref-install.md) sin especificar un número de versión, en el que caso NuGet instala la versión más reciente.)</span><span class="sxs-lookup"><span data-stu-id="142cc-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="142cc-108">Nota: `update` no funciona con la CLI que se ejecuta en Mono (Mac OSX o Linux) o cuando se usa el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="142cc-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="142cc-109">El `update` comando también actualiza las referencias de ensamblado en el archivo de proyecto, siempre que los que hace referencia ya existe.</span><span class="sxs-lookup"><span data-stu-id="142cc-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="142cc-110">Si un paquete actualizado tiene un ensamblado se ha agregado, es una nueva referencia *no* agregado.</span><span class="sxs-lookup"><span data-stu-id="142cc-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="142cc-111">También nuevas dependencias de paquete no tienen sus referencias de ensamblado agregados.</span><span class="sxs-lookup"><span data-stu-id="142cc-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="142cc-112">Para incluir estas operaciones como parte de una actualización, actualice el paquete en Visual Studio mediante la UI de administrador de paquetes o la consola de administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="142cc-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="142cc-113">Este comando también se puede usar para actualizar nuget.exe propio mediante el *-self* marca.</span><span class="sxs-lookup"><span data-stu-id="142cc-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="142cc-114">Uso</span><span class="sxs-lookup"><span data-stu-id="142cc-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="142cc-115">donde `<configPath>` identifica ya sea un `packages.config` o archivo de solución que se enumera las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="142cc-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="142cc-116">Opciones</span><span class="sxs-lookup"><span data-stu-id="142cc-116">Options</span></span>

| <span data-ttu-id="142cc-117">Opción</span><span class="sxs-lookup"><span data-stu-id="142cc-117">Option</span></span> | <span data-ttu-id="142cc-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="142cc-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="142cc-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="142cc-119">ConfigFile</span></span> | <span data-ttu-id="142cc-120">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="142cc-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="142cc-121">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="142cc-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="142cc-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="142cc-122">FileConflictAction</span></span> | <span data-ttu-id="142cc-123">Especifica la acción que se realizará cuando se le pida sobrescribir u omitir los archivos existentes que se hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="142cc-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="142cc-124">Los valores son *sobrescribir, omitir ninguno*.</span><span class="sxs-lookup"><span data-stu-id="142cc-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="142cc-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="142cc-125">ForceEnglishOutput</span></span> | <span data-ttu-id="142cc-126">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="142cc-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="142cc-127">Ayuda</span><span class="sxs-lookup"><span data-stu-id="142cc-127">Help</span></span> | <span data-ttu-id="142cc-128">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="142cc-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="142cc-129">Id.</span><span class="sxs-lookup"><span data-stu-id="142cc-129">Id</span></span> | <span data-ttu-id="142cc-130">Especifica una lista de identificadores para la actualización del paquete.</span><span class="sxs-lookup"><span data-stu-id="142cc-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="142cc-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="142cc-131">MSBuildPath</span></span> | <span data-ttu-id="142cc-132">*(4.0 y versiones posteriores)*  Especifica la ruta de acceso de MSBuild que use con el comando, tiene prioridad sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="142cc-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="142cc-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="142cc-133">MSBuildVersion</span></span> | <span data-ttu-id="142cc-134">*(3.2 y versiones posteriores)*  Especifica la versión de MSBuild que se usará con este comando.</span><span class="sxs-lookup"><span data-stu-id="142cc-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="142cc-135">Los valores admitidos son 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="142cc-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="142cc-136">De forma predeterminada que se selecciona la versión de MSBuild en su ruta de acceso, en caso contrario, el valor predeterminado es la última versión instalada de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="142cc-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="142cc-137">No interactivo</span><span class="sxs-lookup"><span data-stu-id="142cc-137">NonInteractive</span></span> | <span data-ttu-id="142cc-138">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="142cc-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="142cc-139">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="142cc-139">PreRelease</span></span> | <span data-ttu-id="142cc-140">Permite la actualización a las versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="142cc-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="142cc-141">Esta marca no es necesaria al actualizar paquetes de versión preliminar que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="142cc-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="142cc-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="142cc-142">RepositoryPath</span></span> | <span data-ttu-id="142cc-143">Especifica la carpeta local donde están instalados los paquetes.</span><span class="sxs-lookup"><span data-stu-id="142cc-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="142cc-144">Safe</span><span class="sxs-lookup"><span data-stu-id="142cc-144">Safe</span></span> | <span data-ttu-id="142cc-145">Especifica que sólo actualiza con la versión más alta disponible dentro de la misma versión principal y secundaria que se instalará el paquete instalado.</span><span class="sxs-lookup"><span data-stu-id="142cc-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="142cc-146">Self</span><span class="sxs-lookup"><span data-stu-id="142cc-146">Self</span></span> | <span data-ttu-id="142cc-147">Nuget.exe actualizaciones a la versión más reciente; todos los demás argumentos se pasan por alto.</span><span class="sxs-lookup"><span data-stu-id="142cc-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="142cc-148">Origen</span><span class="sxs-lookup"><span data-stu-id="142cc-148">Source</span></span> | <span data-ttu-id="142cc-149">Especifica la lista de orígenes de paquetes (como las direcciones URL) para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="142cc-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="142cc-150">Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, consulte [del comportamiento de configuración de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="142cc-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="142cc-151">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="142cc-151">Verbosity</span></span> | <span data-ttu-id="142cc-152">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="142cc-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="142cc-153">Versión</span><span class="sxs-lookup"><span data-stu-id="142cc-153">Version</span></span> | <span data-ttu-id="142cc-154">Cuando se usa con un Id. de paquete, especifica la versión del paquete para actualizar.</span><span class="sxs-lookup"><span data-stu-id="142cc-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="142cc-155">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="142cc-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="142cc-156">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="142cc-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
