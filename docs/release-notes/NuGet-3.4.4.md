---
title: Notas de la versión de NuGet 3.4.4
description: Notas de la versión de NuGet 3.4.4 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820872"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="c9869-103">Notas de la versión de NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="c9869-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="c9869-104">[Notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [notas de la versión 3.5 Beta de NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="c9869-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="c9869-105">El objetivo principal de esta versión fue las mejoras a la calidad del 3.4.3 versión de nuget.exe con algunas correcciones a la extensión de Visual Studio también.</span><span class="sxs-lookup"><span data-stu-id="c9869-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="c9869-106">Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="c9869-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="c9869-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="c9869-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="c9869-108">Registro de cambios completo</span><span class="sxs-lookup"><span data-stu-id="c9869-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="c9869-109">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="c9869-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="c9869-110">Cambios</span><span class="sxs-lookup"><span data-stu-id="c9869-110">Changes</span></span>

- <span data-ttu-id="c9869-111">Mejoras de módulo: Mejoras empaquetado símbolos, empaquetado con `project.json` y más [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="c9869-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="c9869-112">Mostrar excepciones cuando se produce un error de búsqueda de proyectos en el comando de actualización [\#605] ()https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="c9869-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="c9869-113">Lee el tipo de paquete de la entrada `.nuspec` y `project.json` cuando empaquetado [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="c9869-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="c9869-114">Asegúrese de NuGet.Shared no es un proyecto.</span><span class="sxs-lookup"><span data-stu-id="c9869-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="c9869-115">\#602</span><span class="sxs-lookup"><span data-stu-id="c9869-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="c9869-116">Usar el tiempo de espera de inserción como el tiempo de espera de la respuesta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="c9869-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="c9869-117">Archivos de paquete con tiempos de futuras no tendrán sus tiempos usa [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="c9869-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="c9869-118">Actualizar `NuGet.Core.dll` versión 2.12.0 para solucionar el problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="c9869-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="c9869-119">Admitir./NuGet.CommandLine.XPlat - v \<detalle\> \<modo\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="c9869-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="c9869-120">Mostrar error restaurar sin `project.json` o `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="c9869-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="c9869-121">Corregir las versiones de dependencia cuando difieren de las versiones necesarias [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="c9869-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>