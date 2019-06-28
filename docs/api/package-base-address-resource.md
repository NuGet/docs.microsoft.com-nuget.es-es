---
title: Contenido del paquete, NuGet API
description: La dirección base del paquete es una interfaz sencilla para capturar el propio paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426764"
---
# <a name="package-content"></a><span data-ttu-id="93bd6-103">Contenido del paquete</span><span class="sxs-lookup"><span data-stu-id="93bd6-103">Package Content</span></span>

<span data-ttu-id="93bd6-104">Es posible generar una dirección URL para capturar el contenido de un paquete arbitrario (el archivo .nupkg) mediante la API de V3.</span><span class="sxs-lookup"><span data-stu-id="93bd6-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="93bd6-105">El recurso usado para recuperar el contenido del paquete es el `PackageBaseAddress` encontrar el recurso en el [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="93bd6-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="93bd6-106">Este recurso también permite la detección de todas las versiones de un paquete, aparece o no enumerado.</span><span class="sxs-lookup"><span data-stu-id="93bd6-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="93bd6-107">Este recurso se conoce comúnmente como el "paquete base dirección" o como contenedor"plano".</span><span class="sxs-lookup"><span data-stu-id="93bd6-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="93bd6-108">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="93bd6-108">Versioning</span></span>

<span data-ttu-id="93bd6-109">La siguiente `@type` se usa el valor:</span><span class="sxs-lookup"><span data-stu-id="93bd6-109">The following `@type` value is used:</span></span>

<span data-ttu-id="93bd6-110">Valor de@type</span><span class="sxs-lookup"><span data-stu-id="93bd6-110">@type value</span></span>              | <span data-ttu-id="93bd6-111">Notas</span><span class="sxs-lookup"><span data-stu-id="93bd6-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="93bd6-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="93bd6-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="93bd6-113">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="93bd6-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="93bd6-114">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="93bd6-114">Base URL</span></span>

<span data-ttu-id="93bd6-115">La dirección URL base para las siguientes API es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="93bd6-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="93bd6-116">En el siguiente documento, la dirección URL base del marcador de posición `{@id}` se usará.</span><span class="sxs-lookup"><span data-stu-id="93bd6-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="93bd6-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="93bd6-117">HTTP methods</span></span>

<span data-ttu-id="93bd6-118">Todas las direcciones URL se encuentra en la compatibilidad con recursos de registro de los métodos HTTP `GET` y `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="93bd6-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="93bd6-119">Enumerar versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="93bd6-119">Enumerate package versions</span></span>

<span data-ttu-id="93bd6-120">Si el cliente sabe que un identificador de paquete y desea descubrir que las versiones del paquete el paquete de código fuente disponible, el cliente puede construir una dirección URL de predicción para enumerar todas las versiones de paquete.</span><span class="sxs-lookup"><span data-stu-id="93bd6-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="93bd6-121">Esta lista está pensada para ser una "lista de directorios" para la API de contenido de paquete que se mencionan a continuación.</span><span class="sxs-lookup"><span data-stu-id="93bd6-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="93bd6-122">Esta lista contiene ambas versiones del paquete figuran.</span><span class="sxs-lookup"><span data-stu-id="93bd6-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="93bd6-123">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="93bd6-123">Request parameters</span></span>

<span data-ttu-id="93bd6-124">Name</span><span class="sxs-lookup"><span data-stu-id="93bd6-124">Name</span></span>     | <span data-ttu-id="93bd6-125">En</span><span class="sxs-lookup"><span data-stu-id="93bd6-125">In</span></span>     | <span data-ttu-id="93bd6-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="93bd6-126">Type</span></span>    | <span data-ttu-id="93bd6-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="93bd6-127">Required</span></span> | <span data-ttu-id="93bd6-128">Notas</span><span class="sxs-lookup"><span data-stu-id="93bd6-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="93bd6-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="93bd6-129">LOWER_ID</span></span> | <span data-ttu-id="93bd6-130">Resolución</span><span class="sxs-lookup"><span data-stu-id="93bd6-130">URL</span></span>    | <span data-ttu-id="93bd6-131">cadena</span><span class="sxs-lookup"><span data-stu-id="93bd6-131">string</span></span>  | <span data-ttu-id="93bd6-132">sí</span><span class="sxs-lookup"><span data-stu-id="93bd6-132">yes</span></span>      | <span data-ttu-id="93bd6-133">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="93bd6-133">The package ID, lowercase</span></span>

<span data-ttu-id="93bd6-134">El `LOWER_ID` valor es el identificador de paquete deseado utilizando las reglas implementadas por en minúsculas. La red [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="93bd6-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="93bd6-135">Respuesta</span><span class="sxs-lookup"><span data-stu-id="93bd6-135">Response</span></span>

<span data-ttu-id="93bd6-136">Si el origen del paquete no tiene que no hay ninguna versión del identificador del paquete suministrado, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="93bd6-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="93bd6-137">Si el origen del paquete tiene una o varias versiones, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="93bd6-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="93bd6-138">El cuerpo de respuesta es un objeto JSON con la siguiente propiedad:</span><span class="sxs-lookup"><span data-stu-id="93bd6-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="93bd6-139">Name</span><span class="sxs-lookup"><span data-stu-id="93bd6-139">Name</span></span>     | <span data-ttu-id="93bd6-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="93bd6-140">Type</span></span>             | <span data-ttu-id="93bd6-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="93bd6-141">Required</span></span> | <span data-ttu-id="93bd6-142">Notas</span><span class="sxs-lookup"><span data-stu-id="93bd6-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="93bd6-143">versiones</span><span class="sxs-lookup"><span data-stu-id="93bd6-143">versions</span></span> | <span data-ttu-id="93bd6-144">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="93bd6-144">array of strings</span></span> | <span data-ttu-id="93bd6-145">sí</span><span class="sxs-lookup"><span data-stu-id="93bd6-145">yes</span></span>      | <span data-ttu-id="93bd6-146">El paquete Id. disponibles</span><span class="sxs-lookup"><span data-stu-id="93bd6-146">The package IDs available</span></span>

<span data-ttu-id="93bd6-147">Las cadenas en el `versions` matriz todos minúscula, [normalizar las cadenas de versión de NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="93bd6-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="93bd6-148">Las cadenas de versión no contienen los metadatos de la compilación de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="93bd6-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="93bd6-149">La intención es que las cadenas de versión que se encuentra en esta matriz se pueden usar literalmente para el `LOWER_VERSION` tokens que se encuentra en los siguientes puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="93bd6-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="93bd6-150">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="93bd6-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="93bd6-151">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="93bd6-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="93bd6-152">Descargar contenido de paquete (archivo .nupkg)</span><span class="sxs-lookup"><span data-stu-id="93bd6-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="93bd6-153">Si el cliente sabe que un identificador de paquete y la versión y desea descargar el contenido del paquete, solo deberá construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="93bd6-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="93bd6-154">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="93bd6-154">Request parameters</span></span>

<span data-ttu-id="93bd6-155">Name</span><span class="sxs-lookup"><span data-stu-id="93bd6-155">Name</span></span>          | <span data-ttu-id="93bd6-156">En</span><span class="sxs-lookup"><span data-stu-id="93bd6-156">In</span></span>     | <span data-ttu-id="93bd6-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="93bd6-157">Type</span></span>   | <span data-ttu-id="93bd6-158">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="93bd6-158">Required</span></span> | <span data-ttu-id="93bd6-159">Notas</span><span class="sxs-lookup"><span data-stu-id="93bd6-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="93bd6-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="93bd6-160">LOWER_ID</span></span>      | <span data-ttu-id="93bd6-161">Resolución</span><span class="sxs-lookup"><span data-stu-id="93bd6-161">URL</span></span>    | <span data-ttu-id="93bd6-162">cadena</span><span class="sxs-lookup"><span data-stu-id="93bd6-162">string</span></span> | <span data-ttu-id="93bd6-163">sí</span><span class="sxs-lookup"><span data-stu-id="93bd6-163">yes</span></span>      | <span data-ttu-id="93bd6-164">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="93bd6-164">The package ID, lowercase</span></span>
<span data-ttu-id="93bd6-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="93bd6-165">LOWER_VERSION</span></span> | <span data-ttu-id="93bd6-166">Resolución</span><span class="sxs-lookup"><span data-stu-id="93bd6-166">URL</span></span>    | <span data-ttu-id="93bd6-167">cadena</span><span class="sxs-lookup"><span data-stu-id="93bd6-167">string</span></span> | <span data-ttu-id="93bd6-168">sí</span><span class="sxs-lookup"><span data-stu-id="93bd6-168">yes</span></span>      | <span data-ttu-id="93bd6-169">La versión del paquete, normalizar y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="93bd6-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="93bd6-170">Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. La red [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="93bd6-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="93bd6-171">.</span><span class="sxs-lookup"><span data-stu-id="93bd6-171">method.</span></span>

<span data-ttu-id="93bd6-172">El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [reglas de normalización](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="93bd6-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="93bd6-173">Esto significa que los metadatos de compilación que se permiten la especificación de SemVer 2.0.0 en este caso se deben excluir.</span><span class="sxs-lookup"><span data-stu-id="93bd6-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="93bd6-174">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="93bd6-174">Response body</span></span>

<span data-ttu-id="93bd6-175">Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="93bd6-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="93bd6-176">El cuerpo de respuesta será el contenido del paquete.</span><span class="sxs-lookup"><span data-stu-id="93bd6-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="93bd6-177">Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="93bd6-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="93bd6-178">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="93bd6-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="93bd6-179">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="93bd6-179">Sample response</span></span>

<span data-ttu-id="93bd6-180">El flujo binario que es el archivo .nupkg para Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="93bd6-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="93bd6-181">Descargue el manifiesto del paquete (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="93bd6-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="93bd6-182">Si el cliente sabe que un identificador de paquete y la versión y desea descargar el manifiesto del paquete, solo deberá construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="93bd6-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="93bd6-183">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="93bd6-183">Request parameters</span></span>

<span data-ttu-id="93bd6-184">Name</span><span class="sxs-lookup"><span data-stu-id="93bd6-184">Name</span></span>          | <span data-ttu-id="93bd6-185">En</span><span class="sxs-lookup"><span data-stu-id="93bd6-185">In</span></span>     | <span data-ttu-id="93bd6-186">Tipo</span><span class="sxs-lookup"><span data-stu-id="93bd6-186">Type</span></span>   | <span data-ttu-id="93bd6-187">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="93bd6-187">Required</span></span> | <span data-ttu-id="93bd6-188">Notas</span><span class="sxs-lookup"><span data-stu-id="93bd6-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="93bd6-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="93bd6-189">LOWER_ID</span></span>      | <span data-ttu-id="93bd6-190">Resolución</span><span class="sxs-lookup"><span data-stu-id="93bd6-190">URL</span></span>    | <span data-ttu-id="93bd6-191">cadena</span><span class="sxs-lookup"><span data-stu-id="93bd6-191">string</span></span> | <span data-ttu-id="93bd6-192">sí</span><span class="sxs-lookup"><span data-stu-id="93bd6-192">yes</span></span>      | <span data-ttu-id="93bd6-193">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="93bd6-193">The package ID, lowercase</span></span>
<span data-ttu-id="93bd6-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="93bd6-194">LOWER_VERSION</span></span> | <span data-ttu-id="93bd6-195">Resolución</span><span class="sxs-lookup"><span data-stu-id="93bd6-195">URL</span></span>    | <span data-ttu-id="93bd6-196">cadena</span><span class="sxs-lookup"><span data-stu-id="93bd6-196">string</span></span> | <span data-ttu-id="93bd6-197">sí</span><span class="sxs-lookup"><span data-stu-id="93bd6-197">yes</span></span>      | <span data-ttu-id="93bd6-198">La versión del paquete, normalizar y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="93bd6-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="93bd6-199">Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. La red [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="93bd6-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="93bd6-200">El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [reglas de normalización](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="93bd6-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="93bd6-201">Esto significa que los metadatos de compilación que se permiten la especificación de SemVer 2.0.0 en este caso se deben excluir.</span><span class="sxs-lookup"><span data-stu-id="93bd6-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="93bd6-202">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="93bd6-202">Response body</span></span>

<span data-ttu-id="93bd6-203">Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="93bd6-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="93bd6-204">El cuerpo de respuesta será el manifiesto del paquete, que es el archivo .nuspec contenidos en los archivos .nupkg correspondiente.</span><span class="sxs-lookup"><span data-stu-id="93bd6-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="93bd6-205">El archivo .nuspec es un documento XML.</span><span class="sxs-lookup"><span data-stu-id="93bd6-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="93bd6-206">Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="93bd6-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="93bd6-207">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="93bd6-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="93bd6-208">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="93bd6-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
