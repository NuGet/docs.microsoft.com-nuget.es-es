---
title: "Comando de instalación de NuGet CLI | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Referencia para el comando de instalación nuget.exe"
keywords: "NuGet instalar referencia, el comando de paquete de instalación"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="5816c-104">Instale el comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5816c-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="5816c-105">**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="5816c-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5816c-106">Descarga e instala un paquete en un proyecto, de forma predeterminada en la carpeta actual, usando orígenes del paquete especificado.</span><span class="sxs-lookup"><span data-stu-id="5816c-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="5816c-107">Para descargar un paquete directamente fuera del contexto de un proyecto, visite la página del paquete en [nuget.org](https://www.nuget.org) y seleccione la **descargar** vínculo.</span><span class="sxs-lookup"><span data-stu-id="5816c-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span> 

<span data-ttu-id="5816c-108">Si no se especifica ningún origen de los indicados en el archivo de configuración global, `%APPDATA%\NuGet\NuGet.Config`, se utilizan.</span><span class="sxs-lookup"><span data-stu-id="5816c-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="5816c-109">Vea [configuración de comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="5816c-109">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="5816c-110">Si no se especifica ningún paquete específico, `install` instala todos los paquetes que se muestran en el proyecto `packages.config` archivo, lo que similar a [ `restore` ](#restore).</span><span class="sxs-lookup"><span data-stu-id="5816c-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](#restore).</span></span> <span data-ttu-id="5816c-111">(El `install` comando no funciona con `project.json`.)</span><span class="sxs-lookup"><span data-stu-id="5816c-111">(The `install` command does not work with `project.json`.)</span></span>

<span data-ttu-id="5816c-112">El `install` comando no modifica un archivo de proyecto o `packages.config`; de este modo es similar a `restore` ya que se solo agrega paquetes en el disco, pero no cambia las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="5816c-112">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="5816c-113">Para agregar una dependencia, agregue un proyecto a través del Administrador de paquetes de interfaz de usuario o la consola en Visual Studio o modificar `packages.config` y, a continuación, ejecute cualquiera `install` o `restore`.</span><span class="sxs-lookup"><span data-stu-id="5816c-113">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span> <span data-ttu-id="5816c-114">Para los proyectos con `project.json`, puede modificar ese archivo y, a continuación, ejecutar `restore`.</span><span class="sxs-lookup"><span data-stu-id="5816c-114">For projects using `project.json`, you can modify that file and then run `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="5816c-115">Uso</span><span class="sxs-lookup"><span data-stu-id="5816c-115">Usage</span></span>

```
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="5816c-116">donde `<packageID>` nombres el paquete que desea instalar (con la versión más reciente), o `<configFilePath>` identifica el `packages.config` archivo que enumera los paquetes que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="5816c-116">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="5816c-117">Puede indicar una versión específica con la `-Version` opción.</span><span class="sxs-lookup"><span data-stu-id="5816c-117">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="5816c-118">Opciones</span><span class="sxs-lookup"><span data-stu-id="5816c-118">Options</span></span>

| <span data-ttu-id="5816c-119">Opción</span><span class="sxs-lookup"><span data-stu-id="5816c-119">Option</span></span> | <span data-ttu-id="5816c-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="5816c-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5816c-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5816c-121">ConfigFile</span></span> | <span data-ttu-id="5816c-122">*(2.5 +)*  NuGet el archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="5816c-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="5816c-123">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="5816c-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="5816c-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="5816c-124">DisableParallelProcessing</span></span> | <span data-ttu-id="5816c-125">Deshabilita la instalación de varios paquetes en paralelo.</span><span class="sxs-lookup"><span data-stu-id="5816c-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="5816c-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="5816c-126">ExcludeVersion</span></span> | <span data-ttu-id="5816c-127">Instala el paquete en una carpeta denominada con solo el nombre del paquete y no el número de versión.</span><span class="sxs-lookup"><span data-stu-id="5816c-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="5816c-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="5816c-128">FallbackSource</span></span> | <span data-ttu-id="5816c-129">*(3.2 +)*  Una lista de orígenes de paquetes que se usará como de reservas en caso de que el paquete no se encuentra en el servidor principal o el origen predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5816c-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="5816c-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5816c-130">ForceEnglishOutput</span></span> | <span data-ttu-id="5816c-131">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="5816c-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5816c-132">Framework</span><span class="sxs-lookup"><span data-stu-id="5816c-132">Framework</span></span> | <span data-ttu-id="5816c-133">*(4.4 +)*  Utilizado para seleccionar las dependencias de .NET framework de destino.</span><span class="sxs-lookup"><span data-stu-id="5816c-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="5816c-134">El valor predeterminado es 'Any' Si no se especifica.</span><span class="sxs-lookup"><span data-stu-id="5816c-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="5816c-135">Ayuda</span><span class="sxs-lookup"><span data-stu-id="5816c-135">Help</span></span> | <span data-ttu-id="5816c-136">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="5816c-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="5816c-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="5816c-137">NoCache</span></span> | <span data-ttu-id="5816c-138">Impide que NuGet use paquetes de memorias caché del equipo local.</span><span class="sxs-lookup"><span data-stu-id="5816c-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="5816c-139">No interactivo</span><span class="sxs-lookup"><span data-stu-id="5816c-139">NonInteractive</span></span> | <span data-ttu-id="5816c-140">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="5816c-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5816c-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="5816c-141">OutputDirectory</span></span> | <span data-ttu-id="5816c-142">Especifica la carpeta en la que se instalan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="5816c-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="5816c-143">Si no se especifica ninguna carpeta, se usa la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="5816c-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="5816c-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="5816c-144">PackageSaveMode</span></span> | <span data-ttu-id="5816c-145">Especifica los tipos de archivos para guardar después de la instalación de paquete: uno de `nuspec`, `nupkg`, o `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="5816c-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="5816c-146">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="5816c-146">PreRelease</span></span> | <span data-ttu-id="5816c-147">Permite que los paquetes de versión preliminar para instalarse.</span><span class="sxs-lookup"><span data-stu-id="5816c-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="5816c-148">Esta marca no es necesaria al restaurar paquetes con `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="5816c-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="5816c-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="5816c-149">RequireConsent</span></span> | <span data-ttu-id="5816c-150">Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="5816c-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="5816c-151">Para obtener más información, consulte [la restauración del paquete](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="5816c-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="5816c-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="5816c-152">SolutionDirectory</span></span> | <span data-ttu-id="5816c-153">Especifica la carpeta raíz de la solución para el que se va a restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="5816c-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="5816c-154">Origen</span><span class="sxs-lookup"><span data-stu-id="5816c-154">Source</span></span> | <span data-ttu-id="5816c-155">Especifica la lista de orígenes de paquetes (como las direcciones URL) para usar.</span><span class="sxs-lookup"><span data-stu-id="5816c-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="5816c-156">Si se omite, el comando utiliza los orígenes proporcionados en archivos de configuración, consulte [NuGet configurar comportamiento](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5816c-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="5816c-157">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="5816c-157">Verbosity</span></span> | <span data-ttu-id="5816c-158">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="5816c-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="5816c-159">Versión</span><span class="sxs-lookup"><span data-stu-id="5816c-159">Version</span></span> | <span data-ttu-id="5816c-160">Especifica la versión del paquete para instalar.</span><span class="sxs-lookup"><span data-stu-id="5816c-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="5816c-161">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5816c-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5816c-162">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5816c-162">Examples</span></span>

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
