---
title: Notas de la versión de NuGet 2.8.5
description: Notas de la versión para incluir NuGet 2.8.5 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548630"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="4fbc8-103">Notas de la versión de NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="4fbc8-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="4fbc8-104">[Notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [notas de la versión de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="4fbc8-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="4fbc8-105">NuGet 2.8.5 se lanzó el 30 de marzo de 2015.</span><span class="sxs-lookup"><span data-stu-id="4fbc8-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="4fbc8-106">Es una actualización secundaria a nuestro 2.8.3 VSIX con algunos dirigida correcciones.</span><span class="sxs-lookup"><span data-stu-id="4fbc8-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="4fbc8-107">En esta versión, se ha agregado compatibilidad con el cuadro de diálogo Administrador de paquetes de NuGet para [DNX Monikers de la plataforma de destino](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="4fbc8-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="4fbc8-108">Estos nuevos monikers de la plataforma que se admiten son:</span><span class="sxs-lookup"><span data-stu-id="4fbc8-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="4fbc8-109">**core50** - un moniker de la plataforma (TFM) que es compatible con Core CLR de destino 'base'.</span><span class="sxs-lookup"><span data-stu-id="4fbc8-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="4fbc8-110">**dnx452** : mediante la 4.5.2 completa de aplicaciones específicas basados en DNX TFM de una versión de framework</span><span class="sxs-lookup"><span data-stu-id="4fbc8-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="4fbc8-111">**dnx46** : con la versión 4.6 completa del marco de aplicaciones específicas basados en DNX un TFM</span><span class="sxs-lookup"><span data-stu-id="4fbc8-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="4fbc8-112">**dnxcore50** : aplicaciones específicas basados en DNX un TFM utilizando la versión 5.0 de núcleo de framework</span><span class="sxs-lookup"><span data-stu-id="4fbc8-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="4fbc8-113">Uno se arregló que impedía paquetes instalen en proyectos FSharp correctamente:</span><span class="sxs-lookup"><span data-stu-id="4fbc8-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400