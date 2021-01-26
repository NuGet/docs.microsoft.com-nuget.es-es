---
title: Notas de la versión de NuGet 3,4
description: Notas de la versión de NuGet 3,4, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776421"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="683a6-103">Notas de la versión de NuGet 3,4</span><span class="sxs-lookup"><span data-stu-id="683a6-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="683a6-104">[Notas de la versión de NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Notas de la versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="683a6-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="683a6-105">NuGet 3,4 se lanzó el 30 de marzo de 2016 como parte de la versión Visual Studio 2015 Update 2 y Visual Studio 15 Preview, y se creó con unos cuantos principios en mente:</span><span class="sxs-lookup"><span data-stu-id="683a6-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="683a6-106">Compatibilidad entre plataformas</span><span class="sxs-lookup"><span data-stu-id="683a6-106">Cross-Platform support</span></span>
* <span data-ttu-id="683a6-107">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="683a6-107">Performance improvements</span></span>
* <span data-ttu-id="683a6-108">Mejoras en la interfaz de usuario secundaria</span><span class="sxs-lookup"><span data-stu-id="683a6-108">Minor UI improvements</span></span>

<span data-ttu-id="683a6-109">Las siguientes características se agregaron anteriormente en RC y se han actualizado o completado para la versión 3,4:</span><span class="sxs-lookup"><span data-stu-id="683a6-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="683a6-110">Nuevas características</span><span class="sxs-lookup"><span data-stu-id="683a6-110">New Features</span></span>

* <span data-ttu-id="683a6-111">Los clientes de NuGet ahora admiten la codificación de contenido gzip de los repositorios</span><span class="sxs-lookup"><span data-stu-id="683a6-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="683a6-112">Compatibilidad con archivos PDB desde paquetes en proyectos de xproj</span><span class="sxs-lookup"><span data-stu-id="683a6-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="683a6-113">Compatibilidad con acciones de compilación de iOS y Android en el elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="683a6-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="683a6-114">Compatibilidad con los monikers de netstandard y netstandardapp Framework</span><span class="sxs-lookup"><span data-stu-id="683a6-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="683a6-115">Nuevas características de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="683a6-115">New User Interface Features</span></span>

* <span data-ttu-id="683a6-116">Mejoras significativas en el rendimiento, especialmente en las pestañas instalado, actualizaciones y consolidación</span><span class="sxs-lookup"><span data-stu-id="683a6-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="683a6-117">El origen de "todos los orígenes de paquetes" agregado está disponible con la combinación de resultados de búsqueda adecuada</span><span class="sxs-lookup"><span data-stu-id="683a6-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="683a6-118">Las pestañas instalado y actualizaciones ahora están ordenadas alfabéticamente</span><span class="sxs-lookup"><span data-stu-id="683a6-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="683a6-119">Se ha agregado un botón de actualización que permite actualizar una búsqueda</span><span class="sxs-lookup"><span data-stu-id="683a6-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="683a6-120">Opciones de compilación más recientes en la parte superior de la lista de versiones</span><span class="sxs-lookup"><span data-stu-id="683a6-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="683a6-121">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="683a6-121">Updates and Improvements</span></span>

* <span data-ttu-id="683a6-122">Los paquetes a los que se hace referencia en `project.json` que tienen una versión flotante no se actualizarán en todas las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="683a6-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="683a6-123">En su lugar, solo se actualizarán cuando estén obligados a restaurar, limpiar, recompilar o modificar `project.json` .</span><span class="sxs-lookup"><span data-stu-id="683a6-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="683a6-124">los orígenes de repositorios de nuget.org ya no se fuerzan en una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="683a6-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="683a6-125">NuGet ya no restaura paquetes en proyectos compartidos ni escribe un archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="683a6-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="683a6-126">Hemos mejorado el error de red y el control de reintentos para servidores inaccesibles o de respuesta lenta.</span><span class="sxs-lookup"><span data-stu-id="683a6-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="683a6-127">Los comportamientos del teclado y del mouse se han mejorado en la interfaz de usuario del administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="683a6-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="683a6-128">Ahora se admite el esquema más reciente `project.json` en dnx.</span><span class="sxs-lookup"><span data-stu-id="683a6-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="683a6-129">Últimos cambios</span><span class="sxs-lookup"><span data-stu-id="683a6-129">Breaking Changes</span></span>

* <span data-ttu-id="683a6-130">Los números de versión del paquete ahora se normalizan con el formato *principal*. *secundaria*. *revisión* - *versión preliminar*   Cada una de las principales, secundarias y de revisión se tratan como enteros y colocan los ceros a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="683a6-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="683a6-131">La información de versión preliminar se trata como una cadena y no se le aplica ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="683a6-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="683a6-132">Estos números se utilizan en las consultas de los clientes de NuGet y la búsqueda proporcionada por el servicio nuget.org.</span><span class="sxs-lookup"><span data-stu-id="683a6-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="683a6-133">Puede encontrar más detalles en los documentos de NuGet en [versiones preliminares](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="683a6-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="683a6-134">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="683a6-134">Known Issues</span></span>

* <span data-ttu-id="683a6-135">**Problema:** Los usuarios de Windows 10 v1511 pueden experimentar problemas o incluso un bloqueo de Visual Studio con PowerShell en Visual Studio en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="683a6-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="683a6-136">Instalación o desinstalación de paquetes que tienen scripts install.ps1/uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="683a6-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="683a6-137">Cargar proyectos que tienen un script init.ps1 (como EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="683a6-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="683a6-138">Publicación de contenido web</span><span class="sxs-lookup"><span data-stu-id="683a6-138">Publishing web content</span></span>

* <span data-ttu-id="683a6-139">**Solución alternativa:** Asegúrese de que la instalación de Windows 10 tenga aplicadas las revisiones más recientes, especiales el 2016 de enero (KB 3124263) o una actualización posterior.</span><span class="sxs-lookup"><span data-stu-id="683a6-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="683a6-140">Puede encontrar más detalles en el [problema de GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="683a6-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="683a6-141">**Problema:** Las redirecciones de protocolo de NuGet v2 se interrumpen.</span><span class="sxs-lookup"><span data-stu-id="683a6-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="683a6-142">Los repositorios de NuGet personalizados que redireccionan solicitudes a un host alternativo no respetan la solicitud de redirección.</span><span class="sxs-lookup"><span data-stu-id="683a6-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="683a6-143">**Solución alternativa:**  Para solucionar este problema, configure el URI del repositorio de paquetes en configuración para que apunte a la ubicación del servidor redirigido.</span><span class="sxs-lookup"><span data-stu-id="683a6-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="683a6-144">Para obtener más información, consulte [#387 de solicitud de incorporación](https://github.com/NuGet/NuGet.Client/pull/387)de cambios de github.</span><span class="sxs-lookup"><span data-stu-id="683a6-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="683a6-145">Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que se puede encontrar en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="683a6-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>