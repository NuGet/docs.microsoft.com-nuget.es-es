---
title: Límites, API de NuGet de frecuencia
description: Las APIs NuGet habrá aplica límites de velocidad para evitar abusos.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548682"
---
# <a name="rate-limits"></a><span data-ttu-id="1191e-103">Límites de velocidad</span><span class="sxs-lookup"><span data-stu-id="1191e-103">Rate Limits</span></span>

<span data-ttu-id="1191e-104">La API de NuGet.org aplica la limitación de velocidad para evitar abusos.</span><span class="sxs-lookup"><span data-stu-id="1191e-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="1191e-105">Las solicitudes que superen el límite de velocidad devuelven el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="1191e-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="1191e-106">Además de los límites de frecuencia de uso de la limitación de solicitudes, algunas API de aplicar la cuota.</span><span class="sxs-lookup"><span data-stu-id="1191e-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="1191e-107">Las solicitudes que superan la cuota, devuelven el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="1191e-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="1191e-108">Las siguientes tablas enumeran los límites de frecuencia para la API de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="1191e-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="1191e-109">Búsqueda de paquetes</span><span class="sxs-lookup"><span data-stu-id="1191e-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="1191e-110">Se recomienda el uso de NuGet.org [API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) actualmente para la búsqueda de alto rendimiento y no tienen ningún límite.</span><span class="sxs-lookup"><span data-stu-id="1191e-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="1191e-111">API de búsquedas de V1 y V2, se aplican los límites de followins:</span><span class="sxs-lookup"><span data-stu-id="1191e-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="1191e-112">API</span><span class="sxs-lookup"><span data-stu-id="1191e-112">API</span></span> | <span data-ttu-id="1191e-113">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="1191e-113">Limit Type</span></span> | <span data-ttu-id="1191e-114">Valor de límite</span><span class="sxs-lookup"><span data-stu-id="1191e-114">Limit Value</span></span> | <span data-ttu-id="1191e-115">API usecase</span><span class="sxs-lookup"><span data-stu-id="1191e-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="1191e-116">**OBTENER** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="1191e-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="1191e-117">IP</span><span class="sxs-lookup"><span data-stu-id="1191e-117">IP</span></span> | <span data-ttu-id="1191e-118">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="1191e-118">1000 / minute</span></span> | <span data-ttu-id="1191e-119">Consultar los metadatos del paquete de NuGet a través de OData v1 `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="1191e-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="1191e-120">**OBTENER** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="1191e-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="1191e-121">IP</span><span class="sxs-lookup"><span data-stu-id="1191e-121">IP</span></span> | <span data-ttu-id="1191e-122">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="1191e-122">3000 / minute</span></span> | <span data-ttu-id="1191e-123">Buscar paquetes de NuGet a través del punto de conexión v1 búsqueda</span><span class="sxs-lookup"><span data-stu-id="1191e-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="1191e-124">**OBTENER** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="1191e-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="1191e-125">IP</span><span class="sxs-lookup"><span data-stu-id="1191e-125">IP</span></span> | <span data-ttu-id="1191e-126">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="1191e-126">20000 / minute</span></span> | <span data-ttu-id="1191e-127">Consultar los metadatos de paquete de NuGet a través de OData v2 `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="1191e-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="1191e-128">**OBTENER** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="1191e-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="1191e-129">IP</span><span class="sxs-lookup"><span data-stu-id="1191e-129">IP</span></span> | <span data-ttu-id="1191e-130">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="1191e-130">100 / minute</span></span> | <span data-ttu-id="1191e-131">Consultar el número de paquetes de NuGet a través de OData v2 `Packages` colección</span><span class="sxs-lookup"><span data-stu-id="1191e-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="1191e-132">Paquete de insertar y quitar de la lista</span><span class="sxs-lookup"><span data-stu-id="1191e-132">Package Push and Unlist</span></span>

| <span data-ttu-id="1191e-133">API</span><span class="sxs-lookup"><span data-stu-id="1191e-133">API</span></span> | <span data-ttu-id="1191e-134">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="1191e-134">Limit Type</span></span> | <span data-ttu-id="1191e-135">Valor de límite</span><span class="sxs-lookup"><span data-stu-id="1191e-135">Limit Value</span></span> | <span data-ttu-id="1191e-136">API usecase</span><span class="sxs-lookup"><span data-stu-id="1191e-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="1191e-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="1191e-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="1191e-138">Clave de API</span><span class="sxs-lookup"><span data-stu-id="1191e-138">API Key</span></span> | <span data-ttu-id="1191e-139">250 / hora</span><span class="sxs-lookup"><span data-stu-id="1191e-139">250 / hour</span></span> | <span data-ttu-id="1191e-140">Cargar un nuevo paquete de NuGet (versión) a través del punto de conexión de inserción de v2</span><span class="sxs-lookup"><span data-stu-id="1191e-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="1191e-141">**ELIMINAR** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="1191e-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="1191e-142">Clave de API</span><span class="sxs-lookup"><span data-stu-id="1191e-142">API Key</span></span> | <span data-ttu-id="1191e-143">250 / hora</span><span class="sxs-lookup"><span data-stu-id="1191e-143">250 / hour</span></span> | <span data-ttu-id="1191e-144">Quitar de la lista un paquete de NuGet (versión) a través del punto de conexión v2</span><span class="sxs-lookup"><span data-stu-id="1191e-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
