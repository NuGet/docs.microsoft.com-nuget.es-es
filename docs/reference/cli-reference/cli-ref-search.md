---
title: Comando de búsqueda de la CLI de NuGet
description: Referencia del comando nuget.exe search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323666"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="5cf57-103">comando search (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="5cf57-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="5cf57-104">**Se aplica a: consumo** de &bullet; **paquetes Versiones admitidas:** 5.8+</span><span class="sxs-lookup"><span data-stu-id="5cf57-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="5cf57-105">Busca un origen determinado mediante la cadena de consulta proporcionada.</span><span class="sxs-lookup"><span data-stu-id="5cf57-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="5cf57-106">Si no se especifica ningún origen, se usan todos los orígenes definidos en %AppData%\NuGet\NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="5cf57-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="5cf57-107">Uso</span><span class="sxs-lookup"><span data-stu-id="5cf57-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="5cf57-108">donde los términos de búsqueda se aplican a los nombres de paquetes, etiquetas y descripciones de paquetes igual que cuando se usan en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5cf57-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="5cf57-109">Opciones</span><span class="sxs-lookup"><span data-stu-id="5cf57-109">Options</span></span>

| <span data-ttu-id="5cf57-110">NOMBRE</span><span class="sxs-lookup"><span data-stu-id="5cf57-110">Name</span></span> | <span data-ttu-id="5cf57-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="5cf57-111">Description</span></span> | <span data-ttu-id="5cf57-112">Uso</span><span class="sxs-lookup"><span data-stu-id="5cf57-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="5cf57-113">Prelanzamiento</span><span class="sxs-lookup"><span data-stu-id="5cf57-113">PreRelease</span></span> | <span data-ttu-id="5cf57-114">Los paquetes de versión previa no se incluyen de forma predeterminada, pero se pueden incluir mediante este argumento.</span><span class="sxs-lookup"><span data-stu-id="5cf57-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="5cf57-115">-Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="5cf57-115">-PreRelease</span></span> |
| <span data-ttu-id="5cf57-116">Source</span><span class="sxs-lookup"><span data-stu-id="5cf57-116">Source</span></span> | <span data-ttu-id="5cf57-117">Orígenes de paquete específicos para buscar en lugar de consultar los orígenes predeterminados __ennuget.config__</span><span class="sxs-lookup"><span data-stu-id="5cf57-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="5cf57-118">-Source `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="5cf57-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="5cf57-119">Take</span><span class="sxs-lookup"><span data-stu-id="5cf57-119">Take</span></span> | <span data-ttu-id="5cf57-120">Número de resultados que se devuelven.</span><span class="sxs-lookup"><span data-stu-id="5cf57-120">The number of results to return.</span></span> <span data-ttu-id="5cf57-121">El valor predeterminado es 20.</span><span class="sxs-lookup"><span data-stu-id="5cf57-121">The default value is 20.</span></span> | <span data-ttu-id="5cf57-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="5cf57-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="5cf57-123">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="5cf57-123">Verbosity</span></span> | <span data-ttu-id="5cf57-124">Nivel de detalle que se mostrará en la salida.</span><span class="sxs-lookup"><span data-stu-id="5cf57-124">The level of detail to display in the output.</span></span> <span data-ttu-id="5cf57-125">El valor predeterminado es _normal._</span><span class="sxs-lookup"><span data-stu-id="5cf57-125">The default is _normal_.</span></span> <span data-ttu-id="5cf57-126">(Vea la nota siguiente)</span><span class="sxs-lookup"><span data-stu-id="5cf57-126">(See the note below)</span></span>  | <span data-ttu-id="5cf57-127">-Verbosity `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="5cf57-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="5cf57-128">Ayuda</span><span class="sxs-lookup"><span data-stu-id="5cf57-128">Help</span></span> | <span data-ttu-id="5cf57-129">Muestra información de ayuda para el comando</span><span class="sxs-lookup"><span data-stu-id="5cf57-129">Displays help information for the command</span></span> | <span data-ttu-id="5cf57-130">-Help</span><span class="sxs-lookup"><span data-stu-id="5cf57-130">-Help</span></span> |

<span data-ttu-id="5cf57-131">Consulte también Variables [de entorno.](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5cf57-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="5cf57-132">Niveles de detalle:</span><span class="sxs-lookup"><span data-stu-id="5cf57-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="5cf57-133">_quiet:_ id. de paquete, versión</span><span class="sxs-lookup"><span data-stu-id="5cf57-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="5cf57-134">_normal:_ id. de paquete, versión, descargas, versión preliminar de descripción</span><span class="sxs-lookup"><span data-stu-id="5cf57-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="5cf57-135">_detallado:_ id. de paquete, versión, descargas, descripción completa, otra información como la dirección URL de consulta</span><span class="sxs-lookup"><span data-stu-id="5cf57-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="5cf57-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5cf57-136">Examples</span></span>

<span data-ttu-id="5cf57-137">Busque *paquetes relacionados con* el registro de orígenes predeterminados:</span><span class="sxs-lookup"><span data-stu-id="5cf57-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="5cf57-138">Busque *paquetes relacionados* con el registro con un nivel de detalle detallado:</span><span class="sxs-lookup"><span data-stu-id="5cf57-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="5cf57-139">Busque *paquetes relacionados con* el registro y muestre solo los 5 primeros resultados:</span><span class="sxs-lookup"><span data-stu-id="5cf57-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="5cf57-140">Busque *paquetes relacionados* con JSON, incluidas las versiones anteriores, de la fuente o fuente especificadas:</span><span class="sxs-lookup"><span data-stu-id="5cf57-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="5cf57-141">Busque *paquetes relacionados* con JSON de varios orígenes o fuentes:</span><span class="sxs-lookup"><span data-stu-id="5cf57-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
