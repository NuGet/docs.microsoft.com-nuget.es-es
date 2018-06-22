---
title: Notas de la versión RC 3.4 de NuGet
description: Notas de la versión de NuGet 3.4 RC incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820825"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="3709f-103">Notas de la versión RC 3.4 de NuGet</span><span class="sxs-lookup"><span data-stu-id="3709f-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="3709f-104">[Notas de la versión de NuGet 3.3](../release-notes/nuget-3.3.md) | [notas de la versión de NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="3709f-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="3709f-105">NuGet 3.4-RC se publicó el 3 de marzo de 2016 junto con Visual Studio 2015 Update 2 RC y se ha generado con unos principios en mente:</span><span class="sxs-lookup"><span data-stu-id="3709f-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="3709f-106">La compatibilidad multiplataforma</span><span class="sxs-lookup"><span data-stu-id="3709f-106">Cross-Platform support</span></span>
* <span data-ttu-id="3709f-107">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="3709f-107">Performance improvements</span></span>
* <span data-ttu-id="3709f-108">Pequeñas mejoras de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="3709f-108">Minor UI improvements</span></span>

<span data-ttu-id="3709f-109">Las siguientes características están disponibles en esta RC, y hay más previstos para la versión final 3,4.</span><span class="sxs-lookup"><span data-stu-id="3709f-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="3709f-110">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="3709f-110">New Features</span></span>

* <span data-ttu-id="3709f-111">Los clientes de NuGet ahora admiten la codificación de contenido gzip de repositorios</span><span class="sxs-lookup"><span data-stu-id="3709f-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="3709f-112">Compatibilidad con archivos PDB de paquetes en proyectos xproj</span><span class="sxs-lookup"><span data-stu-id="3709f-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="3709f-113">Compatibilidad con iOS y Android acciones en el elemento de archivos de compilación</span><span class="sxs-lookup"><span data-stu-id="3709f-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="3709f-114">Compatibilidad con los monikers netstandard y netstandardapp de framework</span><span class="sxs-lookup"><span data-stu-id="3709f-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="3709f-115">Nuevas características de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="3709f-115">New User Interface Features</span></span>

* <span data-ttu-id="3709f-116">Mejoras de rendimiento significativas especialmente en las pestañas instalado, actualizaciones y consolidar</span><span class="sxs-lookup"><span data-stu-id="3709f-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="3709f-117">Instala y pestañas de las actualizaciones ahora aparecen ordenadas alfabéticamente</span><span class="sxs-lookup"><span data-stu-id="3709f-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="3709f-118">Agregar un botón de actualización que permite una búsqueda que se va a actualizar</span><span class="sxs-lookup"><span data-stu-id="3709f-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="3709f-119">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="3709f-119">Updates and Improvements</span></span>

* <span data-ttu-id="3709f-120">Paquetes que se hace referencia en `project.json` que tienen un flotante versión no se actualiza en cada compilación.</span><span class="sxs-lookup"><span data-stu-id="3709f-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="3709f-121">En su lugar, actualizará solo cuando se le obligaba a restaurar, limpiar, volver a generar o modificar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="3709f-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="3709f-122">orígenes del repositorio NuGet.org ya no se convierten obligatoriamente en una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="3709f-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="3709f-123">NuGet no restaura los paquetes en los proyectos compartidos ni escribe un archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="3709f-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="3709f-124">Se ha mejorado el error de red y vuelva a intentar un control para servidores inaccesibles o lenta a responder.</span><span class="sxs-lookup"><span data-stu-id="3709f-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="3709f-125">Se han mejorado los comportamientos de teclado y mouse (ratón) en la UI del Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3709f-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="3709f-126">Ahora se admite la versión más reciente `project.json` esquema de DNX.</span><span class="sxs-lookup"><span data-stu-id="3709f-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="3709f-127">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="3709f-127">Known Issues</span></span>

<span data-ttu-id="3709f-128">Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="3709f-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>