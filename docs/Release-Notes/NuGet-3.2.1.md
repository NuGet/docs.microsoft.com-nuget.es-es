---
title: "Notas de la versión de NuGet 3.2.1 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.2.1 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.2.1 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c9c2457c33eb3630f632c98bf0cf96703c3a548
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="880c1-104">Notas de la versión de NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="880c1-104">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="880c1-105">[Notas de la versión 3.2 de NuGet](../release-notes/nuget-3.2.md) | [notas de la versión 3.3 de NuGet](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="880c1-105">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="880c1-106">NuGet 3.2.1 para la línea de comandos se publicó el 12 de octubre de 2015 con una serie de optimizaciones y soluciones para la versión 3.2 y está disponible en [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="880c1-106">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="880c1-107">Mejoras</span><span class="sxs-lookup"><span data-stu-id="880c1-107">Improvements</span></span>

* <span data-ttu-id="880c1-108">NuGet ahora usa el archivo de configuración con las mayúsculas y minúsculas original de `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="880c1-108">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="880c1-109">Esto es importante en sistemas operativos entre mayúsculas y minúsculas [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="880c1-109">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="880c1-110">Restauración de NuGet ahora hará caso omiso de proyectos dnx (`*.xproj`) que debe procesarse con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="880c1-110">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="880c1-111">Optimiza el uso de la red cuando se trabaja con `index.json` y datos de registro del paquete [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="880c1-111">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="880c1-112">Descarga de recursos mejorado controlan para ser más eficaces con los servicios de v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="880c1-112">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="880c1-113">Correcciones</span><span class="sxs-lookup"><span data-stu-id="880c1-113">Fixes</span></span>

* <span data-ttu-id="880c1-114">Actualización de NuGet se actualiza correctamente `.csproj` / `.vcxproj` referencias [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="880c1-114">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="880c1-115">Ahora que impide que una carpeta .nuget local se crea cuando no se encuentra un SpecialFolders.UserProfile [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="880c1-115">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="880c1-116">El control mejorado de paquetes en la memoria caché local que se hayan dañado durante la descarga [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="880c1-116">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="880c1-117">Una lista completa de temas que se tratan de la extensión de línea de comandos y Visual Studio se encuentran en NuGet GitHub [3.2.1 hito](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="880c1-117">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="880c1-118">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="880c1-118">Known Issues</span></span>

<span data-ttu-id="880c1-119">Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="880c1-119">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>