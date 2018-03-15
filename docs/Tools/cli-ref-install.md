---
title: "Comando de instalación de NuGet CLI | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referencia para el comando de instalación nuget.exe"
keywords: "NuGet instalar referencia, el comando de paquete de instalación"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8d5f53c833fb42c9fe37d0629eab33e8f0bc70d7
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="7ab7c-104">Instale el comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7ab7c-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="7ab7c-105">**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="7ab7c-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7ab7c-106">Descarga e instala un paquete en un proyecto, de forma predeterminada en la carpeta actual, usando orígenes del paquete especificado.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="7ab7c-107">Para descargar un paquete directamente fuera del contexto de un proyecto, visite la página del paquete en [nuget.org](https://www.nuget.org) y seleccione la **descargar** vínculo.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="7ab7c-108">Si no se especifica ningún origen de los indicados en el archivo de configuración global, `%APPDATA%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux), se utilizan.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="7ab7c-109">Vea [NuGet configurar comportamiento](../consume-packages/configuring-nuget-behavior.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="7ab7c-110">Si no se especifica ningún paquete específico, `install` instala todos los paquetes que se muestran en el proyecto `packages.config` archivo, lo que similar a [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7ab7c-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="7ab7c-111">El `install` comando no modifica un archivo de proyecto o `packages.config`; de este modo es similar a `restore` ya que se solo agrega paquetes en el disco, pero no cambia las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="7ab7c-112">Para agregar una dependencia, agregue un proyecto a través del Administrador de paquetes de interfaz de usuario o la consola en Visual Studio o modificar `packages.config` y, a continuación, ejecute cualquiera `install` o `restore`.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="7ab7c-113">Uso</span><span class="sxs-lookup"><span data-stu-id="7ab7c-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="7ab7c-114">donde `<packageID>` nombres el paquete que desea instalar (con la versión más reciente), o `<configFilePath>` identifica el `packages.config` archivo que enumera los paquetes que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="7ab7c-115">Puede indicar una versión específica con la `-Version` opción.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="7ab7c-116">Opciones</span><span class="sxs-lookup"><span data-stu-id="7ab7c-116">Options</span></span>

| <span data-ttu-id="7ab7c-117">Opción</span><span class="sxs-lookup"><span data-stu-id="7ab7c-117">Option</span></span> | <span data-ttu-id="7ab7c-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="7ab7c-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7ab7c-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7ab7c-119">ConfigFile</span></span> | <span data-ttu-id="7ab7c-120">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7ab7c-121">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7ab7c-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="7ab7c-122">DependencyVersion</span></span> | <span data-ttu-id="7ab7c-123">*(4.4 +)*  Especifica una versión concreta, reemplazar el comportamiento predeterminado de la resolución de dependencia.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="7ab7c-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="7ab7c-124">DisableParallelProcessing</span></span> | <span data-ttu-id="7ab7c-125">Deshabilita la instalación de varios paquetes en paralelo.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="7ab7c-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="7ab7c-126">ExcludeVersion</span></span> | <span data-ttu-id="7ab7c-127">Instala el paquete en una carpeta denominada con solo el nombre del paquete y no el número de versión.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="7ab7c-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="7ab7c-128">FallbackSource</span></span> | <span data-ttu-id="7ab7c-129">*(3.2 +)*  Una lista de orígenes de paquetes que se usará como de reservas en caso de que el paquete no se encuentra en el servidor principal o el origen predeterminado.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="7ab7c-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7ab7c-130">ForceEnglishOutput</span></span> | <span data-ttu-id="7ab7c-131">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7ab7c-132">Framework</span><span class="sxs-lookup"><span data-stu-id="7ab7c-132">Framework</span></span> | <span data-ttu-id="7ab7c-133">*(4.4 +)*  Utilizado para seleccionar las dependencias de .NET framework de destino.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="7ab7c-134">El valor predeterminado es 'Any' Si no se especifica.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="7ab7c-135">Ayuda</span><span class="sxs-lookup"><span data-stu-id="7ab7c-135">Help</span></span> | <span data-ttu-id="7ab7c-136">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="7ab7c-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="7ab7c-137">NoCache</span></span> | <span data-ttu-id="7ab7c-138">Impide que NuGet use paquetes de memorias caché del equipo local.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="7ab7c-139">No interactivo</span><span class="sxs-lookup"><span data-stu-id="7ab7c-139">NonInteractive</span></span> | <span data-ttu-id="7ab7c-140">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7ab7c-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="7ab7c-141">OutputDirectory</span></span> | <span data-ttu-id="7ab7c-142">Especifica la carpeta en la que se instalan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="7ab7c-143">Si no se especifica ninguna carpeta, se usa la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="7ab7c-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="7ab7c-144">PackageSaveMode</span></span> | <span data-ttu-id="7ab7c-145">Especifica los tipos de archivos para guardar después de la instalación de paquete: uno de `nuspec`, `nupkg`, o `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="7ab7c-146">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="7ab7c-146">PreRelease</span></span> | <span data-ttu-id="7ab7c-147">Permite que los paquetes de versión preliminar para instalarse.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="7ab7c-148">Esta marca no es necesaria al restaurar paquetes con `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="7ab7c-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="7ab7c-149">RequireConsent</span></span> | <span data-ttu-id="7ab7c-150">Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="7ab7c-151">Para obtener más información, consulte [la restauración del paquete](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7ab7c-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="7ab7c-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="7ab7c-152">SolutionDirectory</span></span> | <span data-ttu-id="7ab7c-153">Especifica la carpeta raíz de la solución para el que se va a restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="7ab7c-154">Origen</span><span class="sxs-lookup"><span data-stu-id="7ab7c-154">Source</span></span> | <span data-ttu-id="7ab7c-155">Especifica la lista de orígenes de paquetes (como las direcciones URL) para usar.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="7ab7c-156">Si se omite, el comando utiliza los orígenes proporcionados en archivos de configuración, consulte [NuGet configurar comportamiento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7ab7c-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="7ab7c-157">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="7ab7c-157">Verbosity</span></span> | <span data-ttu-id="7ab7c-158">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="7ab7c-159">Versión</span><span class="sxs-lookup"><span data-stu-id="7ab7c-159">Version</span></span> | <span data-ttu-id="7ab7c-160">Especifica la versión del paquete para instalar.</span><span class="sxs-lookup"><span data-stu-id="7ab7c-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="7ab7c-161">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7ab7c-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7ab7c-162">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7ab7c-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
