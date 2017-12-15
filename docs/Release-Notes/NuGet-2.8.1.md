---
title: "Notas de la versión de NuGet 2.8.1 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: eebbbae4-fc6a-4c05-9102-4ec66b4c64a4
description: "Notas de la versión de NuGet 2.8.1 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.8.1 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac33369644d312591bfe8c06540935b2c6063c5d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="054cb-104">Notas de la versión de NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="054cb-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="054cb-105">[Notas de la versión de NuGet 2.8](../release-notes/nuget-2.8.md) | [notas de la versión de NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="054cb-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="054cb-106">NuGet 2.8.1 se publicó en el 2 de abril de 2014.</span><span class="sxs-lookup"><span data-stu-id="054cb-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="054cb-107">Características importantes de la versión</span><span class="sxs-lookup"><span data-stu-id="054cb-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="054cb-108">Soporte técnico para los proyectos de Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="054cb-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="054cb-109">Esta versión ahora es compatible con los monikers de framework de destino nuevo siguientes que pueden usarse para proyectos de destino Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="054cb-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="054cb-110">WindowsPhone81 / WP81 (para los proyectos de Windows Phone basadas en Silverlight)</span><span class="sxs-lookup"><span data-stu-id="054cb-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="054cb-111">WindowsPhoneApp81 / WPA81 (para los proyectos de aplicación de Windows Phone WinRT-based)</span><span class="sxs-lookup"><span data-stu-id="054cb-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="054cb-112">Actualización de la extensión de WebMatrix de NuGet</span><span class="sxs-lookup"><span data-stu-id="054cb-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="054cb-113">Esta versión actualiza el cliente de NuGet que se encuentra en WebMatrix para [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 y pone con ofrece como transformaciones XDT.</span><span class="sxs-lookup"><span data-stu-id="054cb-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="054cb-114">Lo que es más importante, el 2.6.1 actualización principal permite al cliente de WebMatrix instalar paquetes de NuGet que contienen versiones más recientes de la `.nuspec` esquema, que incluye los paquetes de NuGet de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="054cb-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="054cb-115">Para obtener más información acerca de la actualización de la extensión de WebMatrix, vea los específico [notas de la versión](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="054cb-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="054cb-116">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="054cb-116">Bug Fixes</span></span>
<span data-ttu-id="054cb-117">Además de estas características, esta versión de NuGet incluye otras correcciones de errores.</span><span class="sxs-lookup"><span data-stu-id="054cb-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="054cb-118">No hay 16 problemas total cubiertos en la versión.</span><span class="sxs-lookup"><span data-stu-id="054cb-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="054cb-119">Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8.1, por favor, vista la [NuGet Issue Tracker para esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="054cb-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="054cb-120">Reshipping con Visual Studio «14» CTP</span><span class="sxs-lookup"><span data-stu-id="054cb-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="054cb-121">En CTP de Visual Studio "14" publicada el 3 de junio de 2014, NuGet 2.8.1 se incluye en el cuadro.</span><span class="sxs-lookup"><span data-stu-id="054cb-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="054cb-122">Las características que admite permanecen en el par con otros 2.8.1 VSIXes como el de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="054cb-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
