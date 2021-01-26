---
title: Notas de la versión de 3,5 RC
description: Notas de la versión de NuGet 3,5 RC, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780199"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="abb4f-103">Notas de la versión de NuGet 3,5 RC</span><span class="sxs-lookup"><span data-stu-id="abb4f-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="abb4f-104">[Notas de la versión de NuGet 3,5-beta2](../release-notes/nuget-3.5-Beta2.md)  |  [Notas de la versión de NuGet 3,5-RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="abb4f-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="abb4f-105">la versión 3,5 se centra en mejorar la calidad y el rendimiento de los clientes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="abb4f-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="abb4f-106">Además, hemos incluido algunas características, como la compatibilidad con [carpetas de reserva](https://github.com/NuGet/Home/issues/2899), la compatibilidad con [PackageType](https://github.com/NuGet/Home/issues/2476) en `.nuspec` y más.</span><span class="sxs-lookup"><span data-stu-id="abb4f-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="abb4f-107">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="abb4f-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="abb4f-108">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="abb4f-108">Bug Fixes</span></span>

* <span data-ttu-id="abb4f-109">Se produce un error en la instalación o restauración de un paquete con "el paquete contiene varios `.nuspec` archivos".</span><span class="sxs-lookup"><span data-stu-id="abb4f-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="abb4f-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="abb4f-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="abb4f-111">el paquete de Nuget agrega `.tt` archivos a la carpeta de contenido con independencia de lo que [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="abb4f-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="abb4f-112">el archivo csproj de Nuget Pack (with `project.json` ) se bloquea si no hay packOptions y Owner en el archivo JSON [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="abb4f-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="abb4f-113">el paquete de Nuget para `project.json` omite las etiquetas packOptions como Summary, authors, Owners, etc- [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="abb4f-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="abb4f-114">el paquete de Nuget omite las dependencias en la salida `.nuspec` de `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="abb4f-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="abb4f-115">La actualización de varios paquetes con reversión deja el proyecto en un estado interrumpido: [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="abb4f-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="abb4f-116">ContentFiles en cualquiera no se agregan para los proyectos de netstandard: [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="abb4f-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="abb4f-117">No se puede empaquetar la biblioteca que tiene como destino .net Standard correctamente- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="abb4f-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="abb4f-118">Archivo-> nuevo proyecto de biblioteca de clases > de proyectos (portable) error en VS2015 y Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="abb4f-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="abb4f-119">Error de NuGet-1.0.0-\* no es una cadena de versión válida: [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="abb4f-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="abb4f-120">Find-Package no se puede mostrar pero Install-Package trabajos- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="abb4f-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="abb4f-121">Error al "Install-Package jQuery. Validation" en dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="abb4f-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="abb4f-122">Cuando se instala VS 2015 Update 3 en un frente a que usa NuGet versión 3.5.0 se produce un error: [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="abb4f-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="abb4f-123">Interfaz de usuario del administrador de paquetes: no muestra la nueva versión después de actualizar un paquete- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="abb4f-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="abb4f-124">-ApiKey en la línea de comandos de eliminación no se lee ni envía en 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="abb4f-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="abb4f-125">Cadena incorrecta: una versión estable de un paquete no debe tener una dependencia de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="abb4f-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="abb4f-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="abb4f-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="abb4f-127">Creación de una excepción de proyecto de PCL (net46 y Windows 10) NullRef.</span><span class="sxs-lookup"><span data-stu-id="abb4f-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="abb4f-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="abb4f-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="abb4f-129">La actualización de Nuget debe proporcionar un mensaje informativo cuando una versión superior está restringida por la restricción allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="abb4f-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="abb4f-130">El complemento de credencial salió del error-1/error al descargar el paquete al usar proveedores de credenciales con varios orígenes: [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="abb4f-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="abb4f-131">paquete de Nuget: falta Newtonsoft.Jsen la dependencia del paquete [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="abb4f-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="abb4f-132">Error en ExecuteSynchronizedCore en Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="abb4f-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="abb4f-133">VS no es compatible con las variables de entorno de repositoryPath (nuget.exe sí) [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="abb4f-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="abb4f-134">Corregir problemas de accesibilidad: [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="abb4f-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="abb4f-135">Se rechazan los marcos portátiles con perfiles con guiones.</span><span class="sxs-lookup"><span data-stu-id="abb4f-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="abb4f-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="abb4f-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="abb4f-137">El administrador de paquetes NuGet debe dejar claro que la lista de opciones en los detalles de los paquetes no se aplica a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="abb4f-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="abb4f-138">Error de actualización de 3.3.0 de NuGet con ' restricción adicional... definido en packages.config impide esta operación. "</span><span class="sxs-lookup"><span data-stu-id="abb4f-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="abb4f-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="abb4f-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="abb4f-140">La instalación de un paquete desde un origen local que no existe produce un mensaje fantasma [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="abb4f-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="abb4f-141">El filtro "la actualización es válido" muestra las actualizaciones que infringen la restricción de versión- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="abb4f-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="abb4f-142">Mejoras de rendimiento</span><span class="sxs-lookup"><span data-stu-id="abb4f-142">Performance Improvements</span></span>

* <span data-ttu-id="abb4f-143">Rendimiento: mejorar el análisis de la plataforma de destino de ContentModel: [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="abb4f-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="abb4f-144">Rendimiento: Evite leer `runtime.json` archivos de restauraciones que no tengan rid [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="abb4f-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="abb4f-145">En los equipos de CI, la restauración de una aplicación Web ASP.NET de ejemplo se ha reducido de más de 15 segundos a 3 segundos.</span><span class="sxs-lookup"><span data-stu-id="abb4f-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="abb4f-146">Rendimiento: la consola del administrador de paquetes init.ps1 tiempo de carga [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="abb4f-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="abb4f-147">Tiempo de apertura de PackageManagerConsole mejorado en algunos casos, de 132s a decenas.</span><span class="sxs-lookup"><span data-stu-id="abb4f-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="abb4f-148">Solución de problemas de rendimiento de ReSharper en la actualización de NuGet: [#3044](https://github.com/NuGet/Home/issues/3044): en un proyecto de ejemplo, el tiempo necesario para instalar paquetes se reduce de 140S a 68S.</span><span class="sxs-lookup"><span data-stu-id="abb4f-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="abb4f-149">DCR</span><span class="sxs-lookup"><span data-stu-id="abb4f-149">DCRs</span></span>

* <span data-ttu-id="abb4f-150">NuGet debe informar a los usuarios de que la actualización o instalación en un PCL basado en dotnet TFM podría causar problemas [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="abb4f-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="abb4f-151">Advertir instalación o actualización erróneas del proyecto w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="abb4f-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="abb4f-152">Agregar compatibilidad con netcoreapp11 y netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="abb4f-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="abb4f-153">Imprimir el contenido del encabezado NuGet-Warning en la consola en nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="abb4f-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="abb4f-154">Aprovechar el atributo Assemblymetadata (para `.nuspec` reemplazos de tokens: [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="abb4f-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="abb4f-155">Quite la propiedad Locked del archivo de bloqueo- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="abb4f-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="abb4f-156">Los paquetes de símbolos no deben usarse nunca en la instalación o actualización #2807</span><span class="sxs-lookup"><span data-stu-id="abb4f-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="abb4f-157">Características</span><span class="sxs-lookup"><span data-stu-id="abb4f-157">Features</span></span>

* <span data-ttu-id="abb4f-158">Compatibilidad con carpetas de paquetes de reserva: [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="abb4f-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="abb4f-159">Diseñar e implementar una noción de tipo de paquete para admitir paquetes de herramientas- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="abb4f-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="abb4f-160">API para obtener la ruta de acceso a la carpeta de paquetes globales: [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="abb4f-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="abb4f-161">Compatibilidad de actualización de paquetes nativos: [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="abb4f-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
