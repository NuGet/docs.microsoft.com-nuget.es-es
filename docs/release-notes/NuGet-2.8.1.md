---
title: Notas de la versión de NuGet 2.8.1
description: Notas de la versión de 2.8.1 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776765"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="59735-103">Notas de la versión de NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="59735-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="59735-104">Notas de la [versión de NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Notas de la versión de NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="59735-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="59735-105">2.8.1 de NuGet se publicó el 2 de abril de 2014.</span><span class="sxs-lookup"><span data-stu-id="59735-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="59735-106">Características destacadas de la versión</span><span class="sxs-lookup"><span data-stu-id="59735-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="59735-107">Compatibilidad con proyectos de Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="59735-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="59735-108">Esta versión admite ahora los siguientes monikers de la plataforma de destino que se pueden usar para tener como destino Windows Phone proyectos de 8,1:</span><span class="sxs-lookup"><span data-stu-id="59735-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="59735-109">WindowsPhone81/WP81 (para proyectos de Windows Phone basados en Silverlight)</span><span class="sxs-lookup"><span data-stu-id="59735-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="59735-110">WindowsPhoneApp81/WPA81 (para proyectos de aplicaciones Windows Phone basados en WinRT)</span><span class="sxs-lookup"><span data-stu-id="59735-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="59735-111">Actualización de la extensión de WebMatrix de NuGet</span><span class="sxs-lookup"><span data-stu-id="59735-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="59735-112">Esta versión actualiza el cliente de NuGet que se encuentra en WebMatrix a [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 y aporta características de ti como transformaciones XDT.</span><span class="sxs-lookup"><span data-stu-id="59735-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="59735-113">Lo que es más importante, la actualización principal de 2.6.1 permite al cliente de WebMatrix instalar paquetes NuGet que contienen versiones más recientes del `.nuspec` esquema, que incluye los paquetes Nuget de ASP.net.</span><span class="sxs-lookup"><span data-stu-id="59735-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="59735-114">Para obtener más información sobre la actualización de la extensión WebMatrix, consulte las notas de la [versión](../release-notes/nuget-2.6.1-for-WebMatrix.md)específicas.</span><span class="sxs-lookup"><span data-stu-id="59735-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="59735-115">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="59735-115">Bug Fixes</span></span>
<span data-ttu-id="59735-116">Además de estas características, esta versión de NuGet incluye otras correcciones de errores.</span><span class="sxs-lookup"><span data-stu-id="59735-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="59735-117">Se han solucionado 16 problemas totales en la versión.</span><span class="sxs-lookup"><span data-stu-id="59735-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="59735-118">Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2.8.1, consulte el [seguimiento de problemas de Nuget en esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="59735-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="59735-119">Reenvío con Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="59735-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="59735-120">En Visual Studio "14" CTP publicado el 3 de junio de 2014, 2.8.1 de NuGet se incluye en el cuadro.</span><span class="sxs-lookup"><span data-stu-id="59735-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="59735-121">Las características que admite permanecen en su par con otras VSIXes de 2.8.1, como la de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="59735-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
