---
title: Comando de búsqueda de la CLI de NuGet
description: Referencia del comando nuget.exe Search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779163"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="6dda4-103">comando Search (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="6dda4-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="6dda4-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 5,8 +</span><span class="sxs-lookup"><span data-stu-id="6dda4-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="6dda4-105">Busca un origen determinado mediante la cadena de consulta proporcionada.</span><span class="sxs-lookup"><span data-stu-id="6dda4-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="6dda4-106">Si no se especifica ningún origen, se usan todos los orígenes definidos en% AppData% \NuGet\NuGet.config.</span><span class="sxs-lookup"><span data-stu-id="6dda4-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="6dda4-107">Uso</span><span class="sxs-lookup"><span data-stu-id="6dda4-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="6dda4-108">donde se aplican los términos de búsqueda a los nombres de paquetes, etiquetas y descripciones de paquetes tal y como se usan en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6dda4-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="6dda4-109">Opciones</span><span class="sxs-lookup"><span data-stu-id="6dda4-109">Options</span></span>

| <span data-ttu-id="6dda4-110">NOMBRE</span><span class="sxs-lookup"><span data-stu-id="6dda4-110">Name</span></span> | <span data-ttu-id="6dda4-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dda4-111">Description</span></span> | <span data-ttu-id="6dda4-112">Uso</span><span class="sxs-lookup"><span data-stu-id="6dda4-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="6dda4-113">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="6dda4-113">PreRelease</span></span> | <span data-ttu-id="6dda4-114">Los paquetes de versión preliminar no se incluyen de forma predeterminada, pero se pueden incluir con este argumento.</span><span class="sxs-lookup"><span data-stu-id="6dda4-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="6dda4-115">-Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="6dda4-115">-PreRelease</span></span> |
| <span data-ttu-id="6dda4-116">Source</span><span class="sxs-lookup"><span data-stu-id="6dda4-116">Source</span></span> | <span data-ttu-id="6dda4-117">Orígenes de paquetes específicos para buscar en lugar de consultar los orígenes predeterminados en __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="6dda4-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="6dda4-118">-Origen `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="6dda4-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="6dda4-119">Take</span><span class="sxs-lookup"><span data-stu-id="6dda4-119">Take</span></span> | <span data-ttu-id="6dda4-120">Número de resultados que se van a devolver.</span><span class="sxs-lookup"><span data-stu-id="6dda4-120">The number of results to return.</span></span> <span data-ttu-id="6dda4-121">El valor predeterminado es 20.</span><span class="sxs-lookup"><span data-stu-id="6dda4-121">The default value is 20.</span></span> | <span data-ttu-id="6dda4-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="6dda4-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="6dda4-123">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="6dda4-123">Verbosity</span></span> | <span data-ttu-id="6dda4-124">Nivel de detalle que se va a mostrar en el resultado.</span><span class="sxs-lookup"><span data-stu-id="6dda4-124">The level of detail to display in the output.</span></span> <span data-ttu-id="6dda4-125">El valor predeterminado es _normal_.</span><span class="sxs-lookup"><span data-stu-id="6dda4-125">The default is _normal_.</span></span> <span data-ttu-id="6dda4-126">(Consulte la nota siguiente)</span><span class="sxs-lookup"><span data-stu-id="6dda4-126">(See the note below)</span></span>  | <span data-ttu-id="6dda4-127">-Nivel de detalle `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="6dda4-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="6dda4-128">Ayuda</span><span class="sxs-lookup"><span data-stu-id="6dda4-128">Help</span></span> | <span data-ttu-id="6dda4-129">Muestra información de ayuda para el comando</span><span class="sxs-lookup"><span data-stu-id="6dda4-129">Displays help information for the command</span></span> | <span data-ttu-id="6dda4-130">-Help</span><span class="sxs-lookup"><span data-stu-id="6dda4-130">-Help</span></span> |

<span data-ttu-id="6dda4-131">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6dda4-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="6dda4-132">Niveles de detalle:</span><span class="sxs-lookup"><span data-stu-id="6dda4-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="6dda4-133">IDENTIFICADOR de paquete _silencioso_ , versión</span><span class="sxs-lookup"><span data-stu-id="6dda4-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="6dda4-134">_normal_ : ID. de paquete, versión, descargas, vista previa de la descripción</span><span class="sxs-lookup"><span data-stu-id="6dda4-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="6dda4-135">_detallado_ : ID. de paquete, versión, descargas, Descripción completa, otra información, como la dirección URL de la consulta</span><span class="sxs-lookup"><span data-stu-id="6dda4-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="6dda4-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6dda4-136">Examples</span></span>

<span data-ttu-id="6dda4-137">Buscar paquetes relacionados con el *registro* de orígenes predeterminados:</span><span class="sxs-lookup"><span data-stu-id="6dda4-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="6dda4-138">Busque paquetes relacionados con el *registro* con detalle detallado:</span><span class="sxs-lookup"><span data-stu-id="6dda4-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="6dda4-139">Busque paquetes relacionados con el *registro* y muestre solo los 5 resultados principales:</span><span class="sxs-lookup"><span data-stu-id="6dda4-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="6dda4-140">Busque paquetes relacionados con *JSON*, incluidas versiones preliminares, de origen/fuente especificado:</span><span class="sxs-lookup"><span data-stu-id="6dda4-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="6dda4-141">Buscar paquetes relacionados con *JSON* desde varios orígenes y fuentes:</span><span class="sxs-lookup"><span data-stu-id="6dda4-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
