---
title: Contenido del paquete, NuGet API
description: La dirección base del paquete es una interfaz sencilla para capturar el propio paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547159"
---
# <a name="package-content"></a><span data-ttu-id="7cfbc-103">Contenido del paquete</span><span class="sxs-lookup"><span data-stu-id="7cfbc-103">Package Content</span></span>

<span data-ttu-id="7cfbc-104">Es posible generar una dirección URL para capturar el contenido de un paquete arbitrario (el archivo .nupkg) mediante la API de V3.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="7cfbc-105">El recurso usado para recuperar el contenido del paquete es el `PackageBaseAddress` encontrar el recurso en el [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7cfbc-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="7cfbc-106">Este recurso también permite la detección de todas las versiones de un paquete, aparece o no enumerado.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="7cfbc-107">Este recurso se conoce comúnmente como el "paquete base dirección" o como contenedor"plano".</span><span class="sxs-lookup"><span data-stu-id="7cfbc-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="7cfbc-108">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="7cfbc-108">Versioning</span></span>

<span data-ttu-id="7cfbc-109">La siguiente `@type` se usa el valor:</span><span class="sxs-lookup"><span data-stu-id="7cfbc-109">The following `@type` value is used:</span></span>

<span data-ttu-id="7cfbc-110">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="7cfbc-110">@type value</span></span>              | <span data-ttu-id="7cfbc-111">Notas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="7cfbc-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="7cfbc-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="7cfbc-113">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="7cfbc-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="7cfbc-114">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="7cfbc-114">Base URL</span></span>

<span data-ttu-id="7cfbc-115">La dirección URL base para las siguientes API es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="7cfbc-116">En el siguiente documento, la dirección URL base del marcador de posición `{@id}` se usará.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7cfbc-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="7cfbc-117">HTTP methods</span></span>

<span data-ttu-id="7cfbc-118">Todas las direcciones URL se encuentra en la compatibilidad con recursos de registro de los métodos HTTP `GET` y `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="7cfbc-119">Enumerar versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="7cfbc-119">Enumerate package versions</span></span>

<span data-ttu-id="7cfbc-120">Si el cliente sabe que un identificador de paquete y desea descubrir que las versiones del paquete el paquete de código fuente disponible, el cliente puede construir una dirección URL de predicción para enumerar todas las versiones de paquete.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="7cfbc-121">Esta lista está pensada para ser una "lista de directorios" para la API de contenido de paquete que se mencionan a continuación.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="7cfbc-122">Esta lista contiene ambas versiones del paquete figuran.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="7cfbc-123">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="7cfbc-123">Request parameters</span></span>

<span data-ttu-id="7cfbc-124">nombre</span><span class="sxs-lookup"><span data-stu-id="7cfbc-124">Name</span></span>     | <span data-ttu-id="7cfbc-125">En</span><span class="sxs-lookup"><span data-stu-id="7cfbc-125">In</span></span>     | <span data-ttu-id="7cfbc-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-126">Type</span></span>    | <span data-ttu-id="7cfbc-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7cfbc-127">Required</span></span> | <span data-ttu-id="7cfbc-128">Notas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="7cfbc-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="7cfbc-129">LOWER_ID</span></span> | <span data-ttu-id="7cfbc-130">Resolución</span><span class="sxs-lookup"><span data-stu-id="7cfbc-130">URL</span></span>    | <span data-ttu-id="7cfbc-131">cadena</span><span class="sxs-lookup"><span data-stu-id="7cfbc-131">string</span></span>  | <span data-ttu-id="7cfbc-132">sí</span><span class="sxs-lookup"><span data-stu-id="7cfbc-132">yes</span></span>      | <span data-ttu-id="7cfbc-133">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-133">The package ID, lowercase</span></span>

<span data-ttu-id="7cfbc-134">El `LOWER_ID` valor es el identificador de paquete deseado utilizando las reglas implementadas por en minúsculas. La red [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="7cfbc-135">Respuesta</span><span class="sxs-lookup"><span data-stu-id="7cfbc-135">Response</span></span>

<span data-ttu-id="7cfbc-136">Si el origen del paquete no tiene que no hay ninguna versión del identificador del paquete suministrado, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="7cfbc-137">Si el origen del paquete tiene una o varias versiones, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="7cfbc-138">El cuerpo de respuesta es un objeto JSON con la siguiente propiedad:</span><span class="sxs-lookup"><span data-stu-id="7cfbc-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="7cfbc-139">nombre</span><span class="sxs-lookup"><span data-stu-id="7cfbc-139">Name</span></span>     | <span data-ttu-id="7cfbc-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-140">Type</span></span>             | <span data-ttu-id="7cfbc-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7cfbc-141">Required</span></span> | <span data-ttu-id="7cfbc-142">Notas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="7cfbc-143">versiones</span><span class="sxs-lookup"><span data-stu-id="7cfbc-143">versions</span></span> | <span data-ttu-id="7cfbc-144">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-144">array of strings</span></span> | <span data-ttu-id="7cfbc-145">sí</span><span class="sxs-lookup"><span data-stu-id="7cfbc-145">yes</span></span>      | <span data-ttu-id="7cfbc-146">El paquete Id. disponibles</span><span class="sxs-lookup"><span data-stu-id="7cfbc-146">The package IDs available</span></span>

<span data-ttu-id="7cfbc-147">Las cadenas en el `versions` matriz todos minúscula, [normalizar las cadenas de versión de NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="7cfbc-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="7cfbc-148">Las cadenas de versión no contienen los metadatos de la compilación de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="7cfbc-149">La intención es que las cadenas de versión que se encuentra en esta matriz se pueden usar literalmente para el `LOWER_VERSION` tokens que se encuentra en los siguientes puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7cfbc-150">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="7cfbc-151">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="7cfbc-152">Descargar contenido de paquete (archivo .nupkg)</span><span class="sxs-lookup"><span data-stu-id="7cfbc-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="7cfbc-153">Si el cliente sabe que un identificador de paquete y la versión y desea descargar el contenido del paquete, solo deberá construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="7cfbc-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="7cfbc-154">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="7cfbc-154">Request parameters</span></span>

<span data-ttu-id="7cfbc-155">nombre</span><span class="sxs-lookup"><span data-stu-id="7cfbc-155">Name</span></span>          | <span data-ttu-id="7cfbc-156">En</span><span class="sxs-lookup"><span data-stu-id="7cfbc-156">In</span></span>     | <span data-ttu-id="7cfbc-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-157">Type</span></span>   | <span data-ttu-id="7cfbc-158">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7cfbc-158">Required</span></span> | <span data-ttu-id="7cfbc-159">Notas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7cfbc-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="7cfbc-160">LOWER_ID</span></span>      | <span data-ttu-id="7cfbc-161">Resolución</span><span class="sxs-lookup"><span data-stu-id="7cfbc-161">URL</span></span>    | <span data-ttu-id="7cfbc-162">cadena</span><span class="sxs-lookup"><span data-stu-id="7cfbc-162">string</span></span> | <span data-ttu-id="7cfbc-163">sí</span><span class="sxs-lookup"><span data-stu-id="7cfbc-163">yes</span></span>      | <span data-ttu-id="7cfbc-164">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-164">The package ID, lowercase</span></span>
<span data-ttu-id="7cfbc-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="7cfbc-165">LOWER_VERSION</span></span> | <span data-ttu-id="7cfbc-166">Resolución</span><span class="sxs-lookup"><span data-stu-id="7cfbc-166">URL</span></span>    | <span data-ttu-id="7cfbc-167">cadena</span><span class="sxs-lookup"><span data-stu-id="7cfbc-167">string</span></span> | <span data-ttu-id="7cfbc-168">sí</span><span class="sxs-lookup"><span data-stu-id="7cfbc-168">yes</span></span>      | <span data-ttu-id="7cfbc-169">La versión del paquete, normalizar y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="7cfbc-170">Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. La red [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="7cfbc-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="7cfbc-171">.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-171">method.</span></span>

<span data-ttu-id="7cfbc-172">El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [reglas de normalización](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="7cfbc-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="7cfbc-173">Esto significa que los metadatos de compilación que se permiten la especificación de SemVer 2.0.0 en este caso se deben excluir.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="7cfbc-174">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="7cfbc-174">Response body</span></span>

<span data-ttu-id="7cfbc-175">Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="7cfbc-176">El cuerpo de respuesta será el contenido del paquete.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="7cfbc-177">Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7cfbc-178">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="7cfbc-179">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-179">Sample response</span></span>

<span data-ttu-id="7cfbc-180">El flujo binario que es el archivo .nupkg para Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="7cfbc-181">Descargue el manifiesto del paquete (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="7cfbc-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="7cfbc-182">Si el cliente sabe que un identificador de paquete y la versión y desea descargar el manifiesto del paquete, solo deberá construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="7cfbc-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="7cfbc-183">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="7cfbc-183">Request parameters</span></span>

<span data-ttu-id="7cfbc-184">nombre</span><span class="sxs-lookup"><span data-stu-id="7cfbc-184">Name</span></span>          | <span data-ttu-id="7cfbc-185">En</span><span class="sxs-lookup"><span data-stu-id="7cfbc-185">In</span></span>     | <span data-ttu-id="7cfbc-186">Tipo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-186">Type</span></span>    | <span data-ttu-id="7cfbc-187">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7cfbc-187">Required</span></span> | <span data-ttu-id="7cfbc-188">Notas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="7cfbc-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="7cfbc-189">LOWER_ID</span></span>      | <span data-ttu-id="7cfbc-190">Resolución</span><span class="sxs-lookup"><span data-stu-id="7cfbc-190">URL</span></span>    | <span data-ttu-id="7cfbc-191">cadena</span><span class="sxs-lookup"><span data-stu-id="7cfbc-191">string</span></span>  | <span data-ttu-id="7cfbc-192">sí</span><span class="sxs-lookup"><span data-stu-id="7cfbc-192">yes</span></span>      | <span data-ttu-id="7cfbc-193">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-193">The package ID, lowercase</span></span>
<span data-ttu-id="7cfbc-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="7cfbc-194">LOWER_VERSION</span></span> | <span data-ttu-id="7cfbc-195">Resolución</span><span class="sxs-lookup"><span data-stu-id="7cfbc-195">URL</span></span>    | <span data-ttu-id="7cfbc-196">enteros</span><span class="sxs-lookup"><span data-stu-id="7cfbc-196">integer</span></span> | <span data-ttu-id="7cfbc-197">sí</span><span class="sxs-lookup"><span data-stu-id="7cfbc-197">yes</span></span>      | <span data-ttu-id="7cfbc-198">La versión del paquete, normalizar y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="7cfbc-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="7cfbc-199">Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. La red [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="7cfbc-200">El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [reglas de normalización](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="7cfbc-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="7cfbc-201">Esto significa que los metadatos de compilación que se permiten la especificación de SemVer 2.0.0 en este caso se deben excluir.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="7cfbc-202">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="7cfbc-202">Response body</span></span>

<span data-ttu-id="7cfbc-203">Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="7cfbc-204">El cuerpo de respuesta será el manifiesto del paquete, que es el archivo .nuspec contenidos en los archivos .nupkg correspondiente.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="7cfbc-205">El archivo .nuspec es un documento XML.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="7cfbc-206">Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="7cfbc-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7cfbc-207">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="7cfbc-208">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7cfbc-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
