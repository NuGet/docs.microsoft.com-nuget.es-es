---
title: Notas de la versión de NuGet 3.4.2
description: Notas de la versión para incluir NuGet 3.4.2 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549156"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="a0e1e-103">Notas de la versión de NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="a0e1e-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="a0e1e-104">[Notas de la versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="a0e1e-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="a0e1e-105">NuGet 3.4.2 se lanzó el 8 de abril de 2016 para resolver varios problemas que se han identificado en la 3.4 y 3.4.1 de versión.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="a0e1e-106">NuGet.exe 3.4.2 RC ya está disponible</span><span class="sxs-lookup"><span data-stu-id="a0e1e-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="a0e1e-107">Puede descargar la versión release candidate de nuget.exe 3.4.2 [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="a0e1e-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="a0e1e-108">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="a0e1e-108">Updates and Improvements</span></span>

* <span data-ttu-id="a0e1e-109">Hemos mejorado considerablemente el rendimiento de las actualizaciones en un escenario concreto, donde las actualizaciones en los paquetes con gráficos de dependencia profunda tardaron mucho tiempo y permanece en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="a0e1e-110">restauración de NuGet sin que el tráfico de red es 2,5 x – 3 veces más rápido en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="a0e1e-111">Además de este cambio, hemos corregido un problema donde nos estábamos alcanzar la red dos veces al recuento de obtención de la actualización en la interfaz de usuario de VS.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="a0e1e-112">Esto fue parcialmente responsable de algunos clientes de problemas de tiempo de espera con experiencia en 3.4 y 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="a0e1e-113">Se ha agregado compatibilidad con la configuración de no_proxy</span><span class="sxs-lookup"><span data-stu-id="a0e1e-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="a0e1e-114">Correcciones</span><span class="sxs-lookup"><span data-stu-id="a0e1e-114">Fixes</span></span>

* <span data-ttu-id="a0e1e-115">Se ha corregido un problema donde el origen de nuget.org faltaba en la configuración de NuGet o la configuración después de actualizar a 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="a0e1e-116">Se ha corregido un problema donde un cambio de mayúsculas y minúsculas en FindPackagesById en 3.4.1 interrumpe Artifactory.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="a0e1e-117">Se ha corregido un problema con el estándar FIPS que causaba errores con la restauración de NuGet con nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="a0e1e-118">Se ha corregido un bloqueo al examinar los orígenes con la dirección URL de icono no válido.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="a0e1e-119">Se han corregido los problemas con la combinación de versiones y las entradas de todos los orígenes' de'.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="a0e1e-120">Problemas conocidos en 3.4.2 Windows x86 Commandline (RC)</span><span class="sxs-lookup"><span data-stu-id="a0e1e-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="a0e1e-121">Estos problemas se corregirán temprana próxima semana antes de que lleguen a RTM.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="a0e1e-122">Ejecución de restauración de nuget en una solución se producirá un error si el archivo de solución se coloca en una jerarquía de carpetas menor que los archivos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="a0e1e-123">Ejecutar comando de eliminación de nuget en un paquete con la fuente de V2 se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="a0e1e-124">Usar fuente V3 en su lugar.</span><span class="sxs-lookup"><span data-stu-id="a0e1e-124">Use V3 feed instead.</span></span>


<span data-ttu-id="a0e1e-125">Para obtener la lista completa de correcciones y mejoras en esta versión, consulte la lista de problemas [aquí](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="a0e1e-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>