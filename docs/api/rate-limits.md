---
title: Límites, NuGet API de frecuencia
description: Las APIs NuGet habrá aplica límites de velocidad para evitar abusos.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: e236d685a700d0f47480336cece8edfd44c28863
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="rate-limits"></a><span data-ttu-id="c0be9-103">Límites de velocidad</span><span class="sxs-lookup"><span data-stu-id="c0be9-103">Rate Limits</span></span>

<span data-ttu-id="c0be9-104">La API de NuGet.org aplica la limitación de velocidad para evitar abusos.</span><span class="sxs-lookup"><span data-stu-id="c0be9-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="c0be9-105">Solicitud que supere el límite de velocidad devolverá el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0be9-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="c0be9-106">Las tablas siguientes muestran los límites de frecuencia para la API de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c0be9-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="c0be9-107">Búsqueda de paquete</span><span class="sxs-lookup"><span data-stu-id="c0be9-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="c0be9-108">Recomendamos el uso de NuGet.org [API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) actualmente para la búsqueda de un rendimiento superior y no tiene ningún límite.</span><span class="sxs-lookup"><span data-stu-id="c0be9-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="c0be9-109">Para V1 y V2 API de búsqueda, se aplican los límites de followins:</span><span class="sxs-lookup"><span data-stu-id="c0be9-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="c0be9-110">API</span><span class="sxs-lookup"><span data-stu-id="c0be9-110">API</span></span> | <span data-ttu-id="c0be9-111">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="c0be9-111">Limit Type</span></span> | <span data-ttu-id="c0be9-112">Valor del límite</span><span class="sxs-lookup"><span data-stu-id="c0be9-112">Limit Value</span></span> | <span data-ttu-id="c0be9-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="c0be9-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="c0be9-114">**OBTENER** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="c0be9-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="c0be9-115">IP</span><span class="sxs-lookup"><span data-stu-id="c0be9-115">IP</span></span> | <span data-ttu-id="c0be9-116">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="c0be9-116">1000 / minute</span></span> | <span data-ttu-id="c0be9-117">Consultar los metadatos de paquete de NuGet a través de OData v1 `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="c0be9-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="c0be9-118">**OBTENER** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="c0be9-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="c0be9-119">IP</span><span class="sxs-lookup"><span data-stu-id="c0be9-119">IP</span></span> | <span data-ttu-id="c0be9-120">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="c0be9-120">3000 / minute</span></span> | <span data-ttu-id="c0be9-121">Buscar paquetes de NuGet a través del extremo de la búsqueda de v1</span><span class="sxs-lookup"><span data-stu-id="c0be9-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="c0be9-122">**OBTENER** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="c0be9-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="c0be9-123">IP</span><span class="sxs-lookup"><span data-stu-id="c0be9-123">IP</span></span> | <span data-ttu-id="c0be9-124">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="c0be9-124">20000 / minute</span></span> | <span data-ttu-id="c0be9-125">Consultar los metadatos de paquete de NuGet a través de OData v2 `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="c0be9-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="c0be9-126">**OBTENER** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="c0be9-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="c0be9-127">IP</span><span class="sxs-lookup"><span data-stu-id="c0be9-127">IP</span></span> | <span data-ttu-id="c0be9-128">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="c0be9-128">100 / minute</span></span> | <span data-ttu-id="c0be9-129">Consultar el número de paquetes de NuGet a través de OData v2 `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="c0be9-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="c0be9-130">Paquete de inserción y ocultar</span><span class="sxs-lookup"><span data-stu-id="c0be9-130">Package Push and Unlist</span></span>

| <span data-ttu-id="c0be9-131">API</span><span class="sxs-lookup"><span data-stu-id="c0be9-131">API</span></span> | <span data-ttu-id="c0be9-132">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="c0be9-132">Limit Type</span></span> | <span data-ttu-id="c0be9-133">Valor del límite</span><span class="sxs-lookup"><span data-stu-id="c0be9-133">Limit Value</span></span> | <span data-ttu-id="c0be9-134">API usecase</span><span class="sxs-lookup"><span data-stu-id="c0be9-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="c0be9-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="c0be9-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="c0be9-136">Clave de API</span><span class="sxs-lookup"><span data-stu-id="c0be9-136">API Key</span></span> | <span data-ttu-id="c0be9-137">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="c0be9-137">100 / minute</span></span> | <span data-ttu-id="c0be9-138">Cargar un nuevo paquete de NuGet (versión) a través del extremo de inserción de v2</span><span class="sxs-lookup"><span data-stu-id="c0be9-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="c0be9-139">**ELIMINAR** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="c0be9-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="c0be9-140">Clave de API</span><span class="sxs-lookup"><span data-stu-id="c0be9-140">API Key</span></span> | <span data-ttu-id="c0be9-141">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="c0be9-141">100 / minute</span></span> | <span data-ttu-id="c0be9-142">Ocultar un paquete de NuGet (versión) a través del extremo de v2</span><span class="sxs-lookup"><span data-stu-id="c0be9-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
