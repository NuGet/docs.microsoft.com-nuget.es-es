---
title: Notas de la versión de NuGet 5,6
description: Notas de la versión de NuGet 5,6, incluidas nuevas características, correcciones de errores y DCR.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727810"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="82d21-103">Notas de la versión de NuGet 5,6</span><span class="sxs-lookup"><span data-stu-id="82d21-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="82d21-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="82d21-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="82d21-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="82d21-105">NuGet version</span></span> | <span data-ttu-id="82d21-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82d21-106">Available in Visual Studio version</span></span>| <span data-ttu-id="82d21-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="82d21-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="82d21-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="82d21-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="82d21-109">Visual Studio 2019 versión 16.6</span><span class="sxs-lookup"><span data-stu-id="82d21-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="82d21-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="82d21-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="82d21-111"><sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="82d21-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="82d21-112">Resumen: novedades en 5,6</span><span class="sxs-lookup"><span data-stu-id="82d21-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="82d21-113">Compatibilidad con paquetes de versión preliminar con versiones flotantes.</span><span class="sxs-lookup"><span data-stu-id="82d21-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="82d21-114">`Version="*-*"`, `Version="1.*-*"` y son similares a las versiones más recientes, incluidas las versiones preliminares, dentro del intervalo especificado: [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="82d21-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="82d21-115">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="82d21-115">Issues fixed in this release</span></span>

<span data-ttu-id="82d21-116">**Detectar**</span><span class="sxs-lookup"><span data-stu-id="82d21-116">**Bugs:**</span></span>

* <span data-ttu-id="82d21-117">`nuget push *.nupkg`se produce un error cuando snupkg no existe: [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="82d21-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="82d21-118">Pack, y otras rutas de acceso de código, que no dependen de la configuración regional.</span><span class="sxs-lookup"><span data-stu-id="82d21-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="82d21-119">Usar RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="82d21-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="82d21-120">Rendimiento: la especificación de DG para escenarios de proyecto descargados no se debe escribir en las restauraciones de vista previa: [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="82d21-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="82d21-121">Restauración: mejorar el rendimiento mediante el almacenamiento en caché del gráfico de dependencias de la solución- [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="82d21-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="82d21-122">La interfaz de usuario de PM no funciona para los proyectos de estilo SDK después de instalar un paquete con la consola PM- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="82d21-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="82d21-123">No se puede mostrar el icono incrustado en la interfaz de usuario de PM con la fuente de paquetes local, dependiendo de/vs \ [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="82d21-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="82d21-124">NuGetVersion. TryParseStrict () debe devolver false si no se puede analizar- [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="82d21-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="82d21-125">`nuget.exe push`ayuda para `-source` , debe sugerir el uso del nombre de origen, no de la dirección URL de origen- [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="82d21-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="82d21-126">`dotnet nuget add package SourceUri`crea un nombre de origen de paquete predeterminado incorrecto: [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="82d21-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="82d21-127">El lector de pantalla no anuncia "buscando..." mensaje al cambiar de pestañas: [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="82d21-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="82d21-128">Accesibilidad: el color del rectángulo de foco no es accesible CP pestañas de la interfaz de usuario en el tema oscuro: [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="82d21-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="82d21-129">Nuget. exe 5,5 no se puede restaurar con MSBuild 14 o inferior [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="82d21-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="82d21-130">No registrar las horas de milisegundos en los mensajes de restauración: [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="82d21-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="82d21-131">Crear IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="82d21-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="82d21-132">La selección de versiones de MSBuild funciona mal en algunas culturas que no están en inglés, [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="82d21-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="82d21-133">Falta el formato predeterminado en `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="82d21-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="82d21-134">Rendimiento: RestoreOperationLogger tiene afinidad de subprocesos innecesarias- [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="82d21-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="82d21-135">Creación automatizada de documentos para `dotnet nuget` comandos- [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="82d21-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="82d21-136">El nivel de detalle predeterminado no debe notificar la restauración de NOOP del proyecto [#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="82d21-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="82d21-137">`-DependencyVersion`Parámetro de compatibilidad para `NuGet.exe update` , similar a [#7694](https://github.com/NuGet/Home/issues/7694) de comandos de instalación</span><span class="sxs-lookup"><span data-stu-id="82d21-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="82d21-138">**DCR**</span><span class="sxs-lookup"><span data-stu-id="82d21-138">**DCRs:**</span></span>

* <span data-ttu-id="82d21-139">Agregar compatibilidad inicial para el marco de destino de .net 5.0: [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="82d21-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="82d21-140">Ordenar paquetes por identificador en la pestaña actualizaciones de la interfaz de usuario de PM- [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="82d21-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="82d21-141">**[Lista de todos los problemas corregidos en esta versión: 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="82d21-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
