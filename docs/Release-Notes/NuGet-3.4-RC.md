---
title: "Notas de la versión RC 3.4 de NuGet | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.4 RC incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.4 RC notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="4543c-104">Notas de la versión RC 3.4 de NuGet</span><span class="sxs-lookup"><span data-stu-id="4543c-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="4543c-105">[Notas de la versión de NuGet 3.3](../release-notes/nuget-3.3.md) | [notas de la versión de NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="4543c-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="4543c-106">NuGet 3.4-RC se publicó el 3 de marzo de 2016 junto con Visual Studio 2015 Update 2 RC y se ha generado con unos principios en mente:</span><span class="sxs-lookup"><span data-stu-id="4543c-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="4543c-107">La compatibilidad multiplataforma</span><span class="sxs-lookup"><span data-stu-id="4543c-107">Cross-Platform support</span></span>
* <span data-ttu-id="4543c-108">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="4543c-108">Performance improvements</span></span>
* <span data-ttu-id="4543c-109">Pequeñas mejoras de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="4543c-109">Minor UI improvements</span></span>

<span data-ttu-id="4543c-110">Las siguientes características están disponibles en esta RC, y hay más previstos para la versión final 3,4.</span><span class="sxs-lookup"><span data-stu-id="4543c-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="4543c-111">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="4543c-111">New Features</span></span>

* <span data-ttu-id="4543c-112">Los clientes de NuGet ahora admiten la codificación de contenido gzip de repositorios</span><span class="sxs-lookup"><span data-stu-id="4543c-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="4543c-113">Compatibilidad con archivos PDB de paquetes en proyectos xproj</span><span class="sxs-lookup"><span data-stu-id="4543c-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="4543c-114">Compatibilidad con iOS y Android acciones en el elemento de archivos de compilación</span><span class="sxs-lookup"><span data-stu-id="4543c-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="4543c-115">Compatibilidad con los monikers netstandard y netstandardapp de framework</span><span class="sxs-lookup"><span data-stu-id="4543c-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="4543c-116">Nuevas características de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="4543c-116">New User Interface Features</span></span>

* <span data-ttu-id="4543c-117">Mejoras de rendimiento significativas especialmente en las pestañas instalado, actualizaciones y consolidar</span><span class="sxs-lookup"><span data-stu-id="4543c-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="4543c-118">Instala y pestañas de las actualizaciones ahora aparecen ordenadas alfabéticamente</span><span class="sxs-lookup"><span data-stu-id="4543c-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="4543c-119">Agregar un botón de actualización que permite una búsqueda que se va a actualizar</span><span class="sxs-lookup"><span data-stu-id="4543c-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="4543c-120">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="4543c-120">Updates and Improvements</span></span>

* <span data-ttu-id="4543c-121">Paquetes que se hace referencia en `project.json` que tienen un flotante versión no se actualiza en cada compilación.</span><span class="sxs-lookup"><span data-stu-id="4543c-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="4543c-122">En su lugar, actualizará solo cuando se le obligaba a restaurar, limpiar, volver a generar o modificar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4543c-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="4543c-123">orígenes del repositorio NuGet.org ya no se convierten obligatoriamente en una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4543c-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="4543c-124">NuGet no restaura los paquetes en los proyectos compartidos ni escribe un archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="4543c-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="4543c-125">Se ha mejorado el error de red y vuelva a intentar un control para servidores inaccesibles o lenta a responder.</span><span class="sxs-lookup"><span data-stu-id="4543c-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="4543c-126">Se han mejorado los comportamientos de teclado y mouse (ratón) en la UI del Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4543c-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="4543c-127">Ahora se admite la versión más reciente `project.json` esquema de DNX.</span><span class="sxs-lookup"><span data-stu-id="4543c-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="4543c-128">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="4543c-128">Known Issues</span></span>

<span data-ttu-id="4543c-129">Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="4543c-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>