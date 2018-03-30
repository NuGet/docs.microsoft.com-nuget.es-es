---
title: Notas de la versión de NuGet 4.4 RTM | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de la versión de NuGet 4.3 RTM incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
keywords: Notas de la versión de NuGet 4.3 RTM, correcciones de errores, problemas, conocidos, características agregadas, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6c122dc3d9b576a2ea5f094746a830e5fab5637e
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="3c0f7-104">Notas de la versión de NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="3c0f7-104">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="3c0f7-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="3c0f7-106">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="3c0f7-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="3c0f7-107">Problemas con .NET 2.0 Standard con .NET Framework y NuGet</span><span class="sxs-lookup"><span data-stu-id="3c0f7-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="3c0f7-108">.NET Standard y sus herramientas se han diseñado de forma que los proyectos destinados a .NET Framework 4.6.1 puedan usar los paquetes y proyectos de NuGet que tienen como destino .NET Standard 2.0 o versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="3c0f7-109">[En este documento](https://github.com/dotnet/standard/issues/481) se resumen los problemas relacionados con ese escenario, el plan para abordarlos, así como soluciones alternativas que se pueden implementar con el estado actual de las herramientas.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="3c0f7-110">Mientras usa la Consola del Administrador de paquetes, puede que la tecla "Entrar" no funcione</span><span class="sxs-lookup"><span data-stu-id="3c0f7-110">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="3c0f7-111">Problema</span><span class="sxs-lookup"><span data-stu-id="3c0f7-111">Issue</span></span>

<span data-ttu-id="3c0f7-112">En algunas ocasiones, la tecla Entrar no funciona en la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-112">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="3c0f7-113">Si ve esto, revise el progreso de la corrección y proporcione información útil adicional sobre los pasos de reproducción.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-113">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="3c0f7-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="3c0f7-115">Solución</span><span class="sxs-lookup"><span data-stu-id="3c0f7-115">Workaround</span></span>

<span data-ttu-id="3c0f7-116">Reinicie Visual Studio y abra la consola de Administración de paquetes antes de abrir la solución.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-116">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="3c0f7-117">Como alternativa, intente eliminar el archivo `project.lock.json` y restaurarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-117">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="3c0f7-118">No se puede ver, agregar ni actualizar DotNetCLITools con el Administrador de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="3c0f7-118">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="3c0f7-119">Problema</span><span class="sxs-lookup"><span data-stu-id="3c0f7-119">Issue</span></span>

<span data-ttu-id="3c0f7-120">El Administrador de paquetes de NuGet no muestra ni permite agregar o actualizar DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-120">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="3c0f7-121">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="3c0f7-121">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="3c0f7-122">Solución</span><span class="sxs-lookup"><span data-stu-id="3c0f7-122">Workaround</span></span>

<span data-ttu-id="3c0f7-123">DotNetCLIToolReferences se debe editar manualmente en el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-123">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="3c0f7-124">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta</span><span class="sxs-lookup"><span data-stu-id="3c0f7-124">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="3c0f7-125">Problema</span><span class="sxs-lookup"><span data-stu-id="3c0f7-125">Issue</span></span>

<span data-ttu-id="3c0f7-126">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta, en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-126">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="3c0f7-127">Esto sucede cuando usa PackageReferences como el formato del administrador de paquete.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-127">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="3c0f7-128">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="3c0f7-128">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="3c0f7-129">Solución</span><span class="sxs-lookup"><span data-stu-id="3c0f7-129">Workaround</span></span>

<span data-ttu-id="3c0f7-130">Haga una restauración manual.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-130">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="3c0f7-131">Un paquete en un proyecto de .NET Core que contiene un ensamblado con una firma no válida puede desencadenar un bucle infinito de restauración</span><span class="sxs-lookup"><span data-stu-id="3c0f7-131">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="3c0f7-132">Problema</span><span class="sxs-lookup"><span data-stu-id="3c0f7-132">Issue</span></span>

<span data-ttu-id="3c0f7-133">En algunas ocasiones, al usar un paquete que contiene un ensamblado con una firma no válida o cuando la versión del paquete está establecida con el valor "DateTime", la restauración automática del paquete se ejecutará en un bucle infinito (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="3c0f7-133">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="3c0f7-134">Solución</span><span class="sxs-lookup"><span data-stu-id="3c0f7-134">Workaround</span></span>

<span data-ttu-id="3c0f7-135">No hay ninguna solución alternativa para este problema.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-135">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="3c0f7-136">Problemas corregidos en el período de NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="3c0f7-136">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="3c0f7-137">[Notas de la versión de NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md): enumera todos los problemas corregidos en NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="3c0f7-137">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="3c0f7-138">Características</span><span class="sxs-lookup"><span data-stu-id="3c0f7-138">Features</span></span>

- <span data-ttu-id="3c0f7-139">Compatibilidad con la carga de solución ligera en escenarios de PMC e interfaz de usuario de PM de NuGet: [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-139">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="3c0f7-140">El destino pack de msbuild debe tener un enlace público para ejecutar destinos de usuario antes que a sí mismo: [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-140">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="3c0f7-141">Característica: agregar el modificador dependencyVersion a nuget install: [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-141">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="3c0f7-142">uap10.0.TODO.0 se debe asignar a .NET Standard 2.0 para NuGet: [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-142">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="3c0f7-143">Admitir la SKU de Visual Studio Build Tools con msbuild /t:restore: [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-143">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="3c0f7-144">Durante la restauración, generar un error si la compatibilidad de .NET 4.6.1 para .NET Standard 2.0 es necesaria pero no está instalada: [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-144">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="3c0f7-145">Interfaz de usuario del cliente de reserva de prefijos de Id. de paquete: [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-145">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="3c0f7-146">Entregar componentes de NuGet localizados para admitir la localización de dotnet.exe: [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-146">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="3c0f7-147">Errores</span><span class="sxs-lookup"><span data-stu-id="3c0f7-147">Bugs</span></span>

- <span data-ttu-id="3c0f7-148">El uso de mayúsculas y minúsculas diferentes en las rutas de acceso de proyecto puede causar que la restauración pierda PackageReference: [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-148">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="3c0f7-149">Mover los códigos de error con números de advertencia al intervalo de error: [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-149">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="3c0f7-150">Error engañoso cuando se desconoce si la versión de .NET Standard es compatible la plataforma de destino: [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-150">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="3c0f7-151">Archivos de prueba con licencias confusas: [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-151">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="3c0f7-152">Faltan encabezados de licencia en las plantillas de prueba EndToEnd: [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-152">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="3c0f7-153">La restauración de packages.config muestra los errores como NU1000: [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-153">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="3c0f7-154">La instalación de nuget.exe debe tener DisableParallelProcessing en mono: [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-154">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="3c0f7-155">La instalación de nuget.exe deshabilita incorrectamente el almacenamiento en caché: [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-155">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="3c0f7-156">VS: la ejecución del comando restore para packages.config cuando se deshabilita la restauración muestra un mensaje incorrecto: [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-156">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="3c0f7-157">VS: la ejecución del comando restore cuando se deshabilita la restauración muestra un mensaje confuso: [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-157">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="3c0f7-158">GetRestoreDotnetCliToolsTask produce un error cuando faltan metadatos de la versión: [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-158">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="3c0f7-159">Agregar paquete de dotnet puede borrar las líneas vacías de un archivo csproj: [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-159">dotnet add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="3c0f7-160">Los nombres de origen de la configuración de credenciales en NuGet.Config distinguen mayúsculas de minúsculas: [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="3c0f7-161">Al habilitar GeneratePackageOnBuild se eliminó el historial de paquetes completo: [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="3c0f7-162">La restauración no restaurará los paquetes mono.cecil o semver, pero todos los demás se restauran:</span><span class="sxs-lookup"><span data-stu-id="3c0f7-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="3c0f7-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="3c0f7-164">Errores y advertencias: error incorrecto cuando un origen no está disponible:</span><span class="sxs-lookup"><span data-stu-id="3c0f7-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="3c0f7-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="3c0f7-166">[DesignConsistency] El texto de estado de la instalación de NuGet no se ve correctamente en el tema oscuro actual:</span><span class="sxs-lookup"><span data-stu-id="3c0f7-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="3c0f7-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="3c0f7-168">Actualizar los paquetes en las actualizaciones e instalaciones de la solución para todos los proyectos: [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="3c0f7-169">dotnet pack se comporta de forma diferente en TargetFramework que en TargetFrameworks: [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-169">dotnet pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="3c0f7-170">Los archivos DLL incluidos en la carpeta Tools generan advertencias: [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-170">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="3c0f7-171">NuGet.ContentModel consume demasiada memoria para las operaciones de cadena: [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-171">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="3c0f7-172">RuntimeEnvironmentHelper.IsLinux devuelve true para OSX: [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-172">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="3c0f7-173">"dotnet pack" coloca nuspec en obj en lugar de obj\Debug: [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-173">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="3c0f7-174">Actualización de paquetes NuGet muy lenta: [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-174">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="3c0f7-175">CPS no está sincronizado con la restauración con soluciones más grandes en las que no se ha activado LSL (restauración de solución ligera): [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-175">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="3c0f7-176">SemVer 2.0: nuget pack con la versión proporcionada ignora los metadatos (3.5.0-rtm-1938): [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-176">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="3c0f7-177">install package de Nuget.exe (3.+) con el número de versión y la marca ExcludeVersion no actualiza el paquete a la versión más reciente: [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-177">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="3c0f7-178">La restauración de project.json debe advertir si los paquetes de nivel superior infringen las restricciones: [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-178">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="3c0f7-179">-ConfigFile no establece la configuración personalizada en el comando install: [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-179">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="3c0f7-180">La instalación de nuget.exe no respeta el modificador "-DisableParallelProcessing": [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-180">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="3c0f7-181">En DotNet.exe o msbuild.exe se siguen usando orígenes deshabilitados: [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-181">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="3c0f7-182">Corregir bloqueos en el escenario de LSL: [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-182">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="3c0f7-183">DCR</span><span class="sxs-lookup"><span data-stu-id="3c0f7-183">DCRs</span></span>

- <span data-ttu-id="3c0f7-184">Compatibilidad con TargetFramework en nuget.exe install: [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-184">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="3c0f7-185">Agregar cadenas UserAgent de la tarea de msbuild diferentes (netcore frente a msbuild de escritorio): [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-185">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="3c0f7-186">PackagePathResolver.GetPackageDirectoryName debe ser virtual: [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-186">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="3c0f7-187">[DesignConsistency] Aparece un mensaje confuso al agregar un paquete NuGet: [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-187">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="3c0f7-188">[Advertencias y errores] NoWarn no fluye de manera transitiva a través de las referencias de P2P: [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-188">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="3c0f7-189">Carga de solución ligera: núcleo común para la interfaz de usuario de PM, PMC e IV: [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-189">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="3c0f7-190">Carga de solución ligera: compatibilidad con PMC: [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-190">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="3c0f7-191">Agregar compatibilidad para el destino de MSBuild previo a la restauración que genera Visual Studio: [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-191">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="3c0f7-192">Agregar un destino público a NuGet.targets al que se pueda hacer referencia mediante BeforeTargets: [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-192">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="3c0f7-193">El destino de pack no puede crear contentFile con acciones de compilación correctamente: [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-193">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="3c0f7-194">RestoreOperationLogger.Do bloquea los subprocesos del grupo de subprocesos: [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-194">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="3c0f7-195">Docs</span><span class="sxs-lookup"><span data-stu-id="3c0f7-195">Docs</span></span>

- <span data-ttu-id="3c0f7-196">Documentos para las marcas DependencyVersion y Framework del comando Install: [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-196">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="3c0f7-197">Actualización de la documentación de advertencias y errores de NuGet: [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="3c0f7-197">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="3c0f7-198">Vínculos a problemas de GitHub corregidos en 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="3c0f7-198">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="3c0f7-199">Lista de problemas 1</span><span class="sxs-lookup"><span data-stu-id="3c0f7-199">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="3c0f7-200">Lista de problemas 2</span><span class="sxs-lookup"><span data-stu-id="3c0f7-200">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="3c0f7-201">Lista de problemas 3</span><span class="sxs-lookup"><span data-stu-id="3c0f7-201">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
