---
title: Notas de la versión de NuGet 5.10
description: Notas de la versión de NuGet 5.10, incluidas nuevas características, correcciones de errores y DCR.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356504"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="a5e82-103">Notas de la versión de NuGet 5.10</span><span class="sxs-lookup"><span data-stu-id="a5e82-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="a5e82-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="a5e82-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a5e82-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="a5e82-105">NuGet version</span></span> | <span data-ttu-id="a5e82-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a5e82-106">Available in Visual Studio version</span></span> | <span data-ttu-id="a5e82-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="a5e82-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="a5e82-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="a5e82-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a5e82-109">Visual Studio 2019, versión 16.10</span><span class="sxs-lookup"><span data-stu-id="a5e82-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a5e82-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a5e82-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="a5e82-111"><sup>1 Instalado</sup> con Visual Studio 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="a5e82-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="a5e82-112">Visual Studio 16.10, MSBuild 16.10 y .NET 5.0.300+ NuGet.exe 5.10 o posterior.</span><span class="sxs-lookup"><span data-stu-id="a5e82-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="a5e82-113">Resumen: Novedades de la versión 5.10</span><span class="sxs-lookup"><span data-stu-id="a5e82-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="a5e82-114">Firma: implemente el comando dotnet trusted-signers [- #8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="a5e82-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="a5e82-115">Hacer que la validación predeterminada esté deshabilitada en Linux, pero habilitada de forma predeterminada en [Windows: #10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="a5e82-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="a5e82-116">Agregar una variable ENV para la comprobación de firma de paquetes en .NET 5+ Linux/MAC: [#10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="a5e82-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="a5e82-117">Mejora del rendimiento de la instalación de nuevos paquetes para soluciones de [gran tamaño: #10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="a5e82-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="a5e82-118">Agregue el tipo de `nfproj` proyecto a la lista de supportedProjectExtensions para la CLI de Nuget.</span><span class="sxs-lookup"><span data-stu-id="a5e82-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="a5e82-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="a5e82-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a5e82-120">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="a5e82-120">Issues fixed in this release</span></span>

* <span data-ttu-id="a5e82-121">Suprimir el <requireLicenseAcceptance> elemento al empaquetar un [proyecto: #5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="a5e82-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="a5e82-122">[CPVM] La advertencia de versión preliminar debe mostrarse en la cli de [dotnet: #10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="a5e82-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="a5e82-123">Actualice los tokens de color de fondo y primer plano de PMUI a CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span><span class="sxs-lookup"><span data-stu-id="a5e82-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="a5e82-124">[Bug Bash] El error "operación cancelada por el usuario" se muestra en la ventana Lista de errores al cambiar rápidamente entre pestañas en la interfaz de usuario de [PM: #10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="a5e82-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="a5e82-125">Interfaz de usuario de PM: mejorar el rendimiento de la instalación de paquetes en el nivel de [solución: #10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="a5e82-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="a5e82-126">Reemplace GetService por GetServiceAsync en cualquier lugar de NuGet.Clients: [#3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="a5e82-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="a5e82-127">NuGet.exe de rendimiento del paquete con `..` la ruta de acceso [relativa: #5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="a5e82-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="a5e82-128">El rendimiento del "paquete nuget" disminuye con niveles crecientes en las rutas de acceso de [origen: #5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="a5e82-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="a5e82-129">NuGet no genera errores al empaquetar nuspec con archivos duplicados.</span><span class="sxs-lookup"><span data-stu-id="a5e82-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="a5e82-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="a5e82-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="a5e82-131">Paquete NuGet "El dateTimeOffset especificado no se puede convertir en una marca de tiempo de archivo [ZIP": #7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="a5e82-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="a5e82-132">Las marcas de tiempo del archivo del paquete empaquetado se desplazan por la zona [horaria: #7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="a5e82-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="a5e82-133">NU1004 debe contener información más útil: [#7696](https://github.com/NuGet/Home/issues/7696)</span><span class="sxs-lookup"><span data-stu-id="a5e82-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="a5e82-134">[Bug Bash] [Error de prueba] El archivo de bloqueo vacío o con formato no debe actualizarse al ejecutar "dotnet restore --use-lock-file --locked-mode": [#8640](https://github.com/NuGet/Home/issues/8640)</span><span class="sxs-lookup"><span data-stu-id="a5e82-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="a5e82-135">NuGetVersionRange permite analizar intervalos lógicamente incorrectos: [#9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="a5e82-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="a5e82-136">La interfaz de usuario de PM no puede mostrar un color de fondo distintivo entre los orígenes de paquetes seleccionados y los que mantienen el [puntero: #9538](https://github.com/NuGet/Home/issues/9538)</span><span class="sxs-lookup"><span data-stu-id="a5e82-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="a5e82-137">El lector de pantalla no lee la casilla para seleccionar los proyectos en los que se va a [instalar : #9578](https://github.com/NuGet/Home/issues/9578)</span><span class="sxs-lookup"><span data-stu-id="a5e82-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="a5e82-138">La selección predeterminada del menú desplegable Versiones del panel de detalles debe ser Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="a5e82-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="a5e82-139">Quite la cuenta de solución alternativa para algunos SDK de .NET 5 informe TargetPlatformMoniker de ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="a5e82-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="a5e82-140">dotnet nuget verify es demasiado silencioso: [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="a5e82-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="a5e82-141">VersionRange no puede analizar intervalos de un solo [dígito: #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="a5e82-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="a5e82-142">El administrador de soluciones de VS produce una excepción null para durante la [depuración: #10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="a5e82-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="a5e82-143">Traslado de mensajes de excepción de la CLI a archivos de recursos de [cadena: #10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="a5e82-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="a5e82-144">Quitar código no encontrado (TabItemButtonAutomationPeer): [#10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="a5e82-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="a5e82-145">El menú contextual de actualización debe desplazarse hasta el primer elemento [seleccionado: #10498](https://github.com/NuGet/Home/issues/10498)</span><span class="sxs-lookup"><span data-stu-id="a5e82-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="a5e82-146">Los detalles de PMUI de la solución tienen barras horizontales [superpuestas: #10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="a5e82-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="a5e82-147">Firma: los detalles de la firma principal no se muestran cuando el certificado ha expirado y la marca de tiempo no es de [confianza: #10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="a5e82-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="a5e82-148">No tener ningún orígenes habilitado impide que se muestre la interfaz de usuario de PM [#10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="a5e82-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="a5e82-149">Los metadatos del paquete (detalles, desuso) a veces no se extraen nuget.org en CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="a5e82-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="a5e82-150">Se produce un error en la inicialización de PMUI con una excepción durante la sesión [de depuración: #10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="a5e82-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="a5e82-151">La restauración de nuget produce un error de comprobación de integridad del paquete big endian sistema: [#10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="a5e82-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="a5e82-152">FormatException se produce en lugar de [PackagingException: #10595](https://github.com/NuGet/Home/issues/10595)</span><span class="sxs-lookup"><span data-stu-id="a5e82-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="a5e82-153">CPVM: problemas de simultaneidad en el algoritmo de recorrido del [grafo: #10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="a5e82-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="a5e82-154">Adición de telemetría de la versión de PowerShell de [PMC: #10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="a5e82-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="a5e82-155">Mejora del rendimiento de ordenación de NuGetVersion: [#10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="a5e82-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="a5e82-156">Agregar firmantes de confianza tiene argumentos incoherentes: [#10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="a5e82-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="a5e82-157">Vs2019 v16.9.0: al cambiar las pestañas de NuGet Administrador de paquetes de "Actualizaciones" a "Instalado" no se actualiza el marco.</span><span class="sxs-lookup"><span data-stu-id="a5e82-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="a5e82-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="a5e82-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="a5e82-159">Quite la "v" del número de versión en PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span><span class="sxs-lookup"><span data-stu-id="a5e82-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="a5e82-160">INuGetProjectService.GetInstalledPackagesAsync inicia antes de recibir la nominación del sistema de proyectos de [CPS: #10681](https://github.com/NuGet/Home/issues/10681)</span><span class="sxs-lookup"><span data-stu-id="a5e82-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="a5e82-161">Los iconos incrustados provocan el acceso denegado desde el origen "Microsoft Visual Studio sin conexión" en la pestaña [Examinar : #10687](https://github.com/NuGet/Home/issues/10687)</span><span class="sxs-lookup"><span data-stu-id="a5e82-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="a5e82-162">INuGetProjectService.GetInstalledPackagesAsync inicia cuando MSBuildProjectExtensionsPath no está [establecido: #10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="a5e82-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="a5e82-163">"dotnet nuget remove source nuget.org" no funciona la primera vez: [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="a5e82-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="a5e82-164">Nuget bloquea un subproceso de grupo de subprocesos en un método asincrónico que realiza una llamada sincrónica al subproceso de interfaz de [usuario: #10775](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="a5e82-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="a5e82-165">Tools -> Options -> NuGet Administrador de paquetes string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="a5e82-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="a5e82-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` es código no encontrado y daña el [rendimiento: #10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="a5e82-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="a5e82-167">Uso del icono incrustado en paquetes del SDK de [NuGet: #10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="a5e82-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="a5e82-168">Actualización de la lista de licencias de [SPDX: #10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="a5e82-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="a5e82-169">**[Lista de todos los problemas corregidos en esta versión: 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="a5e82-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="a5e82-170">**[Lista de confirmaciones de esta versión: 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="a5e82-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="a5e82-171">Contribuciones de la comunidad</span><span class="sxs-lookup"><span data-stu-id="a5e82-171">Community contributions</span></span>

<span data-ttu-id="a5e82-172">Gracias a todos los colaboradores que ayudaron a que esta versión de NuGet sea impresionante.</span><span class="sxs-lookup"><span data-stu-id="a5e82-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="a5e82-173">Quién</span><span class="sxs-lookup"><span data-stu-id="a5e82-173">Who</span></span>|<span data-ttu-id="a5e82-174">Prs</span><span class="sxs-lookup"><span data-stu-id="a5e82-174">PRs</span></span>|<span data-ttu-id="a5e82-175">Issues</span><span class="sxs-lookup"><span data-stu-id="a5e82-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="a5e82-176">z</span><span class="sxs-lookup"><span data-stu-id="a5e82-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="a5e82-177">3991</span><span class="sxs-lookup"><span data-stu-id="a5e82-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="a5e82-178">VersionRange no puede analizar intervalos de un solo [dígito: #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="a5e82-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="a5e82-179">omajid</span><span class="sxs-lookup"><span data-stu-id="a5e82-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="a5e82-180">3860</span><span class="sxs-lookup"><span data-stu-id="a5e82-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="a5e82-181">NuGet.Client build.sh está roto: [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="a5e82-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="a5e82-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="a5e82-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="a5e82-183">3623</span><span class="sxs-lookup"><span data-stu-id="a5e82-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="a5e82-184">NuGet.Client build.sh está roto: [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="a5e82-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="a5e82-185">BlackGad</span><span class="sxs-lookup"><span data-stu-id="a5e82-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="a5e82-186">3953</span><span class="sxs-lookup"><span data-stu-id="a5e82-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="a5e82-187">El rendimiento del "paquete nuget" disminuye con niveles crecientes en las rutas de acceso de [origen: #5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="a5e82-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="a5e82-188">BlackGad</span><span class="sxs-lookup"><span data-stu-id="a5e82-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="a5e82-189">3953</span><span class="sxs-lookup"><span data-stu-id="a5e82-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="a5e82-190">NuGet.exe problema de rendimiento del paquete con .</span><span class="sxs-lookup"><span data-stu-id="a5e82-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="a5e82-191">ruta de acceso [relativa: #5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="a5e82-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="a5e82-192">marcin-yunsjunto</span><span class="sxs-lookup"><span data-stu-id="a5e82-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="a5e82-193">3940</span><span class="sxs-lookup"><span data-stu-id="a5e82-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="a5e82-194">CPVM: problemas de simultaneidad en el algoritmo de recorrido del [grafo: #10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="a5e82-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="a5e82-195">josesimoes</span><span class="sxs-lookup"><span data-stu-id="a5e82-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="a5e82-196">3943</span><span class="sxs-lookup"><span data-stu-id="a5e82-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="a5e82-197">Agregue el tipo de proyecto nfproj a la lista de supportedProjectExtensions para la CLI de Nuget.</span><span class="sxs-lookup"><span data-stu-id="a5e82-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="a5e82-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="a5e82-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="a5e82-199">Bienvenida a los comentarios</span><span class="sxs-lookup"><span data-stu-id="a5e82-199">Feedback welcome</span></span>

<span data-ttu-id="a5e82-200">Sus comentarios son importantes.</span><span class="sxs-lookup"><span data-stu-id="a5e82-200">Your feedback is important to us.</span></span>  <span data-ttu-id="a5e82-201">Si hay algún problema con esta versión, consulte los problemas de [GitHub](https://github.com/NuGet/Home/issues) [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) problemas existentes.</span><span class="sxs-lookup"><span data-stu-id="a5e82-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="a5e82-202">Si hay nuevos problemas en NuGet, informe de un [problema de GitHub.](https://github.com/NuGet/Home/issues/new)</span><span class="sxs-lookup"><span data-stu-id="a5e82-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="a5e82-203">Para problemas generales de la experiencia [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) de NuGet, háganoslo saber a través de la opción Notificar un problema que se encuentra en su IDE favorito en Ayuda **> notificar un problema.**</span><span class="sxs-lookup"><span data-stu-id="a5e82-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
