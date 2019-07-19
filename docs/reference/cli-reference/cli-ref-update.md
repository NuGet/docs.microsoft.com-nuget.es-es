---
title: Comando de actualización de la CLI de NuGet
description: Referencia del comando de actualización de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327512"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="589ed-103">Comando update (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="589ed-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="589ed-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: todas</span><span class="sxs-lookup"><span data-stu-id="589ed-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="589ed-105">Actualiza todos los paquetes de un proyecto (mediante `packages.config`) a las versiones más recientes disponibles.</span><span class="sxs-lookup"><span data-stu-id="589ed-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="589ed-106">Se recomienda ejecutar [' restore '](cli-ref-restore.md) antes de ejecutar el `update`.</span><span class="sxs-lookup"><span data-stu-id="589ed-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="589ed-107">(Para actualizar un paquete individual, use [`nuget install`](cli-ref-install.md) sin especificar un número de versión, en cuyo caso NuGet instala la versión más reciente).</span><span class="sxs-lookup"><span data-stu-id="589ed-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="589ed-108">Nota: `update` no funciona con la CLI que se ejecuta en mono (Mac OSX o Linux) o cuando se usa el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="589ed-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="589ed-109">El `update` comando también actualiza las referencias de ensamblado en el archivo de proyecto, siempre que dichas referencias ya existan.</span><span class="sxs-lookup"><span data-stu-id="589ed-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="589ed-110">Si un paquete actualizado tiene un ensamblado agregado, *no* se agregará una nueva referencia.</span><span class="sxs-lookup"><span data-stu-id="589ed-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="589ed-111">Las dependencias de paquetes nuevas tampoco tienen agregadas las referencias de ensamblado.</span><span class="sxs-lookup"><span data-stu-id="589ed-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="589ed-112">Para incluir estas operaciones como parte de una actualización, actualice el paquete en Visual Studio mediante la interfaz de usuario del administrador de paquetes o la consola del administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="589ed-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="589ed-113">Este comando también se puede usar para actualizar el propio Nuget. exe mediante la marca *-Self* .</span><span class="sxs-lookup"><span data-stu-id="589ed-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="589ed-114">Uso</span><span class="sxs-lookup"><span data-stu-id="589ed-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="589ed-115">donde `<configPath>` identifica un `packages.config` archivo de solución o que muestra las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="589ed-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="589ed-116">Opciones</span><span class="sxs-lookup"><span data-stu-id="589ed-116">Options</span></span>

| <span data-ttu-id="589ed-117">Opción</span><span class="sxs-lookup"><span data-stu-id="589ed-117">Option</span></span> | <span data-ttu-id="589ed-118">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="589ed-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="589ed-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="589ed-119">ConfigFile</span></span> | <span data-ttu-id="589ed-120">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="589ed-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="589ed-121">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="589ed-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="589ed-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="589ed-122">FileConflictAction</span></span> | <span data-ttu-id="589ed-123">Especifica la acción que se llevará a cabo cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="589ed-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="589ed-124">Los valores son *sobrescribir, omitir, ninguno*.</span><span class="sxs-lookup"><span data-stu-id="589ed-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="589ed-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="589ed-125">ForceEnglishOutput</span></span> | <span data-ttu-id="589ed-126">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="589ed-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="589ed-127">Help</span><span class="sxs-lookup"><span data-stu-id="589ed-127">Help</span></span> | <span data-ttu-id="589ed-128">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="589ed-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="589ed-129">Id</span><span class="sxs-lookup"><span data-stu-id="589ed-129">Id</span></span> | <span data-ttu-id="589ed-130">Especifica una lista de los identificadores de paquete que se van a actualizar.</span><span class="sxs-lookup"><span data-stu-id="589ed-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="589ed-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="589ed-131">MSBuildPath</span></span> | <span data-ttu-id="589ed-132">*(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el `-MSBuildVersion`comando, que tiene prioridad sobre.</span><span class="sxs-lookup"><span data-stu-id="589ed-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="589ed-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="589ed-133">MSBuildVersion</span></span> | <span data-ttu-id="589ed-134">*(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando.</span><span class="sxs-lookup"><span data-stu-id="589ed-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="589ed-135">Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="589ed-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="589ed-136">De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="589ed-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="589ed-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="589ed-137">NonInteractive</span></span> | <span data-ttu-id="589ed-138">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="589ed-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="589ed-139">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="589ed-139">PreRelease</span></span> | <span data-ttu-id="589ed-140">Permite la actualización a versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="589ed-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="589ed-141">Esta marca no es necesaria cuando se actualizan los paquetes de versión preliminar que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="589ed-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="589ed-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="589ed-142">RepositoryPath</span></span> | <span data-ttu-id="589ed-143">Especifica la carpeta local en la que se instalan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="589ed-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="589ed-144">Segura</span><span class="sxs-lookup"><span data-stu-id="589ed-144">Safe</span></span> | <span data-ttu-id="589ed-145">Especifica que solo se instalarán las actualizaciones con la versión más alta disponible dentro de la misma versión principal y secundaria que el paquete instalado.</span><span class="sxs-lookup"><span data-stu-id="589ed-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="589ed-146">Mismo</span><span class="sxs-lookup"><span data-stu-id="589ed-146">Self</span></span> | <span data-ttu-id="589ed-147">Actualiza Nuget. exe a la versión más reciente; el resto de los argumentos se omiten.</span><span class="sxs-lookup"><span data-stu-id="589ed-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="589ed-148">source</span><span class="sxs-lookup"><span data-stu-id="589ed-148">Source</span></span> | <span data-ttu-id="589ed-149">Especifica la lista de orígenes de paquetes (como direcciones URL) que se usarán para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="589ed-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="589ed-150">Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, vea [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="589ed-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="589ed-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="589ed-151">Verbosity</span></span> | <span data-ttu-id="589ed-152">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="589ed-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="589ed-153">`Version`</span><span class="sxs-lookup"><span data-stu-id="589ed-153">Version</span></span> | <span data-ttu-id="589ed-154">Cuando se usa con un identificador de paquete, especifica la versión del paquete que se va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="589ed-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="589ed-155">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="589ed-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="589ed-156">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="589ed-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
