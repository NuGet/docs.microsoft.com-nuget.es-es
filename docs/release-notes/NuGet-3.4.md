---
title: Notas de la versión 3.4 de NuGet
description: Notas de la versión de NuGet 3.4, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820477"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="528ba-103">Notas de la versión 3.4 de NuGet</span><span class="sxs-lookup"><span data-stu-id="528ba-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="528ba-104">[Notas de la versión RC 3.4 de NuGet](../release-notes/nuget-3.4-RC.md) | [notas de la versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="528ba-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="528ba-105">NuGet 3.4 publicó el 30 de marzo de 2016 como parte de Visual Studio 2015 Update 2 y la versión preliminar de Visual Studio 15 y se ha generado con unos principios en mente:</span><span class="sxs-lookup"><span data-stu-id="528ba-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="528ba-106">La compatibilidad multiplataforma</span><span class="sxs-lookup"><span data-stu-id="528ba-106">Cross-Platform support</span></span>
* <span data-ttu-id="528ba-107">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="528ba-107">Performance improvements</span></span>
* <span data-ttu-id="528ba-108">Pequeñas mejoras de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="528ba-108">Minor UI improvements</span></span>

<span data-ttu-id="528ba-109">Las siguientes características se agregaron previamente en la versión RC y se han actualizado o completado para la versión 3.4:</span><span class="sxs-lookup"><span data-stu-id="528ba-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="528ba-110">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="528ba-110">New Features</span></span>

* <span data-ttu-id="528ba-111">Los clientes de NuGet ahora admiten la codificación de contenido gzip de repositorios</span><span class="sxs-lookup"><span data-stu-id="528ba-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="528ba-112">Compatibilidad con archivos PDB de paquetes en proyectos xproj</span><span class="sxs-lookup"><span data-stu-id="528ba-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="528ba-113">Compatibilidad con iOS y Android acciones en el elemento de archivos de compilación</span><span class="sxs-lookup"><span data-stu-id="528ba-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="528ba-114">Compatibilidad con los monikers netstandard y netstandardapp de framework</span><span class="sxs-lookup"><span data-stu-id="528ba-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="528ba-115">Nuevas características de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="528ba-115">New User Interface Features</span></span>

* <span data-ttu-id="528ba-116">Mejoras de rendimiento significativas especialmente en las pestañas instalado, actualizaciones y consolidar</span><span class="sxs-lookup"><span data-stu-id="528ba-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="528ba-117">El origen 'Todos los orígenes de paquetes' agregado está disponible con la combinación de resultado de búsqueda correcto</span><span class="sxs-lookup"><span data-stu-id="528ba-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="528ba-118">Instala y pestañas de las actualizaciones ahora aparecen ordenadas alfabéticamente</span><span class="sxs-lookup"><span data-stu-id="528ba-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="528ba-119">Agregar un botón de actualización que permite una búsqueda que se va a actualizar</span><span class="sxs-lookup"><span data-stu-id="528ba-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="528ba-120">Opciones de compilación más recientes en la parte superior de la lista de versiones</span><span class="sxs-lookup"><span data-stu-id="528ba-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="528ba-121">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="528ba-121">Updates and Improvements</span></span>

* <span data-ttu-id="528ba-122">Paquetes que se hace referencia en `project.json` que tienen un flotante versión no se actualiza en cada compilación.</span><span class="sxs-lookup"><span data-stu-id="528ba-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="528ba-123">En su lugar, actualizará solo cuando se le obligaba a restaurar, limpiar, volver a generar o modificar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="528ba-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="528ba-124">orígenes del repositorio NuGet.org ya no se convierten obligatoriamente en una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="528ba-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="528ba-125">NuGet no restaura los paquetes en los proyectos compartidos ni escribe un archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="528ba-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="528ba-126">Se ha mejorado el error de red y vuelva a intentar un control para servidores inaccesibles o lenta a responder.</span><span class="sxs-lookup"><span data-stu-id="528ba-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="528ba-127">Se han mejorado los comportamientos de teclado y mouse (ratón) en la UI del Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="528ba-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="528ba-128">Ahora se admite la versión más reciente `project.json` esquema de DNX.</span><span class="sxs-lookup"><span data-stu-id="528ba-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="528ba-129">Cambios importantes</span><span class="sxs-lookup"><span data-stu-id="528ba-129">Breaking Changes</span></span>

* <span data-ttu-id="528ba-130">Ahora se normalizan los números de versión de paquete en el formato *principal*. *secundaria*. *revisión*-*preliminar* cada uno de los principales, secundarias y aplicar las revisiones se tratan como enteros y coloque los ceros a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="528ba-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="528ba-131">La información de versión preliminar se trata como una cadena y no se aplicarán los cambios a él.</span><span class="sxs-lookup"><span data-stu-id="528ba-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="528ba-132">Estos números se utilizan en consultas por los clientes de NuGet y la búsqueda proporcionada por el servicio de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="528ba-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="528ba-133">Pueden encontrar más detalles en la documentación de NuGet en [versiones de lanzamiento](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="528ba-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="528ba-134">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="528ba-134">Known Issues</span></span>

* <span data-ttu-id="528ba-135">**Problema:** a los usuarios de Windows 10 v1511 pueden experimentar problemas o incluso un bloqueo de Visual Studio con Powershell en Visual Studio en los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="528ba-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="528ba-136">Instalación / desinstalación de paquetes que tienen install.ps1 / uninstall.ps1 scripts</span><span class="sxs-lookup"><span data-stu-id="528ba-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="528ba-137">Carga de los proyectos que tienen un script init.ps1 (por ejemplo, Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="528ba-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="528ba-138">Publicación de contenido web</span><span class="sxs-lookup"><span data-stu-id="528ba-138">Publishing web content</span></span>

* <span data-ttu-id="528ba-139">**Solución alternativa:** Asegúrese de que la instalación de Windows 10 tiene las revisiones más recientes que se aplica, expecially el enero de 2016 (KB 3124263) o una actualización posterior.</span><span class="sxs-lookup"><span data-stu-id="528ba-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="528ba-140">Encuentran más detalles en [problema de GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="528ba-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="528ba-141">**Problema:** Las redirecciones de protocolo de NuGet v2 se interrumpen.</span><span class="sxs-lookup"><span data-stu-id="528ba-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="528ba-142">Los repositorios de NuGet personalizados que redireccionan solicitudes a un host alternativo no respetan la solicitud de redirección.</span><span class="sxs-lookup"><span data-stu-id="528ba-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="528ba-143">**Solución alternativa:** para solucionar este problema, configure el URI del repositorio de configuración para apuntar a la ubicación del servidor redirigido.</span><span class="sxs-lookup"><span data-stu-id="528ba-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="528ba-144">Para obtener más información, consulte [solicitud de extracción de GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="528ba-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="528ba-145">Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="528ba-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>