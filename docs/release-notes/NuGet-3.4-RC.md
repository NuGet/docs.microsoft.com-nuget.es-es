---
title: Notas de la versión de NuGet 3,4-RC
description: Notas de la versión de NuGet 3,4 RC, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780241"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="4907b-103">Notas de la versión de NuGet 3,4-RC</span><span class="sxs-lookup"><span data-stu-id="4907b-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="4907b-104">Notas de la [versión de NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Notas de la versión de NuGet 3,4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="4907b-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="4907b-105">NuGet 3,4-RC se lanzó el 3 de marzo de 2016 junto con Visual Studio 2015 Update 2 RC y se creó con unos cuantos principios en mente:</span><span class="sxs-lookup"><span data-stu-id="4907b-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="4907b-106">Compatibilidad entre plataformas</span><span class="sxs-lookup"><span data-stu-id="4907b-106">Cross-Platform support</span></span>
* <span data-ttu-id="4907b-107">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="4907b-107">Performance improvements</span></span>
* <span data-ttu-id="4907b-108">Mejoras en la interfaz de usuario secundaria</span><span class="sxs-lookup"><span data-stu-id="4907b-108">Minor UI improvements</span></span>

<span data-ttu-id="4907b-109">Las siguientes características están disponibles en este RC, con más planeada para la versión final de 3,4.</span><span class="sxs-lookup"><span data-stu-id="4907b-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="4907b-110">Nuevas características</span><span class="sxs-lookup"><span data-stu-id="4907b-110">New Features</span></span>

* <span data-ttu-id="4907b-111">Los clientes de NuGet ahora admiten la codificación de contenido gzip de los repositorios</span><span class="sxs-lookup"><span data-stu-id="4907b-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="4907b-112">Compatibilidad con archivos PDB desde paquetes en proyectos de xproj</span><span class="sxs-lookup"><span data-stu-id="4907b-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="4907b-113">Compatibilidad con acciones de compilación de iOS y Android en el elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="4907b-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="4907b-114">Compatibilidad con los monikers de netstandard y netstandardapp Framework</span><span class="sxs-lookup"><span data-stu-id="4907b-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="4907b-115">Nuevas características de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="4907b-115">New User Interface Features</span></span>

* <span data-ttu-id="4907b-116">Mejoras significativas en el rendimiento, especialmente en las pestañas instalado, actualizaciones y consolidación</span><span class="sxs-lookup"><span data-stu-id="4907b-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="4907b-117">Las pestañas instalado y actualizaciones ahora están ordenadas alfabéticamente</span><span class="sxs-lookup"><span data-stu-id="4907b-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="4907b-118">Se ha agregado un botón de actualización que permite actualizar una búsqueda</span><span class="sxs-lookup"><span data-stu-id="4907b-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="4907b-119">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="4907b-119">Updates and Improvements</span></span>

* <span data-ttu-id="4907b-120">Los paquetes a los que se hace referencia en `project.json` que tienen una versión flotante no se actualizarán en todas las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="4907b-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="4907b-121">En su lugar, solo se actualizarán cuando estén obligados a restaurar, limpiar, recompilar o modificar `project.json` .</span><span class="sxs-lookup"><span data-stu-id="4907b-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="4907b-122">los orígenes de repositorios de nuget.org ya no se fuerzan en una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4907b-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="4907b-123">NuGet ya no restaura paquetes en proyectos compartidos ni escribe un archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="4907b-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="4907b-124">Hemos mejorado el error de red y el control de reintentos para servidores inaccesibles o de respuesta lenta.</span><span class="sxs-lookup"><span data-stu-id="4907b-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="4907b-125">Los comportamientos del teclado y del mouse se han mejorado en la interfaz de usuario del administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4907b-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="4907b-126">Ahora se admite el esquema más reciente `project.json` en dnx.</span><span class="sxs-lookup"><span data-stu-id="4907b-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="4907b-127">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="4907b-127">Known Issues</span></span>

<span data-ttu-id="4907b-128">Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que se puede encontrar en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="4907b-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>