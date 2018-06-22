---
title: Notas de la versión de NuGet 2.8.2
description: Notas de la versión de NuGet 2.8.2 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821335"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="34cda-103">Notas de la versión de NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="34cda-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="34cda-104">[Notas de la versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="34cda-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="34cda-105">NuGet 2.8.2 se publicó en el 22 de mayo de 2014.</span><span class="sxs-lookup"><span data-stu-id="34cda-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="34cda-106">Esta versión solo incluye cambios en la línea de comandos nuget.exe, el paquete de NuGet.Server y otros paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="34cda-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="34cda-107">La versión no incluía una extensión de Visual Studio actualizado o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="34cda-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="34cda-108">Actualizaciones importantes</span><span class="sxs-lookup"><span data-stu-id="34cda-108">Notable Updates</span></span>

<span data-ttu-id="34cda-109">Las actualizaciones más importantes se encontraban en la línea de comandos nuget.exe y el paquete de NuGet.Server (para las fuentes de NuGet hospedados por sí mismo).</span><span class="sxs-lookup"><span data-stu-id="34cda-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="34cda-110">Correcciones de errores importantes nuget.exe</span><span class="sxs-lookup"><span data-stu-id="34cda-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="34cda-111">NuGet.exe inserción produce un error y sigue reintentando</span><span class="sxs-lookup"><span data-stu-id="34cda-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="34cda-112">NuGet.exe inserción no envía correctamente las credenciales de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="34cda-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="34cda-113">NuGet.exe inserción no siga Redirección temporal</span><span class="sxs-lookup"><span data-stu-id="34cda-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="34cda-114">Corrección de errores importantes NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="34cda-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="34cda-115">Valor incorrecto de IsAbsoluteLatestVersion devuelto por NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="34cda-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="34cda-116">Paquetes actualizado</span><span class="sxs-lookup"><span data-stu-id="34cda-116">Packages Updated</span></span>

<span data-ttu-id="34cda-117">La línea de comandos nuget.exe y correcciones de NuGet.Server se incluyen como actualizaciones de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="34cda-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="34cda-118">No hay otros paquetes actualizado con 2.8.2 así.</span><span class="sxs-lookup"><span data-stu-id="34cda-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="34cda-119">Esta es la lista de paquetes actualizados:</span><span class="sxs-lookup"><span data-stu-id="34cda-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="34cda-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="34cda-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="34cda-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="34cda-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="34cda-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="34cda-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="34cda-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="34cda-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="34cda-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (el paquete, no la extensión)</span><span class="sxs-lookup"><span data-stu-id="34cda-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="34cda-125">Todos los cambios</span><span class="sxs-lookup"><span data-stu-id="34cda-125">All Changes</span></span>
<span data-ttu-id="34cda-126">No hay 10 problemas solucionados en la versión.</span><span class="sxs-lookup"><span data-stu-id="34cda-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="34cda-127">Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8.2, por favor, vista la [NuGet Issue Tracker para esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="34cda-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
