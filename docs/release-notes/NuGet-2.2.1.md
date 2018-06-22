---
title: Notas de la versión de NuGet 2.2.1
description: Notas de la versión de NuGet 2.2.1 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819298"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="e360a-103">Notas de la versión de NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="e360a-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="e360a-104">[Notas de la versión de NuGet 2.2](../release-notes/nuget-2.2.md) | [notas de la versión de NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="e360a-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="e360a-105">NuGet 2.2.1 se publicó en el 15 de febrero de 2013.</span><span class="sxs-lookup"><span data-stu-id="e360a-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="e360a-106">El número de versión de extensión de VS es 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="e360a-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="e360a-107">Actualización de localización</span><span class="sxs-lookup"><span data-stu-id="e360a-107">Localization Refresh</span></span>
<span data-ttu-id="e360a-108">Cuando NuGet se envía como parte de Visual Studio 2012, se localizó totalmente en inglés + 13 otros lenguajes.</span><span class="sxs-lookup"><span data-stu-id="e360a-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="e360a-109">Desde entonces, incluidos NuGet 2.1 y 2.2 pero no tenía se ha actualizado la localización.</span><span class="sxs-lookup"><span data-stu-id="e360a-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="e360a-110">La versión de NuGet 2.2.1 actualiza la localización.</span><span class="sxs-lookup"><span data-stu-id="e360a-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="e360a-111">Interfaz de usuario y la consola de PowerShell de NuGet están localizados en los siguientes idiomas:</span><span class="sxs-lookup"><span data-stu-id="e360a-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="e360a-112">Chino (simplificado)</span><span class="sxs-lookup"><span data-stu-id="e360a-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="e360a-113">Chino (tradicional)</span><span class="sxs-lookup"><span data-stu-id="e360a-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="e360a-114">Checo</span><span class="sxs-lookup"><span data-stu-id="e360a-114">Czech</span></span>
1. <span data-ttu-id="e360a-115">Inglés</span><span class="sxs-lookup"><span data-stu-id="e360a-115">English</span></span>
1. <span data-ttu-id="e360a-116">Francés</span><span class="sxs-lookup"><span data-stu-id="e360a-116">French</span></span>
1. <span data-ttu-id="e360a-117">Alemán</span><span class="sxs-lookup"><span data-stu-id="e360a-117">German</span></span>
1. <span data-ttu-id="e360a-118">Italiano</span><span class="sxs-lookup"><span data-stu-id="e360a-118">Italian</span></span>
1. <span data-ttu-id="e360a-119">Japonés</span><span class="sxs-lookup"><span data-stu-id="e360a-119">Japanese</span></span>
1. <span data-ttu-id="e360a-120">Coreano</span><span class="sxs-lookup"><span data-stu-id="e360a-120">Korean</span></span>
1. <span data-ttu-id="e360a-121">Polaco</span><span class="sxs-lookup"><span data-stu-id="e360a-121">Polish</span></span>
1. <span data-ttu-id="e360a-122">Portugués (Brasil)</span><span class="sxs-lookup"><span data-stu-id="e360a-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="e360a-123">Ruso</span><span class="sxs-lookup"><span data-stu-id="e360a-123">Russian</span></span>
1. <span data-ttu-id="e360a-124">Español</span><span class="sxs-lookup"><span data-stu-id="e360a-124">Spanish</span></span>
1. <span data-ttu-id="e360a-125">Turco</span><span class="sxs-lookup"><span data-stu-id="e360a-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="e360a-126">Plantillas de Visual Studio admiten varios repositorios de paquete preinstalado</span><span class="sxs-lookup"><span data-stu-id="e360a-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="e360a-127">Si generar plantillas de Visual Studio, puede usar NuGet para [preinstalar paquetes](../visual-studio-extensibility/visual-studio-templates.md) como parte de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e360a-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="e360a-128">Hasta ahora, esta característica era una limitación que todos los paquetes necesitan para proceden del mismo origen.</span><span class="sxs-lookup"><span data-stu-id="e360a-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="e360a-129">Sin embargo, con NuGet 2.2.1 puede tener paquetes instalados desde varios repositorios (dentro de la plantilla, una extensión VSIX o una carpeta en el disco definida en el registro).</span><span class="sxs-lookup"><span data-stu-id="e360a-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="e360a-130">El escenario principal para esta característica son plantillas de proyecto ASP.NET personalizadas.</span><span class="sxs-lookup"><span data-stu-id="e360a-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="e360a-131">Las plantillas ASP.NET integradas usan paquetes preinstalados, extraer paquetes desde el disco local.</span><span class="sxs-lookup"><span data-stu-id="e360a-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="e360a-132">Ahora puede crear una plantilla de proyecto ASP.NET personalizada que usa los paquetes existentes instalados con ASP.NET pero agregar paquetes de NuGet adicionales en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e360a-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e360a-133">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="e360a-133">Bug Fixes</span></span>
<span data-ttu-id="e360a-134">NuGet 2.2.1 incluye algunas correcciones de errores de destino.</span><span class="sxs-lookup"><span data-stu-id="e360a-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="e360a-135">Para obtener una lista de trabajo elementos corregidos en NuGet 2.2.1, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="e360a-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="e360a-136">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="e360a-136">Known Issues</span></span>

<span data-ttu-id="e360a-137">Si está ampliando plantillas de proyecto ASP.NET, todos los repositorios de paquete preinstalado deben usar el mismo valor para el `isPreunzipped` atributo.</span><span class="sxs-lookup"><span data-stu-id="e360a-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
