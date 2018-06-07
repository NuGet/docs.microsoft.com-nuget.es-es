---
title: Comando de actualización de NuGet CLI
description: Referencia para el comando de actualización nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39e269b10a0cf144d5971d2af9f82a606e0b6904
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817712"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="882d8-103">Comando update (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="882d8-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="882d8-104">**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="882d8-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="882d8-105">Actualiza todos los paquetes en un proyecto (mediante `packages.config`) a sus versiones más recientes disponibles.</span><span class="sxs-lookup"><span data-stu-id="882d8-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="882d8-106">Se recomienda ejecutar ['restore'](cli-ref-restore.md) antes de ejecutar el `update`.</span><span class="sxs-lookup"><span data-stu-id="882d8-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="882d8-107">(Para actualizar un paquete individual, utilice [ `nuget install` ](cli-ref-install.md) sin especificar un número de versión, en el que NuGet mayúscula instala la versión más reciente.)</span><span class="sxs-lookup"><span data-stu-id="882d8-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="882d8-108">Nota: `update` no funciona con la CLI ejecutando bajo Mono (Mac OSX o Linux) o cuando se usa el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="882d8-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="882d8-109">El `update` comando también actualiza las referencias de ensamblado en el archivo de proyecto, proporcionado por las que hace referencia ya existe.</span><span class="sxs-lookup"><span data-stu-id="882d8-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="882d8-110">Si un paquete actualizado no tiene un ensamblado agregado, es una nueva referencia *no* agregado.</span><span class="sxs-lookup"><span data-stu-id="882d8-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="882d8-111">También nuevas dependencias de paquete no tienen sus referencias de ensamblado agregados.</span><span class="sxs-lookup"><span data-stu-id="882d8-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="882d8-112">Para incluir estas operaciones como parte de una actualización, actualice el paquete en Visual Studio mediante la UI del Administrador de paquetes o la consola de administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="882d8-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="882d8-113">Este comando también puede utilizarse para actualizar nuget.exe propio mediante el *-self* marca.</span><span class="sxs-lookup"><span data-stu-id="882d8-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="882d8-114">Uso</span><span class="sxs-lookup"><span data-stu-id="882d8-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="882d8-115">donde `<configPath>` identifica ya sea un `packages.config` o un archivo de solución que enumera las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="882d8-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="882d8-116">Opciones</span><span class="sxs-lookup"><span data-stu-id="882d8-116">Options</span></span>

| <span data-ttu-id="882d8-117">Opción</span><span class="sxs-lookup"><span data-stu-id="882d8-117">Option</span></span> | <span data-ttu-id="882d8-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="882d8-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="882d8-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="882d8-119">ConfigFile</span></span> | <span data-ttu-id="882d8-120">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="882d8-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="882d8-121">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="882d8-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="882d8-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="882d8-122">FileConflictAction</span></span> | <span data-ttu-id="882d8-123">Especifica la acción que se realizará cuando se le pregunte para sobrescribir u omitir los archivos existentes al que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="882d8-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="882d8-124">Los valores son *sobrescribir, omitir, ninguno*.</span><span class="sxs-lookup"><span data-stu-id="882d8-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="882d8-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="882d8-125">ForceEnglishOutput</span></span> | <span data-ttu-id="882d8-126">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="882d8-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="882d8-127">Ayuda</span><span class="sxs-lookup"><span data-stu-id="882d8-127">Help</span></span> | <span data-ttu-id="882d8-128">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="882d8-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="882d8-129">Id.</span><span class="sxs-lookup"><span data-stu-id="882d8-129">Id</span></span> | <span data-ttu-id="882d8-130">Especifica una lista de identificadores para la actualización de paquete.</span><span class="sxs-lookup"><span data-stu-id="882d8-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="882d8-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="882d8-131">MSBuildPath</span></span> | <span data-ttu-id="882d8-132">*(4.0 +)*  Especifica la ruta de acceso de MSBuild para usar con el comando, tiene prioridad sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="882d8-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="882d8-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="882d8-133">MSBuildVersion</span></span> | <span data-ttu-id="882d8-134">*(3.2 +)*  Especifica la versión de MSBuild que se utilizará con este comando.</span><span class="sxs-lookup"><span data-stu-id="882d8-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="882d8-135">Valores admitidos son 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="882d8-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="882d8-136">De forma predeterminada, se seleccionará el MSBuild en la ruta de acceso, en caso contrario, valor predeterminado es la última versión instalada de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="882d8-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="882d8-137">No interactivo</span><span class="sxs-lookup"><span data-stu-id="882d8-137">NonInteractive</span></span> | <span data-ttu-id="882d8-138">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="882d8-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="882d8-139">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="882d8-139">PreRelease</span></span> | <span data-ttu-id="882d8-140">Permite la actualización a las versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="882d8-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="882d8-141">Esta marca no es necesaria al actualizar paquetes de versión preliminar que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="882d8-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="882d8-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="882d8-142">RepositoryPath</span></span> | <span data-ttu-id="882d8-143">Especifica la carpeta local donde están instalados los paquetes.</span><span class="sxs-lookup"><span data-stu-id="882d8-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="882d8-144">Seguridad de</span><span class="sxs-lookup"><span data-stu-id="882d8-144">Safe</span></span> | <span data-ttu-id="882d8-145">Especifica que solo se actualiza con la versión más reciente disponible dentro de la misma versión principal y secundaria tal y como se instalará el paquete instalado.</span><span class="sxs-lookup"><span data-stu-id="882d8-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="882d8-146">En sí mismo</span><span class="sxs-lookup"><span data-stu-id="882d8-146">Self</span></span> | <span data-ttu-id="882d8-147">Nuget.exe actualizaciones a la versión más reciente; todos los demás argumentos se pasan por alto.</span><span class="sxs-lookup"><span data-stu-id="882d8-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="882d8-148">Origen</span><span class="sxs-lookup"><span data-stu-id="882d8-148">Source</span></span> | <span data-ttu-id="882d8-149">Especifica la lista de orígenes de paquetes (como las direcciones URL) para utilizar para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="882d8-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="882d8-150">Si se omite, el comando utiliza los orígenes proporcionados en archivos de configuración, consulte [NuGet configurar comportamiento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="882d8-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="882d8-151">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="882d8-151">Verbosity</span></span> | <span data-ttu-id="882d8-152">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="882d8-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="882d8-153">Versión</span><span class="sxs-lookup"><span data-stu-id="882d8-153">Version</span></span> | <span data-ttu-id="882d8-154">Cuando se usa con un Id. de paquete, especifica la versión del paquete para actualizar.</span><span class="sxs-lookup"><span data-stu-id="882d8-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="882d8-155">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="882d8-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="882d8-156">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="882d8-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
