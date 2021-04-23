---
title: Notas de la versión de NuGet 5.0 RTM
description: Notas de la versión de NuGet 5.0, incluidos problemas conocidos, correcciones de errores, nuevas características y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901751"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="7cb28-103">Notas de la versión de NuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="7cb28-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="7cb28-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="7cb28-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="7cb28-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="7cb28-105">NuGet version</span></span> | <span data-ttu-id="7cb28-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7cb28-106">Available in Visual Studio version</span></span>| <span data-ttu-id="7cb28-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="7cb28-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="7cb28-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="7cb28-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="7cb28-109">Visual Studio 2019, versión 16.0</span><span class="sxs-lookup"><span data-stu-id="7cb28-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="7cb28-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="7cb28-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="7cb28-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="7cb28-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="7cb28-112">Visual Studio 2019, versión 16.0.4</span><span class="sxs-lookup"><span data-stu-id="7cb28-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="7cb28-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="7cb28-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="7cb28-114"><sup>1</sup> Instalado con Visual Studio 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="7cb28-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="7cb28-115"><sup>2</sup> Disponible como instalación opcional con Visual Studio 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="7cb28-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="7cb28-116">Resumen: Novedades de la versión 5.0</span><span class="sxs-lookup"><span data-stu-id="7cb28-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="7cb28-117">Compatibilidad con la restauración [de soluciones](/visualstudio/ide/filtered-solutions) filtradas en Visual Studio 2019: [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="7cb28-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="7cb28-118">`BuildTransitive` la carpeta permite que los paquetes contribuyan de forma transitiva a destinos o propiedades al proyecto [host: #6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="7cb28-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="7cb28-119">Mejor compatibilidad con escenarios packageReference en las API de IVs de [NuGet: #7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="7cb28-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="7cb28-120">`nuget.exe pack project.json` ha quedado en [desuso: #7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="7cb28-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="7cb28-121">Gen 1 Proveedor de credenciales complemento ha sido reemplazado por [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) y pronto estará en desuso: [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="7cb28-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7cb28-122">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="7cb28-122">Issues fixed in this release</span></span>

<span data-ttu-id="7cb28-123">**Errores**</span><span class="sxs-lookup"><span data-stu-id="7cb28-123">**Bugs**</span></span>

* <span data-ttu-id="7cb28-124">Al realizar una restauración NoOp, evite \*.dgspec.jsal escribir en el directorio obj [: #7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="7cb28-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="7cb28-125">Los permisos de los archivos creados dentro de ~/.nuget están demasiado [abiertos: #7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="7cb28-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="7cb28-126">`dotnet list package --outdated` no funciona con orígenes que necesitan autenticación: [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="7cb28-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="7cb28-127">NuGet.VisualStudio.IVsPackageInstaller: llamar a en un proyecto sin referencias de paquete siempre usa packages.config, incluso si el valor predeterminado está establecido en PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="7cb28-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="7cb28-128">PMC: Update-Package reinstalación produce un error ("No se encuentra el paquete") en los paquetes deslistados.</span><span class="sxs-lookup"><span data-stu-id="7cb28-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="7cb28-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="7cb28-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="7cb28-130">Agregar aviso de terceros en nuestro repositorio y [VSIX: #7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="7cb28-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="7cb28-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage debe instalar la versión más reciente cuando no se proporciona ninguna [versión: #7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="7cb28-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="7cb28-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="7cb28-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="7cb28-133">Al restaurar con el archivo de bloqueo, no se debe generar la advertencia NU1603.</span><span class="sxs-lookup"><span data-stu-id="7cb28-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="7cb28-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="7cb28-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="7cb28-135">NuGet no debe imprimir la ruta de acceso del proyecto durante la restauración con un registro [mínimo: #7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="7cb28-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="7cb28-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="7cb28-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="7cb28-137">Adición de NuGet.Packaging.Core con TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="7cb28-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="7cb28-138">plugins_cache ruta de acceso más corta para funcionar [bien: #7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="7cb28-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="7cb28-139">Se prefiere la ruta de acceso para la detección de msbuild si el usuario no ha solicitado una versión específica de msbuild: [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="7cb28-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="7cb28-140">`nuget.exe /?` debe enumerar las versiones correctas de msbuild: [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="7cb28-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="7cb28-141">NuGet.targets(498,5): error: No se encontró una parte de la ruta de acceso '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="7cb28-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="7cb28-142">restore enumera innecesariamente el contenido de todas las versiones del paquete al que se hace referencia en la memoria caché de [la máquina: #7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="7cb28-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="7cb28-143">La detección automática de MSBuild siempre selecciona la versión 16.0 después de instalar VS 2019 Preview [- #7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="7cb28-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="7cb28-144">El paquete dotnet list de una solución genera entradas duplicadas para [framework: #7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="7cb28-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="7cb28-145">Excepción "El nombre de ruta de acceso vacía no es legal" al llamar a IVsPackageInstaller.InstallPackage en proyectos antiguos y la carpeta packages no existe.</span><span class="sxs-lookup"><span data-stu-id="7cb28-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="7cb28-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="7cb28-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="7cb28-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="7cb28-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="7cb28-148">La interfaz de usuario de NuGet de VS 16.0 tiene pestañas ilegibles debido a problemas de [color: #7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="7cb28-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="7cb28-149">NuGet.Core & nuget.clients License.txt aclaración: [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="7cb28-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="7cb28-150">La restauración enumera innecesariamente la carpeta de paquetes global para intentar determinar el [tipo: #7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="7cb28-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="7cb28-151">Los errores del cumplimiento del archivo de bloqueo deben aparecer en la ventana Lista de errores [( #7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="7cb28-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="7cb28-152">Corrección NuGet.Configproblemas de uration: [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="7cb28-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="7cb28-153">Adaptarse a MSBuild actualizando su ubicación de [instalación: #7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="7cb28-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="7cb28-154">NuGet.Build.Tasks.Pack debe ser una dependencia de [desarrollo: #7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="7cb28-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="7cb28-155">Agregar punto de extensión de paquete para incluir símbolos de [depuración: #7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="7cb28-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="7cb28-156">`dotnet pack` debe conservar el intervalo de versiones de dependencia en el nupkg creado (incluso si se usa la versión [flotante): #7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="7cb28-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="7cb28-157">`dotnet restore` se produce un error en el origen autenticado cuando la configuración de nivel de usuario también tiene [origen: #7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="7cb28-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="7cb28-158">Pack no debe restringir el conjunto de BuildActions para los archivos de [contenido: #7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="7cb28-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="7cb28-159">El uso de ProjectReference que requiere AssetTargetFallback para realizarse correctamente, debe advertir.</span><span class="sxs-lookup"><span data-stu-id="7cb28-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="7cb28-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="7cb28-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="7cb28-161">Interbloqueo debido a problemas de subprocesos al llamar a CPS (CommonProjectSystem): [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="7cb28-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="7cb28-162">`dotnet add package` no usa credenciales de la configuración global para un origen especificado en la configuración [local: #6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="7cb28-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="7cb28-163">Problemas de subprocesos con MEF que se llama en rutas de acceso de código [asincrónico: #6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="7cb28-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="7cb28-164">Firma: error notificado dos veces y sin pila de [llamadas: #6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="7cb28-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="7cb28-165">La instalación de un paquete firmado con un certificado de firma que no es de confianza debería mostrar un [error: #6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="7cb28-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="7cb28-166">NoOps de restauración incorrecta de NuGet cuando dos proyectos comparten el directorio [obj: #6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="7cb28-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="7cb28-167">No se puede usar PAT `dotnet restore` con en Linux con paquetes de fuente autenticada: [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="7cb28-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="7cb28-168">dotnet restore se produce un error debido a una fuente de alimentación de toda la [máquina deshabilitada: #5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="7cb28-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="7cb28-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="7cb28-169">**DCRs**</span></span>

* <span data-ttu-id="7cb28-170">Advertir de la eliminación futura de "dotnet pack project.js[on": #7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="7cb28-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="7cb28-171">Agregar una advertencia de desuso para el complemento de credenciales [gen1: #7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="7cb28-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="7cb28-172">Firma: se ha habilitado el repositorio para requerir la comprobación del cliente de todos los paquetes como repositorio firmados (a través del recurso RepositorySignatures/5.0.0) [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="7cb28-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="7cb28-173">limitar el número de solicitud HTTP por origen a NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="7cb28-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="7cb28-174">NuGet debe tener como destino Net472 (para ayudar a limpiar la compilación 16.0 de VSIX): [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="7cb28-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="7cb28-175">PMC: quitar el comando OpenPackagePage [: #7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="7cb28-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="7cb28-176">Hacer que NetCoreApp 3.0 se asigne a NetStandard 2.1: [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="7cb28-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="7cb28-177">Adición de compatibilidad con netstandard2.0 a paquetes NuGet.\*: [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="7cb28-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="7cb28-178">Permitir a los autores de paquetes definir el comportamiento transitivo de los recursos de [compilación: #6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="7cb28-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="7cb28-179">Compatibilidad con la característica filtro de soluciones de VS 2019.</span><span class="sxs-lookup"><span data-stu-id="7cb28-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="7cb28-180">También admite proyectos que no están en la solución o proyectos descargados.</span><span class="sxs-lookup"><span data-stu-id="7cb28-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="7cb28-181">Primero es necesario restaurar la solución completa (a través de la CLI o VS): [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="7cb28-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="7cb28-182">Ensamblados de NuGet 5.0 para requerir .NET 4.7.2 (mediante cambio de TFM): [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="7cb28-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="7cb28-183">NuGetLicenseData de NuGet.Packaging debe ser un tipo público.</span><span class="sxs-lookup"><span data-stu-id="7cb28-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="7cb28-184">Actualice los metadatos de licencia ingeridos desde spdx.</span><span class="sxs-lookup"><span data-stu-id="7cb28-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="7cb28-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="7cb28-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="7cb28-186">Eliminación de las API de configuración [obsoletas: #7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="7cb28-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="7cb28-187">Tiempos de espera de restauración de solución alternativa en sistemas con 1 [CPU: #6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="7cb28-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="7cb28-188">NuGet prefiere la autenticación NTLM incluso si hay credenciales en NuGet.config: agregar la opción de configuración para filtrar los tipos de autenticación por las [credenciales: #5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="7cb28-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="7cb28-189">Habilitación de EmbedInteropTypes para PackageReference (Packages.Config capacidad de coincidencia): [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="7cb28-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="7cb28-190">**[Lista de todos los problemas corregidos en esta versión: 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="7cb28-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="7cb28-191">Resumen: Novedades de la versión 5.0.2</span><span class="sxs-lookup"><span data-stu-id="7cb28-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="7cb28-192">Seguridad (cuando se ejecuta mediante dotnet.exe o mono.exe): la carpeta obj debe crearse con los permisos correctos [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="7cb28-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="7cb28-193">nuget.exe restauración en mono/MacOS produce un error con nuget.config y `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="7cb28-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="7cb28-194">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="7cb28-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="7cb28-195">Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma.</span><span class="sxs-lookup"><span data-stu-id="7cb28-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="7cb28-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="7cb28-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="7cb28-197">Problema</span><span class="sxs-lookup"><span data-stu-id="7cb28-197">Issue</span></span>
<span data-ttu-id="7cb28-198">Cuando se usa dotnet.exe 2.x para restaurar un proyecto que tiene como destinos múltiples netcoreapp 1.x y netcoreapp 2.x, la carpeta de reserva se trata como una fuente de archivos.</span><span class="sxs-lookup"><span data-stu-id="7cb28-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="7cb28-199">Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.</span><span class="sxs-lookup"><span data-stu-id="7cb28-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="7cb28-200">Solución alternativa</span><span class="sxs-lookup"><span data-stu-id="7cb28-200">Workaround</span></span>
<span data-ttu-id="7cb28-201">Deshabilite el uso de la carpeta de reserva estableciendo `RestoreAdditionalProjectSources` en nothing:</span><span class="sxs-lookup"><span data-stu-id="7cb28-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="7cb28-202">Úsese esto con precaución, ya que los paquetes que se restaurarían desde la carpeta de reserva ahora se descargarán de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="7cb28-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>