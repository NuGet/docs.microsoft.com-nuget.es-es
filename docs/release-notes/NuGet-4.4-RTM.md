---
title: Notas de la versión de NuGet 4.4 RTM
description: Notas de la versión de NuGet 4.3 RTM incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498695"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="2566a-103">Notas de la versión de NuGet 4.4</span><span class="sxs-lookup"><span data-stu-id="2566a-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="2566a-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="2566a-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="2566a-105">Resumen: Novedades de la versión 4.4.0</span><span class="sxs-lookup"><span data-stu-id="2566a-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="2566a-106">Resumen: Novedades de la versión 4.4.2</span><span class="sxs-lookup"><span data-stu-id="2566a-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="2566a-107">Corrección de seguridad: Premisos demasiado amplios de los archivos creados en ~/.nuget: [n.º 7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="2566a-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="2566a-108">Resumen: Novedades de la versión 4.4.3</span><span class="sxs-lookup"><span data-stu-id="2566a-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="2566a-109">Corrección de seguridad: Posible ruta relativa de los archivos de NUPKG por encima del directorio NUPKG: [n.º 7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="2566a-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="2566a-110">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="2566a-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="2566a-111">Problemas con .NET 2.0 Standard con .NET Framework y NuGet</span><span class="sxs-lookup"><span data-stu-id="2566a-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="2566a-112">.NET Standard y sus herramientas se han diseñado de forma que los proyectos destinados a .NET Framework 4.6.1 puedan usar los paquetes y proyectos de NuGet que tienen como destino .NET Standard 2.0 o versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="2566a-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="2566a-113">[En este documento](https://github.com/dotnet/standard/issues/481) se resumen los problemas relacionados con ese escenario, el plan para abordarlos, así como soluciones alternativas que se pueden implementar con el estado actual de las herramientas.</span><span class="sxs-lookup"><span data-stu-id="2566a-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="2566a-114">Mientras usa la Consola del Administrador de paquetes, puede que la tecla "Entrar" no funcione</span><span class="sxs-lookup"><span data-stu-id="2566a-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="2566a-115">Problema</span><span class="sxs-lookup"><span data-stu-id="2566a-115">Issue</span></span>

<span data-ttu-id="2566a-116">En algunas ocasiones, la tecla Entrar no funciona en la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="2566a-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="2566a-117">Si ve esto, revise el progreso de la corrección y proporcione información útil adicional sobre los pasos de reproducción.</span><span class="sxs-lookup"><span data-stu-id="2566a-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="2566a-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="2566a-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="2566a-119">Solución</span><span class="sxs-lookup"><span data-stu-id="2566a-119">Workaround</span></span>

<span data-ttu-id="2566a-120">Reinicie Visual Studio y abra la consola de Administración de paquetes antes de abrir la solución.</span><span class="sxs-lookup"><span data-stu-id="2566a-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="2566a-121">Como alternativa, intente eliminar el archivo `project.lock.json` y restaurarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2566a-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="2566a-122">No se puede ver, agregar ni actualizar DotNetCLITools con el Administrador de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="2566a-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="2566a-123">Problema</span><span class="sxs-lookup"><span data-stu-id="2566a-123">Issue</span></span>

<span data-ttu-id="2566a-124">El Administrador de paquetes de NuGet no muestra ni permite agregar o actualizar DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="2566a-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="2566a-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="2566a-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="2566a-126">Solución</span><span class="sxs-lookup"><span data-stu-id="2566a-126">Workaround</span></span>

<span data-ttu-id="2566a-127">DotNetCLIToolReferences se debe editar manualmente en el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2566a-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="2566a-128">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta</span><span class="sxs-lookup"><span data-stu-id="2566a-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="2566a-129">Problema</span><span class="sxs-lookup"><span data-stu-id="2566a-129">Issue</span></span>

<span data-ttu-id="2566a-130">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta, en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2566a-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="2566a-131">Esto sucede cuando usa PackageReferences como el formato del administrador de paquete.</span><span class="sxs-lookup"><span data-stu-id="2566a-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="2566a-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="2566a-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="2566a-133">Solución</span><span class="sxs-lookup"><span data-stu-id="2566a-133">Workaround</span></span>

<span data-ttu-id="2566a-134">Haga una restauración manual.</span><span class="sxs-lookup"><span data-stu-id="2566a-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="2566a-135">Un paquete en un proyecto de .NET Core que contiene un ensamblado con una firma no válida puede desencadenar un bucle infinito de restauración</span><span class="sxs-lookup"><span data-stu-id="2566a-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="2566a-136">Problema</span><span class="sxs-lookup"><span data-stu-id="2566a-136">Issue</span></span>

<span data-ttu-id="2566a-137">En algunas ocasiones, al usar un paquete que contiene un ensamblado con una firma no válida o cuando la versión del paquete está establecida con el valor "DateTime", la restauración automática del paquete se ejecutará en un bucle infinito (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="2566a-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="2566a-138">Solución</span><span class="sxs-lookup"><span data-stu-id="2566a-138">Workaround</span></span>

<span data-ttu-id="2566a-139">No hay ninguna solución alternativa para este problema.</span><span class="sxs-lookup"><span data-stu-id="2566a-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="2566a-140">Problemas corregidos en el período de NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="2566a-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="2566a-141">[Notas de la versión de NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md): enumera todos los problemas corregidos en NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="2566a-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="2566a-142">Características</span><span class="sxs-lookup"><span data-stu-id="2566a-142">Features</span></span>

- <span data-ttu-id="2566a-143">Compatibilidad con la carga de solución ligera en escenarios de PMC e interfaz de usuario de PM de NuGet: [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="2566a-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="2566a-144">El destino pack de msbuild debe tener un enlace público para ejecutar destinos de usuario antes que a sí mismo: [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="2566a-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="2566a-145">Característica: incorporación del modificador dependencyVersion a nuget install: [n.º 1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="2566a-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="2566a-146">uap10.0.TODO.0 se debe asignar a .NET Standard 2.0 para NuGet: [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="2566a-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="2566a-147">Admitir la SKU de Visual Studio Build Tools con msbuild /t:restore: [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="2566a-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="2566a-148">Durante la restauración, generar un error si la compatibilidad de .NET 4.6.1 para .NET Standard 2.0 es necesaria pero no está instalada: [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="2566a-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="2566a-149">Interfaz de usuario del cliente de reserva de prefijos de Id. de paquete: [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="2566a-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="2566a-150">Entregar componentes de NuGet localizados para admitir la localización de dotnet.exe: [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="2566a-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="2566a-151">Errores</span><span class="sxs-lookup"><span data-stu-id="2566a-151">Bugs</span></span>

- <span data-ttu-id="2566a-152">El uso de mayúsculas y minúsculas diferentes en las rutas de acceso de proyecto puede causar que la restauración pierda PackageReference: [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="2566a-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="2566a-153">Mover los códigos de error con números de advertencia al intervalo de error: [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="2566a-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="2566a-154">Error engañoso cuando se desconoce si la versión de .NET Standard es compatible la plataforma de destino: [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="2566a-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="2566a-155">Archivos de prueba con licencias confusas: [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="2566a-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="2566a-156">Faltan encabezados de licencia en las plantillas de prueba EndToEnd: [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="2566a-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="2566a-157">La restauración de packages.config muestra los errores como NU1000: [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="2566a-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="2566a-158">La instalación de nuget.exe debe tener DisableParallelProcessing en mono: [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="2566a-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="2566a-159">La instalación de nuget.exe deshabilita incorrectamente el almacenamiento en caché: [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="2566a-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="2566a-160">VS: la ejecución del comando restore para packages.config cuando se deshabilita la restauración muestra un mensaje incorrecto: [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="2566a-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="2566a-161">VS: la ejecución del comando restore cuando se deshabilita la restauración muestra un mensaje confuso: [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="2566a-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="2566a-162">GetRestoreDotnetCliToolsTask produce un error cuando faltan metadatos de la versión: [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="2566a-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="2566a-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="2566a-163">dotnet</span></span>
  - <span data-ttu-id="2566a-164">dotnet add package puede borrar las líneas vacías de un archivo csproj: [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="2566a-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="2566a-165">Los nombres de origen de la configuración de credenciales en NuGet.Config distinguen mayúsculas de minúsculas: [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="2566a-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="2566a-166">Al habilitar GeneratePackageOnBuild se eliminó el historial de paquetes completo: [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="2566a-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="2566a-167">La restauración no restaurará los paquetes mono.cecil o semver, pero todos los demás se restauran:</span><span class="sxs-lookup"><span data-stu-id="2566a-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="2566a-168">[#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="2566a-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="2566a-169">Errores y advertencias: error incorrecto cuando un origen no está disponible:</span><span class="sxs-lookup"><span data-stu-id="2566a-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="2566a-170">[#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="2566a-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="2566a-171">[DesignConsistency] El texto de estado de la instalación de NuGet no se ve correctamente en el tema oscuro actual:</span><span class="sxs-lookup"><span data-stu-id="2566a-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="2566a-172">[#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="2566a-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="2566a-173">Actualizar los paquetes en las actualizaciones e instalaciones de la solución para todos los proyectos: [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="2566a-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="2566a-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="2566a-174">dotnet</span></span>
  - <span data-ttu-id="2566a-175">dotnetcore pack se comporta de forma diferente en TargetFramework que en TargetFrameworks: [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="2566a-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="2566a-176">Los archivos DLL incluidos en la carpeta Tools generan advertencias: [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="2566a-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="2566a-177">NuGet.ContentModel consume demasiada memoria para las operaciones de cadena: [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="2566a-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="2566a-178">RuntimeEnvironmentHelper.IsLinux devuelve true para OSX: [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="2566a-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="2566a-179">"dotnet pack" coloca nuspec en obj en lugar de obj\Debug: [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="2566a-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="2566a-180">Actualización de paquetes NuGet muy lenta: [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="2566a-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="2566a-181">CPS no está sincronizado con la restauración con soluciones más grandes en las que no se ha activado LSL (restauración de solución ligera): [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="2566a-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="2566a-182">SemVer 2.0: nuget pack con la versión proporcionada ignora los metadatos (3.5.0-rtm-1938): [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="2566a-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="2566a-183">install package de Nuget.exe (3.+) con el número de versión y la marca ExcludeVersion no actualiza el paquete a la versión más reciente: [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="2566a-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="2566a-184">La restauración de project.json debe advertir si los paquetes de nivel superior infringen las restricciones: [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="2566a-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="2566a-185">-ConfigFile no establece la configuración personalizada en el comando install: [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="2566a-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="2566a-186">La instalación de nuget.exe no respeta el modificador "-DisableParallelProcessing": [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="2566a-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="2566a-187">En DotNet.exe o msbuild.exe se siguen usando orígenes deshabilitados: [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="2566a-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="2566a-188">Corregir bloqueos en el escenario de LSL: [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="2566a-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="2566a-189">DCR</span><span class="sxs-lookup"><span data-stu-id="2566a-189">DCRs</span></span>

- <span data-ttu-id="2566a-190">Compatibilidad con TargetFramework en nuget.exe install: [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="2566a-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="2566a-191">Agregar cadenas UserAgent de la tarea de msbuild diferentes (netcore frente a msbuild de escritorio): [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="2566a-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="2566a-192">PackagePathResolver.GetPackageDirectoryName debe ser virtual: [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="2566a-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="2566a-193">[DesignConsistency] Aparece un mensaje confuso al agregar un paquete NuGet: [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="2566a-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="2566a-194">[Advertencias y errores] NoWarn no fluye de manera transitiva a través de las referencias de P2P: [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="2566a-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="2566a-195">Carga de solución ligera: núcleo común para la IU de IV, PM y PMC: [n.º 5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="2566a-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="2566a-196">Carga de solución ligera: compatibilidad con PMC: [n.º 5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="2566a-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="2566a-197">Agregar compatibilidad para el destino de MSBuild previo a la restauración que genera Visual Studio: [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="2566a-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="2566a-198">Agregar un destino público a NuGet.targets al que se pueda hacer referencia mediante BeforeTargets: [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="2566a-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="2566a-199">Imposibilidad de crear correctamente contentFile con acciones de compilación por parte del destino del paquete: [n.º 4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="2566a-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="2566a-200">RestoreOperationLogger.Do bloquea los subprocesos del grupo de subprocesos: [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="2566a-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="2566a-201">Docs</span><span class="sxs-lookup"><span data-stu-id="2566a-201">Docs</span></span>

- <span data-ttu-id="2566a-202">Documentos para las marcas DependencyVersion y Framework del comando Install: [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="2566a-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="2566a-203">Actualización de la documentación de advertencias y errores de NuGet: [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="2566a-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="2566a-204">Vínculos a problemas de GitHub corregidos en 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="2566a-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="2566a-205">Lista de problemas 1</span><span class="sxs-lookup"><span data-stu-id="2566a-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="2566a-206">Lista de problemas 2</span><span class="sxs-lookup"><span data-stu-id="2566a-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="2566a-207">Lista de problemas 3</span><span class="sxs-lookup"><span data-stu-id="2566a-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
