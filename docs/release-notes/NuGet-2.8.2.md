---
title: Notas de la versión de NuGet 2.8.2
description: Notas de la versión de 2.8.2 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780365"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="24e46-103">Notas de la versión de NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="24e46-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="24e46-104">Notas de la [versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="24e46-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="24e46-105">2.8.2 de NuGet se lanzó el 22 de mayo de 2014.</span><span class="sxs-lookup"><span data-stu-id="24e46-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="24e46-106">Esta versión solo incluye los cambios en el nuget.exe línea de comandos, el paquete NuGet. Server y otros paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="24e46-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="24e46-107">La versión no incluía una extensión de Visual Studio o una extensión WebMatrix actualizada.</span><span class="sxs-lookup"><span data-stu-id="24e46-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="24e46-108">Actualizaciones importantes</span><span class="sxs-lookup"><span data-stu-id="24e46-108">Notable Updates</span></span>

<span data-ttu-id="24e46-109">Las actualizaciones más destacadas estaban en la línea de comandos nuget.exe y el paquete NuGet. Server (para las fuentes NuGet autohospedadas).</span><span class="sxs-lookup"><span data-stu-id="24e46-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="24e46-110">Correcciones de errores nuget.exe importantes</span><span class="sxs-lookup"><span data-stu-id="24e46-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="24e46-111"> Se produce un error en lanuget.exe de la extracción y sigue intentándolo</span><span class="sxs-lookup"><span data-stu-id="24e46-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="24e46-112">nuget.exe la instalación de inserciones no envía las credenciales de autenticación básicas correctamente</span><span class="sxs-lookup"><span data-stu-id="24e46-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="24e46-113">nuget.exe inserciones no sigue la redirección temporal</span><span class="sxs-lookup"><span data-stu-id="24e46-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="24e46-114">Corrección de errores importantes de NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="24e46-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="24e46-115">Valor incorrecto de IsAbsoluteLatestVersion devuelto por NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="24e46-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="24e46-116">Paquetes actualizados</span><span class="sxs-lookup"><span data-stu-id="24e46-116">Packages Updated</span></span>

<span data-ttu-id="24e46-117">Las correcciones de nuget.exe línea de comandos y NuGet. Server se incluyen como actualizaciones de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="24e46-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="24e46-118">También había otros paquetes actualizados con 2.8.2.</span><span class="sxs-lookup"><span data-stu-id="24e46-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="24e46-119">Esta es la lista de paquetes actualizados:</span><span class="sxs-lookup"><span data-stu-id="24e46-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="24e46-120">NuGet. Core</span><span class="sxs-lookup"><span data-stu-id="24e46-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="24e46-121">NuGet. CommandLine</span><span class="sxs-lookup"><span data-stu-id="24e46-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="24e46-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="24e46-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="24e46-123">NuGet. Build</span><span class="sxs-lookup"><span data-stu-id="24e46-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="24e46-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (el paquete, no la extensión)</span><span class="sxs-lookup"><span data-stu-id="24e46-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="24e46-125">Todos los cambios</span><span class="sxs-lookup"><span data-stu-id="24e46-125">All Changes</span></span>
<span data-ttu-id="24e46-126">Se han solucionado 10 problemas en la versión.</span><span class="sxs-lookup"><span data-stu-id="24e46-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="24e46-127">Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2.8.2, consulte el [seguimiento de problemas de Nuget en esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="24e46-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
