---
title: Límites de frecuencia | Documentos de Microsoft
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Las APIs NuGet habrá aplica límites de velocidad para evitar abusos.
keywords: Velocidad de NuGet API, limitar
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="e7c42-104">Límites de velocidad</span><span class="sxs-lookup"><span data-stu-id="e7c42-104">Rate Limits</span></span>

<span data-ttu-id="e7c42-105">La API de NuGet.org aplica la limitación de velocidad para evitar abusos.</span><span class="sxs-lookup"><span data-stu-id="e7c42-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="e7c42-106">Solicitud que supere el límite de velocidad devolverá el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7c42-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="e7c42-107">Las tablas siguientes muestran los límites de frecuencia para la API de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="e7c42-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="e7c42-108">Búsqueda de paquete</span><span class="sxs-lookup"><span data-stu-id="e7c42-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="e7c42-109">Recomendamos el uso de NuGet.org [API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) actualmente para la búsqueda de un rendimiento superior y no tiene ningún límite.</span><span class="sxs-lookup"><span data-stu-id="e7c42-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="e7c42-110">Para V1 y V2 API de búsqueda, se aplican los límites de followins:</span><span class="sxs-lookup"><span data-stu-id="e7c42-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="e7c42-111">API</span><span class="sxs-lookup"><span data-stu-id="e7c42-111">API</span></span> | <span data-ttu-id="e7c42-112">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="e7c42-112">Limit Type</span></span> | <span data-ttu-id="e7c42-113">Valor del límite</span><span class="sxs-lookup"><span data-stu-id="e7c42-113">Limit Value</span></span> | <span data-ttu-id="e7c42-114">API usecase</span><span class="sxs-lookup"><span data-stu-id="e7c42-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="e7c42-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="e7c42-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="e7c42-116">IP</span><span class="sxs-lookup"><span data-stu-id="e7c42-116">IP</span></span> | <span data-ttu-id="e7c42-117">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="e7c42-117">1000 / minute</span></span> | <span data-ttu-id="e7c42-118">Consultar los metadatos de paquete de NuGet a través de OData v1 `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="e7c42-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="e7c42-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="e7c42-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="e7c42-120">IP</span><span class="sxs-lookup"><span data-stu-id="e7c42-120">IP</span></span> | <span data-ttu-id="e7c42-121">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="e7c42-121">3000 / minute</span></span> | <span data-ttu-id="e7c42-122">Buscar paquetes de NuGet a través del extremo de la búsqueda de v1</span><span class="sxs-lookup"><span data-stu-id="e7c42-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="e7c42-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="e7c42-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="e7c42-124">IP</span><span class="sxs-lookup"><span data-stu-id="e7c42-124">IP</span></span> | <span data-ttu-id="e7c42-125">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="e7c42-125">20000 / minute</span></span> | <span data-ttu-id="e7c42-126">Consultar los metadatos de paquete de NuGet a través de OData v2 `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="e7c42-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="e7c42-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="e7c42-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="e7c42-128">IP</span><span class="sxs-lookup"><span data-stu-id="e7c42-128">IP</span></span> | <span data-ttu-id="e7c42-129">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="e7c42-129">100 / minute</span></span> | <span data-ttu-id="e7c42-130">Consultar el número de paquetes de NuGet a través de OData v2 `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="e7c42-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="e7c42-131">Paquete de inserción y ocultar</span><span class="sxs-lookup"><span data-stu-id="e7c42-131">Package Push and Unlist</span></span>

| <span data-ttu-id="e7c42-132">API</span><span class="sxs-lookup"><span data-stu-id="e7c42-132">API</span></span> | <span data-ttu-id="e7c42-133">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="e7c42-133">Limit Type</span></span> | <span data-ttu-id="e7c42-134">Valor del límite</span><span class="sxs-lookup"><span data-stu-id="e7c42-134">Limit Value</span></span> | <span data-ttu-id="e7c42-135">APU usecase</span><span class="sxs-lookup"><span data-stu-id="e7c42-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="e7c42-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="e7c42-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="e7c42-137">Clave de API</span><span class="sxs-lookup"><span data-stu-id="e7c42-137">API Key</span></span> | <span data-ttu-id="e7c42-138">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="e7c42-138">100 / minute</span></span> | <span data-ttu-id="e7c42-139">Cargar un nuevo paquete de NuGet (versión) a través del extremo de inserción de v2</span><span class="sxs-lookup"><span data-stu-id="e7c42-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="e7c42-140">**ELIMINAR** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="e7c42-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="e7c42-141">Clave de API</span><span class="sxs-lookup"><span data-stu-id="e7c42-141">API Key</span></span> | <span data-ttu-id="e7c42-142">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="e7c42-142">100 / minute</span></span> | <span data-ttu-id="e7c42-143">Ocultar un paquete de NuGet (versión) a través del extremo de v2</span><span class="sxs-lookup"><span data-stu-id="e7c42-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
