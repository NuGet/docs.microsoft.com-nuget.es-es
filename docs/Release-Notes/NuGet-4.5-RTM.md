---
title: "Notas de la versión de NuGet 4.5 RTM | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 12/4/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 4.5 RTM, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR."
keywords: "Notas de la versión de NuGet 4.5 RTM, correcciones de errores, problemas conocidos, características agregadas y DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: e4727d46812cbfeb2e7094ddf28bf4e738e8aeea
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="6fcae-104">Notas de la versión de NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="6fcae-104">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="6fcae-105">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="6fcae-105">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="6fcae-106">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="6fcae-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="6fcae-107">Problemas con .NET 2.0 Standard con .NET Framework y NuGet</span><span class="sxs-lookup"><span data-stu-id="6fcae-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="6fcae-108">.NET Standard y sus herramientas se han diseñado de forma que los proyectos destinados a .NET Framework 4.6.1 puedan usar los paquetes y proyectos de NuGet que tienen como destino .NET Standard 2.0 o versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="6fcae-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="6fcae-109">[En este documento](https://github.com/dotnet/standard/issues/481) se resumen los problemas relacionados con ese escenario, el plan para abordarlos, así como soluciones alternativas que se pueden implementar con el estado actual de las herramientas.</span><span class="sxs-lookup"><span data-stu-id="6fcae-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="6fcae-110">No se puede ver, agregar ni actualizar DotNetCLITools con el Administrador de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="6fcae-110">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="6fcae-111">Problema</span><span class="sxs-lookup"><span data-stu-id="6fcae-111">Issue</span></span>

<span data-ttu-id="6fcae-112">El Administrador de paquetes de NuGet no muestra ni permite agregar o actualizar DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="6fcae-112">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="6fcae-113">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="6fcae-113">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="6fcae-114">Solución</span><span class="sxs-lookup"><span data-stu-id="6fcae-114">Workaround</span></span>

<span data-ttu-id="6fcae-115">DotNetCLIToolReferences se debe editar manualmente en el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="6fcae-115">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="6fcae-116">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta</span><span class="sxs-lookup"><span data-stu-id="6fcae-116">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="6fcae-117">Problema</span><span class="sxs-lookup"><span data-stu-id="6fcae-117">Issue</span></span>

<span data-ttu-id="6fcae-118">Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta, en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fcae-118">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="6fcae-119">Esto sucede cuando usa PackageReferences como el formato del administrador de paquete.</span><span class="sxs-lookup"><span data-stu-id="6fcae-119">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="6fcae-120">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="6fcae-120">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="6fcae-121">Solución</span><span class="sxs-lookup"><span data-stu-id="6fcae-121">Workaround</span></span>

<span data-ttu-id="6fcae-122">Haga una restauración manual.</span><span class="sxs-lookup"><span data-stu-id="6fcae-122">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="6fcae-123">Un paquete en un proyecto de .NET Core que contiene un ensamblado con una firma no válida puede desencadenar un bucle infinito de restauración</span><span class="sxs-lookup"><span data-stu-id="6fcae-123">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="6fcae-124">Problema</span><span class="sxs-lookup"><span data-stu-id="6fcae-124">Issue</span></span>

<span data-ttu-id="6fcae-125">En algunas ocasiones, al usar un paquete que contiene un ensamblado con una firma no válida o cuando la versión del paquete está establecida con el valor "DateTime", la restauración automática del paquete se ejecutará en un bucle infinito [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="6fcae-125">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="6fcae-126">Solución</span><span class="sxs-lookup"><span data-stu-id="6fcae-126">Workaround</span></span>

<span data-ttu-id="6fcae-127">No hay ninguna solución alternativa para este problema.</span><span class="sxs-lookup"><span data-stu-id="6fcae-127">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="6fcae-128">Problemas corregidos en el período de NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="6fcae-128">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="6fcae-129">Para los problemas corregidos en NuGet 4.4 RTM, consulte las [notas de la versión de NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="6fcae-129">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="6fcae-130">Características</span><span class="sxs-lookup"><span data-stu-id="6fcae-130">Features</span></span>

- <span data-ttu-id="6fcae-131">Deshabilitar la inserción automática de un paquete de símbolos: [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="6fcae-131">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="6fcae-132">Errores</span><span class="sxs-lookup"><span data-stu-id="6fcae-132">Bugs</span></span>

- <span data-ttu-id="6fcae-133">[Regresión] en 15.5p1: se omite Portable0.0: [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="6fcae-133">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="6fcae-134">Faltan recursos de los paquetes después de la restauración: [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="6fcae-134">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="6fcae-135">Los proveedores de credenciales de complementos no funcionan con los URI que contienen espacios: [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="6fcae-135">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="6fcae-136">Si se produce un error al restaurar el paquete, se debe imprimir el error en la salida, aunque la opción de detalle mínimo esté activada: [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="6fcae-136">If package failed to restore, error should be printed i the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="6fcae-137">dotnet restore a nivel de solución no sigue ProjectReference con ReferenceOutputAssembly al comportar incorrectamente errores de compilación aleatorios: [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="6fcae-137">dotnet restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="6fcae-138">Autocompletar en PMC funciona incorrectamente con métodos de objeto: [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="6fcae-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="6fcae-139">Se produce un error en la restauración de nuget.exe con el conjunto de herramientas de Visual Studio 2015: [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="6fcae-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="6fcae-140">Crear instancias de perf - pmc en vs2017 es costoso: [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="6fcae-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="6fcae-141">Lentitud para obtener información de dependencias en una conexión lenta: [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="6fcae-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="6fcae-142">Se produce un error de uninstall-package w/ -RemoveDependencies si varios paquetes comparten una dependencia común: [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="6fcae-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="6fcae-143">Finalizar NuGet.Core.nupkg para la publicación: [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="6fcae-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="6fcae-144">El paquete de NuGet resuelve el Id. de dependencia del nombre de directorio cuando se usa -IncludeProjectReferences para csproj + project.json: [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="6fcae-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="6fcae-145">El inicializador de tipo para "NuGet.ProxyCache" generó una excepción: [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="6fcae-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="6fcae-146">problema de rendimiento en la restauración de nuget con kudu: [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="6fcae-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="6fcae-147">Se produce un error en el cliente de la interfaz de usuario al mostrar errores o advertencias cuando la búsqueda está por delante de los blobs de registro: [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="6fcae-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="6fcae-148">Get-Packages-Updates genera una consulta incorrecta: [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="6fcae-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="6fcae-149">Vínculos a problemas de GitHub corregidos en 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="6fcae-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="6fcae-150">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="6fcae-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
