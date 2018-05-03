---
title: Notas de la versión RC de NuGet 3.0
description: Notas de la versión de NuGet 3.0 RC incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="7e8a6-103">Notas de la versión RC de NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="7e8a6-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="7e8a6-104">[Notas de la versión de NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 notas de la versión de RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="7e8a6-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="7e8a6-105">NuGet 3.0 RC se publicó en 29 de abril de 2015 con la versión de Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="7e8a6-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="7e8a6-106">Esta versión tiene un número de correcciones de errores importantes, mejoras de rendimiento y las actualizaciones para admitir los marcos de nuevo.</span><span class="sxs-lookup"><span data-stu-id="7e8a6-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="7e8a6-107">Solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7e8a6-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="7e8a6-108">Continuo enfoque en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="7e8a6-108">Continued Focus on Performance</span></span>

<span data-ttu-id="7e8a6-109">Estabilidad y rendimiento de las consultas de NuGet siguen siendo un tema que nos hemos centrado en.</span><span class="sxs-lookup"><span data-stu-id="7e8a6-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="7e8a6-110">Con esta versión, debe iniciar ver las operaciones de búsqueda muy rápida en el sitio Web y NuGet UI.</span><span class="sxs-lookup"><span data-stu-id="7e8a6-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="7e8a6-111">Estamos supervisando el servicio y cómo utilizar el servicio para que podamos seguir optimizar estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="7e8a6-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="7e8a6-112">Problemas importantes se han resuelto</span><span class="sxs-lookup"><span data-stu-id="7e8a6-112">Significant Issues Resolved</span></span>

<span data-ttu-id="7e8a6-113">Para los clientes de NuGet se estabilizan, se resuelven muchos problemas como parte de esta versión.</span><span class="sxs-lookup"><span data-stu-id="7e8a6-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="7e8a6-114">Esta es una lista breve de algunos de los problemas más importantes que se resuelven:</span><span class="sxs-lookup"><span data-stu-id="7e8a6-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="7e8a6-115">Como parte de cambiar el nombre de la plataforma de K de ASP.NET 5, monikers de framework se han actualizado para controlar dnx y dnxcore [vínculo](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="7e8a6-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="7e8a6-116">Agregar documentación de Ayuda de vínculos en la interfaz de usuario de Visual Studio [vínculo](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="7e8a6-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="7e8a6-117">Mejor control de referencias complejas en `.nuspec` con referencias de framework delimitada por comas [vínculo](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="7e8a6-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="7e8a6-118">Soporte para referencias culturales japonés fijo [vínculo](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="7e8a6-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="7e8a6-119">Cliente actualizado para permitir que los proyectos de ASP.NET 5 usar nuevos extremos v3 [vínculo](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="7e8a6-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="7e8a6-120">Carpeta de paquetes de controlador actualizado mejor con control de código fuente [vínculo](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="7e8a6-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="7e8a6-121">Soporte para los paquetes de satélite fijo [vínculo](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="7e8a6-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="7e8a6-122">Se ha corregido la compatibilidad con archivos de contenido específica del marco [vínculo](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="7e8a6-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="7e8a6-123">Revisión de la presencia de GitHub</span><span class="sxs-lookup"><span data-stu-id="7e8a6-123">GitHub presence overhaul</span></span>

<span data-ttu-id="7e8a6-124">Hemos realizado algunos cambios en nuestros [del origen de los repositorios de código en GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="7e8a6-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="7e8a6-125">Si tiene algún problema con el cliente de NuGet Visual Studio, los comandos de Powershell o la línea de comandos ejecutable puede registrar esos problemas y supervisar su progreso en nuestro [lista de problemas de repositorio de GitHub principal](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="7e8a6-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="7e8a6-126">Estamos haciendo un seguimiento problemas para la galería en nuestro [repositorio de GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="7e8a6-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="7e8a6-127">Permanezca atento</span><span class="sxs-lookup"><span data-stu-id="7e8a6-127">Stay Tuned</span></span>

<span data-ttu-id="7e8a6-128">Por favor, esté atento [nuestro blog](http://blog.nuget.org) para obtener más progreso y anuncios de NuGet 3.0.</span><span class="sxs-lookup"><span data-stu-id="7e8a6-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>