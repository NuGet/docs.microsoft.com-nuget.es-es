---
title: Notas de la versión 2.9 RC de NuGet
description: Notas de la versión de NuGet 2.9 RC incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548329"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="2e022-103">Notas de la versión 2.9 RC de NuGet</span><span class="sxs-lookup"><span data-stu-id="2e022-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="2e022-104">[Notas de la versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [notas de la versión de NuGet 3.0 versión preliminar](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="2e022-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="2e022-105">2.9 de NuGet se lanzó el 10 de septiembre de 2015 como una actualización de la 2.8.7 VSIX para Visual Studio 2012 y 2013.</span><span class="sxs-lookup"><span data-stu-id="2e022-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="2e022-106">Actualizaciones de esta versión</span><span class="sxs-lookup"><span data-stu-id="2e022-106">Updates in this release</span></span>

* <span data-ttu-id="2e022-107">Ahora omitiendo el procesamiento de paquetes si sus contenidos `.nuspec` documento tiene un formato incorrecto: [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="2e022-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="2e022-108">Se ha corregido el control multipartwebrequest de \r\n para escenarios de Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="2e022-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="2e022-109">Se ha corregido la integración con los eventos de compilación en las ediciones de Visual Studio Community 2013 - [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="2e022-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="2e022-110">La lista completa de las correcciones de esta versión se puede encontrar en GitHub en el [2.8.8 hito](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="2e022-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
