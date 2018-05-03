---
title: Notas de la versión de NuGet 2.8.5
description: Notas de la versión de NuGet 2.8.5 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="15049-103">Notas de la versión de NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="15049-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="15049-104">[Notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [notas de la versión de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="15049-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="15049-105">NuGet 2.8.5 se publicó el 30 de marzo de 2015.</span><span class="sxs-lookup"><span data-stu-id="15049-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="15049-106">Es una actualización secundaria a nuestro 2.8.3 VSIX con algunos dirigida correcciones.</span><span class="sxs-lookup"><span data-stu-id="15049-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="15049-107">En esta versión, se agregó la compatibilidad de cuadro de diálogo Administrador de paquetes de NuGet para [Monikers de Framework de destino de DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="15049-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="15049-108">Estos nuevos monikers de framework que se admiten se incluyen:</span><span class="sxs-lookup"><span data-stu-id="15049-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="15049-109">**core50** : un moniker de la plataforma (TFM) que es compatible con el núcleo de CLR de destino 'base'.</span><span class="sxs-lookup"><span data-stu-id="15049-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="15049-110">**dnx452** : TFM A aplicaciones específicas basadas en DNX mediante la 4.5.2 completa versión de framework</span><span class="sxs-lookup"><span data-stu-id="15049-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="15049-111">**dnx46** : TFM A aplicaciones específicas basadas en DNX utilizando la versión 4.6 completa de framework</span><span class="sxs-lookup"><span data-stu-id="15049-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="15049-112">**dnxcore50** : TFM A aplicaciones específicas basadas en DNX utilizando la versión 5.0 de núcleo de framework</span><span class="sxs-lookup"><span data-stu-id="15049-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="15049-113">Se corrigió producidos por paquetes evita que se instale correctamente en proyectos de FSharp a un error:</span><span class="sxs-lookup"><span data-stu-id="15049-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400