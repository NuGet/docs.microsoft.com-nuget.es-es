---
title: Notas de la versión 5.0 preview de NuGet
description: Notas de la versión para las versiones preliminares de NuGet 5.0 incluidos problemas conocidos, correcciones de errores, nuevas características y dcr.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247664"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="52872-103">Notas de la versión preliminar 5.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="52872-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="52872-104">Versiones 5.0 Preview de NuGet</span><span class="sxs-lookup"><span data-stu-id="52872-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="52872-105">13 de febrero de 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="52872-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="52872-106">23 de enero de 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="52872-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="52872-107">Resumen: Novedades en NuGet 5.0 Preview 3</span><span class="sxs-lookup"><span data-stu-id="52872-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="52872-108">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="52872-108">Issues fixed in this release</span></span> 

<span data-ttu-id="52872-109">**Errores:**</span><span class="sxs-lookup"><span data-stu-id="52872-109">**Bugs:**</span></span>

* <span data-ttu-id="52872-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="52872-110">nuget.exe /?</span></span> <span data-ttu-id="52872-111">debe enumerar las versiones correctas de msbuild - [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="52872-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="52872-112">NuGet.targets(498,5): error: No se encontró una parte de la ruta de acceso ' / tmp/NuGetScratch - en mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="52872-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="52872-113">restauración innecesariamente enumera el contenido de todas las versiones de paquete que se hace referencia en la caché del equipo - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="52872-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="52872-114">Detección automática de MSBuild siempre selecciona 16.0 después de obtener una vista previa en la instalación de VS 2019 - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="52872-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="52872-115">paquete de dotnet lista en una solución genera entradas duplicadas para framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="52872-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="52872-116">Excepción "el nombre de ruta de acceso vacía no es legal" cuando IVsPackageInstaller.InstallPackage que realiza la llamada en el antiguo proyectos y paquetes de la carpeta no existe.</span><span class="sxs-lookup"><span data-stu-id="52872-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="52872-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="52872-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="52872-118">nivel de detalle de MSBuild/t: Restore mínimo debe ser más mínimo - [4695 #](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="52872-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="52872-119">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="52872-119">**DCRs**</span></span>

* <span data-ttu-id="52872-120">Permitir que los autores de paquetes definir el comportamiento de compilación activos transitiva - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="52872-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="52872-121">Habilitar la restauración en VS se realice correctamente si un proyecto no forma parte de la solución o no está cargado, pero anteriormente se ha restaurado - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="52872-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="52872-122">Resumen: Novedades de 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="52872-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="52872-123">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="52872-123">Issues fixed in this release</span></span>

<span data-ttu-id="52872-124">**Errores:**</span><span class="sxs-lookup"><span data-stu-id="52872-124">**Bugs:**</span></span>

* <span data-ttu-id="52872-125">VS de 16.0 NuGet UI tiene pestañas ilegibles debido a problemas de color - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="52872-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="52872-126">NuGet.Core & NuGet.Clients License.txt aclaración - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="52872-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="52872-127">Restauración innecesariamente enumera la carpeta de paquetes global en intentar determinar el tipo - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="52872-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="52872-128">Errores de cumplimiento del archivo de bloqueo deberían aparecer en la ventana Lista de errores - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="52872-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="52872-129">Solucionar problemas de NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="52872-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="52872-130">Adaptarse a la actualización de MSBuild de la ubicación de instalación.</span><span class="sxs-lookup"><span data-stu-id="52872-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="52872-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="52872-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="52872-132">NuGet.Build.Tasks.Pack debe ser una dependencia de desarrollo - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="52872-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="52872-133">Agregar paquete de punto de extensión para incluir depurar símbolos - [7234 #](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="52872-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="52872-134">dotnet pack debe conservar el intervalo de versiones de dependencia en el nupkg creado.</span><span class="sxs-lookup"><span data-stu-id="52872-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="52872-135">(incluso si se usa la versión flotante) - [7232 #](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="52872-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="52872-136">restauración de dotnet se produce un error en un origen autenticado cuando la configuración de nivel de usuario también tiene el origen: [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="52872-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="52872-137">Módulo no debe restringir el conjunto de BuildActions para archivos de contenido - [7155 #](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="52872-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="52872-138">Mediante un projectreference que requiere AssetTargetFallback se realice correctamente, debería advertir.</span><span class="sxs-lookup"><span data-stu-id="52872-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="52872-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="52872-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="52872-140">Interbloqueo debido a problemas de subprocesamiento al llamar a CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="52872-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="52872-141">dotnet Agregar paquete no utilice credenciales desde la configuración global para un origen especificado en la configuración local: [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="52872-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="52872-142">Problemas de subprocesamiento con MEF que se va a llamar en async codepaths - [6771 #](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="52872-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="52872-143">De firma: error notificado dos veces y sin la pila de llamadas - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="52872-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="52872-144">Instalar un paquete firmado con certificado de firma de confianza debería mostrar el error - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="52872-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="52872-145">Restauración de NuGet incorrectamente NOOP cuando 2 proyectos están compartiendo el directorio obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="52872-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="52872-146">No se puede usar PAT con dotnet se restaura en Linux con paquetes de fuente autenticado - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="52872-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="52872-147">se produce un error en la restauración de dotnet debido a la amplia deshabilitado máquina fuente - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="52872-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="52872-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="52872-148">**DCRs**</span></span>

* <span data-ttu-id="52872-149">Los ensamblados de NuGet 5.0 requieren .NET 4.7.2 (a través de cambio TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="52872-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="52872-150">NuGetLicenseData desde NuGet.Packaging debe ser un tipo público.</span><span class="sxs-lookup"><span data-stu-id="52872-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="52872-151">Actualizar los metadatos de licencia ingerido desde spdx.</span><span class="sxs-lookup"><span data-stu-id="52872-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="52872-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="52872-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="52872-153">Quitar de la API de configuración obsoletas - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="52872-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="52872-154">Tiempos de espera de restauración de solución alternativa en sistemas con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="52872-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="52872-155">NuGet prefiere la autenticación NTLM, incluso si no hay credenciales en NuGet.config: agregar la opción de configuración para filtrar los tipos de autenticación de credenciales: [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="52872-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="52872-156">Habilitar EmbedInteropTypes packagereference (capacidad de búsqueda de coincidencias Packages.Config) - [2365 #](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="52872-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="52872-157">Lista de todos los problemas corregidos en esta versión 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="52872-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="52872-158">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="52872-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="52872-159">dotnet nuget push --interactive produce un error en un equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="52872-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="52872-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="52872-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="52872-161">**Problema** el `--interactive` argumento no se reenvía mediante la cli de dotnet y da como resultado el error `error: Missing value for option 'interactive'` 
 **solución** ejecute cualquier otro comando de dotnet con la opción interactiva como `dotnet restore --interactive` y autenticarse.</span><span class="sxs-lookup"><span data-stu-id="52872-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="52872-162">La autenticación se puede almacenar en caché por el proveedor de credenciales.</span><span class="sxs-lookup"><span data-stu-id="52872-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="52872-163">Después, ejecute `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="52872-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="52872-164">Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma.</span><span class="sxs-lookup"><span data-stu-id="52872-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="52872-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="52872-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="52872-166">**Problema** al usar dotnet.exe 2.x para restaurar esa netcoreapp varios destino de un proyecto 1.x y netcoreapp 2.x, la carpeta de reserva se trata como un archivo de fuente.</span><span class="sxs-lookup"><span data-stu-id="52872-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="52872-167">Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.</span><span class="sxs-lookup"><span data-stu-id="52872-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="52872-168">**Solución alternativa** deshabilitar el uso de la carpeta reserva estableciendo el `RestoreAdditionalProjectSources` en nothing.</span><span class="sxs-lookup"><span data-stu-id="52872-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="52872-169">`<RestoreAdditionalProjectSources/>` Use esta opción con precaución, ya que provocará que muchos paquetes, que de otro modo se habrían restaurado de la carpeta de reserva, se descarguen de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="52872-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
