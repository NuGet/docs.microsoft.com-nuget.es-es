---
title: "Notas de la versión RC de NuGet 3.0 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.0 RC incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.0 RC notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="3b003-104">Notas de la versión RC de NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="3b003-104">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="3b003-105">[Notas de la versión de NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 notas de la versión de RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="3b003-105">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="3b003-106">NuGet 3.0 RC se publicó en 29 de abril de 2015 con la versión de Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="3b003-106">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="3b003-107">Esta versión tiene un número de correcciones de errores importantes, mejoras de rendimiento y las actualizaciones para admitir los marcos de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3b003-107">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="3b003-108">Solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3b003-108">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="3b003-109">Continuo enfoque en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="3b003-109">Continued Focus on Performance</span></span>

<span data-ttu-id="3b003-110">Estabilidad y rendimiento de las consultas de NuGet siguen siendo un tema que nos hemos centrado en.</span><span class="sxs-lookup"><span data-stu-id="3b003-110">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="3b003-111">Con esta versión, debe iniciar ver las operaciones de búsqueda muy rápida en el sitio Web y NuGet UI.</span><span class="sxs-lookup"><span data-stu-id="3b003-111">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="3b003-112">Estamos supervisando el servicio y cómo utilizar el servicio para que podamos seguir optimizar estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="3b003-112">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="3b003-113">Problemas importantes se han resuelto</span><span class="sxs-lookup"><span data-stu-id="3b003-113">Significant Issues Resolved</span></span>

<span data-ttu-id="3b003-114">Para los clientes de NuGet se estabilizan, se resuelven muchos problemas como parte de esta versión.</span><span class="sxs-lookup"><span data-stu-id="3b003-114">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="3b003-115">Esta es una lista breve de algunos de los problemas más importantes que se resuelven:</span><span class="sxs-lookup"><span data-stu-id="3b003-115">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="3b003-116">Como parte de cambiar el nombre de la plataforma de K de ASP.NET 5, monikers de framework se han actualizado para controlar dnx y dnxcore [vínculo](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="3b003-116">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="3b003-117">Agregar documentación de Ayuda de vínculos en la interfaz de usuario de Visual Studio [vínculo](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="3b003-117">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="3b003-118">Mejor control de referencias complejas en `.nuspec` con referencias de framework delimitada por comas [vínculo](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="3b003-118">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="3b003-119">Soporte para referencias culturales japonés fijo [vínculo](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="3b003-119">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="3b003-120">Cliente actualizado para permitir que los proyectos de ASP.NET 5 usar nuevos extremos v3 [vínculo](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="3b003-120">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="3b003-121">Carpeta de paquetes de controlador actualizado mejor con control de código fuente [vínculo](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="3b003-121">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="3b003-122">Soporte para los paquetes de satélite fijo [vínculo](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="3b003-122">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="3b003-123">Se ha corregido la compatibilidad con archivos de contenido específica del marco [vínculo](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="3b003-123">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="3b003-124">Revisión de la presencia de GitHub</span><span class="sxs-lookup"><span data-stu-id="3b003-124">GitHub presence overhaul</span></span>

<span data-ttu-id="3b003-125">Hemos realizado algunos cambios en nuestros [del origen de los repositorios de código en GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="3b003-125">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="3b003-126">Si tiene algún problema con el cliente de NuGet Visual Studio, los comandos de Powershell o la línea de comandos ejecutable puede registrar esos problemas y supervisar su progreso en nuestro [lista de problemas de repositorio de GitHub principal](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="3b003-126">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="3b003-127">Estamos haciendo un seguimiento problemas para la galería en nuestro [repositorio de GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="3b003-127">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="3b003-128">Permanezca atento</span><span class="sxs-lookup"><span data-stu-id="3b003-128">Stay Tuned</span></span>

<span data-ttu-id="3b003-129">Por favor, esté atento [nuestro blog](http://blog.nuget.org) para obtener más progreso y anuncios de NuGet 3.0.</span><span class="sxs-lookup"><span data-stu-id="3b003-129">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>