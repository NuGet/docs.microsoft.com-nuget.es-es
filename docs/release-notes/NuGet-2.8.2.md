---
title: Notas de la versión de NuGet 2.8.2
description: Notas de la versión para incluir NuGet 2.8.2 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551153"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="d40d5-103">Notas de la versión de NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="d40d5-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="d40d5-104">[Notas de la versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="d40d5-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="d40d5-105">NuGet 2.8.2 se publicó en el 22 de mayo de 2014.</span><span class="sxs-lookup"><span data-stu-id="d40d5-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="d40d5-106">Esta versión incluye solo los cambios realizados en la línea de comandos nuget.exe, el paquete NuGet.Server y otros paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d40d5-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="d40d5-107">La versión no incluía una extensión actualizada de Visual Studio o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="d40d5-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="d40d5-108">Actualizaciones importantes</span><span class="sxs-lookup"><span data-stu-id="d40d5-108">Notable Updates</span></span>

<span data-ttu-id="d40d5-109">Las actualizaciones más importantes se encontraban en la línea de comandos de nuget.exe y el paquete NuGet.Server (para las fuentes de NuGet autohospedados).</span><span class="sxs-lookup"><span data-stu-id="d40d5-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="d40d5-110">Correcciones de errores importantes nuget.exe</span><span class="sxs-lookup"><span data-stu-id="d40d5-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="d40d5-111">NuGet.exe se produce un error de inserción y sigue reintentando</span><span class="sxs-lookup"><span data-stu-id="d40d5-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="d40d5-112">Inserción de NuGet.exe no envía correctamente las credenciales de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="d40d5-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="d40d5-113">Inserción de NuGet.exe no siga Redirección temporal</span><span class="sxs-lookup"><span data-stu-id="d40d5-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="d40d5-114">Corrección de errores importantes NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="d40d5-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="d40d5-115">Valor incorrecto de IsAbsoluteLatestVersion devuelto por NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="d40d5-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="d40d5-116">Paquetes actualizados</span><span class="sxs-lookup"><span data-stu-id="d40d5-116">Packages Updated</span></span>

<span data-ttu-id="d40d5-117">La línea de comandos de nuget.exe y NuGet.Server correcciones se incluyen como actualizaciones de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d40d5-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="d40d5-118">Se han producido otros paquetes actualizados con 2.8.2 también.</span><span class="sxs-lookup"><span data-stu-id="d40d5-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="d40d5-119">Esta es la lista de paquetes actualizadas:</span><span class="sxs-lookup"><span data-stu-id="d40d5-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="d40d5-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="d40d5-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="d40d5-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="d40d5-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="d40d5-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="d40d5-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="d40d5-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="d40d5-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="d40d5-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (el paquete, no la extensión)</span><span class="sxs-lookup"><span data-stu-id="d40d5-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="d40d5-125">Todos los cambios</span><span class="sxs-lookup"><span data-stu-id="d40d5-125">All Changes</span></span>
<span data-ttu-id="d40d5-126">Se produjeron los 10 problemas solucionados en la versión.</span><span class="sxs-lookup"><span data-stu-id="d40d5-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="d40d5-127">Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8.2, por favor, ver el [Issue Tracker para esta versión de NuGet](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="d40d5-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
