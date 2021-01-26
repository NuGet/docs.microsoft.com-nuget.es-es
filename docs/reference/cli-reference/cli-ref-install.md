---
title: Comando de instalación de la CLI de NuGet
description: Referencia del comando de instalación de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779259"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="4717c-103">comando de instalación (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="4717c-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="4717c-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: todas</span><span class="sxs-lookup"><span data-stu-id="4717c-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4717c-105">Descarga e instala un paquete en un proyecto, de forma predeterminada en la carpeta actual, con los orígenes de paquete especificados.</span><span class="sxs-lookup"><span data-stu-id="4717c-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="4717c-106">Para descargar un paquete directamente fuera del contexto de un proyecto, visite la página del paquete en [Nuget.org](https://www.nuget.org) y seleccione el vínculo de **descarga** .</span><span class="sxs-lookup"><span data-stu-id="4717c-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="4717c-107">Si no se especifican orígenes, se usan los que aparecen en el archivo de configuración global, `%appdata%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="4717c-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="4717c-108">Consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="4717c-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="4717c-109">Si no se especifica ningún paquete específico, `install` instala todos los paquetes enumerados en el `packages.config` archivo del proyecto, lo que hace que sea similar a [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="4717c-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="4717c-110">El `install` comando no modifica un archivo de proyecto o `packages.config` ; de esta manera es similar a `restore` en que solo agrega paquetes al disco, pero no cambia las dependencias de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="4717c-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="4717c-111">Para agregar una dependencia, agregue un paquete a través de la interfaz de usuario del administrador de paquetes o la consola en Visual Studio, o bien modifique `packages.config` y, a continuación, ejecute `install` o `restore` .</span><span class="sxs-lookup"><span data-stu-id="4717c-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="4717c-112">Uso</span><span class="sxs-lookup"><span data-stu-id="4717c-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="4717c-113">donde `<packageID>` nombra el paquete que se va a instalar (con la versión más reciente) o `<configFilePath>` identifica el `packages.config` archivo que muestra los paquetes que se van a instalar.</span><span class="sxs-lookup"><span data-stu-id="4717c-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="4717c-114">Puede indicar una versión específica con la `-Version` opción.</span><span class="sxs-lookup"><span data-stu-id="4717c-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="4717c-115">Opciones</span><span class="sxs-lookup"><span data-stu-id="4717c-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="4717c-116">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="4717c-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4717c-117">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="4717c-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="4717c-118">*(4.4 +)* La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:</span><span class="sxs-lookup"><span data-stu-id="4717c-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="4717c-119">*Más bajo* (valor predeterminado): la versión más baja</span><span class="sxs-lookup"><span data-stu-id="4717c-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="4717c-120">*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</span><span class="sxs-lookup"><span data-stu-id="4717c-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="4717c-121">*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</span><span class="sxs-lookup"><span data-stu-id="4717c-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="4717c-122">*Más alto*: la versión más alta</span><span class="sxs-lookup"><span data-stu-id="4717c-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="4717c-123">*Omitir*: no se usarán paquetes de dependencia</span><span class="sxs-lookup"><span data-stu-id="4717c-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="4717c-124">Descargar directamente sin llenar ninguna caché con metadatos o binarios.</span><span class="sxs-lookup"><span data-stu-id="4717c-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="4717c-125">Deshabilita la instalación de varios paquetes en paralelo.</span><span class="sxs-lookup"><span data-stu-id="4717c-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="4717c-126">Instala el paquete en una carpeta denominada con solo el nombre del paquete y no el número de versión.</span><span class="sxs-lookup"><span data-stu-id="4717c-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="4717c-127">*(3,2 +)* Una lista de orígenes de paquetes que se usarán como reserva en caso de que el paquete no se encuentre en el origen principal o en el predeterminado.</span><span class="sxs-lookup"><span data-stu-id="4717c-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="4717c-128">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="4717c-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="4717c-129">*(4.4 +)* Plataforma de destino que se usa para seleccionar las dependencias.</span><span class="sxs-lookup"><span data-stu-id="4717c-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="4717c-130">Si no se especifica, el valor predeterminado es "any".</span><span class="sxs-lookup"><span data-stu-id="4717c-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="4717c-131">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="4717c-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="4717c-132">Impide que NuGet use paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="4717c-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="4717c-133">Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="4717c-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="4717c-134">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="4717c-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="4717c-135">Especifica la carpeta en la que se instalan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="4717c-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="4717c-136">Si no se especifica ninguna carpeta, se usa la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="4717c-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="4717c-137">Especifica los tipos de archivos que se van a guardar después de la instalación del paquete: uno de `nuspec` , `nupkg` o `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="4717c-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="4717c-138">Permite que se instalen paquetes de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="4717c-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="4717c-139">Esta marca no es necesaria al restaurar paquetes con `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="4717c-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="4717c-140">Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="4717c-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="4717c-141">Para obtener más información, vea [restauración de paquetes](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="4717c-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="4717c-142">Especifica la carpeta raíz de la solución para la que se van a restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="4717c-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="4717c-143">Especifica la lista de orígenes de paquetes (como direcciones URL) que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="4717c-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="4717c-144">Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, vea [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="4717c-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="4717c-145">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="4717c-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="4717c-146">Permite especificar la versión del paquete que se instalará.</span><span class="sxs-lookup"><span data-stu-id="4717c-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="4717c-147">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4717c-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4717c-148">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="4717c-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
