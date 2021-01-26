---
title: Notas de la versión de NuGet 2,9-RC
description: Notas de la versión de NuGet 2,9 RC, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780316"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="28e81-103">Notas de la versión de NuGet 2,9-RC</span><span class="sxs-lookup"><span data-stu-id="28e81-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="28e81-104">Notas de la [versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)  |  [Notas de la versión de NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="28e81-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="28e81-105">NuGet 2,9 se lanzó el 10 de septiembre de 2015 como una actualización de 2.8.7 VSIX para Visual Studio 2012 y 2013.</span><span class="sxs-lookup"><span data-stu-id="28e81-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="28e81-106">Actualizaciones en esta versión</span><span class="sxs-lookup"><span data-stu-id="28e81-106">Updates in this release</span></span>

* <span data-ttu-id="28e81-107">Omitiendo ahora los paquetes de procesamiento si su `.nuspec` documento contenido tiene un formato incorrecto- [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="28e81-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="28e81-108">Se corrigió el control de multipartwebrequest de \r\n para escenarios de UNIX/Linux: [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="28e81-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="28e81-109">Se corrigió la integración con eventos de compilación en Visual Studio 2013 Community Edition- [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="28e81-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="28e81-110">La lista completa de correcciones de esta versión se puede encontrar en GitHub en el [hito 2.8.8](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="28e81-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
