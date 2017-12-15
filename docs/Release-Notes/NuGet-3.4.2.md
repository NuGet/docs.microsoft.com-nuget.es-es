---
title: "Notas de la versión de NuGet 3.4.2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b514da09-da1f-416b-9bfc-692f08fb6957
description: "Notas de la versión de NuGet 3.4.2 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.4.2 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6761c59b6dc85b9a8503041928c2707549006d9c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="32980-104">Notas de la versión de NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="32980-104">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="32980-105">[Notas de la versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="32980-105">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="32980-106">Se liberó NuGet 3.4.2 del 8 de abril de 2016 soluciona algunos problemas que se identificaron en el 3.4 y 3.4.1 liberar.</span><span class="sxs-lookup"><span data-stu-id="32980-106">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="32980-107">NuGet.exe 3.4.2 RC ya está disponible</span><span class="sxs-lookup"><span data-stu-id="32980-107">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="32980-108">Puede descargar la versión release candidate de nuget.exe 3.4.2 [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="32980-108">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="32980-109">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="32980-109">Updates and Improvements</span></span>

* <span data-ttu-id="32980-110">Hemos mejorado significativamente el rendimiento de las actualizaciones en un escenario específico, donde las actualizaciones en los paquetes con gráficos de dependencia profunda tardaron mucho tiempo y había bloqueado Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="32980-110">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="32980-111">restauración de NuGet sin tráfico de red es 2,5 x – 3 veces más rápidos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="32980-111">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="32980-112">Además de este cambio, se ha corregido un problema donde se estábamos alcanzar la red dos veces cuando la actualización de filas cuentan en la interfaz de usuario de VS.</span><span class="sxs-lookup"><span data-stu-id="32980-112">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="32980-113">Esto era parcialmente responsable para algunos clientes de problemas de tiempo de espera con experiencia en 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="32980-113">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="32980-114">Se agregó compatibilidad para la configuración de no_proxy</span><span class="sxs-lookup"><span data-stu-id="32980-114">Added support for no_proxy setting</span></span>

##<a name="fixes"></a><span data-ttu-id="32980-115">Correcciones</span><span class="sxs-lookup"><span data-stu-id="32980-115">Fixes</span></span>

* <span data-ttu-id="32980-116">Se ha corregido un problema donde nuget.org origen faltaba en valores de configuración de NuGet o configuración después de actualizar a 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="32980-116">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="32980-117">Se ha corregido un problema donde un cambio de mayúsculas y minúsculas en FindPackagesById en 3.4.1 interrumpe Artifactory.</span><span class="sxs-lookup"><span data-stu-id="32980-117">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="32980-118">Se ha corregido un problema con FIPS que produjeron errores con la restauración de NuGet con nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="32980-118">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="32980-119">Se ha corregido un bloqueo al examinar los orígenes de dirección URL de icono no válido.</span><span class="sxs-lookup"><span data-stu-id="32980-119">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="32980-120">Se han corregido los problemas con la combinación de versiones y las entradas de todos los orígenes' de'.</span><span class="sxs-lookup"><span data-stu-id="32980-120">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="32980-121">Problemas conocidos en 3.4.2 línea de comandos de Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="32980-121">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="32980-122">Estos problemas se corregirán primeras semanas siguientes antes de que lleguen a RTM.</span><span class="sxs-lookup"><span data-stu-id="32980-122">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="32980-123">Ejecutando restauración de nuget en una solución se producirá un error si el archivo de solución se coloca en una jerarquía de carpetas inferior que los archivos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="32980-123">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="32980-124">Ejecuta el comando de eliminación de nuget en un paquete mediante la fuente V2 se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="32980-124">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="32980-125">Usar fuentes de distribución de V3 en su lugar.</span><span class="sxs-lookup"><span data-stu-id="32980-125">Use V3 feed instead.</span></span>


<span data-ttu-id="32980-126">Para obtener la lista completa de correcciones y mejoras en esta versión, visite la lista de problemas [aquí](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="32980-126">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>