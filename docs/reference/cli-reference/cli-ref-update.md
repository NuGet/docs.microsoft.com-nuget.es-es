---
title: Comando de actualización de la CLI de NuGet
description: Referencia del comando nuget.exe update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323653"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="c2ae3-103">Comando update (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="c2ae3-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="c2ae3-104">**Se aplica a: consumo de** &bullet; **paquetes Versiones admitidas:** todas</span><span class="sxs-lookup"><span data-stu-id="c2ae3-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c2ae3-105">Actualiza todos los paquetes de un proyecto (mediante `packages.config`) a las versiones más recientes disponibles.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="c2ae3-106">Se recomienda ejecutar ["restore"](cli-ref-restore.md) antes de ejecutar `update` .</span><span class="sxs-lookup"><span data-stu-id="c2ae3-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="c2ae3-107">(Para actualizar un paquete individual, use sin especificar un número de versión, en cuyo caso [`nuget install`](cli-ref-install.md) NuGet instala la versión más reciente).</span><span class="sxs-lookup"><span data-stu-id="c2ae3-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="c2ae3-108">Nota: no funciona con la CLI que se ejecuta `update` en Mono (Mac OSX o Linux) ni cuando se usa el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="c2ae3-109">El `update` comando también actualiza las referencias de ensamblado en el archivo de proyecto, siempre que esas referencias ya existan.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="c2ae3-110">Si un paquete actualizado tiene un ensamblado agregado, no se agrega *una* nueva referencia.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="c2ae3-111">Las nuevas dependencias de paquete tampoco tienen sus referencias de ensamblado agregadas.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="c2ae3-112">Para incluir estas operaciones como parte de una actualización, actualice el paquete en Visual Studio mediante la interfaz Administrador de paquetes usuario o la Administrador de paquetes consola.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="c2ae3-113">Este comando también se puede usar para actualizar nuget.exe mediante la *marca -self.*</span><span class="sxs-lookup"><span data-stu-id="c2ae3-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="c2ae3-114">Uso</span><span class="sxs-lookup"><span data-stu-id="c2ae3-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="c2ae3-115">donde `<configPath>` identifica un archivo de solución o que enumera las `packages.config` dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="c2ae3-116">Opciones</span><span class="sxs-lookup"><span data-stu-id="c2ae3-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c2ae3-117">Archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c2ae3-118">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) `~/.nuget/NuGet/NuGet.Config` o o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c2ae3-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="c2ae3-119">Especifica la versión de los paquetes de dependencia que se usarán, que puede ser una de las siguientes:</span><span class="sxs-lookup"><span data-stu-id="c2ae3-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="c2ae3-120">*Más* bajo (valor predeterminado): la versión más baja</span><span class="sxs-lookup"><span data-stu-id="c2ae3-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="c2ae3-121">*HighestPatch:* la versión con la revisión principal, secundaria más baja y más alta</span><span class="sxs-lookup"><span data-stu-id="c2ae3-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="c2ae3-122">*HighestMinor:* la versión con la revisión más baja principal, secundaria más alta y más alta</span><span class="sxs-lookup"><span data-stu-id="c2ae3-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="c2ae3-123">*Más* alto: la versión más alta</span><span class="sxs-lookup"><span data-stu-id="c2ae3-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="c2ae3-124">*Omitir:* no se usarán paquetes de dependencia</span><span class="sxs-lookup"><span data-stu-id="c2ae3-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="c2ae3-125">Especifica la acción predeterminada cuando ya existe un archivo de un paquete en el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="c2ae3-126">Establezca en `Overwrite` para sobrescribir siempre los archivos.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="c2ae3-127">Establezca en `Ignore` para omitir archivos.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="c2ae3-128">La acción, el valor predeterminado, solicitará cada archivo en conflicto a menos que se especifique o , que se `PromptUser` aplicará a todos los archivos `OverwriteAll` `IgnoreAll` restantes.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c2ae3-129">*(3.5+)* Fuerza nuget.exe ejecutar mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c2ae3-130">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="c2ae3-131">Especifica una lista de los iDs de paquete que se actualizarán.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="c2ae3-132">*(4.0+)* Especifica la ruta de acceso de MSBuild que se usará con el comando , teniendo prioridad sobre `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="c2ae3-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="c2ae3-133">*(3.2+)* Especifica la versión de MSBuild que se usará con este comando.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="c2ae3-134">Los valores admitidos son 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="c2ae3-135">De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión instalada más alta de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c2ae3-136">Suprime las solicitudes de confirmación o entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="c2ae3-137">Permite actualizar a versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="c2ae3-138">Esta marca no es necesaria al actualizar los paquetes de versión preliminar que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="c2ae3-139">Especifica la carpeta local donde se instalan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="c2ae3-140">Especifica que solo se instalarán las actualizaciones con la versión más alta disponible dentro de la misma versión principal y secundaria que el paquete instalado.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="c2ae3-141">Actualizaciones `nuget.exe` a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="c2ae3-142">`-Source` se puede usar, pero se omiten todos los demás argumentos.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="c2ae3-143">Si no se proporciona ningún origen, comprueba `nuget.org` si hay actualizaciones independientemente de la `NuGet.Config` configuración.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="c2ae3-144">Especifica la lista de orígenes de paquetes (como direcciones URL) que se usarán para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="c2ae3-145">Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración; vea [Configuraciones comunes de NuGet.](../../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="c2ae3-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c2ae3-146">Especifica la cantidad de detalles que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c2ae3-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="c2ae3-147">Cuando se usa con un identificador de paquete, especifica la versión del paquete que se actualizará.</span><span class="sxs-lookup"><span data-stu-id="c2ae3-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="c2ae3-148">Consulte también Variables [de entorno.](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c2ae3-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c2ae3-149">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c2ae3-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
