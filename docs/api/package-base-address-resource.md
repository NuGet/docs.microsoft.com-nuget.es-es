---
title: Contenido del paquete, NuGet API
description: La dirección base del paquete es una interfaz sencilla para capturar el propio paquete.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819182"
---
# <a name="package-content"></a><span data-ttu-id="435b2-103">Contenido del paquete</span><span class="sxs-lookup"><span data-stu-id="435b2-103">Package Content</span></span>

<span data-ttu-id="435b2-104">Es posible generar una dirección URL para recuperar contenido de un paquete arbitrario (el archivo .nupkg) mediante la API V3.</span><span class="sxs-lookup"><span data-stu-id="435b2-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="435b2-105">El recurso que se utiliza para capturar el contenido del paquete es el `PackageBaseAddress` recurso se encuentra en la [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="435b2-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="435b2-106">Este recurso también habilita la detección de todas las versiones de un paquete, que se indica o dados de baja.</span><span class="sxs-lookup"><span data-stu-id="435b2-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="435b2-107">Este recurso se conoce normalmente como la "paquete base dirección" o "contenedor sin formato".</span><span class="sxs-lookup"><span data-stu-id="435b2-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="435b2-108">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="435b2-108">Versioning</span></span>

<span data-ttu-id="435b2-109">El siguiente `@type` valor se utiliza:</span><span class="sxs-lookup"><span data-stu-id="435b2-109">The following `@type` value is used:</span></span>

<span data-ttu-id="435b2-110">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="435b2-110">@type value</span></span>              | <span data-ttu-id="435b2-111">Notas</span><span class="sxs-lookup"><span data-stu-id="435b2-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="435b2-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="435b2-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="435b2-113">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="435b2-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="435b2-114">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="435b2-114">Base URL</span></span>

<span data-ttu-id="435b2-115">La dirección URL base para las API siguientes es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="435b2-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="435b2-116">En el siguiente documento, el marcador de posición de la dirección URL base `{@id}` se usará.</span><span class="sxs-lookup"><span data-stu-id="435b2-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="435b2-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="435b2-117">HTTP methods</span></span>

<span data-ttu-id="435b2-118">Todas las direcciones URL se encuentra en el soporte de registro del recurso los métodos HTTP `GET` y `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="435b2-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="435b2-119">Enumerar las versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="435b2-119">Enumerate package versions</span></span>

<span data-ttu-id="435b2-120">Si el cliente sabe que un identificador de paquete y desea descubrir que versiones del paquete el paquete de origen tiene disponible, el cliente puede construir una dirección URL de predicción para enumerar todas las versiones de paquete.</span><span class="sxs-lookup"><span data-stu-id="435b2-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="435b2-121">Esta lista se ha diseñado para ser una "lista de directorios" para la API de contenido de paquete que se mencionan más abajo.</span><span class="sxs-lookup"><span data-stu-id="435b2-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="435b2-122">Esta lista contiene ambas versiones de la lista y que no figuran en el paquete.</span><span class="sxs-lookup"><span data-stu-id="435b2-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="435b2-123">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="435b2-123">Request parameters</span></span>

<span data-ttu-id="435b2-124">nombre</span><span class="sxs-lookup"><span data-stu-id="435b2-124">Name</span></span>     | <span data-ttu-id="435b2-125">En</span><span class="sxs-lookup"><span data-stu-id="435b2-125">In</span></span>     | <span data-ttu-id="435b2-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="435b2-126">Type</span></span>    | <span data-ttu-id="435b2-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="435b2-127">Required</span></span> | <span data-ttu-id="435b2-128">Notas</span><span class="sxs-lookup"><span data-stu-id="435b2-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="435b2-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="435b2-129">LOWER_ID</span></span> | <span data-ttu-id="435b2-130">Resolución</span><span class="sxs-lookup"><span data-stu-id="435b2-130">URL</span></span>    | <span data-ttu-id="435b2-131">cadena</span><span class="sxs-lookup"><span data-stu-id="435b2-131">string</span></span>  | <span data-ttu-id="435b2-132">sí</span><span class="sxs-lookup"><span data-stu-id="435b2-132">yes</span></span>      | <span data-ttu-id="435b2-133">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="435b2-133">The package ID, lowercase</span></span>

<span data-ttu-id="435b2-134">El `LOWER_ID` valor es el identificador de paquete deseado en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="435b2-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="435b2-135">Respuesta</span><span class="sxs-lookup"><span data-stu-id="435b2-135">Response</span></span>

<span data-ttu-id="435b2-136">Si el origen del paquete no tiene ninguna versión del identificador del paquete suministrado, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="435b2-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="435b2-137">Si el origen del paquete tiene una o varias versiones, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="435b2-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="435b2-138">El cuerpo de respuesta es un objeto JSON con la siguiente propiedad:</span><span class="sxs-lookup"><span data-stu-id="435b2-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="435b2-139">nombre</span><span class="sxs-lookup"><span data-stu-id="435b2-139">Name</span></span>     | <span data-ttu-id="435b2-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="435b2-140">Type</span></span>             | <span data-ttu-id="435b2-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="435b2-141">Required</span></span> | <span data-ttu-id="435b2-142">Notas</span><span class="sxs-lookup"><span data-stu-id="435b2-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="435b2-143">versiones</span><span class="sxs-lookup"><span data-stu-id="435b2-143">versions</span></span> | <span data-ttu-id="435b2-144">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="435b2-144">array of strings</span></span> | <span data-ttu-id="435b2-145">sí</span><span class="sxs-lookup"><span data-stu-id="435b2-145">yes</span></span>      | <span data-ttu-id="435b2-146">El paquete identificadores disponibles</span><span class="sxs-lookup"><span data-stu-id="435b2-146">The package IDs available</span></span>

<span data-ttu-id="435b2-147">Las cadenas en el `versions` matriz todos minúscula, [normalizar las cadenas de versión de NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="435b2-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="435b2-148">Las cadenas de versión no contienen ningún metadato de compilación SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="435b2-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="435b2-149">La intención es que las cadenas de versión que se encuentra en esta matriz pueden utilizarse literalmente para el `LOWER_VERSION` tokens ubicados en los siguientes extremos.</span><span class="sxs-lookup"><span data-stu-id="435b2-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="435b2-150">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="435b2-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="435b2-151">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="435b2-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="435b2-152">Descargar contenido de paquete (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="435b2-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="435b2-153">Si el cliente sabe que un identificador de paquete y la versión y desea descargar el contenido del paquete, solo tiene construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="435b2-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="435b2-154">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="435b2-154">Request parameters</span></span>

<span data-ttu-id="435b2-155">nombre</span><span class="sxs-lookup"><span data-stu-id="435b2-155">Name</span></span>          | <span data-ttu-id="435b2-156">En</span><span class="sxs-lookup"><span data-stu-id="435b2-156">In</span></span>     | <span data-ttu-id="435b2-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="435b2-157">Type</span></span>   | <span data-ttu-id="435b2-158">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="435b2-158">Required</span></span> | <span data-ttu-id="435b2-159">Notas</span><span class="sxs-lookup"><span data-stu-id="435b2-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="435b2-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="435b2-160">LOWER_ID</span></span>      | <span data-ttu-id="435b2-161">Resolución</span><span class="sxs-lookup"><span data-stu-id="435b2-161">URL</span></span>    | <span data-ttu-id="435b2-162">cadena</span><span class="sxs-lookup"><span data-stu-id="435b2-162">string</span></span> | <span data-ttu-id="435b2-163">sí</span><span class="sxs-lookup"><span data-stu-id="435b2-163">yes</span></span>      | <span data-ttu-id="435b2-164">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="435b2-164">The package ID, lowercase</span></span>
<span data-ttu-id="435b2-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="435b2-165">LOWER_VERSION</span></span> | <span data-ttu-id="435b2-166">Resolución</span><span class="sxs-lookup"><span data-stu-id="435b2-166">URL</span></span>    | <span data-ttu-id="435b2-167">cadena</span><span class="sxs-lookup"><span data-stu-id="435b2-167">string</span></span> | <span data-ttu-id="435b2-168">sí</span><span class="sxs-lookup"><span data-stu-id="435b2-168">yes</span></span>      | <span data-ttu-id="435b2-169">La versión del paquete, normalizar y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="435b2-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="435b2-170">Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="435b2-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="435b2-171">El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [las reglas de normalización](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="435b2-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="435b2-172">Esto significa que los metadatos de compilación está permitido por la especificación de SemVer 2.0.0 se deben excluir en este caso.</span><span class="sxs-lookup"><span data-stu-id="435b2-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="435b2-173">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="435b2-173">Response body</span></span>

<span data-ttu-id="435b2-174">Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="435b2-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="435b2-175">El cuerpo de respuesta será el contenido del paquete.</span><span class="sxs-lookup"><span data-stu-id="435b2-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="435b2-176">Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="435b2-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="435b2-177">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="435b2-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="435b2-178">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="435b2-178">Sample response</span></span>

<span data-ttu-id="435b2-179">La secuencia binaria que sea el .nupkg para Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="435b2-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="435b2-180">Descargue el manifiesto del paquete (NuSpec)</span><span class="sxs-lookup"><span data-stu-id="435b2-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="435b2-181">Si el cliente sabe que un identificador de paquete y la versión y desea descargar el manifiesto del paquete, solo tiene construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="435b2-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="435b2-182">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="435b2-182">Request parameters</span></span>

<span data-ttu-id="435b2-183">nombre</span><span class="sxs-lookup"><span data-stu-id="435b2-183">Name</span></span>          | <span data-ttu-id="435b2-184">En</span><span class="sxs-lookup"><span data-stu-id="435b2-184">In</span></span>     | <span data-ttu-id="435b2-185">Tipo</span><span class="sxs-lookup"><span data-stu-id="435b2-185">Type</span></span>    | <span data-ttu-id="435b2-186">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="435b2-186">Required</span></span> | <span data-ttu-id="435b2-187">Notas</span><span class="sxs-lookup"><span data-stu-id="435b2-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="435b2-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="435b2-188">LOWER_ID</span></span>      | <span data-ttu-id="435b2-189">Resolución</span><span class="sxs-lookup"><span data-stu-id="435b2-189">URL</span></span>    | <span data-ttu-id="435b2-190">cadena</span><span class="sxs-lookup"><span data-stu-id="435b2-190">string</span></span>  | <span data-ttu-id="435b2-191">sí</span><span class="sxs-lookup"><span data-stu-id="435b2-191">yes</span></span>      | <span data-ttu-id="435b2-192">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="435b2-192">The package ID, lowercase</span></span>
<span data-ttu-id="435b2-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="435b2-193">LOWER_VERSION</span></span> | <span data-ttu-id="435b2-194">Resolución</span><span class="sxs-lookup"><span data-stu-id="435b2-194">URL</span></span>    | <span data-ttu-id="435b2-195">enteros</span><span class="sxs-lookup"><span data-stu-id="435b2-195">integer</span></span> | <span data-ttu-id="435b2-196">sí</span><span class="sxs-lookup"><span data-stu-id="435b2-196">yes</span></span>      | <span data-ttu-id="435b2-197">La versión del paquete, normalizar y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="435b2-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="435b2-198">Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="435b2-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="435b2-199">El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [las reglas de normalización](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="435b2-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="435b2-200">Esto significa que los metadatos de compilación está permitido por la especificación de SemVer 2.0.0 se deben excluir en este caso.</span><span class="sxs-lookup"><span data-stu-id="435b2-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="435b2-201">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="435b2-201">Response body</span></span>

<span data-ttu-id="435b2-202">Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="435b2-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="435b2-203">El cuerpo de respuesta será el manifiesto del paquete, que es el NuSpec contenidos en el .nupkg correspondiente.</span><span class="sxs-lookup"><span data-stu-id="435b2-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="435b2-204">El NuSpec es un documento XML.</span><span class="sxs-lookup"><span data-stu-id="435b2-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="435b2-205">Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="435b2-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="435b2-206">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="435b2-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="435b2-207">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="435b2-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
