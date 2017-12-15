---
title: "Notas de la versión de NuGet 2.8.2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "Notas de la versión de NuGet 2.8.2 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.8.2 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="338aa-104">Notas de la versión de NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="338aa-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="338aa-105">[Notas de la versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="338aa-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="338aa-106">NuGet 2.8.2 se publicó en el 22 de mayo de 2014.</span><span class="sxs-lookup"><span data-stu-id="338aa-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="338aa-107">Esta versión solo incluye cambios en la línea de comandos nuget.exe, el paquete de NuGet.Server y otros paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="338aa-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="338aa-108">La versión no incluía una extensión de Visual Studio actualizado o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="338aa-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="338aa-109">Actualizaciones importantes</span><span class="sxs-lookup"><span data-stu-id="338aa-109">Notable Updates</span></span>

<span data-ttu-id="338aa-110">Las actualizaciones más importantes se encontraban en la línea de comandos nuget.exe y el paquete de NuGet.Server (para las fuentes de NuGet hospedados por sí mismo).</span><span class="sxs-lookup"><span data-stu-id="338aa-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="338aa-111">Correcciones de errores importantes nuget.exe</span><span class="sxs-lookup"><span data-stu-id="338aa-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="338aa-112">NuGet.exe inserción produce un error y sigue reintentando</span><span class="sxs-lookup"><span data-stu-id="338aa-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="338aa-113">NuGet.exe inserción no envía correctamente las credenciales de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="338aa-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="338aa-114">NuGet.exe inserción no siga Redirección temporal</span><span class="sxs-lookup"><span data-stu-id="338aa-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="338aa-115">Corrección de errores importantes NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="338aa-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="338aa-116">Valor incorrecto de IsAbsoluteLatestVersion devuelto por NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="338aa-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="338aa-117">Paquetes actualizado</span><span class="sxs-lookup"><span data-stu-id="338aa-117">Packages Updated</span></span>

<span data-ttu-id="338aa-118">La línea de comandos nuget.exe y correcciones de NuGet.Server se incluyen como actualizaciones de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="338aa-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="338aa-119">No hay otros paquetes actualizado con 2.8.2 así.</span><span class="sxs-lookup"><span data-stu-id="338aa-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="338aa-120">Esta es la lista de paquetes actualizados:</span><span class="sxs-lookup"><span data-stu-id="338aa-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="338aa-121">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="338aa-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="338aa-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="338aa-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="338aa-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="338aa-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="338aa-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="338aa-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="338aa-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (el paquete, no la extensión)</span><span class="sxs-lookup"><span data-stu-id="338aa-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="338aa-126">Todos los cambios</span><span class="sxs-lookup"><span data-stu-id="338aa-126">All Changes</span></span>
<span data-ttu-id="338aa-127">No hay 10 problemas solucionados en la versión.</span><span class="sxs-lookup"><span data-stu-id="338aa-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="338aa-128">Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8.2, por favor, vista la [NuGet Issue Tracker para esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="338aa-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
