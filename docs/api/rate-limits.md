---
title: Límites de frecuencia, API de NuGet
description: Las API de NuGet tendrán límites de frecuencia aplicados para evitar el abuso.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813200"
---
# <a name="rate-limits"></a><span data-ttu-id="e8eb7-103">Límites de velocidad</span><span class="sxs-lookup"><span data-stu-id="e8eb7-103">Rate Limits</span></span>

<span data-ttu-id="e8eb7-104">La API de NuGet.org aplica la limitación de velocidad para impedir el abuso.</span><span class="sxs-lookup"><span data-stu-id="e8eb7-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="e8eb7-105">Las solicitudes que superan el límite de velocidad devuelven el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="e8eb7-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="e8eb7-106">Además de la limitación de solicitudes con límites de frecuencia, algunas API también aplican la cuota.</span><span class="sxs-lookup"><span data-stu-id="e8eb7-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="e8eb7-107">Las solicitudes que superan la cuota devuelven el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="e8eb7-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="e8eb7-108">En las tablas siguientes se enumeran los límites de frecuencia de la API de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="e8eb7-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="e8eb7-109">Búsqueda de paquetes</span><span class="sxs-lookup"><span data-stu-id="e8eb7-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="e8eb7-110">Se recomienda el uso de las [API de búsqueda de V3](search-query-service-resource.md) en la organización, ya que no tiene una tasa limitada actualmente.</span><span class="sxs-lookup"><span data-stu-id="e8eb7-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="e8eb7-111">En el caso de las API de búsqueda V1 y V2, se aplican los límites siguientes:</span><span class="sxs-lookup"><span data-stu-id="e8eb7-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="e8eb7-112">API</span><span class="sxs-lookup"><span data-stu-id="e8eb7-112">API</span></span> | <span data-ttu-id="e8eb7-113">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="e8eb7-113">Limit Type</span></span> | <span data-ttu-id="e8eb7-114">Valor límite</span><span class="sxs-lookup"><span data-stu-id="e8eb7-114">Limit Value</span></span> | <span data-ttu-id="e8eb7-115">API usecase</span><span class="sxs-lookup"><span data-stu-id="e8eb7-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="e8eb7-116">**Obtener** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="e8eb7-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="e8eb7-117">IP</span><span class="sxs-lookup"><span data-stu-id="e8eb7-117">IP</span></span> | <span data-ttu-id="e8eb7-118">1000/minuto</span><span class="sxs-lookup"><span data-stu-id="e8eb7-118">1000 / minute</span></span> | <span data-ttu-id="e8eb7-119">Consulta de metadatos de paquetes NuGet mediante la colección de `Packages` de OData de v1</span><span class="sxs-lookup"><span data-stu-id="e8eb7-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="e8eb7-120">**Obtener** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="e8eb7-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="e8eb7-121">IP</span><span class="sxs-lookup"><span data-stu-id="e8eb7-121">IP</span></span> | <span data-ttu-id="e8eb7-122">3000/minuto</span><span class="sxs-lookup"><span data-stu-id="e8eb7-122">3000 / minute</span></span> | <span data-ttu-id="e8eb7-123">Buscar paquetes NuGet a través del punto de conexión de búsqueda v1</span><span class="sxs-lookup"><span data-stu-id="e8eb7-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="e8eb7-124">**Obtener** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="e8eb7-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="e8eb7-125">IP</span><span class="sxs-lookup"><span data-stu-id="e8eb7-125">IP</span></span> | <span data-ttu-id="e8eb7-126">20000/minuto</span><span class="sxs-lookup"><span data-stu-id="e8eb7-126">20000 / minute</span></span> | <span data-ttu-id="e8eb7-127">Consulta de metadatos de paquetes NuGet a través de V2 OData `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="e8eb7-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="e8eb7-128">**Obtener** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="e8eb7-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="e8eb7-129">IP</span><span class="sxs-lookup"><span data-stu-id="e8eb7-129">IP</span></span> | <span data-ttu-id="e8eb7-130">100/minuto</span><span class="sxs-lookup"><span data-stu-id="e8eb7-130">100 / minute</span></span> | <span data-ttu-id="e8eb7-131">Consultar el recuento de paquetes NuGet mediante la colección de `Packages` OData V2</span><span class="sxs-lookup"><span data-stu-id="e8eb7-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="e8eb7-132">Instalación y deslista de paquetes</span><span class="sxs-lookup"><span data-stu-id="e8eb7-132">Package Push and Unlist</span></span>

| <span data-ttu-id="e8eb7-133">API</span><span class="sxs-lookup"><span data-stu-id="e8eb7-133">API</span></span> | <span data-ttu-id="e8eb7-134">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="e8eb7-134">Limit Type</span></span> | <span data-ttu-id="e8eb7-135">Valor límite</span><span class="sxs-lookup"><span data-stu-id="e8eb7-135">Limit Value</span></span> | <span data-ttu-id="e8eb7-136">API usecase</span><span class="sxs-lookup"><span data-stu-id="e8eb7-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="e8eb7-137">**Colocar** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="e8eb7-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="e8eb7-138">Clave de API</span><span class="sxs-lookup"><span data-stu-id="e8eb7-138">API Key</span></span> | <span data-ttu-id="e8eb7-139">350 por hora</span><span class="sxs-lookup"><span data-stu-id="e8eb7-139">350 / hour</span></span> | <span data-ttu-id="e8eb7-140">Carga de un nuevo paquete NuGet (versión) a través del punto de conexión de inserciones V2</span><span class="sxs-lookup"><span data-stu-id="e8eb7-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="e8eb7-141">**Eliminar** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="e8eb7-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="e8eb7-142">Clave de API</span><span class="sxs-lookup"><span data-stu-id="e8eb7-142">API Key</span></span> | <span data-ttu-id="e8eb7-143">250 por hora</span><span class="sxs-lookup"><span data-stu-id="e8eb7-143">250 / hour</span></span> | <span data-ttu-id="e8eb7-144">Mostrar un paquete NuGet (versión) a través del punto de conexión V2</span><span class="sxs-lookup"><span data-stu-id="e8eb7-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
