---
title: Notas de la versión de NuGet 2.2.1
description: Notas de la versión de NuGet 2.2.1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776803"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="b76a1-103">Notas de la versión de NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b76a1-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="b76a1-104">Notas de la [versión de NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Notas de la versión de NuGet 2,5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="b76a1-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="b76a1-105">NuGet 2.2.1 se lanzó el 15 de febrero de 2013.</span><span class="sxs-lookup"><span data-stu-id="b76a1-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="b76a1-106">El número de versión de la extensión de VS es 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="b76a1-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="b76a1-107">Actualización de la localización</span><span class="sxs-lookup"><span data-stu-id="b76a1-107">Localization Refresh</span></span>
<span data-ttu-id="b76a1-108">Cuando NuGet se incluye como parte de Visual Studio 2012, estaba totalmente localizado en inglés + 13 otros idiomas.</span><span class="sxs-lookup"><span data-stu-id="b76a1-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="b76a1-109">Desde entonces, se han enviado NuGet 2,1 y 2,2, pero la localización no se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="b76a1-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="b76a1-110">La versión 2.2.1 de NuGet actualiza nuestra localización.</span><span class="sxs-lookup"><span data-stu-id="b76a1-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="b76a1-111">La interfaz de usuario de NuGet y la consola de PowerShell se localizan en los siguientes idiomas:</span><span class="sxs-lookup"><span data-stu-id="b76a1-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="b76a1-112">Chino (simplificado)</span><span class="sxs-lookup"><span data-stu-id="b76a1-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="b76a1-113">Chino (tradicional)</span><span class="sxs-lookup"><span data-stu-id="b76a1-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="b76a1-114">Checo</span><span class="sxs-lookup"><span data-stu-id="b76a1-114">Czech</span></span>
1. <span data-ttu-id="b76a1-115">Inglés</span><span class="sxs-lookup"><span data-stu-id="b76a1-115">English</span></span>
1. <span data-ttu-id="b76a1-116">Francés</span><span class="sxs-lookup"><span data-stu-id="b76a1-116">French</span></span>
1. <span data-ttu-id="b76a1-117">Alemán</span><span class="sxs-lookup"><span data-stu-id="b76a1-117">German</span></span>
1. <span data-ttu-id="b76a1-118">Italiano</span><span class="sxs-lookup"><span data-stu-id="b76a1-118">Italian</span></span>
1. <span data-ttu-id="b76a1-119">Japonés</span><span class="sxs-lookup"><span data-stu-id="b76a1-119">Japanese</span></span>
1. <span data-ttu-id="b76a1-120">Coreano</span><span class="sxs-lookup"><span data-stu-id="b76a1-120">Korean</span></span>
1. <span data-ttu-id="b76a1-121">Polaco</span><span class="sxs-lookup"><span data-stu-id="b76a1-121">Polish</span></span>
1. <span data-ttu-id="b76a1-122">Portugués (Brasil)</span><span class="sxs-lookup"><span data-stu-id="b76a1-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="b76a1-123">Ruso</span><span class="sxs-lookup"><span data-stu-id="b76a1-123">Russian</span></span>
1. <span data-ttu-id="b76a1-124">Español</span><span class="sxs-lookup"><span data-stu-id="b76a1-124">Spanish</span></span>
1. <span data-ttu-id="b76a1-125">Turco</span><span class="sxs-lookup"><span data-stu-id="b76a1-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="b76a1-126">Las plantillas de Visual Studio admiten varios repositorios de paquetes preinstalados</span><span class="sxs-lookup"><span data-stu-id="b76a1-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="b76a1-127">Si genera plantillas de Visual Studio, puede usar NuGet para [Preinstalar paquetes](../visual-studio-extensibility/visual-studio-templates.md) como parte de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="b76a1-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="b76a1-128">Hasta ahora, esta característica tenía una limitación de que todos los paquetes debían provienen del mismo origen.</span><span class="sxs-lookup"><span data-stu-id="b76a1-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="b76a1-129">Sin embargo, con NuGet 2.2.1, puede tener paquetes instalados desde varios repositorios (dentro de la plantilla, un VSIX o una carpeta en el disco definidos en el registro).</span><span class="sxs-lookup"><span data-stu-id="b76a1-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="b76a1-130">El escenario principal de esta característica son las plantillas de proyecto de ASP.NET personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b76a1-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="b76a1-131">Las plantillas ASP.NET integradas usan paquetes preinstalados, extrayendo paquetes del disco local.</span><span class="sxs-lookup"><span data-stu-id="b76a1-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="b76a1-132">Ahora puede crear una plantilla de proyecto ASP.NET personalizada que use los paquetes existentes instalados por ASP.NET, pero agregue paquetes NuGet adicionales a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="b76a1-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b76a1-133">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="b76a1-133">Bug Fixes</span></span>
<span data-ttu-id="b76a1-134">NuGet 2.2.1 incluye algunas correcciones de errores de destino.</span><span class="sxs-lookup"><span data-stu-id="b76a1-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="b76a1-135">Para obtener una lista de los elementos de trabajo corregidos en NuGet 2.2.1, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b76a1-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="b76a1-136">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="b76a1-136">Known Issues</span></span>

<span data-ttu-id="b76a1-137">Si va a extender plantillas de proyecto de ASP.NET, todos los repositorios de paquetes preinstalados deben usar el mismo valor para el `isPreunzipped` atributo.</span><span class="sxs-lookup"><span data-stu-id="b76a1-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
