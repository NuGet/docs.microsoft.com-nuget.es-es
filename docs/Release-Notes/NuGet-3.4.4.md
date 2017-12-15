---
title: "Notas de la versión de NuGet 3.4.4 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f0aa9bb-75e5-429d-9954-3cb41a909c14
description: "Notas de la versión de NuGet 3.4.4 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.4.4 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 51ddb918d2269990588e9cba4d15ffeb878de5f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="c53ce-104">Notas de la versión de NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="c53ce-104">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="c53ce-105">[Notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [notas de la versión 3.5 Beta de NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="c53ce-105">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="c53ce-106">El objetivo principal de esta versión fue las mejoras a la calidad del 3.4.3 versión de nuget.exe con algunas correcciones a la extensión de Visual Studio también.</span><span class="sxs-lookup"><span data-stu-id="c53ce-106">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="c53ce-107">Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="c53ce-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="c53ce-108">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="c53ce-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="c53ce-109">Registro de cambios completo</span><span class="sxs-lookup"><span data-stu-id="c53ce-109">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="c53ce-110">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="c53ce-110">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="c53ce-111">Cambios</span><span class="sxs-lookup"><span data-stu-id="c53ce-111">Changes</span></span>

- <span data-ttu-id="c53ce-112">Mejoras de módulo: Mejoras empaquetado símbolos, empaquetado con `project.json` y más [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="c53ce-112">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="c53ce-113">Mostrar excepciones cuando se produce un error de búsqueda de proyectos en el comando de actualización [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="c53ce-113">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="c53ce-114">Lee el tipo de paquete de la entrada `.nuspec` y `project.json` cuando empaquetado [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="c53ce-114">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="c53ce-115">Asegúrese de NuGet.Shared no es un proyecto.</span><span class="sxs-lookup"><span data-stu-id="c53ce-115">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="c53ce-116">\#602</span><span class="sxs-lookup"><span data-stu-id="c53ce-116">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="c53ce-117">Usar el tiempo de espera de inserción como el tiempo de espera de la respuesta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="c53ce-117">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="c53ce-118">Archivos de paquete con tiempos de futuras no tendrán sus tiempos usa [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="c53ce-118">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="c53ce-119">Actualizar `NuGet.Core.dll` versión 2.12.0 para solucionar el problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="c53ce-119">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="c53ce-120">Admitir./NuGet.CommandLine.XPlat - v \<detalle\> \<modo\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="c53ce-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="c53ce-121">Mostrar error restaurar sin `project.json` o `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="c53ce-121">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="c53ce-122">Corregir las versiones de dependencia cuando difieren de las versiones necesarias [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="c53ce-122">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>