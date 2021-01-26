---
title: Notas de la versión de NuGet 3.2.1
description: Notas de la versión de NuGet 3.2.1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776518"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="cef57-103">Notas de la versión de NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="cef57-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="cef57-104">Notas de la [versión de NuGet 3,2](../release-notes/nuget-3.2.md)  |  [Notas de la versión de NuGet 3,3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="cef57-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="cef57-105">NuGet 3.2.1 para la línea de comandos se lanzó el 12 de octubre de 2015 con una serie de optimizaciones y correcciones para la versión 3,2 y está disponible en [Dist.Nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="cef57-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="cef57-106">Mejoras</span><span class="sxs-lookup"><span data-stu-id="cef57-106">Improvements</span></span>

* <span data-ttu-id="cef57-107">NuGet ahora usa el archivo de configuración con el uso de mayúsculas y minúsculas original de `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="cef57-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="cef57-108">Esto es importante en sistemas operativos con distinción de mayúsculas y minúsculas [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="cef57-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="cef57-109">La restauración de NuGet ahora pasará por alto los proyectos de DNX ( `*.xproj` ) que deben procesarse con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="cef57-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="cef57-110">Uso de red optimizado al trabajar con `index.json` datos de registro de paquetes [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="cef57-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="cef57-111">Mejor control de la descarga de recursos para ser más sólido con los servicios V2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="cef57-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="cef57-112">Correcciones</span><span class="sxs-lookup"><span data-stu-id="cef57-112">Fixes</span></span>

* <span data-ttu-id="cef57-113">La actualización de NuGet actualiza correctamente `.csproj` / `.vcxproj` las referencias [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="cef57-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="cef57-114">Ahora se impide que se cree una carpeta local. Nuget cuando no se encuentra SpecialFolders. UserProfile [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="cef57-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="cef57-115">Control mejorado de los paquetes en la memoria caché local que están dañados durante la descarga [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="cef57-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="cef57-116">Encontrará una lista completa de los problemas que se han solucionado para la extensión de la línea de comandos y de Visual Studio en el hito de GitHub de NuGet [3.2.1](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) .</span><span class="sxs-lookup"><span data-stu-id="cef57-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="cef57-117">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="cef57-117">Known Issues</span></span>

<span data-ttu-id="cef57-118">Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que se puede encontrar en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="cef57-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>