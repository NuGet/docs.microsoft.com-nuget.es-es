---
title: Comando de actualización de la CLI de NuGet
description: Referencia del comando UPDATE de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: cfa7fdcc6af46fd5f4030ba424754291f697bc43
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779139"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="6397e-103">comando Update (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="6397e-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="6397e-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: todas</span><span class="sxs-lookup"><span data-stu-id="6397e-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6397e-105">Actualiza todos los paquetes de un proyecto (mediante `packages.config`) a las versiones más recientes disponibles.</span><span class="sxs-lookup"><span data-stu-id="6397e-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="6397e-106">Se recomienda ejecutar [' restore '](cli-ref-restore.md) antes de ejecutar el `update` .</span><span class="sxs-lookup"><span data-stu-id="6397e-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="6397e-107">(Para actualizar un paquete individual, use [`nuget install`](cli-ref-install.md) sin especificar un número de versión, en cuyo caso NuGet instala la versión más reciente).</span><span class="sxs-lookup"><span data-stu-id="6397e-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="6397e-108">Nota: no `update` funciona con la CLI que se ejecuta en mono (Mac OSX o Linux) o cuando se usa el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6397e-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="6397e-109">El `update` comando también actualiza las referencias de ensamblado en el archivo de proyecto, siempre que dichas referencias ya existan.</span><span class="sxs-lookup"><span data-stu-id="6397e-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="6397e-110">Si un paquete actualizado tiene un ensamblado agregado, *no* se agregará una nueva referencia.</span><span class="sxs-lookup"><span data-stu-id="6397e-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="6397e-111">Las dependencias de paquetes nuevas tampoco tienen agregadas las referencias de ensamblado.</span><span class="sxs-lookup"><span data-stu-id="6397e-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="6397e-112">Para incluir estas operaciones como parte de una actualización, actualice el paquete en Visual Studio mediante la interfaz de usuario del administrador de paquetes o la consola del administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="6397e-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="6397e-113">Este comando también se puede usar para actualizar nuget.exe mediante la marca *-Self* .</span><span class="sxs-lookup"><span data-stu-id="6397e-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="6397e-114">Uso</span><span class="sxs-lookup"><span data-stu-id="6397e-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="6397e-115">donde `<configPath>` identifica un `packages.config` archivo de solución o que muestra las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="6397e-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="6397e-116">Opciones</span><span class="sxs-lookup"><span data-stu-id="6397e-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="6397e-117">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="6397e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6397e-118">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6397e-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="6397e-119">Especifica la versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:</span><span class="sxs-lookup"><span data-stu-id="6397e-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="6397e-120">*Más bajo* (valor predeterminado): la versión más baja</span><span class="sxs-lookup"><span data-stu-id="6397e-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="6397e-121">*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</span><span class="sxs-lookup"><span data-stu-id="6397e-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="6397e-122">*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</span><span class="sxs-lookup"><span data-stu-id="6397e-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="6397e-123">*Más alto*: la versión más alta</span><span class="sxs-lookup"><span data-stu-id="6397e-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="6397e-124">*Omitir*: no se usarán paquetes de dependencia</span><span class="sxs-lookup"><span data-stu-id="6397e-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="6397e-125">Especifica la acción predeterminada cuando un archivo de un paquete ya existe en el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="6397e-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="6397e-126">Establezca en `Overwrite` para sobrescribir siempre los archivos.</span><span class="sxs-lookup"><span data-stu-id="6397e-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="6397e-127">Establezca en `Ignore` para omitir los archivos.</span><span class="sxs-lookup"><span data-stu-id="6397e-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="6397e-128">La `PromptUser` acción, de forma predeterminada, solicitará cada archivo conflictivo a menos `OverwriteAll` que `IgnoreAll` se proporcione o, que se aplicará a todos los archivos restantes.</span><span class="sxs-lookup"><span data-stu-id="6397e-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="6397e-129">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="6397e-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="6397e-130">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="6397e-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="6397e-131">Especifica una lista de los identificadores de paquete que se van a actualizar.</span><span class="sxs-lookup"><span data-stu-id="6397e-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="6397e-132">*(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el comando, que tiene prioridad sobre `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="6397e-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="6397e-133">*(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando.</span><span class="sxs-lookup"><span data-stu-id="6397e-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="6397e-134">Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="6397e-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="6397e-135">De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6397e-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="6397e-136">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="6397e-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="6397e-137">Permite la actualización a versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="6397e-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="6397e-138">Esta marca no es necesaria cuando se actualizan los paquetes de versión preliminar que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="6397e-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="6397e-139">Especifica la carpeta local en la que se instalan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="6397e-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="6397e-140">Especifica que solo se instalarán las actualizaciones con la versión más alta disponible dentro de la misma versión principal y secundaria que el paquete instalado.</span><span class="sxs-lookup"><span data-stu-id="6397e-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="6397e-141">Actualiza nuget.exe a la versión más reciente; el resto de los argumentos se omiten.</span><span class="sxs-lookup"><span data-stu-id="6397e-141">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="6397e-142">Especifica la lista de orígenes de paquetes (como direcciones URL) que se usarán para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="6397e-142">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="6397e-143">Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, vea [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6397e-143">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="6397e-144">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="6397e-144">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="6397e-145">Cuando se usa con un identificador de paquete, especifica la versión del paquete que se va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="6397e-145">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="6397e-146">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6397e-146">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6397e-147">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6397e-147">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
