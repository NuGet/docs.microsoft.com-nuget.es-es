---
title: "Notas de la versión de NuGet 2.2.1 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 2.2.1 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.2.1 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="81262-104">Notas de la versión de NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="81262-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="81262-105">[Notas de la versión de NuGet 2.2](../release-notes/nuget-2.2.md) | [notas de la versión de NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="81262-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="81262-106">NuGet 2.2.1 se publicó en el 15 de febrero de 2013.</span><span class="sxs-lookup"><span data-stu-id="81262-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="81262-107">El número de versión de extensión de VS es 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="81262-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="81262-108">Actualización de localización</span><span class="sxs-lookup"><span data-stu-id="81262-108">Localization Refresh</span></span>
<span data-ttu-id="81262-109">Cuando NuGet se envía como parte de Visual Studio 2012, se localizó totalmente en inglés + 13 otros lenguajes.</span><span class="sxs-lookup"><span data-stu-id="81262-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="81262-110">Desde entonces, incluidos NuGet 2.1 y 2.2 pero no tenía se ha actualizado la localización.</span><span class="sxs-lookup"><span data-stu-id="81262-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="81262-111">La versión de NuGet 2.2.1 actualiza la localización.</span><span class="sxs-lookup"><span data-stu-id="81262-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="81262-112">Interfaz de usuario y la consola de PowerShell de NuGet están localizados en los siguientes idiomas:</span><span class="sxs-lookup"><span data-stu-id="81262-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="81262-113">Chino (simplificado)</span><span class="sxs-lookup"><span data-stu-id="81262-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="81262-114">Chino (tradicional)</span><span class="sxs-lookup"><span data-stu-id="81262-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="81262-115">Checo</span><span class="sxs-lookup"><span data-stu-id="81262-115">Czech</span></span>
1. <span data-ttu-id="81262-116">Inglés</span><span class="sxs-lookup"><span data-stu-id="81262-116">English</span></span>
1. <span data-ttu-id="81262-117">Francés</span><span class="sxs-lookup"><span data-stu-id="81262-117">French</span></span>
1. <span data-ttu-id="81262-118">Alemán</span><span class="sxs-lookup"><span data-stu-id="81262-118">German</span></span>
1. <span data-ttu-id="81262-119">Italiano</span><span class="sxs-lookup"><span data-stu-id="81262-119">Italian</span></span>
1. <span data-ttu-id="81262-120">Japonés</span><span class="sxs-lookup"><span data-stu-id="81262-120">Japanese</span></span>
1. <span data-ttu-id="81262-121">Coreano</span><span class="sxs-lookup"><span data-stu-id="81262-121">Korean</span></span>
1. <span data-ttu-id="81262-122">Polaco</span><span class="sxs-lookup"><span data-stu-id="81262-122">Polish</span></span>
1. <span data-ttu-id="81262-123">Portugués (Brasil)</span><span class="sxs-lookup"><span data-stu-id="81262-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="81262-124">Ruso</span><span class="sxs-lookup"><span data-stu-id="81262-124">Russian</span></span>
1. <span data-ttu-id="81262-125">Español</span><span class="sxs-lookup"><span data-stu-id="81262-125">Spanish</span></span>
1. <span data-ttu-id="81262-126">Turco</span><span class="sxs-lookup"><span data-stu-id="81262-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="81262-127">Plantillas de Visual Studio admiten varios repositorios de paquete preinstalado</span><span class="sxs-lookup"><span data-stu-id="81262-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="81262-128">Si generar plantillas de Visual Studio, puede usar NuGet para [preinstalar paquetes](../visual-studio-extensibility/visual-studio-templates.md) como parte de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="81262-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="81262-129">Hasta ahora, esta característica era una limitación que todos los paquetes necesitan para proceden del mismo origen.</span><span class="sxs-lookup"><span data-stu-id="81262-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="81262-130">Sin embargo, con NuGet 2.2.1 puede tener paquetes instalados desde varios repositorios (dentro de la plantilla, una extensión VSIX o una carpeta en el disco definida en el registro).</span><span class="sxs-lookup"><span data-stu-id="81262-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="81262-131">El escenario principal para esta característica son plantillas de proyecto ASP.NET personalizadas.</span><span class="sxs-lookup"><span data-stu-id="81262-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="81262-132">Las plantillas ASP.NET integradas usan paquetes preinstalados, extraer paquetes desde el disco local.</span><span class="sxs-lookup"><span data-stu-id="81262-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="81262-133">Ahora puede crear una plantilla de proyecto ASP.NET personalizada que usa los paquetes existentes instalados con ASP.NET pero agregar paquetes de NuGet adicionales en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="81262-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="81262-134">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="81262-134">Bug Fixes</span></span>
<span data-ttu-id="81262-135">NuGet 2.2.1 incluye algunas correcciones de errores de destino.</span><span class="sxs-lookup"><span data-stu-id="81262-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="81262-136">Para obtener una lista de trabajo elementos corregidos en NuGet 2.2.1, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="81262-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="81262-137">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="81262-137">Known Issues</span></span>

<span data-ttu-id="81262-138">Si está ampliando plantillas de proyecto ASP.NET, todos los repositorios de paquete preinstalado deben usar el mismo valor para el `isPreunzipped` atributo.</span><span class="sxs-lookup"><span data-stu-id="81262-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
