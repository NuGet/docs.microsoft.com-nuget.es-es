---
title: Notas de la versión de NuGet 2.8.5
description: Notas de la versión de 2.8.5 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780362"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="4198c-103">Notas de la versión de NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="4198c-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="4198c-104">Notas de la [versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Notas de la versión de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="4198c-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="4198c-105">2.8.5 de NuGet se lanzó el 30 de marzo de 2015.</span><span class="sxs-lookup"><span data-stu-id="4198c-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="4198c-106">Es una actualización secundaria de la VSIX 2.8.3 con algunas correcciones de destino.</span><span class="sxs-lookup"><span data-stu-id="4198c-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="4198c-107">En esta versión, se ha agregado el cuadro de diálogo del administrador de paquetes de NuGet para los [monikers de la plataforma de destino DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="4198c-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="4198c-108">Estos nuevos monikers de Framework que se admiten son:</span><span class="sxs-lookup"><span data-stu-id="4198c-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="4198c-109">**core50** : un moniker de la plataforma de destino (TFM) que es compatible con el CLR básico.</span><span class="sxs-lookup"><span data-stu-id="4198c-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="4198c-110">**dnx452** : un TFM específico para aplicaciones basadas en dnx con la versión completa de 4.5.2 del marco de trabajo</span><span class="sxs-lookup"><span data-stu-id="4198c-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="4198c-111">**dnx46** : un TFM específico para aplicaciones basadas en dnx con la versión completa de 4,6 del marco de trabajo</span><span class="sxs-lookup"><span data-stu-id="4198c-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="4198c-112">**dnxcore50** : un TFM específico para aplicaciones basadas en dnx con la versión Core 5,0 del marco de trabajo</span><span class="sxs-lookup"><span data-stu-id="4198c-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="4198c-113">Se corrigió un error que impedía que los paquetes se instalaran correctamente en los proyectos de FSharp:</span><span class="sxs-lookup"><span data-stu-id="4198c-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400