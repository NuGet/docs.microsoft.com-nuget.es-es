---
title: "Índice de servicio, NuGet API | Documentos de Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "El índice de servicio es el punto de entrada de la API de HTTP de NuGet y enumera las capacidades del servidor."
keywords: "Punto de entrada de API de NuGet, detección de punto de conexión de PI NuGetA"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 8de0bc15edc358d091d84da54b8b67c085f29645
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="service-index"></a><span data-ttu-id="52984-104">Índice de servicio</span><span class="sxs-lookup"><span data-stu-id="52984-104">Service index</span></span>

<span data-ttu-id="52984-105">El índice de servicio es un documento JSON que es el punto de entrada para un origen de paquete de NuGet y permite que una implementación de cliente detectar las capacidades del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="52984-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="52984-106">El índice de servicio es un objeto JSON con dos propiedades obligatorias: `version` (la versión de esquema del índice de servicio) y `resources` (los puntos de conexión o las capacidades del origen del paquete).</span><span class="sxs-lookup"><span data-stu-id="52984-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="52984-107">índice de servicio de NuGet.org se encuentra en `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="52984-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="52984-108">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="52984-108">Versioning</span></span>

<span data-ttu-id="52984-109">El `version` valor es una cadena de versión analizable SemVer 2.0.0 que indica la versión del esquema del índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="52984-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="52984-110">La API requiere que la cadena de versión tiene un número de versión principal de `3`.</span><span class="sxs-lookup"><span data-stu-id="52984-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="52984-111">Cuando se realizan cambios no importantes en el esquema de índice de servicio, se aumentará la versión secundaria de la cadena de versión.</span><span class="sxs-lookup"><span data-stu-id="52984-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="52984-112">Cada recurso en el índice de servicio tiene una versión independiente de la versión del esquema de índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="52984-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="52984-113">La versión de esquema actual es `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="52984-113">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="52984-114">El `3.0.0` versión es funcionalmente equivalente a la versión más antigua `3.0.0-beta.1` versión pero debe preferirse tal y como se comunica con más claridad el esquema estable, definido.</span><span class="sxs-lookup"><span data-stu-id="52984-114">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="52984-115">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="52984-115">HTTP methods</span></span>

<span data-ttu-id="52984-116">El índice de servicio está accesible mediante los métodos HTTP `GET` y `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="52984-116">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="52984-117">Recursos</span><span class="sxs-lookup"><span data-stu-id="52984-117">Resources</span></span>

<span data-ttu-id="52984-118">El `resources` propiedad contiene una matriz de recursos admitidos por este origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="52984-118">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="52984-119">Recurso</span><span class="sxs-lookup"><span data-stu-id="52984-119">Resource</span></span>

<span data-ttu-id="52984-120">Un recurso es un objeto en el `resources` matriz.</span><span class="sxs-lookup"><span data-stu-id="52984-120">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="52984-121">Representa una función con control de versiones de un origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="52984-121">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="52984-122">Un recurso tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="52984-122">A resource has the following properties:</span></span>

<span data-ttu-id="52984-123">nombre</span><span class="sxs-lookup"><span data-stu-id="52984-123">Name</span></span>          | <span data-ttu-id="52984-124">Tipo</span><span class="sxs-lookup"><span data-stu-id="52984-124">Type</span></span>   | <span data-ttu-id="52984-125">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="52984-125">Required</span></span> | <span data-ttu-id="52984-126">Notas</span><span class="sxs-lookup"><span data-stu-id="52984-126">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="52984-127">cadena</span><span class="sxs-lookup"><span data-stu-id="52984-127">string</span></span> | <span data-ttu-id="52984-128">sí</span><span class="sxs-lookup"><span data-stu-id="52984-128">yes</span></span>      | <span data-ttu-id="52984-129">La dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="52984-129">The URL to the resource</span></span>
@type         | <span data-ttu-id="52984-130">cadena</span><span class="sxs-lookup"><span data-stu-id="52984-130">string</span></span> | <span data-ttu-id="52984-131">sí</span><span class="sxs-lookup"><span data-stu-id="52984-131">yes</span></span>      | <span data-ttu-id="52984-132">Una constante de cadena que representa el tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="52984-132">A string constant representing the resource type</span></span>
<span data-ttu-id="52984-133">comentario</span><span class="sxs-lookup"><span data-stu-id="52984-133">comment</span></span>       | <span data-ttu-id="52984-134">cadena</span><span class="sxs-lookup"><span data-stu-id="52984-134">string</span></span> | <span data-ttu-id="52984-135">No</span><span class="sxs-lookup"><span data-stu-id="52984-135">no</span></span>       | <span data-ttu-id="52984-136">Una descripción legible del recurso</span><span class="sxs-lookup"><span data-stu-id="52984-136">A human readable description of the resource</span></span>

<span data-ttu-id="52984-137">El `@id` es una dirección URL que debe ser absoluto y debe tener el esquema HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="52984-137">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="52984-138">El `@type` se usa para identificar el protocolo específico que se utilizará al interactuar con los recursos.</span><span class="sxs-lookup"><span data-stu-id="52984-138">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="52984-139">El tipo del recurso es una cadena opaca, pero normalmente no tiene el formato:</span><span class="sxs-lookup"><span data-stu-id="52984-139">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="52984-140">Se esperan que los clientes para codificar de forma rígida el `@type` valores que se comprenden y buscarlos en el índice de un origen paquete de servicio.</span><span class="sxs-lookup"><span data-stu-id="52984-140">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="52984-141">Justo lo `@type` valores en la actualidad se enumeran en los documentos de referencia de recurso individual enumerados en la [Introducción a la API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="52984-141">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="52984-142">Por motivos de esta documentación, la documentación sobre los diferentes recursos básicamente se agruparán por el `{RESOURCE_NAME}` se encuentra en el índice de servicio que es análogo a la agrupación por escenario.</span><span class="sxs-lookup"><span data-stu-id="52984-142">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="52984-143">No hay ningún requisito de que cada recurso tiene un único `@id` o `@type`.</span><span class="sxs-lookup"><span data-stu-id="52984-143">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="52984-144">Depende de la implementación del cliente para determinar qué recursos se deben preferir frente a otro.</span><span class="sxs-lookup"><span data-stu-id="52984-144">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="52984-145">Una posible implementación es que los recursos de la misma o compatible `@type` pueden usarse en un modo round-robin en caso de error de servidor o error de conexión.</span><span class="sxs-lookup"><span data-stu-id="52984-145">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="52984-146">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="52984-146">Sample request</span></span>

<span data-ttu-id="52984-147">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="52984-147">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="52984-148">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="52984-148">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
