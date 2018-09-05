---
title: Notas de la versión Beta de NuGet 3.5
description: Notas de la versión de NuGet 3.5 incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550689"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="1b16e-103">Notas de la versión 3.5 de NuGet</span><span class="sxs-lookup"><span data-stu-id="1b16e-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="1b16e-104">[Notas de la versión 3.5 RC de NuGet](../release-notes/nuget-3.5-RC.md) | [notas de la versión de NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="1b16e-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="1b16e-105">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="1b16e-105">Bug Fixes</span></span>

* <span data-ttu-id="1b16e-106">Módulo no usa MSBuild 14,1 en mono - [3550 #](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="1b16e-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="1b16e-107">Ficha actualización no selecciona la última versión disponible en su lugar, actualizar la versión instalada actualmente de select - [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="1b16e-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="1b16e-108">Se ha corregido el bloqueo después de autenticar una fuente de MyGet de v2 privada y haga clic en "Mostrar x más resultados"- [3469 #](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="1b16e-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="1b16e-109">Los mensajes de registro parecen estar en orden inverso para la interfaz de usuario: [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="1b16e-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="1b16e-110">V3.4.4 - restauración de Nuget produce "no se admite el formato de la ruta de acceso especificada:" [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="1b16e-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="1b16e-111">No respeta la versión beta de NuGet 3.6 cmdLine - Prop Configuration = Release - [3432 #](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="1b16e-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="1b16e-112">Instalar NuGet IKVM lento en un proyecto grande - [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="1b16e-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="1b16e-113">NuGet.exe Update - en se actualiza continuamente propio - [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="1b16e-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="1b16e-114">3.5 instalar o restaurar desde el recurso compartido UNC tiene un rendimiento regresión desde 3.4.4 - [3355 #](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="1b16e-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="1b16e-115">Error al instalar Moq desde la interfaz de usuario de administración de paquetes para un proyecto net451 - [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="1b16e-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="1b16e-116">Ficha de instalación en el nivel de solución no muestra la versión del paquete - [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="1b16e-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="1b16e-117">xproj `project.json` actualización desde la pestaña instalado pierde el estado - [3303 #](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="1b16e-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="1b16e-118">Paquete de NuGet en `.csproj` omite el elemento de archivos vacíos en `.nuspec` archivo - [3257 #](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="1b16e-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="1b16e-119">Proyectos de sitio Web hospedados en IIS no deberían causar restauración genere error - [3235 #](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="1b16e-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="1b16e-120">Las credenciales no se recupera del Nuget.Config al extremo v3 redirige a v2 - [3179 #](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="1b16e-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="1b16e-121">Paquete de NuGet se produce un error al resolver el ensamblado al recuperar los metadatos de ensamblado portátil - [3128 #](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="1b16e-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="1b16e-122">NuGet no se puede encontrar `msbuild.exe` en Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="1b16e-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="1b16e-123">pack de NuGet.exe no permite que una etiqueta de versión preliminar que comienza con números - [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="1b16e-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="1b16e-124">se produce un error en la instalación del paquete NuGet en VS2015E - [1298 #](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="1b16e-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="1b16e-125">allowedVersions filtrar no trabajar en el nivel de solución - [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="1b16e-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="1b16e-126">Aleatoriamente falla la restauración con un elemento con la misma clave ya se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="1b16e-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="1b16e-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="1b16e-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="1b16e-128">No se puede instalar Nuget.Common en `.csproj`  -  [2635 #](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="1b16e-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="1b16e-129">Cuando se usa la interfaz de usuario para buscar un origen de V2, FindPackagesById se llama dos veces para cada identificador - [2517 #](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="1b16e-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="1b16e-130">Los paquetes no pueden depender de los proyectos: [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="1b16e-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="1b16e-131">pack de NuGet.exe - Exclude se documentan pero no admite - [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="1b16e-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="1b16e-132">Problemas con el error, los mensajes cuando "contentFiles" sección de `.nuspec` no es válido - [1686 #](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="1b16e-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="1b16e-133">Inserción siempre envía el paquete completo dos veces con fuentes de paquetes autenticadas - [1501 #](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="1b16e-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="1b16e-134">No se especificó ninguna información cuando una llamada a nuget.exe actualización \*.csproj mientras el proyecto no tiene un `packages.config`  -  [1496 #](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="1b16e-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="1b16e-135">`packages.config` restore no intentará de nuevo en los códigos de estado 5xx de orígenes de V2 - [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="1b16e-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="1b16e-136">Dos puntos en el archivo src en `.nuspec` no funciona - [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="1b16e-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="1b16e-137">Restauración de CoreCLR tiene que pasar por alto las fuentes con cifrado: [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="1b16e-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="1b16e-138">inserción de NuGet.exe control 403 - incorrectamente la solicitud de credenciales - [2910 #](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="1b16e-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="1b16e-139">Actualización de NuGet a través del Administrador de paquetes elimina las propiedades de la `project.json`  -  [2888 #](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="1b16e-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="1b16e-140">NuGet.PackageManagement.VisualStudio intenta cargar "NuGet.TeamFoundationServer14", pero que el nombre de archivo DLL se cambió a "NuGet.TeamFoundationServer" - [2857 #](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="1b16e-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="1b16e-141">Administrador de paquetes de interfaz de usuario no muestra recién actualizado a la versión - [2828 #](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="1b16e-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="1b16e-142">Update-package intentando usar packageid, versión, en lugar de package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="1b16e-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="1b16e-143">NuGet restore csproj debe error si el proyecto no está usando nuget (`packages.config` o `project.json`)- [2766 #](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="1b16e-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="1b16e-144">Error de TFS "[archivo] no puede encontrar en el área de trabajo, o no tiene permiso para acceder a él" durante la actualiza o desinstala cuando se enlaza la solución o proyecto al control de código fuente TFS - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="1b16e-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="1b16e-145">paquete de actualización no recibe las dependencias de paquetes no objetivo - [2724 #](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="1b16e-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="1b16e-146">No hay ninguna manera de establecer el nivel de detalle de los registros de acciones de interfaz de usuario de administrador de paquetes de Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="1b16e-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="1b16e-147">configuración de NuGet no es válido - VS 2015 VSIX (v3.4.3) - [2667 #](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="1b16e-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="1b16e-148">DefaultPushSource en `NuGetDefaults.Config` (`ProgramData\NuGet`) no funciona - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="1b16e-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="1b16e-149">versión de NuGet 3.4.3 - obtener valor no puede ser null en la compilación del paquete - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="1b16e-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="1b16e-150">restauración no está usando las credenciales almacenadas en el archivo Nuget.Config para fuentes VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="1b16e-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="1b16e-151">[restauración de dotnet]--configfile es relativa dir de proyecto en lugar de la dir cmd - [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="1b16e-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="1b16e-152">Asignaciones excesivo en el código de versión comparaciones - [2632 #](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="1b16e-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="1b16e-153">Varias instancias de nuget.exe intentando instalar el mismo paquete en paralelo, se producirá una escritura double - [2628 #](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="1b16e-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="1b16e-154">No se almacena en caché información de dependencia para las operaciones de varios proyectos - [2619 #](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="1b16e-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="1b16e-155">Instalar y actualizar paquetes de descarga sin comprobar la carpeta paquetes first - [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="1b16e-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="1b16e-156">Si la lista de origen del paquete está vacía, no se puede agregar el origen del paquete a través de la interfaz de usuario (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="1b16e-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="1b16e-157">Error engañoso cuando se intenta instalar el paquete que depende de fachadas de tiempo de diseño - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="1b16e-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="1b16e-158">Instalar un paquete desde la consola de PackageManager con la configuración de "All" intenta solo primer origen - [2557 #](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="1b16e-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="1b16e-159">Última versión beta no descomprimir ModernHttpClient - [2518 #](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="1b16e-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="1b16e-160">Bloqueo de VS2015 en el inicio con NuGet generada automáticamente 3.4.1 - [2419 #](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="1b16e-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="1b16e-161">Comando de actualización podría ser un poco más detallado si i solicitarle que ser preempaquetadas... - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="1b16e-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="1b16e-162">VSIX generado localmente debe tener los mismos archivos DLL y que la compilación de CI.</span><span class="sxs-lookup"><span data-stu-id="1b16e-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="1b16e-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="1b16e-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="1b16e-164">Corrija las advertencias de degradación de NuGet en la compilación - [2396 #](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="1b16e-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="1b16e-165">No se puede autenticar el origen del paquete (3 veces) se bloquea indefinidamente - [2362 #](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="1b16e-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="1b16e-166">Contenido del paquete no se restaura correctamente cuando se instala un paquete desde nuget v3.3 + la fuente con el argumento - NoCache cuando el paquete contiene `.nupkg` archivos - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="1b16e-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="1b16e-167">Se produce un error en la instalación de NuGet con todos los orígenes de paquetes, pero falta el 1 de la fuente, el paquete - [2322 #](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="1b16e-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="1b16e-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [2285 #](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="1b16e-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="1b16e-169">Instalar bloques si se produce un error en un único origen de autorización - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="1b16e-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="1b16e-170">`.nuspec` versión intervalo debe reemplazar la versión - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="1b16e-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="1b16e-171">Paquete de actualización lento super - "al intentar recopilar información de dependencias" - [1909 #](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="1b16e-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="1b16e-172">Paquete de NuGet sigiloso degradaciones cuando batch actualizando sus dependencias - [1903 #](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="1b16e-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="1b16e-173">NuGet.exe actualización quita el nombre seguro del ensamblado y el atributo privada.</span><span class="sxs-lookup"><span data-stu-id="1b16e-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="1b16e-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="1b16e-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="1b16e-175">Ruta de acceso relativa de "DefaultPushSource" - [1746 #](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="1b16e-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="1b16e-176">Mejorar los mensajes de error de resolución - [1373 #](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="1b16e-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="1b16e-177">se produce un error en el paquete de actualización en v3 con paquetes no está en el origen especificado - [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="1b16e-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="1b16e-178">Usar rutas de acceso relativas para los orígenes de paquete es problemático al usar - [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="1b16e-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="1b16e-179">Falta la dependencia en un archivo NUPKG generado del proyecto si ya existe una dependencia indirecta con un requisito de versión inferior - [759 #](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="1b16e-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="1b16e-180">Eliminación de un proyecto cierra la ventana de la interfaz de usuario correspondiente, pero, al cambiar el nombre de un proyecto de no cambiar el nombre de la ventana de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1b16e-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="1b16e-181">Tenga en cuenta que realiza escuchas PMC para cambiar el nombre de proyecto y eventos de proyecto de remove - [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="1b16e-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="1b16e-182">[Carga de trabajo de sauces Web] Se bloquea la creación de Razor v3 WSP - [3241 #](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="1b16e-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="1b16e-183">Se produce un error en la instalación y restauración de un paquete determinado con "El paquete contiene varios archivos de nuspec."</span><span class="sxs-lookup"><span data-stu-id="1b16e-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="1b16e-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="1b16e-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="1b16e-185">Minúsculas identificadores & `packages.config` escenarios - [3209 #](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="1b16e-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="1b16e-186">[3.5-beta2] Se produce un error en la restauración de paquetes restaurar paquetes "heredados" - [3208 #](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="1b16e-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="1b16e-187">paquete de NuGet forzosamente agrega archivos .tt a carpeta de contenido con independencia de qué - [3203 #](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="1b16e-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="1b16e-188">paquete de actualización de la aplicación web de ASP.NET genera la advertencia relacionados con el archivo: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="1b16e-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="1b16e-189">NuGet pack csproj (con `project.json`) se bloquea si no hay ningún packOptions y propietario en el archivo JSON: [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="1b16e-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="1b16e-190">paquete de NuGet para `project.json` omite las etiquetas como resumen, los autores y propietarios etcetera - packOptions [3161 #](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="1b16e-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="1b16e-191">Excepción NullReferenceException a través de NuGet.Packaging.PhysicalPackageFile.GetStream - [3160 #](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="1b16e-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="1b16e-192">Paquete de NuGet ignora las dependencias de salida `.nuspec` para `project.json`  -  [3145 #](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="1b16e-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="1b16e-193">Actualizar varios paquetes con reversión deja el proyecto en un estado interrumpido - [3139 #](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="1b16e-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="1b16e-194">No se agregan ContentFiles alguna para los proyectos de netstandard: [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="1b16e-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="1b16e-195">No se puede empaquetar la biblioteca destinadas a .net Standard correctamente - [3108 #](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="1b16e-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="1b16e-196">Archivo -> Nuevo proyecto -> produce un error de proyecto de biblioteca de clases (Portable) en VS2015 y Dev15 - [3094 #](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="1b16e-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="1b16e-197">Error de NuGet - 1.0.0-\* no es una cadena de versión válida - [3070 #](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="1b16e-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="1b16e-198">Find-Package no puede mostrar, pero funciona de Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="1b16e-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="1b16e-199">Error al "Install-Package jquery.validation" en dev15 - [3061 #](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="1b16e-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="1b16e-200">paquete de NuGet de xproj esté de forma predeterminada a la ruta de acceso de destino no válido - [3060 #](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="1b16e-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="1b16e-201">Al instalar VS 2015 update 3 en comparación con una que use NuGet se produce el error en la versión 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="1b16e-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="1b16e-202">"Bloqueado por packages.config" `project.json` (UWP, compilación conocidas también como integrado) proyecto - [3046 #](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="1b16e-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="1b16e-203">actualización instalada por el script de compilación a preview2-003121, que es la compilación de preview2 oficial de la cli de dotnet.</span><span class="sxs-lookup"><span data-stu-id="1b16e-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="1b16e-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="1b16e-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="1b16e-205">Interfaz de usuario del Administrador de paquetes: no muestra la nueva versión después de actualizar un paquete- [3041 #](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="1b16e-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="1b16e-206">-ApiKey en línea de comandos de eliminación no se lectura/envía en 3.5.0-Beta - [3037 #](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="1b16e-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="1b16e-207">Cadena incorrecto: no debe tener una versión estable de un paquete con una dependencia de la versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="1b16e-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="1b16e-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="1b16e-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="1b16e-209">Caché OptimizedZipPackage deja las carpetas vacías - [3029 #](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="1b16e-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="1b16e-210">Creación de get del proyecto PCL (net46 y windows 10) a la excepción NullRef.</span><span class="sxs-lookup"><span data-stu-id="1b16e-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="1b16e-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="1b16e-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="1b16e-212">Actualización de NuGet debe proporcionar un mensaje informativo cuando una versión superior está restringida por restricción allowedVersions - [3013 #](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="1b16e-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="1b16e-213">Problemas de restauración de NuGet v3 - [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="1b16e-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="1b16e-214">Credentials finalizó con un error -1 / error al descargar paquete cuando se usan proveedores de credenciales con varios orígenes - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="1b16e-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="1b16e-215">`project.json` restauración de NuGet provoca una recompilación cuando nada cambia - [2817 #](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="1b16e-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="1b16e-216">Los paquetes de símbolos no debe nunca se usa en la instalación o actualización - [2807 #](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="1b16e-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="1b16e-217">VS no es compatible con las variables de entorno en repositoryPath (nuget.exe hace) - [2763 #](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="1b16e-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="1b16e-218">Etiqueta de la IU sin etiqueta en UI del Administrador de paquetes de accesibilidad: [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="1b16e-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="1b16e-219">Se rechazan los marcos de trabajo portátiles con perfiles con guiones.</span><span class="sxs-lookup"><span data-stu-id="1b16e-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="1b16e-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="1b16e-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="1b16e-221">Administrador de paquetes NuGet debe dejar claro esa lista de opciones en detalle no es aplicable a los paquetes `project.json`  -  [2665 #](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="1b16e-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="1b16e-222">la inserción o eliminación con NuGet.exe no usará la clave de API - [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="1b16e-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="1b16e-223">Quite la propiedad bloqueada el archivo de bloqueo: [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="1b16e-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="1b16e-224">Se produce un error de actualización de NuGet 3.3.0 con '... una restricción adicional definido en packages.config impide esta operación. "</span><span class="sxs-lookup"><span data-stu-id="1b16e-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="1b16e-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="1b16e-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="1b16e-226">Al instalar el paquete desde un origen local que no existe produce un mensaje ficticio: [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="1b16e-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="1b16e-227">Filtro de "Actualización disponible" muestra las actualizaciones que infringen la restricción de versión - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="1b16e-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="1b16e-228">No se puede actualizar los paquetes nativos - [1291 #](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="1b16e-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="1b16e-229">Características</span><span class="sxs-lookup"><span data-stu-id="1b16e-229">Features</span></span>

* <span data-ttu-id="1b16e-230">Admite la configuración CopyLocal en false en referencias agregadas por NuGet: [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="1b16e-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="1b16e-231">compatibilidad con NuGet.exe MSBuild 15 - [1937 #](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="1b16e-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="1b16e-232">Paquete de compatibilidad con.`csproj`</span><span class="sxs-lookup"><span data-stu-id="1b16e-232">Pack support for .`csproj`</span></span><span data-ttu-id="1b16e-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="1b16e-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="1b16e-234">Deshabilitar acción del usuario cuando hay acciones del usuario que se está ejecutadas- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="1b16e-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="1b16e-235">Debe agregar la compatibilidad con NuGet `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="1b16e-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="1b16e-236">Agregar compatibilidad de framework que falta en NuGet 2.x (que ya están en 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="1b16e-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="1b16e-237">Compatibilidad con carpetas de paquetes de reserva - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="1b16e-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="1b16e-238">Diseñar e implementar una noción de tipo de paquete para admitir los paquetes de la herramienta - [2476 #](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="1b16e-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="1b16e-239">Agregar una API para obtener la ruta de acceso a la carpeta de paquetes globales - [2403 #](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="1b16e-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="1b16e-240">Habilitar SemVer 2.0.0 en paquete - [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="1b16e-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="1b16e-241">DCR</span><span class="sxs-lookup"><span data-stu-id="1b16e-241">DCRs</span></span>

* <span data-ttu-id="1b16e-242">inserción de NuGet.exe: parámetro de tiempo de espera no funciona - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="1b16e-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="1b16e-243">Texto de descripción del paquete debe ser seleccionable - [1769 #](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="1b16e-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="1b16e-244">Habilitar nuget.exe producir `.props` y `.targets` archivos para `.nuproj` proyectos [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="1b16e-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="1b16e-245">Agregar extensibilidad API para comparar los marcos con importaciones - [2633 #](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="1b16e-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="1b16e-246">Ocultar opciones de dependencia cuando se usa `project.json`  -  [2486 #](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="1b16e-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="1b16e-247">Encabezado de la versión de nuget.exe en la salida detallada: imprimir [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="1b16e-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="1b16e-248">NuGet se debe a que los usuarios sepan que el actualizar o instalar en un tfm dotnet basado PCL podría causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="1b16e-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="1b16e-249">Advertir incorrecta instalación o actualización de proyectos con tfm = "dotnet" - [3137 #](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="1b16e-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="1b16e-250">Solucionar problemas de rendimiento con NuGet y ReShaper para Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="1b16e-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="1b16e-251">Agregar compatibilidad para netcoreapp11 y netstandard17 - [2998 #](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="1b16e-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="1b16e-252">Atributo de AssemblyMetadata aproveche para `.nuspec` token reemplazos - [2851 #](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="1b16e-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
