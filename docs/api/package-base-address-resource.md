---
title: Contenido del paquete, API de NuGet
description: La dirección base del paquete es una interfaz sencilla para capturar el propio paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488218"
---
# <a name="package-content"></a><span data-ttu-id="0923b-103">Contenido del paquete</span><span class="sxs-lookup"><span data-stu-id="0923b-103">Package Content</span></span>

<span data-ttu-id="0923b-104">Es posible generar una dirección URL para capturar el contenido de un paquete arbitrario (el archivo. nupkg) mediante la API V3.</span><span class="sxs-lookup"><span data-stu-id="0923b-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="0923b-105">El recurso que se usa para obtener el contenido del `PackageBaseAddress` paquete es el recurso que se encuentra en el [Índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="0923b-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="0923b-106">Este recurso también habilita la detección de todas las versiones de un paquete, enumeradas o no enumeradas.</span><span class="sxs-lookup"><span data-stu-id="0923b-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="0923b-107">Este recurso se conoce comúnmente como "dirección base del paquete" o como "contenedor plano".</span><span class="sxs-lookup"><span data-stu-id="0923b-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="0923b-108">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="0923b-108">Versioning</span></span>

<span data-ttu-id="0923b-109">Se usa `@type` el siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="0923b-109">The following `@type` value is used:</span></span>

<span data-ttu-id="0923b-110">Valor de@type</span><span class="sxs-lookup"><span data-stu-id="0923b-110">@type value</span></span>              | <span data-ttu-id="0923b-111">Notas</span><span class="sxs-lookup"><span data-stu-id="0923b-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="0923b-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="0923b-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="0923b-113">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="0923b-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="0923b-114">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="0923b-114">Base URL</span></span>

<span data-ttu-id="0923b-115">La dirección URL base para las siguientes API es el valor de `@id` la propiedad asociada al valor de `@type` recurso mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0923b-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="0923b-116">En el siguiente documento, se usará la dirección `{@id}` URL base del marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="0923b-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0923b-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="0923b-117">HTTP methods</span></span>

<span data-ttu-id="0923b-118">Todas las direcciones URL encontradas en el recurso de registro admiten `HEAD`los métodos `GET` http y.</span><span class="sxs-lookup"><span data-stu-id="0923b-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="0923b-119">Enumerar versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="0923b-119">Enumerate package versions</span></span>

<span data-ttu-id="0923b-120">Si el cliente conoce un identificador de paquete y desea detectar qué versiones de paquete tiene el origen del paquete, el cliente puede crear una dirección URL de predicción para enumerar todas las versiones del paquete.</span><span class="sxs-lookup"><span data-stu-id="0923b-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="0923b-121">Esta lista está pensada como una "lista de directorios" para la API de contenido de paquete que se menciona a continuación.</span><span class="sxs-lookup"><span data-stu-id="0923b-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="0923b-122">Esta lista contiene las versiones de paquetes que se muestran y que no figuran en la lista.</span><span class="sxs-lookup"><span data-stu-id="0923b-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="0923b-123">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="0923b-123">Request parameters</span></span>

<span data-ttu-id="0923b-124">NOMBRE</span><span class="sxs-lookup"><span data-stu-id="0923b-124">Name</span></span>     | <span data-ttu-id="0923b-125">En</span><span class="sxs-lookup"><span data-stu-id="0923b-125">In</span></span>     | <span data-ttu-id="0923b-126">Type</span><span class="sxs-lookup"><span data-stu-id="0923b-126">Type</span></span>    | <span data-ttu-id="0923b-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0923b-127">Required</span></span> | <span data-ttu-id="0923b-128">Notas</span><span class="sxs-lookup"><span data-stu-id="0923b-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="0923b-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="0923b-129">LOWER_ID</span></span> | <span data-ttu-id="0923b-130">URL</span><span class="sxs-lookup"><span data-stu-id="0923b-130">URL</span></span>    | <span data-ttu-id="0923b-131">string</span><span class="sxs-lookup"><span data-stu-id="0923b-131">string</span></span>  | <span data-ttu-id="0923b-132">sí</span><span class="sxs-lookup"><span data-stu-id="0923b-132">yes</span></span>      | <span data-ttu-id="0923b-133">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="0923b-133">The package ID, lowercase</span></span>

<span data-ttu-id="0923b-134">El `LOWER_ID` valor es el identificador de paquete deseado en minúsculas mediante las reglas implementadas por. Método de [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) la red.</span><span class="sxs-lookup"><span data-stu-id="0923b-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="0923b-135">Respuesta</span><span class="sxs-lookup"><span data-stu-id="0923b-135">Response</span></span>

<span data-ttu-id="0923b-136">Si el origen del paquete no tiene ninguna versión del identificador de paquete proporcionado, se devuelve un código de estado 404.</span><span class="sxs-lookup"><span data-stu-id="0923b-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="0923b-137">Si el origen del paquete tiene una o más versiones, se devuelve un código de estado 200.</span><span class="sxs-lookup"><span data-stu-id="0923b-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="0923b-138">El cuerpo de la respuesta es un objeto JSON con la siguiente propiedad:</span><span class="sxs-lookup"><span data-stu-id="0923b-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="0923b-139">NOMBRE</span><span class="sxs-lookup"><span data-stu-id="0923b-139">Name</span></span>     | <span data-ttu-id="0923b-140">Type</span><span class="sxs-lookup"><span data-stu-id="0923b-140">Type</span></span>             | <span data-ttu-id="0923b-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0923b-141">Required</span></span> | <span data-ttu-id="0923b-142">Notas</span><span class="sxs-lookup"><span data-stu-id="0923b-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="0923b-143">versiones</span><span class="sxs-lookup"><span data-stu-id="0923b-143">versions</span></span> | <span data-ttu-id="0923b-144">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="0923b-144">array of strings</span></span> | <span data-ttu-id="0923b-145">sí</span><span class="sxs-lookup"><span data-stu-id="0923b-145">yes</span></span>      | <span data-ttu-id="0923b-146">Los identificadores de paquete disponibles</span><span class="sxs-lookup"><span data-stu-id="0923b-146">The package IDs available</span></span>

<span data-ttu-id="0923b-147">Las cadenas de la `versions` matriz están todas en minúsculas, con las [cadenas de versión de NuGet normalizadas](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="0923b-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="0923b-148">Las cadenas de versión no contienen metadatos de compilación de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="0923b-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="0923b-149">La intención es que las cadenas de versión encontradas en esta matriz se puedan usar literalmente para `LOWER_VERSION` los tokens que se encuentran en los puntos de conexión siguientes.</span><span class="sxs-lookup"><span data-stu-id="0923b-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0923b-150">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0923b-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="0923b-151">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0923b-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="0923b-152">Descargar contenido de paquete (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="0923b-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="0923b-153">Si el cliente conoce un identificador y una versión del paquete y desea descargar el contenido del paquete, solo necesita construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="0923b-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="0923b-154">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="0923b-154">Request parameters</span></span>

<span data-ttu-id="0923b-155">NOMBRE</span><span class="sxs-lookup"><span data-stu-id="0923b-155">Name</span></span>          | <span data-ttu-id="0923b-156">En</span><span class="sxs-lookup"><span data-stu-id="0923b-156">In</span></span>     | <span data-ttu-id="0923b-157">Type</span><span class="sxs-lookup"><span data-stu-id="0923b-157">Type</span></span>   | <span data-ttu-id="0923b-158">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0923b-158">Required</span></span> | <span data-ttu-id="0923b-159">Notas</span><span class="sxs-lookup"><span data-stu-id="0923b-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="0923b-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="0923b-160">LOWER_ID</span></span>      | <span data-ttu-id="0923b-161">URL</span><span class="sxs-lookup"><span data-stu-id="0923b-161">URL</span></span>    | <span data-ttu-id="0923b-162">string</span><span class="sxs-lookup"><span data-stu-id="0923b-162">string</span></span> | <span data-ttu-id="0923b-163">sí</span><span class="sxs-lookup"><span data-stu-id="0923b-163">yes</span></span>      | <span data-ttu-id="0923b-164">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="0923b-164">The package ID, lowercase</span></span>
<span data-ttu-id="0923b-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="0923b-165">LOWER_VERSION</span></span> | <span data-ttu-id="0923b-166">URL</span><span class="sxs-lookup"><span data-stu-id="0923b-166">URL</span></span>    | <span data-ttu-id="0923b-167">string</span><span class="sxs-lookup"><span data-stu-id="0923b-167">string</span></span> | <span data-ttu-id="0923b-168">sí</span><span class="sxs-lookup"><span data-stu-id="0923b-168">yes</span></span>      | <span data-ttu-id="0923b-169">Versión del paquete, normalizado y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="0923b-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="0923b-170">`LOWER_ID` Y`LOWER_VERSION` están en minúsculas mediante las reglas implementadas por. De la red[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="0923b-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="0923b-171">.</span><span class="sxs-lookup"><span data-stu-id="0923b-171">method.</span></span>

<span data-ttu-id="0923b-172">Es la versión del paquete deseada normalizada con [las reglas](../concepts/package-versioning.md#normalized-version-numbers)de normalización de la versión de NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="0923b-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="0923b-173">Esto significa que los metadatos de compilación permitidos por la especificación SemVer 2.0.0 deben excluirse en este caso.</span><span class="sxs-lookup"><span data-stu-id="0923b-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="0923b-174">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="0923b-174">Response body</span></span>

<span data-ttu-id="0923b-175">Si el paquete existe en el origen del paquete, se devuelve un código de estado 200.</span><span class="sxs-lookup"><span data-stu-id="0923b-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="0923b-176">El cuerpo de la respuesta será el contenido del paquete.</span><span class="sxs-lookup"><span data-stu-id="0923b-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="0923b-177">Si el paquete no existe en el origen del paquete, se devuelve un código de estado 404.</span><span class="sxs-lookup"><span data-stu-id="0923b-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0923b-178">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0923b-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="0923b-179">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0923b-179">Sample response</span></span>

<span data-ttu-id="0923b-180">El flujo binario que es el archivo. nupkg para Newtonsoft. JSON 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="0923b-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="0923b-181">Descargar el manifiesto del paquete (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="0923b-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="0923b-182">Si el cliente conoce un identificador y una versión del paquete y desea descargar el manifiesto del paquete, solo necesita construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="0923b-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="0923b-183">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="0923b-183">Request parameters</span></span>

<span data-ttu-id="0923b-184">NOMBRE</span><span class="sxs-lookup"><span data-stu-id="0923b-184">Name</span></span>          | <span data-ttu-id="0923b-185">En</span><span class="sxs-lookup"><span data-stu-id="0923b-185">In</span></span>     | <span data-ttu-id="0923b-186">Type</span><span class="sxs-lookup"><span data-stu-id="0923b-186">Type</span></span>   | <span data-ttu-id="0923b-187">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0923b-187">Required</span></span> | <span data-ttu-id="0923b-188">Notas</span><span class="sxs-lookup"><span data-stu-id="0923b-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="0923b-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="0923b-189">LOWER_ID</span></span>      | <span data-ttu-id="0923b-190">URL</span><span class="sxs-lookup"><span data-stu-id="0923b-190">URL</span></span>    | <span data-ttu-id="0923b-191">string</span><span class="sxs-lookup"><span data-stu-id="0923b-191">string</span></span> | <span data-ttu-id="0923b-192">sí</span><span class="sxs-lookup"><span data-stu-id="0923b-192">yes</span></span>      | <span data-ttu-id="0923b-193">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="0923b-193">The package ID, lowercase</span></span>
<span data-ttu-id="0923b-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="0923b-194">LOWER_VERSION</span></span> | <span data-ttu-id="0923b-195">URL</span><span class="sxs-lookup"><span data-stu-id="0923b-195">URL</span></span>    | <span data-ttu-id="0923b-196">string</span><span class="sxs-lookup"><span data-stu-id="0923b-196">string</span></span> | <span data-ttu-id="0923b-197">sí</span><span class="sxs-lookup"><span data-stu-id="0923b-197">yes</span></span>      | <span data-ttu-id="0923b-198">Versión del paquete, normalizado y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="0923b-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="0923b-199">`LOWER_ID` Y`LOWER_VERSION` están en minúsculas mediante las reglas implementadas por. Método de [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) la red.</span><span class="sxs-lookup"><span data-stu-id="0923b-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="0923b-200">Es la versión del paquete deseada normalizada con [las reglas](../concepts/package-versioning.md#normalized-version-numbers)de normalización de la versión de NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="0923b-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="0923b-201">Esto significa que los metadatos de compilación permitidos por la especificación SemVer 2.0.0 deben excluirse en este caso.</span><span class="sxs-lookup"><span data-stu-id="0923b-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="0923b-202">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="0923b-202">Response body</span></span>

<span data-ttu-id="0923b-203">Si el paquete existe en el origen del paquete, se devuelve un código de estado 200.</span><span class="sxs-lookup"><span data-stu-id="0923b-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="0923b-204">El cuerpo de la respuesta será el manifiesto del paquete, que es el archivo. nuspec incluido en el archivo. nupkg correspondiente.</span><span class="sxs-lookup"><span data-stu-id="0923b-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="0923b-205">El archivo. nuspec es un documento XML.</span><span class="sxs-lookup"><span data-stu-id="0923b-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="0923b-206">Si el paquete no existe en el origen del paquete, se devuelve un código de estado 404.</span><span class="sxs-lookup"><span data-stu-id="0923b-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0923b-207">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0923b-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="0923b-208">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0923b-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
