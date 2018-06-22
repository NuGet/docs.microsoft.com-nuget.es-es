---
title: Notas de la versión 3.1 de NuGet
description: Notas de la versión para 3.1 de NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820883"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="22e48-103">Notas de la versión 3.1 de NuGet</span><span class="sxs-lookup"><span data-stu-id="22e48-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="22e48-104">[Notas de la versión de NuGet 3.0](../release-notes/nuget-3.0.0.md) | [notas de la versión de NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="22e48-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="22e48-105">3.1 de NuGet se publicó en el 27 de julio de 2015 como una extensión integrada para el SDK de plataforma Universal de Windows para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="22e48-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="22e48-106">Se entrega esta versión con el SDK de la plataforma Windows de modo que la experiencia de desarrollo de Windows puede aprovechar el trabajo de multiplataforma de NuGet que se inició previamente.</span><span class="sxs-lookup"><span data-stu-id="22e48-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="22e48-107">Esta versión de extensión de NuGet solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="22e48-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="22e48-108">Se recomienda que los desarrolladores que tienen acceso a la actualización de la Galería de Visual Studio a la versión más reciente que está disponible, como siempre estamos publicando actualizaciones con nuevas características y correcciones de errores.</span><span class="sxs-lookup"><span data-stu-id="22e48-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="22e48-109">Extensión de NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22e48-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="22e48-110">Problemas y características de esta versión se etiquetan en GitHub con el ["soporte transitiva de RTM UWP 3.1" hito](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) en total, se cierran 67 problemas de la versión 3.1.</span><span class="sxs-lookup"><span data-stu-id="22e48-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="22e48-111">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="22e48-111">New Features</span></span>

* <span data-ttu-id="22e48-112">`project.json` soporte técnico para la compatibilidad con Windows UWP y ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="22e48-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="22e48-113">Instalación del paquete transitiva</span><span class="sxs-lookup"><span data-stu-id="22e48-113">Transitive package installation</span></span>

<span data-ttu-id="22e48-114">Descripción y definición de estas características pueden encontrarse en otro lugar en la documentación.</span><span class="sxs-lookup"><span data-stu-id="22e48-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="22e48-115">En desuso</span><span class="sxs-lookup"><span data-stu-id="22e48-115">Deprecated</span></span>

<span data-ttu-id="22e48-116">Las siguientes características ya no están disponibles para Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="22e48-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="22e48-117">Ya no se pueden instalar paquetes de solución de nivel</span><span class="sxs-lookup"><span data-stu-id="22e48-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="22e48-118">Las siguientes características ya no están disponibles para Visual Studio 2015 y proyectos que utilizan el `project.json` especificación</span><span class="sxs-lookup"><span data-stu-id="22e48-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="22e48-119">`install.ps1` y `uninstall.ps1` -estos scripts se pasará por alto durante la instalación del paquete, restaurar, actualizar y desinstalar</span><span class="sxs-lookup"><span data-stu-id="22e48-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="22e48-120">Transformaciones de configuración se pasará por alto</span><span class="sxs-lookup"><span data-stu-id="22e48-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="22e48-121">Contenido se realizando, pero no se copian en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="22e48-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="22e48-122">El equipo está trabajando para volver a implementar esta característica, siga el análisis y progreso a fecha de: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="22e48-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="22e48-123">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="22e48-123">Known Issues</span></span>

<span data-ttu-id="22e48-124">No hay un número de problemas conocidos que se entregan con esta versión.</span><span class="sxs-lookup"><span data-stu-id="22e48-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="22e48-125">Instalación de la versión 3.1 con el SDK de Windows 10 degradará cualquier versión de extensión de NuGet que se instaló previamente</span><span class="sxs-lookup"><span data-stu-id="22e48-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="22e48-126">Línea de comandos de NuGet</span><span class="sxs-lookup"><span data-stu-id="22e48-126">NuGet Command-line</span></span>

<span data-ttu-id="22e48-127">El ejecutable de línea de comandos de NuGet se actualizó y se mueve a una nueva ubicación distribuible para que pueden continuar versiones históricas del nuget.exe para que estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="22e48-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="22e48-128">Puede descargar la versión 3.1 beta de nuget.exe para Windows en: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="22e48-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="22e48-129">La nueva ubicación distribuible reside en el host dist.nuget.org, con una estructura de carpetas que sigue a esta plantilla:</span><span class="sxs-lookup"><span data-stu-id="22e48-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="22e48-130">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="22e48-130">New Features</span></span>

* <span data-ttu-id="22e48-131">NuGet.exe puede restaurar e instalar paquetes en los proyectos que usan un `project.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="22e48-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="22e48-132">NuGet.exe puede conectarse a y usar el protocolo de NuGet v3 en: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="22e48-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="22e48-133">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="22e48-133">Known Issues</span></span> ##

1.    <span data-ttu-id="22e48-134">No se puede ejecutar el paquete con un `project.json` archivo - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="22e48-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="22e48-135">No se admite en Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="22e48-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="22e48-136">No se localiza - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="22e48-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="22e48-137">No está firmado, al igual que existente http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="22e48-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
