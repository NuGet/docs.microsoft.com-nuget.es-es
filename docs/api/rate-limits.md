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
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367939"
---
# <a name="rate-limits"></a><span data-ttu-id="699bf-103">Límites de velocidad</span><span class="sxs-lookup"><span data-stu-id="699bf-103">Rate Limits</span></span>

<span data-ttu-id="699bf-104">La API de NuGet.org aplica la limitación de velocidad para impedir el abuso.</span><span class="sxs-lookup"><span data-stu-id="699bf-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="699bf-105">Las solicitudes que superan el límite de velocidad devuelven el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="699bf-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="699bf-106">Además de la limitación de solicitudes con límites de frecuencia, algunas API también aplican la cuota.</span><span class="sxs-lookup"><span data-stu-id="699bf-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="699bf-107">Las solicitudes que superan la cuota devuelven el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="699bf-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="699bf-108">En las tablas siguientes se enumeran los límites de frecuencia de la API de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="699bf-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="699bf-109">Búsqueda de paquetes</span><span class="sxs-lookup"><span data-stu-id="699bf-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="699bf-110">Se recomienda el uso de las [API de búsqueda de V3](search-query-service-resource.md) en la organización, ya que no tiene una tasa limitada actualmente.</span><span class="sxs-lookup"><span data-stu-id="699bf-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="699bf-111">En el caso de las API de búsqueda V1 y V2, se aplican los límites siguientes:</span><span class="sxs-lookup"><span data-stu-id="699bf-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="699bf-112">API</span><span class="sxs-lookup"><span data-stu-id="699bf-112">API</span></span> | <span data-ttu-id="699bf-113">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="699bf-113">Limit Type</span></span> | <span data-ttu-id="699bf-114">Valor límite</span><span class="sxs-lookup"><span data-stu-id="699bf-114">Limit Value</span></span> | <span data-ttu-id="699bf-115">Caso de uso de la API</span><span class="sxs-lookup"><span data-stu-id="699bf-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="699bf-116">**Obtener**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="699bf-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="699bf-117">IP</span><span class="sxs-lookup"><span data-stu-id="699bf-117">IP</span></span> | <span data-ttu-id="699bf-118">1000/minuto</span><span class="sxs-lookup"><span data-stu-id="699bf-118">1000 / minute</span></span> | <span data-ttu-id="699bf-119">Consulta de metadatos de paquetes NuGet mediante la colección de OData v1 `Packages`</span><span class="sxs-lookup"><span data-stu-id="699bf-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="699bf-120">**Obtener**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="699bf-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="699bf-121">IP</span><span class="sxs-lookup"><span data-stu-id="699bf-121">IP</span></span> | <span data-ttu-id="699bf-122">3000/minuto</span><span class="sxs-lookup"><span data-stu-id="699bf-122">3000 / minute</span></span> | <span data-ttu-id="699bf-123">Buscar paquetes NuGet a través del punto de conexión de búsqueda v1</span><span class="sxs-lookup"><span data-stu-id="699bf-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="699bf-124">**Obtener**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="699bf-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="699bf-125">IP</span><span class="sxs-lookup"><span data-stu-id="699bf-125">IP</span></span> | <span data-ttu-id="699bf-126">20000/minuto</span><span class="sxs-lookup"><span data-stu-id="699bf-126">20000 / minute</span></span> | <span data-ttu-id="699bf-127">Consultar metadatos de paquetes NuGet a través de la colección OData V2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="699bf-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="699bf-128">**Obtener**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="699bf-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="699bf-129">IP</span><span class="sxs-lookup"><span data-stu-id="699bf-129">IP</span></span> | <span data-ttu-id="699bf-130">100/minuto</span><span class="sxs-lookup"><span data-stu-id="699bf-130">100 / minute</span></span> | <span data-ttu-id="699bf-131">Consultar el recuento de paquetes NuGet mediante la colección OData V2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="699bf-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="699bf-132">Instalación y deslista de paquetes</span><span class="sxs-lookup"><span data-stu-id="699bf-132">Package Push and Unlist</span></span>

| <span data-ttu-id="699bf-133">API</span><span class="sxs-lookup"><span data-stu-id="699bf-133">API</span></span> | <span data-ttu-id="699bf-134">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="699bf-134">Limit Type</span></span> | <span data-ttu-id="699bf-135">Valor límite</span><span class="sxs-lookup"><span data-stu-id="699bf-135">Limit Value</span></span> | <span data-ttu-id="699bf-136">Caso de uso de la API</span><span class="sxs-lookup"><span data-stu-id="699bf-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="699bf-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="699bf-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="699bf-138">Clave de API</span><span class="sxs-lookup"><span data-stu-id="699bf-138">API Key</span></span> | <span data-ttu-id="699bf-139">350 por hora</span><span class="sxs-lookup"><span data-stu-id="699bf-139">350 / hour</span></span> | <span data-ttu-id="699bf-140">Carga de un nuevo paquete NuGet (versión) a través del punto de conexión de inserciones V2</span><span class="sxs-lookup"><span data-stu-id="699bf-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="699bf-141">**Eliminar**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="699bf-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="699bf-142">Clave de API</span><span class="sxs-lookup"><span data-stu-id="699bf-142">API Key</span></span> | <span data-ttu-id="699bf-143">250 por hora</span><span class="sxs-lookup"><span data-stu-id="699bf-143">250 / hour</span></span> | <span data-ttu-id="699bf-144">Mostrar un paquete NuGet (versión) a través del punto de conexión V2</span><span class="sxs-lookup"><span data-stu-id="699bf-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="699bf-145">vistas de página del sitio web de nuget.org</span><span class="sxs-lookup"><span data-stu-id="699bf-145">nuget.org website page views</span></span>

<span data-ttu-id="699bf-146">Si tiene acceso a las páginas web de nuget.org mediante programación, considere la posibilidad de investigar nuestras [API de V3](overview.md)documentadas.</span><span class="sxs-lookup"><span data-stu-id="699bf-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="699bf-147">Estos puntos de conexión permiten un acceso más sencillo a los metadatos y al contenido del paquete.</span><span class="sxs-lookup"><span data-stu-id="699bf-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="699bf-148">La API V3 tiene una mejor disponibilidad y tiene un mayor rendimiento que el acceso a las páginas web de la galería de NuGet, que están diseñadas para la interacción del explorador Web.</span><span class="sxs-lookup"><span data-stu-id="699bf-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="699bf-149">API</span><span class="sxs-lookup"><span data-stu-id="699bf-149">API</span></span> | <span data-ttu-id="699bf-150">Tipo de límite</span><span class="sxs-lookup"><span data-stu-id="699bf-150">Limit Type</span></span> | <span data-ttu-id="699bf-151">Valor límite</span><span class="sxs-lookup"><span data-stu-id="699bf-151">Limit Value</span></span> | <span data-ttu-id="699bf-152">Caso de uso de la API</span><span class="sxs-lookup"><span data-stu-id="699bf-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="699bf-153">**Obtener**`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="699bf-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="699bf-154">IP</span><span class="sxs-lookup"><span data-stu-id="699bf-154">IP</span></span> | <span data-ttu-id="699bf-155">50/minuto</span><span class="sxs-lookup"><span data-stu-id="699bf-155">50 / minute</span></span> | <span data-ttu-id="699bf-156">Mostrar la página de detalles del paquete (versión).</span><span class="sxs-lookup"><span data-stu-id="699bf-156">Display package (version) details page.</span></span> 
