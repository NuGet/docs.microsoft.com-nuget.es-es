---
title: Índice de servicio, API de NuGet
description: El índice de servicio es el punto de entrada de la API HTTP de NuGet y enumera las funciones del servidor.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775354"
---
# <a name="service-index"></a><span data-ttu-id="a14b3-103">Índice de servicio</span><span class="sxs-lookup"><span data-stu-id="a14b3-103">Service index</span></span>

<span data-ttu-id="a14b3-104">El índice de servicio es un documento JSON que es el punto de entrada de un origen de paquete NuGet y permite a una implementación de cliente detectar las capacidades del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="a14b3-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="a14b3-105">El índice de servicio es un objeto JSON con dos propiedades obligatorias: `version` (la versión del esquema del índice del servicio) y `resources`  (los puntos de conexión o capacidades del origen del paquete).</span><span class="sxs-lookup"><span data-stu-id="a14b3-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="a14b3-106">el índice de servicio de Nuget. org se encuentra en `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="a14b3-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="a14b3-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="a14b3-107">Versioning</span></span>

<span data-ttu-id="a14b3-108">El `version` valor es una cadena de versión de SemVer 2.0.0 que indica la versión de esquema del índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="a14b3-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="a14b3-109">La API asigna que la cadena de versión tiene un número de versión principal de `3` .</span><span class="sxs-lookup"><span data-stu-id="a14b3-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="a14b3-110">A medida que se realizan cambios no importantes en el esquema de índice de servicio, se aumentará la versión secundaria de la cadena de versión.</span><span class="sxs-lookup"><span data-stu-id="a14b3-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="a14b3-111">Cada recurso del índice de servicio tiene versiones independientes de la versión del esquema de índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="a14b3-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="a14b3-112">La versión de esquema actual es `3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="a14b3-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="a14b3-113">La `3.0.0` versión es funcionalmente equivalente a la `3.0.0-beta.1` versión anterior, pero debe ser preferible a medida que comunica con mayor claridad el esquema definido y estable.</span><span class="sxs-lookup"><span data-stu-id="a14b3-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a14b3-114">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="a14b3-114">HTTP methods</span></span>

<span data-ttu-id="a14b3-115">Se puede tener acceso al índice de servicio mediante métodos HTTP `GET` y `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="a14b3-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="a14b3-116">Recursos</span><span class="sxs-lookup"><span data-stu-id="a14b3-116">Resources</span></span>

<span data-ttu-id="a14b3-117">La `resources` propiedad contiene una matriz de recursos admitidos por este origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="a14b3-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="a14b3-118">Recurso</span><span class="sxs-lookup"><span data-stu-id="a14b3-118">Resource</span></span>

<span data-ttu-id="a14b3-119">Un recurso es un objeto de la `resources` matriz.</span><span class="sxs-lookup"><span data-stu-id="a14b3-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="a14b3-120">Representa una funcionalidad con versión de un origen de paquete.</span><span class="sxs-lookup"><span data-stu-id="a14b3-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="a14b3-121">Un recurso tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="a14b3-121">A resource has the following properties:</span></span>

<span data-ttu-id="a14b3-122">Nombre</span><span class="sxs-lookup"><span data-stu-id="a14b3-122">Name</span></span>          | <span data-ttu-id="a14b3-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="a14b3-123">Type</span></span>   | <span data-ttu-id="a14b3-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a14b3-124">Required</span></span> | <span data-ttu-id="a14b3-125">Notas</span><span class="sxs-lookup"><span data-stu-id="a14b3-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="a14b3-126">string</span><span class="sxs-lookup"><span data-stu-id="a14b3-126">string</span></span> | <span data-ttu-id="a14b3-127">sí</span><span class="sxs-lookup"><span data-stu-id="a14b3-127">yes</span></span>      | <span data-ttu-id="a14b3-128">Dirección URL del recurso.</span><span class="sxs-lookup"><span data-stu-id="a14b3-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="a14b3-129">string</span><span class="sxs-lookup"><span data-stu-id="a14b3-129">string</span></span> | <span data-ttu-id="a14b3-130">sí</span><span class="sxs-lookup"><span data-stu-id="a14b3-130">yes</span></span>      | <span data-ttu-id="a14b3-131">Una constante de cadena que representa el tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="a14b3-131">A string constant representing the resource type</span></span>
<span data-ttu-id="a14b3-132">comment</span><span class="sxs-lookup"><span data-stu-id="a14b3-132">comment</span></span>       | <span data-ttu-id="a14b3-133">string</span><span class="sxs-lookup"><span data-stu-id="a14b3-133">string</span></span> | <span data-ttu-id="a14b3-134">no</span><span class="sxs-lookup"><span data-stu-id="a14b3-134">no</span></span>       | <span data-ttu-id="a14b3-135">Una descripción inteligible del recurso</span><span class="sxs-lookup"><span data-stu-id="a14b3-135">A human readable description of the resource</span></span>

<span data-ttu-id="a14b3-136">`@id`Es una dirección URL que debe ser absoluta y debe tener el esquema http o https.</span><span class="sxs-lookup"><span data-stu-id="a14b3-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="a14b3-137">`@type`Se utiliza para identificar el protocolo específico que se va a utilizar al interactuar con el recurso.</span><span class="sxs-lookup"><span data-stu-id="a14b3-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="a14b3-138">El tipo del recurso es una cadena opaca pero generalmente tiene el formato:</span><span class="sxs-lookup"><span data-stu-id="a14b3-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="a14b3-139">Se espera que los clientes codifiquen de forma rígida los `@type` valores que entienden y los examinan en el índice de servicio del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="a14b3-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="a14b3-140">Los valores exactos que `@type` se usan hoy en día se enumeran en los documentos de referencia de recursos individuales que se enumeran en la [información general](overview.md#resources-and-schema)de la API.</span><span class="sxs-lookup"><span data-stu-id="a14b3-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="a14b3-141">En esta documentación, la documentación sobre los distintos recursos se agrupará básicamente por el `{RESOURCE_NAME}` que se encuentra en el índice del servicio, que es análogo a agrupar por escenario.</span><span class="sxs-lookup"><span data-stu-id="a14b3-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="a14b3-142">No es necesario que cada recurso tenga un único `@id` o `@type` .</span><span class="sxs-lookup"><span data-stu-id="a14b3-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="a14b3-143">Depende de la implementación del cliente determinar qué recurso prefiere sobre otro.</span><span class="sxs-lookup"><span data-stu-id="a14b3-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="a14b3-144">Una posible implementación es que se pueden usar recursos del mismo o compatible `@type` en un modo Round Robin en caso de error de conexión o de servidor.</span><span class="sxs-lookup"><span data-stu-id="a14b3-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a14b3-145">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a14b3-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="a14b3-146">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="a14b3-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
