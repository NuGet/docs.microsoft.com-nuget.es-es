---
title: Notas de la versión de NuGet 3.4.2
description: Notas de la versión de 3.4.2 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780247"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="56c33-103">Notas de la versión de NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="56c33-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="56c33-104">Notas de la [versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="56c33-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="56c33-105">NuGet 3.4.2 se lanzó el 8 de abril de 2016 para solucionar varios problemas que se identificaron en la versión 3,4 y 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="56c33-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="56c33-106">nuget.exe 3.4.2 RC ya está disponible</span><span class="sxs-lookup"><span data-stu-id="56c33-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="56c33-107">Puede descargar el candidato de versión comercial de nuget.exe 3.4.2 [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="56c33-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="56c33-108">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="56c33-108">Updates and Improvements</span></span>

* <span data-ttu-id="56c33-109">Hemos mejorado considerablemente el rendimiento de las actualizaciones en un escenario específico, en el que las actualizaciones de los paquetes con gráficos de dependencias profundos tardan mucho tiempo y no responden a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="56c33-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="56c33-110">la restauración de Nuget sin tráfico de red es 2,5 x – tres veces más rápida en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="56c33-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="56c33-111">Además de este cambio, se ha corregido un problema por el que hemos alcanzado la red dos veces al capturar el número de actualizaciones en la interfaz de usuario de VS.</span><span class="sxs-lookup"><span data-stu-id="56c33-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="56c33-112">Esto era responsable parcialmente de algunos problemas de tiempo de espera que los clientes experimentaron en 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="56c33-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="56c33-113">Compatibilidad agregada para la configuración de no_proxy</span><span class="sxs-lookup"><span data-stu-id="56c33-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="56c33-114">Correcciones</span><span class="sxs-lookup"><span data-stu-id="56c33-114">Fixes</span></span>

* <span data-ttu-id="56c33-115">Se corrigió un problema en el que faltaba el origen de nuget.org en la configuración de NuGet o la configuración después de actualizar a 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="56c33-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="56c33-116">Se corrigió un problema por el que un cambio de mayúsculas y minúsculas en FindPackagesById en 3.4.1 rompe Artifactory.</span><span class="sxs-lookup"><span data-stu-id="56c33-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="56c33-117">Se corrigió un problema con FIPS que causó errores con la restauración de NuGet con nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="56c33-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="56c33-118">Se corrigió un bloqueo al examinar orígenes con una dirección URL de icono no válida.</span><span class="sxs-lookup"><span data-stu-id="56c33-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="56c33-119">Se han corregido problemas con la combinación de versiones y entradas de "todos los orígenes".</span><span class="sxs-lookup"><span data-stu-id="56c33-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="56c33-120">Problemas conocidos de 3.4.2 Windows x86 CommandLine (RC)</span><span class="sxs-lookup"><span data-stu-id="56c33-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="56c33-121">Estos problemas se corregirán antes de la próxima semana antes de que llegue el RTM.</span><span class="sxs-lookup"><span data-stu-id="56c33-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="56c33-122">La ejecución de la restauración de Nuget en una solución producirá un error si el archivo de solución se coloca en una jerarquía de carpetas inferior a la de los archivos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="56c33-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="56c33-123">Se producirá un error al ejecutar el comando DELETE de Nuget en un paquete con la fuente V2.</span><span class="sxs-lookup"><span data-stu-id="56c33-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="56c33-124">En su lugar, utilice la fuente V3.</span><span class="sxs-lookup"><span data-stu-id="56c33-124">Use V3 feed instead.</span></span>


<span data-ttu-id="56c33-125">Para obtener una lista completa de correcciones y mejoras en esta versión, consulte la lista de problemas [aquí](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="56c33-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>