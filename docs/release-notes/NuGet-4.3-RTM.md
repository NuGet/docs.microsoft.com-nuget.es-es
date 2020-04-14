---
title: Notas de la versión de NuGet 4.3 RTM
description: Notas de la versión de NuGet 4.3 RTM incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496590"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="70221-103">Notas de la versión NuGet 4.3</span><span class="sxs-lookup"><span data-stu-id="70221-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="70221-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye NuGet 4.3 RTM que agrega compatibilidad para escenarios nuevos, como .NET Standard 2.0 y .NET Core 2.0, contiene numerosas correcciones de calidad y mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="70221-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="70221-105">En esta versión también se ofrecen varias mejoras como compatibilidad para Versionamiento Semántico 2.0.0, integración de MSBuild de advertencias y errores de NuGet, y mucho más.</span><span class="sxs-lookup"><span data-stu-id="70221-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="70221-106">Resumen: Novedades de la versión 4.3.0</span><span class="sxs-lookup"><span data-stu-id="70221-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="70221-107">Resumen: Novedades de la versión 4.3.1</span><span class="sxs-lookup"><span data-stu-id="70221-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="70221-108">Corrección de seguridad: Premisos demasiado amplios de los archivos creados en ~/.nuget: [n.º 7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="70221-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="70221-109">Corrección de seguridad: Posible ruta relativa de los archivos de NUPKG por encima del directorio NUPKG: [n.º 7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="70221-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="70221-110">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="70221-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="70221-111">La restauración de NuGet puede tratar los orígenes de paquetes deshabilitados como habilitados en algunos casos</span><span class="sxs-lookup"><span data-stu-id="70221-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="70221-112">Problema</span><span class="sxs-lookup"><span data-stu-id="70221-112">Issue</span></span>

<span data-ttu-id="70221-113">En las siguientes técnicas de línea de comandos de restauración se tratan los orígenes de paquetes deshabilitados como habilitados.</span><span class="sxs-lookup"><span data-stu-id="70221-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="70221-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="70221-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="70221-115">`dotnet restore` (ya sea con dotnet.exe, que se incluye con VS, o con el que se incluye con NetCore SDK 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="70221-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="70221-116">Solución</span><span class="sxs-lookup"><span data-stu-id="70221-116">Workaround</span></span>

1. <span data-ttu-id="70221-117">Use Visual Studio (2017 15.3 o posterior) o NuGet.exe (v4.3.0 o posterior).</span><span class="sxs-lookup"><span data-stu-id="70221-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="70221-118">Elimine el origen deshabilitado y siga usando msbuild o dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="70221-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="70221-119">Para la solución, puede usar "Clear" en NuGet.config y, después, definir los orígenes necesarios para esa solución.</span><span class="sxs-lookup"><span data-stu-id="70221-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="70221-120">Mientras usa la Consola del Administrador de paquetes, puede que la tecla "Entrar" no funcione</span><span class="sxs-lookup"><span data-stu-id="70221-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="70221-121">Problema</span><span class="sxs-lookup"><span data-stu-id="70221-121">Issue</span></span>

<span data-ttu-id="70221-122">En algunas ocasiones, la tecla Entrar no funciona en la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="70221-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="70221-123">Si ve esto, revise el progreso de la corrección y proporcione información útil adicional sobre los pasos de reproducción.</span><span class="sxs-lookup"><span data-stu-id="70221-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="70221-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="70221-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="70221-125">Solución</span><span class="sxs-lookup"><span data-stu-id="70221-125">Workaround</span></span>

<span data-ttu-id="70221-126">Reinicie Visual Studio y abra la consola de Administración de paquetes antes de abrir la solución.</span><span class="sxs-lookup"><span data-stu-id="70221-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="70221-127">Como alternativa, intente eliminar el archivo `project.lock.json` y restaurarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="70221-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="70221-128">No se puede ver, agregar ni actualizar DotNetCLITools con el Administrador de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="70221-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="70221-129">Problema</span><span class="sxs-lookup"><span data-stu-id="70221-129">Issue</span></span>

<span data-ttu-id="70221-130">El Administrador de paquetes de NuGet no muestra ni permite agregar o actualizar DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="70221-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="70221-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="70221-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="70221-132">Solución</span><span class="sxs-lookup"><span data-stu-id="70221-132">Workaround</span></span>

<span data-ttu-id="70221-133">DotNetCLIToolReferences se debe editar manualmente en el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="70221-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="70221-134">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta</span><span class="sxs-lookup"><span data-stu-id="70221-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="70221-135">Problema</span><span class="sxs-lookup"><span data-stu-id="70221-135">Issue</span></span>

<span data-ttu-id="70221-136">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta, en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="70221-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="70221-137">Esto sucede cuando usa PackageReferences como el formato del administrador de paquete.</span><span class="sxs-lookup"><span data-stu-id="70221-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="70221-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="70221-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="70221-139">Solución</span><span class="sxs-lookup"><span data-stu-id="70221-139">Workaround</span></span>

<span data-ttu-id="70221-140">Haga una restauración manual.</span><span class="sxs-lookup"><span data-stu-id="70221-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="70221-141">Problemas corregidos en el período de NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="70221-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="70221-142">[Notas de la versión de NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md): enumera todos los problemas corregidos en NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="70221-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="70221-143">Características</span><span class="sxs-lookup"><span data-stu-id="70221-143">Features</span></span>

- <span data-ttu-id="70221-144">Mejorar el rendimiento de restauración de NuGet: implementar NoOp más inteligente para las restauraciones de línea de comandos y VS: [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="70221-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="70221-145">NET Core 2.0: CLI de VS o Dotnet debe empezar a usar la funcionalidad existente de NuGet: carpetas FallBack: [n.º 4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="70221-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="70221-146">NET Core 2.0: permitir a los usuarios ignorar advertencias de restauración específicas (o elevarlas a error): [n.º 4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="70221-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="70221-147">NET Core 2.0: ensamblados localizados de la CLI: [n.º 4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="70221-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="70221-148">NET Core 2.0: registrar todas las advertencias o errores en el archivo de recursos (incluido PackageTargetFallback): [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="70221-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="70221-149">Habilitar compatibilidad con TFM: NetStandard2.0, Tizen: [n.º 4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="70221-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="70221-150">Reducir el número de proyectos de NuGet.Core NuGet.Client (y, por tanto, de archivos DLL): [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="70221-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="70221-151">Agregar la capacidad de marcar advertencias de NuGet como errores: [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="70221-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="70221-152">Errores</span><span class="sxs-lookup"><span data-stu-id="70221-152">Bugs</span></span>

- <span data-ttu-id="70221-153">Se produce un error de msbuild /t:pack con el parámetro "DevelopmentDependency" que no es compatible con la tarea "PackTask": [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="70221-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="70221-154">La estructura de directorios para los archivos de contenido es plana si no se agrega el separador de directorios de Windows al final de PackagePath: [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="70221-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="70221-155">Los proyectos de netcore no admiten la configuración como developmentDependency: [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="70221-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="70221-156">RestoreManagerPackage se carga de forma sincrónica lo que bloquea el subproceso de la interfaz de usuario e interbloquea VS: [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="70221-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="70221-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="70221-157">dotnet</span></span>
  - <span data-ttu-id="70221-158">dotnetcore restore (y, por tanto, msbuild /t:restore) omite los proyectos con una dependencia de proyecto de solución explícita: [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="70221-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="70221-159">Si la solución tiene referencias de proyecto que hacen referencia al mismo proyecto, con distinto uso de mayúsculas y minúsculas, es posible que la restauración no funcione.</span><span class="sxs-lookup"><span data-stu-id="70221-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="70221-160">Esto afecta también a diferentes rutas de acceso relativas, sin una diferencia de uso de mayúsculas y minúsculas: [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="70221-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="70221-161">Los archivos ejecutables restaurados desde paquetes NuGet ya no son ejecutables con .NET Core 2.0: [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="70221-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="70221-162">NuGet.exe acepta los detalles de excepción al analizar el archivo de solución: [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="70221-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="70221-163">Pack coloca los archivos de contenido en una ubicación incorrecta si ContentTargetFolders contiene una ruta de acceso que termina con "/" en Windows: [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="70221-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="70221-164">No se puede restaurar una referencia DotNetCliToolReference para un paquete de herramientas destinado a netcoreapp1.1: [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="70221-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="70221-165">La actualización de la CLI de NuGet deja la condición anterior de versión de paquete en el archivo de proyecto (C++): [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="70221-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="70221-166">DCR</span><span class="sxs-lookup"><span data-stu-id="70221-166">DCRs</span></span>

- <span data-ttu-id="70221-167">Leer DotnetCliToolTargetFramework desde la nominación de CPS: [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="70221-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="70221-168">La comprobación de TPMinV debería funcionar para UWP de estilo de pj: [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="70221-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="70221-169">Mejorar la descripción de la interfaz de usuario para los paquetes con referencia automática: [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="70221-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="70221-170">La restauración de NuGet selecciona activos de compilación de la sección de tiempo de ejecución:</span><span class="sxs-lookup"><span data-stu-id="70221-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="70221-171">[#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="70221-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="70221-172">Colocar el diagnóstico de dependencias en el archivo de bloqueo: [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="70221-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="70221-173">Vínculos a problemas de GitHub corregidos en 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="70221-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="70221-174">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="70221-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
