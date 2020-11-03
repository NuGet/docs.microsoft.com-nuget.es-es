---
title: Notas de la versión de NuGet 5,0 RTM
description: Notas de la versión de NuGet 5,0, incluidos problemas conocidos, correcciones de errores, nuevas características y DCR.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: e4a6be7fb26e3cc4bd297eaf02999f6ac1389b77
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236807"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="31360-103">Notas de la versión de NuGet 5,0</span><span class="sxs-lookup"><span data-stu-id="31360-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="31360-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="31360-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="31360-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="31360-105">NuGet version</span></span> | <span data-ttu-id="31360-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31360-106">Available in Visual Studio version</span></span>| <span data-ttu-id="31360-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="31360-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="31360-108">**ó**</span><span class="sxs-lookup"><span data-stu-id="31360-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="31360-109">Visual Studio 2019, versión 16.0</span><span class="sxs-lookup"><span data-stu-id="31360-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="31360-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="31360-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="31360-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="31360-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="31360-112">Visual Studio 2019 versión 16.0.4</span><span class="sxs-lookup"><span data-stu-id="31360-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="31360-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="31360-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="31360-114"><sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="31360-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="31360-115"><sup>2</sup> Disponible como instalación opcional con Visual Studio 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="31360-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="31360-116">Resumen: novedades en 5,0</span><span class="sxs-lookup"><span data-stu-id="31360-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="31360-117">Compatibilidad con la restauración de [soluciones filtradas](/visualstudio/ide/filtered-solutions?view=vs-2019) en Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="31360-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="31360-118">`BuildTransitive` la carpeta permite que los paquetes contribuyan de forma transitiva a los destinos y las propiedades al proyecto host: [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="31360-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="31360-119">Mejor compatibilidad con escenarios de PackageReference en las API de IV de NuGet: [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="31360-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="31360-120">`nuget.exe pack project.json` está en desuso- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="31360-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="31360-121">El complemento del proveedor de credenciales de gen. 1 ha sido sustituido por la [generación 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) y pronto quedará en desuso: [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="31360-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="31360-122">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="31360-122">Issues fixed in this release</span></span>

<span data-ttu-id="31360-123">**Errores**</span><span class="sxs-lookup"><span data-stu-id="31360-123">**Bugs**</span></span>

* <span data-ttu-id="31360-124">Al realizar una restauración de NoOp, evite \* .dgspec.jsal escribir en el directorio obj [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="31360-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="31360-125">Los permisos de los archivos creados dentro de ~/.Nuget son demasiado abiertos [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="31360-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="31360-126">`dotnet list package --outdated` no funciona con orígenes que necesitan autenticación [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="31360-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="31360-127">NuGet. VisualStudio. IVsPackageInstaller: la llamada a en un proyecto sin referencias de paquete siempre usa packages.config, incluso si el valor predeterminado está establecido en PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="31360-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="31360-128">PMC: Update-Package se produce un error en la reinstalación ("no se puede encontrar el paquete") en los paquetes que se han dado de alta.</span><span class="sxs-lookup"><span data-stu-id="31360-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="31360-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="31360-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="31360-130">Agregue el aviso de terceros en nuestro repositorio y VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="31360-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="31360-131">NuGet. VisualStudio. IVsPackageInstaller. InstallPackage debe instalar la versión más reciente cuando no haya ninguna versión especificada- [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="31360-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="31360-132">--compatibilidad interactiva para la [#7519](https://github.com/NuGet/Home/issues/7519) de Nuget de dotnet</span><span class="sxs-lookup"><span data-stu-id="31360-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="31360-133">Al restaurar con el archivo de bloqueo, no se debe generar la advertencia NU1603.</span><span class="sxs-lookup"><span data-stu-id="31360-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="31360-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="31360-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="31360-135">NuGet no debe imprimir la ruta de acceso del proyecto durante la restauración con un registro mínimo [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="31360-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="31360-136">--compatibilidad interactiva para la eliminación de paquetes de dotnet- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="31360-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="31360-137">Vuelva a agregar NuGet. Packaging. Core con TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="31360-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="31360-138">plugins_cache necesita una ruta de acceso más corta para trabajar correctamente [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="31360-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="31360-139">Preferir la ruta de acceso para la detección de MSBuild si el usuario no solicitó una versión específica de MSBuild: [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="31360-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="31360-140">`nuget.exe /?` deben mostrarse las versiones correctas de MSBuild: [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="31360-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="31360-141">NuGet. targets (498, 5): error: no se encontró una parte de la ruta de acceso '/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="31360-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="31360-142">restore innecesariamente enumera el contenido de todas las versiones del paquete al que se hace referencia en la memoria caché del equipo: [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="31360-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="31360-143">La detección automática de MSBuild siempre selecciona 16,0 después de instalar VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="31360-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="31360-144">el paquete dotnet List de una solución genera entradas duplicadas para Framework- [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="31360-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="31360-145">Excepción: "el nombre de la ruta de acceso vacía no es legal" al llamar a IVsPackageInstaller. InstallPackage en proyectos antiguos y la carpeta de paquetes no existe.</span><span class="sxs-lookup"><span data-stu-id="31360-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="31360-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="31360-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="31360-147">el nivel de detalle mínimo de MSBuild/t: restore debe ser más mínimo [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="31360-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="31360-148">La interfaz de usuario de NuGet de VS 16,0 tiene pestañas ilegibles debido a problemas de color: [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="31360-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="31360-149">NuGet. Core & NuGet. clients License.txt aclaración: [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="31360-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="31360-150">Restore innecesariamente enumera la carpeta del paquete global al intentar determinar el tipo [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="31360-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="31360-151">Los errores de la aplicación de archivos de bloqueo deben aparecer en Lista de errores ventana- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="31360-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="31360-152">Solución de problemas de primario NuGet.Config- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="31360-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="31360-153">Adaptación a MSBuild actualizar su ubicación de instalación: [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="31360-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="31360-154">NuGet. Build. Tasks. Pack debe ser una dependencia de desarrollo [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="31360-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="31360-155">Agregar el punto de extensión del paquete para incluir símbolos de depuración: [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="31360-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="31360-156">`dotnet pack` debe conservar el intervalo de versiones de dependencia en el nupkg creado (aunque se use la versión flotante)- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="31360-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="31360-157">`dotnet restore` error en el origen autenticado cuando la configuración de nivel de usuario también tiene origen [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="31360-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="31360-158">Pack no debe restringir el conjunto de BuildActions para los archivos de contenido [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="31360-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="31360-159">El uso de ProjectReference, que requiere que AssetTargetFallback se realice correctamente, debería advertir.</span><span class="sxs-lookup"><span data-stu-id="31360-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="31360-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="31360-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="31360-161">Interbloqueo debido a problemas de subprocesos al llamar a CPS (CommonProjectSystem)- [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="31360-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="31360-162">`dotnet add package` no usa credenciales de la configuración global para un origen especificado en la configuración local: [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="31360-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="31360-163">Problemas de subprocesos con MEF al que se llama en rutas de acceso de código Async- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="31360-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="31360-164">Firma: error que se ha registrado dos veces y sin pila de llamadas: [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="31360-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="31360-165">La instalación de un paquete firmado con un certificado de firma que no es de confianza debería mostrar el error [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="31360-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="31360-166">La restauración de NuGet no se NOOP correctamente cuando dos proyectos comparten el directorio obj [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="31360-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="31360-167">No se puede usar PAT con `dotnet restore` en Linux con paquetes de fuentes autenticadas: [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="31360-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="31360-168">dotnet restore produce un error debido a la deshabilitación de la alimentación en todo el equipo- [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="31360-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="31360-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="31360-169">**DCRs**</span></span>

* <span data-ttu-id="31360-170">ADVERTENCIA de eliminación futura de "dotnet Pack project.jsen"- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="31360-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="31360-171">Agregar una advertencia de desuso para el complemento de credenciales de GEN1- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="31360-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="31360-172">Firma: repositorio habilitado para requerir la comprobación de cliente de cada paquete como repositorio firmado--a través de la [#7759](https://github.com/NuGet/Home/issues/7759) de recursos de RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="31360-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="31360-173">limite el número de solicitud HTTP por origen a través de NuGet.Config [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="31360-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="31360-174">NuGet debe tener como destino Net472 (para ayudar a limpiar la compilación 16,0 de VSIX)- [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="31360-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="31360-175">PMC: quitar [#7384](https://github.com/NuGet/Home/issues/7384) de comandos de OpenPackagePage</span><span class="sxs-lookup"><span data-stu-id="31360-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="31360-176">Asignación de NetCoreApp 3,0 a NetStandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="31360-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="31360-177">Incorporación de compatibilidad con netstandard 2.0 a los paquetes de NuGet. \* [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="31360-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="31360-178">Permitir a los autores de paquetes definir el comportamiento transitivo de los recursos de compilación: [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="31360-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="31360-179">Compatibilidad con la característica filtro de solución de VS 2019.</span><span class="sxs-lookup"><span data-stu-id="31360-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="31360-180">También admite proyectos que no están en la solución o que no están cargados.</span><span class="sxs-lookup"><span data-stu-id="31360-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="31360-181">Necesidad de restaurar la solución completa (a través de la CLI o VS) en primer lugar [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="31360-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="31360-182">Ensamblados de NuGet 5,0 para requerir .NET 4.7.2 (a través del cambio de TFM)- [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="31360-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="31360-183">NuGetLicenseData de NuGet. el empaquetado debe ser un tipo público.</span><span class="sxs-lookup"><span data-stu-id="31360-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="31360-184">Actualice los metadatos de la licencia de spdx.</span><span class="sxs-lookup"><span data-stu-id="31360-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="31360-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="31360-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="31360-186">Quitar las API de configuración obsoletas: [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="31360-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="31360-187">Solución de tiempos de espera de restauración en sistemas con 1 CPU: [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="31360-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="31360-188">NuGet prefiere la autenticación NTLM aunque haya credenciales en NuGet.config opción Agregar configuración para filtrar los tipos de autenticación para las credenciales- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="31360-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="31360-189">Habilitación de EmbedInteropTypes para PackageReference (funcionalidad de Packages.Config coincidente)- [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="31360-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="31360-190">**[Lista de todos los problemas corregidos en esta versión: 5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="31360-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="31360-191">Resumen: novedades de 5.0.2</span><span class="sxs-lookup"><span data-stu-id="31360-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="31360-192">Seguridad (cuando se ejecuta a través de dotnet.exe o mono.exe): la carpeta obj debe crearse con los permisos correctos [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="31360-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="31360-193">nuget.exe se produce un error en la restauración en mono/MacOS con nuget.config y `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011) personalizados</span><span class="sxs-lookup"><span data-stu-id="31360-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="31360-194">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="31360-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="31360-195">Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma.</span><span class="sxs-lookup"><span data-stu-id="31360-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="31360-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="31360-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="31360-197">Incidencia</span><span class="sxs-lookup"><span data-stu-id="31360-197">Issue</span></span>
<span data-ttu-id="31360-198">Cuando se usa dotnet.exe 2.x para restaurar un proyecto que tiene como destinos múltiples netcoreapp 1.x y netcoreapp 2.x, la carpeta de reserva se trata como una fuente de archivos.</span><span class="sxs-lookup"><span data-stu-id="31360-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="31360-199">Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.</span><span class="sxs-lookup"><span data-stu-id="31360-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="31360-200">Solución alternativa</span><span class="sxs-lookup"><span data-stu-id="31360-200">Workaround</span></span>
<span data-ttu-id="31360-201">Deshabilite el uso de la carpeta de reserva estableciendo el `RestoreAdditionalProjectSources` en nada:</span><span class="sxs-lookup"><span data-stu-id="31360-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="31360-202">Utilícelo con precaución, ya que los paquetes que se restaurarán desde la carpeta de reserva se descargarán ahora desde NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="31360-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>