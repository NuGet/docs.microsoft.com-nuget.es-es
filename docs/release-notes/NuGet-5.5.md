---
title: Notas de la versión de NuGet 5,5
description: Notas de la versión de NuGet 5,5, incluidas nuevas características, correcciones de errores y DCR.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148286"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="e6fe1-103">Notas de la versión de NuGet 5,5</span><span class="sxs-lookup"><span data-stu-id="e6fe1-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="e6fe1-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="e6fe1-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e6fe1-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="e6fe1-105">NuGet version</span></span> | <span data-ttu-id="e6fe1-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e6fe1-106">Available in Visual Studio version</span></span>| <span data-ttu-id="e6fe1-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="e6fe1-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="e6fe1-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="e6fe1-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e6fe1-109">Visual Studio 2019 versión 16,5</span><span class="sxs-lookup"><span data-stu-id="e6fe1-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e6fe1-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e6fe1-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="e6fe1-111"><sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="e6fe1-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="e6fe1-112">Resumen: novedades en 5,5</span><span class="sxs-lookup"><span data-stu-id="e6fe1-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="e6fe1-113">Experiencia mejorada de accesibilidad y lector de pantalla para la interfaz de usuario del administrador de paquetes NuGet en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e6fe1-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="e6fe1-114">Problemas de accesibilidad en experiencias del lector de pantalla, falta altText y el nombre accesible para el cuadro de texto instalado, etc.,- [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="e6fe1-115">Problemas de accesibilidad en las experiencias del lector de pantalla en la lista de paquetes- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="e6fe1-116">Problemas de accesibilidad en las experiencias del lector de pantalla relacionadas con las pestañas "examinar", "instalar", "actualizar" [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="e6fe1-117">El narrador no anuncia la etiqueta de vínculo "Blank", "no dependencies", "Nuget. org", "MIT" [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="e6fe1-118">Compatibilidad con la exposición de iconos independientes en la interfaz de usuario del administrador de paquetes de Visual Studio para paquetes hospedados en fuentes locales: [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="e6fe1-119">Rendimiento de restauración no operativa significativamente mejorado mediante `RestoreUseStaticGraphEvaluation` que acelera las evaluaciones mediante una llamada a las API de grafos estáticos de MSBuild- [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="e6fe1-120">Confiabilidad mejorada de dotnet. exe con complementos de autenticación multiplataforma</span><span class="sxs-lookup"><span data-stu-id="e6fe1-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="e6fe1-121">error de dotnet restore con TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="e6fe1-122">Complemento: "se canceló una tarea"-problema con la autenticación de ADO debido a esto.</span><span class="sxs-lookup"><span data-stu-id="e6fe1-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="e6fe1-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="e6fe1-124">Agregar `dotnet nuget <add|remove|update|disable|enable|list> source` [#4126](https://github.com/NuGet/Home/issues/4126) de comandos</span><span class="sxs-lookup"><span data-stu-id="e6fe1-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="e6fe1-125">Compatibilidad con para `--skip-duplicate` mediante el [#8778](https://github.com/NuGet/Home/issues/8778) de extracción de Nuget de dotnet</span><span class="sxs-lookup"><span data-stu-id="e6fe1-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="e6fe1-126">Compatibilidad `packages.config` con MSBuild/restore- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e6fe1-127">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="e6fe1-127">Issues fixed in this release</span></span>

<span data-ttu-id="e6fe1-128">**Errores**</span><span class="sxs-lookup"><span data-stu-id="e6fe1-128">**Bugs**</span></span>

* <span data-ttu-id="e6fe1-129">Actualización automática del trabajo con las API de V3: [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="e6fe1-130">Versión de dependencia de paquete incorrecta si la versión de dependencia del paquete está establecida en ' \* '- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="e6fe1-131">El mensaje de error ErrorUnsafePackageEntry no está señalando el origen del problema [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="e6fe1-132">No se respeta el archivo de bloqueo en escenarios "\*": [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="e6fe1-133">NuGet. exe no se resuelve como la versión más reciente de un paquete cuando se usa \* en PackageReference (MSBuild/dotnet/VS restore do)- [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="e6fe1-134">paquete dotnet List con varios destinos de proyecto de WPF: [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="e6fe1-135">Mejorar ConcurrencyUtilities (reducir el uso de CPU)- [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="e6fe1-136">Las especificaciones de DG para escenarios de proyecto descargados no se deben escribir en las restauraciones de vista previa: [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="e6fe1-137">Los paquetes NuGet de Visual Studio (RestoreManagerPackage) deben cargarse automáticamente en eventos de compilación de la solución: [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="e6fe1-138">Interbloqueo en VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="e6fe1-139">El cuadro de herramientas de VisualStudio no se rellena desde un paquete NuGet si un proyecto se coloca en una carpeta de soluciones: [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="e6fe1-140">VS: la restauración de la solución no se realiza de forma perpetua debido a la condición de carrera: [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="e6fe1-141">Constante "cargando..." en la pestaña instalado y "buscando</span><span class="sxs-lookup"><span data-stu-id="e6fe1-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="e6fe1-142">.. "en la pestaña actualizaciones: [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="e6fe1-143">Faltan iconos incrustados en la interfaz de usuario de VS PM después de que expire la caché- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="e6fe1-144">Inicio de la interfaz de usuario de FireAndForget PM- [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="e6fe1-145">La implementación de restore: IncludeExcludeFiles. Equals (...) es incorrecta- [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="e6fe1-146">Restore: PackageSpec. Clone () crea un clon distinto de [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="e6fe1-147">La lista de errores se muestra aunque "Mostrar siempre Lista de errores si la compilación termina con errores" no está activada- [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="e6fe1-148">La restauración de gráficos estáticos no debe pasar SolutionPath vacío- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="e6fe1-149">Restore: cierre calculado para cada proyecto 4 veces: [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="e6fe1-150">Restore: DependencyGraphSpec. Load (...) no necesita JObject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="e6fe1-151">Restore: cadenas grandes creadas en el montón de objetos grandes (montón)- [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="e6fe1-152">El archivo Nuget. exe personalizado en mono más reciente podría interrumpirse debido a la resolución del SDK de MSBuild- [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="e6fe1-153">se produce un error en la restauración cuando Nuget. dgspec. JSON es "usado por otro proceso"- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="e6fe1-154">**DCR**</span><span class="sxs-lookup"><span data-stu-id="e6fe1-154">**DCRs**</span></span>

* <span data-ttu-id="e6fe1-155">La lógica de _GetRestoreProjectStyle debe estar en una tarea- [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="e6fe1-156">Agregar información de desuso de forma predeterminada en la pestaña instalado [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="e6fe1-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="e6fe1-157">**[Lista de todos los problemas corregidos en esta versión: 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="e6fe1-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
