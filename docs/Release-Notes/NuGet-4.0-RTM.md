---
title: "Notas de la versión de NuGet 4.0 RC | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 4.0 RTM incluidos problemas conocidos, correcciones de errores, características agregadas y DCR."
keywords: "Notas de la versión de NuGet 4.0 RTM, correcciones de errores, problemas, conocidos, características agregadas, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d1ab89f0decb64a64d04dc293e5273b577e8398b
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="a6b2e-104">Notas de la versión de NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="a6b2e-104">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="a6b2e-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye NuGet 4.0, que agrega compatibilidad para .NET Core, tiene una serie de correcciones de calidad y mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="a6b2e-106">Esta versión también ofrece varias mejoras, como la compatibilidad con PackageReference, comandos de NuGet como destinos de MSBuild, restauraciones de paquetes en segundo plano y mucho más.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a6b2e-107">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="a6b2e-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="a6b2e-108">Es posible que exista un error en la restauración de NuGet cuando tiene varios proyectos que hacen referencia a otro proyecto en una solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="a6b2e-109">Problema</span><span class="sxs-lookup"><span data-stu-id="a6b2e-109">Issue</span></span>

<span data-ttu-id="a6b2e-110">Es posible que la restauración de NuGet no funcione si, en una solución, tiene referencias de proyecto al mismo proyecto con un uso de mayúsculas distinto o con rutas de acceso relativas diferentes.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="a6b2e-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="a6b2e-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="a6b2e-112">Solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-112">Workaround</span></span>

<span data-ttu-id="a6b2e-113">Corrija el uso de mayúsculas o las rutas relativas para que sean iguales en todas las referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="a6b2e-114">Mientras usa la Consola del Administrador de paquetes, puede que la tecla "Entrar" no funcione</span><span class="sxs-lookup"><span data-stu-id="a6b2e-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="a6b2e-115">Problema</span><span class="sxs-lookup"><span data-stu-id="a6b2e-115">Issue</span></span>

<span data-ttu-id="a6b2e-116">En algunas ocasiones, la tecla Entrar no funciona en la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="a6b2e-117">Si ve esto, revise el progreso de la corrección y proporcione información útil adicional sobre los pasos de reproducción.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="a6b2e-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="a6b2e-119">Solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-119">Workaround</span></span>

<span data-ttu-id="a6b2e-120">Reinicie Visual Studio y abra la consola de Administración de paquetes antes de abrir la solución.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="a6b2e-121">Como alternativa, intente eliminar el archivo `project.lock.json` y restaurarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="a6b2e-122">En los proyectos de .NET Core, puede acabar en un bucle de restauración infinito cuando use un paquete que contenga un ensamblado con una signatura no válida</span><span class="sxs-lookup"><span data-stu-id="a6b2e-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="a6b2e-123">Problema</span><span class="sxs-lookup"><span data-stu-id="a6b2e-123">Issue</span></span>

<span data-ttu-id="a6b2e-124">En algunas ocasiones, cuando usa un paquete que contiene un ensamblado con una signatura no válida o cuando la versión del paquete está establecida con el tablero "DateTime", la restauración automática del paquete se ejecutará en un bucle infinito.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="a6b2e-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="a6b2e-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="a6b2e-126">Solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-126">Workaround</span></span>

<span data-ttu-id="a6b2e-127">No hay ninguna solución alternativa para este problema.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-127">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="a6b2e-128">No se puede ver, agregar ni actualizar DotNetCLITools con el Administrador de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="a6b2e-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="a6b2e-129">Problema</span><span class="sxs-lookup"><span data-stu-id="a6b2e-129">Issue</span></span>

<span data-ttu-id="a6b2e-130">El Administrador de paquetes de NuGet no muestra ni permite agregar o actualizar DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="a6b2e-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="a6b2e-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="a6b2e-132">Solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-132">Workaround</span></span>

<span data-ttu-id="a6b2e-133">DotNetCLIToolReferences se debe editar manualmente en el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="a6b2e-134">La restauración de NuGet presentará un error cuando establezca la propiedad PackageId para los proyectos</span><span class="sxs-lookup"><span data-stu-id="a6b2e-134">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="a6b2e-135">Problema</span><span class="sxs-lookup"><span data-stu-id="a6b2e-135">Issue</span></span>

<span data-ttu-id="a6b2e-136">En el caso de los proyectos de .NET Core, la restauración de NuGet en Visual Studio no respeta la propiedad PackageId de los proyectos.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="a6b2e-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="a6b2e-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="a6b2e-138">Solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-138">Workaround</span></span>

<span data-ttu-id="a6b2e-139">Ejecute la restauración con la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="a6b2e-140">Si el proyecto no tiene una carpeta "obj", puede que la restauración del paquete presente un error</span><span class="sxs-lookup"><span data-stu-id="a6b2e-140">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="a6b2e-141">Problema</span><span class="sxs-lookup"><span data-stu-id="a6b2e-141">Issue</span></span>

<span data-ttu-id="a6b2e-142">Visual Studio no puede restaurar PackageReferences si se eliminó la carpeta "obj".</span><span class="sxs-lookup"><span data-stu-id="a6b2e-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="a6b2e-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="a6b2e-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="a6b2e-144">Solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-144">Workaround</span></span>

<span data-ttu-id="a6b2e-145">Cree manualmente la carpeta "obj"; la restauración debería funcionar.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-145">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="a6b2e-146">Actualizar manualmente los paquetes con Update-Package en la consola puede presentar un error</span><span class="sxs-lookup"><span data-stu-id="a6b2e-146">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="a6b2e-147">Problema</span><span class="sxs-lookup"><span data-stu-id="a6b2e-147">Issue</span></span>

<span data-ttu-id="a6b2e-148">Usar Update-Package manualmente en la consola solo funciona una vez para los proyectos de PackageReferences que se acaban de convertir.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="a6b2e-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="a6b2e-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="a6b2e-150">Solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-150">Workaround</span></span>

<span data-ttu-id="a6b2e-151">No hay ninguna solución alternativa para este problema.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="a6b2e-152">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta</span><span class="sxs-lookup"><span data-stu-id="a6b2e-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="a6b2e-153">Problema</span><span class="sxs-lookup"><span data-stu-id="a6b2e-153">Issue</span></span>

<span data-ttu-id="a6b2e-154">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta, en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="a6b2e-155">Esto sucede cuando usa PackageReferences como el formato del administrador de paquete.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="a6b2e-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="a6b2e-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="a6b2e-157">Solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-157">Workaround</span></span>

<span data-ttu-id="a6b2e-158">Haga una restauración manual.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="a6b2e-159">Error de msbuild /t:restore cuando un proyecto dirigido a .NET461 hace referencia a otro proyecto dirigido a .NETStandard</span><span class="sxs-lookup"><span data-stu-id="a6b2e-159">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="a6b2e-160">Problema</span><span class="sxs-lookup"><span data-stu-id="a6b2e-160">Issue</span></span>

<span data-ttu-id="a6b2e-161">Error de msbuild /t:restore cuando un proyecto basado en PackageReference dirigido a .NET461 hace referencia a otro proyecto basado en PackageReference dirigido a .NETStandard.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="a6b2e-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="a6b2e-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="a6b2e-163">Solución</span><span class="sxs-lookup"><span data-stu-id="a6b2e-163">Workaround</span></span>

<span data-ttu-id="a6b2e-164">No hay ninguna solución alternativa para este problema.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="a6b2e-165">Problemas corregidos en el período de NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="a6b2e-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="a6b2e-166">[Notas de la versión de NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md): enumera todos los problemas corregidos en NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="a6b2e-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="a6b2e-167">Características</span><span class="sxs-lookup"><span data-stu-id="a6b2e-167">Features</span></span>

- <span data-ttu-id="a6b2e-168">Localizar cadenas en NuGet.Core.sln: [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-168">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="a6b2e-169">NuGet obliga a cargar proyectos de aplicación web en modo LSL: [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-169">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="a6b2e-170">Compatibilidad con AutoReferenced PackageReference para bloquear cambios de versiones en la interfaz de usuario para los paquetes "instalados mediante SDK": [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-170">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="a6b2e-171">Comunicar correctamente PackageSpec.Version para cualquier dependencia de proyecto (PackageRef): [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-171">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="a6b2e-172">Soporte para quitar referencias en `.csproj` de las líneas de comandos: [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-172">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="a6b2e-173">Compatibilidad con la restauración de proyectos PackageReference (normales y xplat) y la carga de solución ligera: [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-173">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="a6b2e-174">Soporte para agregar referencias de `.csproj` de las líneas de comandos: [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-174">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="a6b2e-175">Compatibilidad con la restauración de NuGet para la carga de solución ligera para `packages.config` o `project.json`: [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-175">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="a6b2e-176">Soporte de contentFiles en archivos de destinos generados por NuGet: [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-176">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="a6b2e-177">Establecer una CI Mono para la validación de nuget.exe en Mac con MSBuild: [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-177">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="a6b2e-178">Sacar NuGet de las dependencias de NuGet.Core v2: [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-178">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="a6b2e-179">Errores</span><span class="sxs-lookup"><span data-stu-id="a6b2e-179">Bugs</span></span>

- <span data-ttu-id="a6b2e-180">La restauración de NuGet en Visual Studio no respeta la propiedad PackageId de los proyectos: [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-180">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="a6b2e-181">Error ProjectSystemCache en NuGet al agregar un paquete en el paquete vsix: [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-181">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="a6b2e-182">El paquete genera una excepción si se usa IncludeSource en un proyecto con varios TFM: [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-182">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="a6b2e-183">VS 2017 RC3 se bloquea al usar una actualización de la administración de paquetes para toda la solución: [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-183">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="a6b2e-184">No se puede desinstalar un paquete recién instalado: [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-184">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="a6b2e-185">Al migrar a PackageRef, las soluciones híbridas tienen un comportamiento de restauración extraño: [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-185">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="a6b2e-186">Efectuar una compilación poco después de haber iniciado una operación de NuGet (instalación, actualización o restauración) puede hacer que VS se bloquee: [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-186">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="a6b2e-187">Suspensión de la interfaz de usuario: Interbloqueo al inicializar NuGet.SolutionRestoreManager.RestoreManagerPackage: [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-187">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="a6b2e-188">El comando add package debería agregar la versión como atributo en lugar de como elemento: [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-188">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="a6b2e-189">Se produce un error de dotnet restore foo.sln -- si las configuraciones de SLN generan proyectos duplicados (pero con una configuración diferente) al restaurar un gráfico: [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-189">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="a6b2e-190">Paquetes de solo contenido: [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="a6b2e-191">De forma predeterminada, optar por no mostrar la opción del selector de formato de paquete: [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="a6b2e-192">Rendimiento: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span><span class="sxs-lookup"><span data-stu-id="a6b2e-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="a6b2e-193">Línea base 26129.02: [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="a6b2e-194">Rendimiento: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="a6b2e-195">Línea base 26105: [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="a6b2e-196">Se produce un error en la nominación en proyectos de varios TFM: [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="a6b2e-197">Rendimiento: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span><span class="sxs-lookup"><span data-stu-id="a6b2e-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="a6b2e-198">Línea base 26123.04: [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="a6b2e-199">vsfeedback: Advertencias del paquete al fijar como destino netcoreapp1.1: [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="a6b2e-200">Se genera la excepción PathTooLongException al intentar agregar un paquete de NuGet a una aplicación web vacía de ASP.NET Core: [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="a6b2e-201">El paquete se ejecuta con demasiada frecuencia. Se produce un error en dotnet pack con "Existe una dependencia circular en el gráfico de dependencias de destino que implica el destino 'Módulo'": [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-201">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="a6b2e-202">El paquete se ejecuta con demasiada frecuencia. La generación de un paquete de NuGet no incluye todas las configuraciones: [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-202">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="a6b2e-203">Se genera la excepción NullReferenceException al agregar NuGet con packageref en un proyecto de C++: [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-203">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="a6b2e-204">Accesibilidad: Narrador no narra la casilla para seleccionar los proyectos en los que se instalará el paquete: [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-204">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="a6b2e-205">Se producen errores esporádicos en NuGet VS17 al conectarse a fuentes de VSO/VSTS; error de VS 365798: [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-205">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="a6b2e-206">contentFiles genera el resultado en una ubicación incorrecta si PackagePath especifica la ruta de acceso como "contentFiles": [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-206">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="a6b2e-207">El destino del paquete anexa la propiedad PackageVersion con VersionSuffix: [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-207">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="a6b2e-208">La especificación de la ruta de acceso del paquete no funciona con dotnet pack: [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-208">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="a6b2e-209">NuGet genera una serie de advertencias sobre importaciones duplicadas durante la restauración: [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-209">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="a6b2e-210">El cuadro de diálogo "Elegir formato del Administrador de paquetes NuGet" se ve mal si hay un tema oscuro: [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-210">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="a6b2e-211">VS se bloquea al restaurar la compilación: [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-211">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="a6b2e-212">Se producen interbloqueos en Visual Studio si se agrega un TFM en targetframeworks, se guarda y se compila.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-212">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="a6b2e-213">10 % de tiempo: [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-213">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="a6b2e-214">El paquete de NuGet no genera el mensaje de operación correcta al empaquetar un proyecto correctamente: [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-214">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="a6b2e-215">Se produce un error en PackTask porque no se encuentra System.IO.Compression 4.1: [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-215">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="a6b2e-216">El paquete se ejecuta con demasiada frecuencia: se producen errores frecuentes en PackTask con conflictos de acceso a archivos: [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-216">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="a6b2e-217">NuGet abre la ventana de salida durante la restauración de fondo: [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-217">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="a6b2e-218">Eliminación de ServiceProvider como patrón de codificación peligroso (lo cual puede producir bloqueos): [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-218">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="a6b2e-219">Rendimiento/suspensión de la interfaz de usuario. Mejorar las lecturas DownloadTimeoutStream: [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-219">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="a6b2e-220">Se produce un interbloqueo en Visual Studio si intenta cerrar un proyecto antes de que haya terminado la restauración de NuGet: [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-220">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="a6b2e-221">Problemas relacionados con PackTask y con el empaquetado de `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-221">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="a6b2e-222">[vsfeedback] No se pueden resolver los paquetes de NuGet en un proyecto nuevo (se debe reiniciar Visual Studio): [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-222">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="a6b2e-223">[vsfeedback] A la lista desplegable "Versión" en la que se muestran las versiones de paquetes disponibles le cuesta mantenerse sincronizada con el paquete de NuGet seleccionado...: [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-223">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="a6b2e-224">Nuget.Client debe usar CPS JoinableTaskFactory al interactuar con CPS para evitar interbloqueos: [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-224">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="a6b2e-225">NuGet 3.5.0 no desempaqueta `.targets` del paquete: [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-225">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="a6b2e-226">dotnet pack no admite title en `.csproj`: [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-226">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="a6b2e-227">Install-Package genera un cuadro de diálogo de error en VS2017 RC: [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-227">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="a6b2e-228">Aparentemente, la actualización de un paquete de un proyecto de .Net Core no funciona, ya que la interfaz de usuario no recibe la actualización de CPS del nominado:</span><span class="sxs-lookup"><span data-stu-id="a6b2e-228">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="a6b2e-229">[#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-229"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="a6b2e-230">Mejorar la advertencia de referencia sin resolver: [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-230">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="a6b2e-231">dotnet pack: ProjectReference pierde información de la versión: [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-231">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="a6b2e-232">Tiempo total transcurrido de las regresiones al crear un proyecto y al volver a compilar en la aplicación Crear UWP: [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-232">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="a6b2e-233">Se muestra un mensaje de restauración correcta incluso después de producirse un error durante la restauración:</span><span class="sxs-lookup"><span data-stu-id="a6b2e-233">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="a6b2e-234">[#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-234"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="a6b2e-235">Volver a publicar Nuget.CommandLine 3.4.4 en Nuget.org: [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-235">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="a6b2e-236">Durante la migración, los proyectos cambian de `project.json` a `.csproj` --- se produce un error de restauración: [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-236">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="a6b2e-237">Error de restauración en un proyecto de prueba xUnit recién creado: [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-237">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="a6b2e-238">Los proyectos principales se pueden bloquear, bloquean la interfaz de usuario al abrirse: [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-238">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="a6b2e-239">Corregir el archivo de destinos para las tareas de compilación: [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-239">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="a6b2e-240">La lista de errores contiene un error después de la solución de compilación, que descarga el proyecto al que se hace referencia: [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-240">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="a6b2e-241">MSB4057: El destino "_GenerateRestoreGraphProjectEntry" no existe en el proyecto:</span><span class="sxs-lookup"><span data-stu-id="a6b2e-241">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="a6b2e-242">[#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-242"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="a6b2e-243">vsfeedback: la interfaz de usuario del administrador de NuGet de la solución se bloquea cuando se seleccionan todos los proyectos: [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-243">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="a6b2e-244">Se produce un error de msbuildpath en nuget.exe si hay una barra diagonal: [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-244">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="a6b2e-245">vsfeedback: La restauración de NuGet proporciona varias advertencias de referencia de proyecto para el proyecto LinqToTwitter: [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-245">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="a6b2e-246">El paquete de `.csproj` no incluye el atributo minClientVersion: [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-246">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="a6b2e-247">Retraso enviado por NuGet.Build.Tasks.Pack.dll firmado en VS2017 (d15rel 26014.00): [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-247">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="a6b2e-248">VSFeedback: se produce un error de restauración para un proyecto de VS 2015 generado con CMake 3.7.1: [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-248">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="a6b2e-249">VSFeedback: los errores de restauración pueden ocultar mensajes de error más completos que podría proporcionar la compilación: [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-249">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="a6b2e-250">[VSFeedback] Se ha producido un error al restaurar los paquetes de NuGet para un proyecto de sitio web: El valor no puede ser nulo:</span><span class="sxs-lookup"><span data-stu-id="a6b2e-250">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="a6b2e-251">[#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-251"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="a6b2e-252">La migración genera una "excepción de referencia a objeto" en NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker: [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-252">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="a6b2e-253">dotnet pack debe empaquetar las herramientas con las versiones con las que se compiló el paquete: [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-253">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="a6b2e-254">La nueva restauración de fondo muestra milisegundos en la barra de estado cuando la restauración tarda segundos: [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-254">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="a6b2e-255">Error de escritura en "Error al resolver todas las referencias de proyecto": [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-255">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="a6b2e-256">Habilitar flujos de trabajo de PCM en los escenarios de referencia de paquete: [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-256">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="a6b2e-257">No se encuentran los paquetes instalados en la interfaz de usuario del Administrador de paquetes: [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-257">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="a6b2e-258">Se produce un error en dotnet pack si PackagePath está vacía: [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-258">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="a6b2e-259">Se produce un error al restaurar una tarea en un escenario de varios usuarios: [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-259">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="a6b2e-260">No se puede cambiar el tipo de contenido al empaquetar con la tarea de empaquetado de NuGet: [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-260">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="a6b2e-261">La copia predeterminada de contentFiles es incorrecta para MsBuild /t:pack: [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-261">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="a6b2e-262">La restauración de paquetes de instalación registra dos veces el mensaje de restauración de paquetes: [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-262">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="a6b2e-263">Quitar barreras de seguridad: La restauración de la sección "runtimes" solo se debería aplicar al proyecto actual: [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-263">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="a6b2e-264">La tarea de empaquetado coloca los archivos de contenido en “content/” y en “contentFiles/”: [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-264">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="a6b2e-265">dotnet pack3 hace divisiones de etiquetas adicionales: [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-265">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="a6b2e-266">dotnet pack: el empaquetado de proyectos con referencias de paquete genera una advertencia de importación duplicada: [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-266">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="a6b2e-267">El registro de restauración de VS no siempre se muestra: [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-267">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="a6b2e-268">El texto de nuget.exe locals -help sigue mencionando la memoria caché de paquetes: [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-268">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="a6b2e-269">Restore3 acopla PackageReferences a TargetFrameworks:</span><span class="sxs-lookup"><span data-stu-id="a6b2e-269">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="a6b2e-270">[#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-270"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="a6b2e-271">NuGet toma una versión no esperada de MSBuild en VS "15" Preview 4 dev.</span><span class="sxs-lookup"><span data-stu-id="a6b2e-271">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="a6b2e-272">símbolo del sistema: [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-272">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="a6b2e-273">Escribir archivos de destinos/propiedades en una restauración errónea: [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-273">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="a6b2e-274">Durante la restauración, NuGet no respeta las mismas correcciones de compatibilidad que MSBuild cuando se ejecuta en la línea de comandos de VS 15: [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-274">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="a6b2e-275">Volver a habilitar PackFromProjectWithDevelopmentDependencySet para VS15: [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-275">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="a6b2e-276">Problemas de Blend con NuGet: [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-276">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="a6b2e-277">Integrar 4.0.0.2067 en repositorios de CLI y SDK para enviarlos con RC2: [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-277">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="a6b2e-278">VS se bloquea al crear una aplicación de consola de Core, cerrar la solución, abrirla y cerrarla: [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-278">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="a6b2e-279">Bloqueo al abrir un proyecto en d15prerel.25916.01: [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-279">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="a6b2e-280">Corregir el mensaje dotnet/nuget.exe locals doc/help: [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-280">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="a6b2e-281">Inspeccionar PackTask para encontrar problemas con espacios en blanco iniciales o finales: [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-281">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="a6b2e-282">dotnet pack empaqueta de un objeto no bin: [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-282">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="a6b2e-283">Aparentemente, dotnet pack siempre establece la versión de ProjectReference en 1.0.0: [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-283">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="a6b2e-284">Se produce un error en dotnet pack con referencias de proyecto y <TargetFramework>: [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-284">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="a6b2e-285">LockRecursionException en ProjectSystemCache.TryGetProjectNameByShortName: [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-285">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="a6b2e-286">Recortar espacio en blanco de las propiedades de MSBuild: [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-286">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="a6b2e-287">Consolidar los dos eventos de proyecto generados al cargar el proyecto: [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-287">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="a6b2e-288">Las bibliotecas P2P del archivo `project.assets.json` tienen una versión incorrecta: [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-288">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="a6b2e-289">Bloqueo en la restauración debido a que la fuente no responde y a que el paquete no está disponible: [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-289">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="a6b2e-290">nuget.exe podría bloquearse si hay una gran cantidad de resultados de error de MSBuild: [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-290">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="a6b2e-291">Se produce un error en la restauración durante la compilación para Blend la primera vez, pero la segunda vez se efectúa correctamente (escenario de VS corregido): [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-291">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="a6b2e-292">DCR</span><span class="sxs-lookup"><span data-stu-id="a6b2e-292">DCRs</span></span>

- <span data-ttu-id="a6b2e-293">migrar vsix de v2 vsix a vsix v3: [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-293">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="a6b2e-294">NuGet debe disponer de un mecanismo para obtener la ruta de acceso al archivo de bloqueo de MSBuild: [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-294">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="a6b2e-295">Agregar recursos de compilación al archivo de recursos y de comprobación de compatibilidad de TFM: [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-295">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="a6b2e-296">Definir un nuevo "Pack" ProjectCapability en los destinos Pack para habilitar las capacidades relacionadas con los paquetes: [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-296">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="a6b2e-297">Ejecutar el paquete como un destino posterior a la compilación condicionado por la propiedad de MSBuild "GeneratePackageOnBuild": [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-297">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="a6b2e-298">Usar la propiedad RestoreProjectStyle de NuGet para crear un proyecto de NuGet específico: [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-298">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="a6b2e-299">Adaptar la restauración para el cambio de referencias de proyecto transitivo: [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-299">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="a6b2e-300">Agregar propiedades de NuGet al archivo de destino de proyectos que no son de UWP: [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-300">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="a6b2e-301">Compatibilidad con TargetPlatformVersion de UWP: [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-301">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="a6b2e-302">Comunicar los metadatos de referencia de proyecto al sistema de proyectos de NuGet: [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-302">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="a6b2e-303">Agregar la interfaz de usuario para el modo de empaquetado: [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-303">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="a6b2e-304">El archivo `.csproj` heredado necesita que NugetTargetMoniker y RuntimeIdentifiers estén establecidos en proyectos/destinos: [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-304">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="a6b2e-305">El paquete de instalación se puede superponer con la restauración automática: [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-305">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="a6b2e-306">El menú contextual QueryStatus no aparece cuando el paquete de VS no está cargado: [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-306">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="a6b2e-307">Restauración de la solución y Restauración de compilación siguen mostrando cuadros de diálogo: [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-307">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="a6b2e-308">Aislar la versión de VSSDK en la compilación de la solución de NuGet.Clients: [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="a6b2e-308">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="a6b2e-309">Vínculos a problemas de GitHub corregidos en RTM</span><span class="sxs-lookup"><span data-stu-id="a6b2e-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="a6b2e-310">Lista de problemas 1</span><span class="sxs-lookup"><span data-stu-id="a6b2e-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="a6b2e-311">Lista de problemas 2</span><span class="sxs-lookup"><span data-stu-id="a6b2e-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="a6b2e-312">Lista de problemas 3</span><span class="sxs-lookup"><span data-stu-id="a6b2e-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="a6b2e-313">Lista de problemas 4</span><span class="sxs-lookup"><span data-stu-id="a6b2e-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="a6b2e-314">Lista de problemas 5</span><span class="sxs-lookup"><span data-stu-id="a6b2e-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
