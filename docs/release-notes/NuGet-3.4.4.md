---
title: Notas de la versión de NuGet 3.4.4
description: Notas de la versión para incluir NuGet 3.4.4 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547478"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="ccf07-103">Notas de la versión de NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="ccf07-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="ccf07-104">[Notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [notas de la versión 3.5 Beta de NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="ccf07-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="ccf07-105">El objetivo principal de esta versión era mejoras en la calidad de 3.4.3 versión de nuget.exe con algunas correcciones a la extensión de Visual Studio también.</span><span class="sxs-lookup"><span data-stu-id="ccf07-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="ccf07-106">Puede descargar el VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="ccf07-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="ccf07-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="ccf07-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="ccf07-108">Registro de cambios completo</span><span class="sxs-lookup"><span data-stu-id="ccf07-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="ccf07-109">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="ccf07-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="ccf07-110">Cambios</span><span class="sxs-lookup"><span data-stu-id="ccf07-110">Changes</span></span>

- <span data-ttu-id="ccf07-111">Mejoras de módulo: Las mejoras de empaquetado de símbolos, empaquetado con `project.json` y más [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="ccf07-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="ccf07-112">Mostrar excepciones cuando se produce un error de búsqueda de proyectos en el comando de actualización [\#605](https://github.com/NuGet/NuGet.Client/pull/605)</span><span class="sxs-lookup"><span data-stu-id="ccf07-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="ccf07-113">Lee el tipo de paquete de la entrada `.nuspec` y `project.json` cuando se empaqueta [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="ccf07-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="ccf07-114">Asegúrese de NuGet.Shared no es un proyecto.</span><span class="sxs-lookup"><span data-stu-id="ccf07-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="ccf07-115">\#602</span><span class="sxs-lookup"><span data-stu-id="ccf07-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="ccf07-116">Use el tiempo de espera de inserción como el tiempo de espera de respuesta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="ccf07-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="ccf07-117">Archivos de paquete con tiempos de futuras no tendrán sus horas usa [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="ccf07-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="ccf07-118">Actualizando `NuGet.Core.dll` versión 2.12.0 para corregir el problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="ccf07-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="ccf07-119">Admitir./NuGet.CommandLine.XPlat - v \<detalle\> \<modo\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="ccf07-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="ccf07-120">Mostrar error restaurar sin `project.json` o `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="ccf07-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="ccf07-121">Corregir las versiones de dependencias cuando difieren de las versiones requeridas [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="ccf07-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>