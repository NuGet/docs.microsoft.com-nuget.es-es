---
title: Notas de la versión de NuGet 3.4.4
description: Notas de la versión de 3.4.4 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780226"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="37bd2-103">Notas de la versión de NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="37bd2-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="37bd2-104">Notas de la [versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [Notas de la versión de NuGet 3,5-beta](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="37bd2-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="37bd2-105">El objetivo principal de esta versión es mejorar la calidad de la versión de 3.4.3 de nuget.exe con algunas correcciones de la extensión de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37bd2-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="37bd2-106">Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="37bd2-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="37bd2-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="37bd2-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="37bd2-108">Registro de cambios completo</span><span class="sxs-lookup"><span data-stu-id="37bd2-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="37bd2-109">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="37bd2-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="37bd2-110">Cambios</span><span class="sxs-lookup"><span data-stu-id="37bd2-110">Changes</span></span>

- <span data-ttu-id="37bd2-111">Mejoras en los paquetes: mejoras en el empaquetado de símbolos, empaquetado con `project.json` y más [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="37bd2-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="37bd2-112">Mostrar excepción cuando se produce un error al buscar proyectos en el comando de actualización [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="37bd2-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="37bd2-113">Leer el tipo de paquete de la entrada `.nuspec` y `project.json` al empaquetar [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="37bd2-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="37bd2-114">Haga que NuGet. Shared no sea un proyecto.</span><span class="sxs-lookup"><span data-stu-id="37bd2-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="37bd2-115">\#602</span><span class="sxs-lookup"><span data-stu-id="37bd2-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="37bd2-116">Usar el tiempo de espera de la inserciones como el tiempo de espera de respuesta HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="37bd2-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="37bd2-117">Los archivos de paquete con tiempos futuros no tendrán su tiempo en usarse [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="37bd2-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="37bd2-118">Actualización `NuGet.Core.dll` de la versión a 2.12.0 para corregir el problema de XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="37bd2-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="37bd2-119">Compatibilidad con./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="37bd2-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="37bd2-120">Mostrar error al restaurar sin `project.json` o `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="37bd2-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="37bd2-121">Corregir versiones de dependencia cuando las versiones requeridas difieren de [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="37bd2-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>