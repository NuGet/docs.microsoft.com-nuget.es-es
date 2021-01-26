---
title: Contenido del paquete, API de NuGet
description: La dirección base del paquete es una interfaz sencilla para capturar el propio paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773930"
---
# <a name="package-content"></a><span data-ttu-id="d7e6f-103">Contenido de un paquete</span><span class="sxs-lookup"><span data-stu-id="d7e6f-103">Package Content</span></span>

<span data-ttu-id="d7e6f-104">Es posible generar una dirección URL para capturar el contenido de un paquete arbitrario (el archivo. nupkg) mediante la API V3.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="d7e6f-105">El recurso que se usa para obtener el contenido del paquete es el `PackageBaseAddress` recurso que se encuentra en el [Índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d7e6f-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="d7e6f-106">Este recurso también habilita la detección de todas las versiones de un paquete, enumeradas o no enumeradas.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="d7e6f-107">Este recurso se conoce comúnmente como "dirección base del paquete" o como "contenedor plano".</span><span class="sxs-lookup"><span data-stu-id="d7e6f-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="d7e6f-108">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="d7e6f-108">Versioning</span></span>

<span data-ttu-id="d7e6f-109">`@type`Se usa el siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="d7e6f-109">The following `@type` value is used:</span></span>

<span data-ttu-id="d7e6f-110">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="d7e6f-110">@type value</span></span>              | <span data-ttu-id="d7e6f-111">Notas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="d7e6f-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="d7e6f-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="d7e6f-113">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="d7e6f-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d7e6f-114">URL base</span><span class="sxs-lookup"><span data-stu-id="d7e6f-114">Base URL</span></span>

<span data-ttu-id="d7e6f-115">La dirección URL base para las siguientes API es el valor de la `@id` propiedad asociada al valor de recurso mencionado anteriormente `@type` .</span><span class="sxs-lookup"><span data-stu-id="d7e6f-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="d7e6f-116">En el siguiente documento, se usará la dirección URL base del marcador de posición `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="d7e6f-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d7e6f-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="d7e6f-117">HTTP methods</span></span>

<span data-ttu-id="d7e6f-118">Todas las direcciones URL encontradas en el recurso de registro admiten los métodos HTTP `GET` y `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="d7e6f-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="d7e6f-119">Enumerar versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="d7e6f-119">Enumerate package versions</span></span>

<span data-ttu-id="d7e6f-120">Si el cliente conoce un identificador de paquete y desea detectar qué versiones de paquete tiene el origen del paquete, el cliente puede crear una dirección URL de predicción para enumerar todas las versiones del paquete.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="d7e6f-121">Esta lista está pensada como una "lista de directorios" para la API de contenido de paquete que se menciona a continuación.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="d7e6f-122">Esta lista contiene las versiones de paquetes que se muestran y que no figuran en la lista.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-122">This list contains both listed and unlisted package versions.</span></span>

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a><span data-ttu-id="d7e6f-123">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="d7e6f-123">Request parameters</span></span>

<span data-ttu-id="d7e6f-124">Nombre</span><span class="sxs-lookup"><span data-stu-id="d7e6f-124">Name</span></span>     | <span data-ttu-id="d7e6f-125">En</span><span class="sxs-lookup"><span data-stu-id="d7e6f-125">In</span></span>     | <span data-ttu-id="d7e6f-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="d7e6f-126">Type</span></span>    | <span data-ttu-id="d7e6f-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d7e6f-127">Required</span></span> | <span data-ttu-id="d7e6f-128">Notas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="d7e6f-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d7e6f-129">LOWER_ID</span></span> | <span data-ttu-id="d7e6f-130">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="d7e6f-130">URL</span></span>    | <span data-ttu-id="d7e6f-131">string</span><span class="sxs-lookup"><span data-stu-id="d7e6f-131">string</span></span>  | <span data-ttu-id="d7e6f-132">sí</span><span class="sxs-lookup"><span data-stu-id="d7e6f-132">yes</span></span>      | <span data-ttu-id="d7e6f-133">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-133">The package ID, lowercased</span></span>

<span data-ttu-id="d7e6f-134">El `LOWER_ID` valor es el identificador de paquete deseado en minúsculas mediante las reglas implementadas por. Método de la red [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .</span><span class="sxs-lookup"><span data-stu-id="d7e6f-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

### <a name="response"></a><span data-ttu-id="d7e6f-135">Response</span><span class="sxs-lookup"><span data-stu-id="d7e6f-135">Response</span></span>

<span data-ttu-id="d7e6f-136">Si el origen del paquete no tiene ninguna versión del identificador de paquete proporcionado, se devuelve un código de estado 404.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="d7e6f-137">Si el origen del paquete tiene una o más versiones, se devuelve un código de estado 200.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="d7e6f-138">El cuerpo de la respuesta es un objeto JSON con la siguiente propiedad:</span><span class="sxs-lookup"><span data-stu-id="d7e6f-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="d7e6f-139">Nombre</span><span class="sxs-lookup"><span data-stu-id="d7e6f-139">Name</span></span>     | <span data-ttu-id="d7e6f-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="d7e6f-140">Type</span></span>             | <span data-ttu-id="d7e6f-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d7e6f-141">Required</span></span> | <span data-ttu-id="d7e6f-142">Notas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="d7e6f-143">versions</span><span class="sxs-lookup"><span data-stu-id="d7e6f-143">versions</span></span> | <span data-ttu-id="d7e6f-144">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-144">array of strings</span></span> | <span data-ttu-id="d7e6f-145">sí</span><span class="sxs-lookup"><span data-stu-id="d7e6f-145">yes</span></span>      | <span data-ttu-id="d7e6f-146">Las versiones disponibles</span><span class="sxs-lookup"><span data-stu-id="d7e6f-146">The versions available</span></span>

<span data-ttu-id="d7e6f-147">Las cadenas de la `versions` matriz están todas en minúsculas, con las [cadenas de versión de NuGet normalizadas](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="d7e6f-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d7e6f-148">Las cadenas de versión no contienen metadatos de compilación de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="d7e6f-149">La intención es que las cadenas de versión encontradas en esta matriz se puedan usar literalmente para los `LOWER_VERSION` tokens que se encuentran en los puntos de conexión siguientes.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d7e6f-150">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d7e6f-150">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a><span data-ttu-id="d7e6f-151">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="d7e6f-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="d7e6f-152">Descargar contenido de paquete (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="d7e6f-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="d7e6f-153">Si el cliente conoce un identificador y una versión del paquete y desea descargar el contenido del paquete, solo necesita construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7e6f-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a><span data-ttu-id="d7e6f-154">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="d7e6f-154">Request parameters</span></span>

<span data-ttu-id="d7e6f-155">Nombre</span><span class="sxs-lookup"><span data-stu-id="d7e6f-155">Name</span></span>          | <span data-ttu-id="d7e6f-156">En</span><span class="sxs-lookup"><span data-stu-id="d7e6f-156">In</span></span>     | <span data-ttu-id="d7e6f-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="d7e6f-157">Type</span></span>   | <span data-ttu-id="d7e6f-158">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d7e6f-158">Required</span></span> | <span data-ttu-id="d7e6f-159">Notas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d7e6f-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d7e6f-160">LOWER_ID</span></span>      | <span data-ttu-id="d7e6f-161">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="d7e6f-161">URL</span></span>    | <span data-ttu-id="d7e6f-162">string</span><span class="sxs-lookup"><span data-stu-id="d7e6f-162">string</span></span> | <span data-ttu-id="d7e6f-163">sí</span><span class="sxs-lookup"><span data-stu-id="d7e6f-163">yes</span></span>      | <span data-ttu-id="d7e6f-164">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-164">The package ID, lowercase</span></span>
<span data-ttu-id="d7e6f-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="d7e6f-165">LOWER_VERSION</span></span> | <span data-ttu-id="d7e6f-166">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="d7e6f-166">URL</span></span>    | <span data-ttu-id="d7e6f-167">string</span><span class="sxs-lookup"><span data-stu-id="d7e6f-167">string</span></span> | <span data-ttu-id="d7e6f-168">sí</span><span class="sxs-lookup"><span data-stu-id="d7e6f-168">yes</span></span>      | <span data-ttu-id="d7e6f-169">Versión del paquete, normalizado y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="d7e6f-170">`LOWER_ID`Y `LOWER_VERSION` están en minúsculas mediante las reglas implementadas por. De la red[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="d7e6f-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span></span>
<span data-ttu-id="d7e6f-171">.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-171">method.</span></span>

<span data-ttu-id="d7e6f-172">`LOWER_VERSION`Es la versión del paquete deseada normalizada con [las reglas de normalización](../concepts/package-versioning.md#normalized-version-numbers)de la versión de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d7e6f-173">Esto significa que los metadatos de compilación permitidos por la especificación SemVer 2.0.0 deben excluirse en este caso.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="d7e6f-174">Response body</span><span class="sxs-lookup"><span data-stu-id="d7e6f-174">Response body</span></span>

<span data-ttu-id="d7e6f-175">Si el paquete existe en el origen del paquete, se devuelve un código de estado 200.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="d7e6f-176">El cuerpo de la respuesta será el contenido del paquete.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="d7e6f-177">Si el paquete no existe en el origen del paquete, se devuelve un código de estado 404.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d7e6f-178">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d7e6f-178">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a><span data-ttu-id="d7e6f-179">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="d7e6f-179">Sample response</span></span>

<span data-ttu-id="d7e6f-180">Secuencia binaria que es. nupkg para Newtonsoft.Jsen 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="d7e6f-181">Descargar el manifiesto del paquete (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="d7e6f-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="d7e6f-182">Si el cliente conoce un identificador y una versión del paquete y desea descargar el manifiesto del paquete, solo necesita construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7e6f-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a><span data-ttu-id="d7e6f-183">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="d7e6f-183">Request parameters</span></span>

<span data-ttu-id="d7e6f-184">Nombre</span><span class="sxs-lookup"><span data-stu-id="d7e6f-184">Name</span></span>          | <span data-ttu-id="d7e6f-185">En</span><span class="sxs-lookup"><span data-stu-id="d7e6f-185">In</span></span>     | <span data-ttu-id="d7e6f-186">Tipo</span><span class="sxs-lookup"><span data-stu-id="d7e6f-186">Type</span></span>   | <span data-ttu-id="d7e6f-187">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d7e6f-187">Required</span></span> | <span data-ttu-id="d7e6f-188">Notas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d7e6f-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d7e6f-189">LOWER_ID</span></span>      | <span data-ttu-id="d7e6f-190">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="d7e6f-190">URL</span></span>    | <span data-ttu-id="d7e6f-191">string</span><span class="sxs-lookup"><span data-stu-id="d7e6f-191">string</span></span> | <span data-ttu-id="d7e6f-192">sí</span><span class="sxs-lookup"><span data-stu-id="d7e6f-192">yes</span></span>      | <span data-ttu-id="d7e6f-193">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-193">The package ID, lowercase</span></span>
<span data-ttu-id="d7e6f-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="d7e6f-194">LOWER_VERSION</span></span> | <span data-ttu-id="d7e6f-195">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="d7e6f-195">URL</span></span>    | <span data-ttu-id="d7e6f-196">string</span><span class="sxs-lookup"><span data-stu-id="d7e6f-196">string</span></span> | <span data-ttu-id="d7e6f-197">sí</span><span class="sxs-lookup"><span data-stu-id="d7e6f-197">yes</span></span>      | <span data-ttu-id="d7e6f-198">Versión del paquete, normalizado y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="d7e6f-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="d7e6f-199">`LOWER_ID`Y `LOWER_VERSION` están en minúsculas mediante las reglas implementadas por. Método de la red [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .</span><span class="sxs-lookup"><span data-stu-id="d7e6f-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

<span data-ttu-id="d7e6f-200">`LOWER_VERSION`Es la versión del paquete deseada normalizada con [las reglas de normalización](../concepts/package-versioning.md#normalized-version-numbers)de la versión de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d7e6f-201">Esto significa que los metadatos de compilación permitidos por la especificación SemVer 2.0.0 deben excluirse en este caso.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="d7e6f-202">Response body</span><span class="sxs-lookup"><span data-stu-id="d7e6f-202">Response body</span></span>

<span data-ttu-id="d7e6f-203">Si el paquete existe en el origen del paquete, se devuelve un código de estado 200.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="d7e6f-204">El cuerpo de la respuesta será el manifiesto del paquete, que es el archivo. nuspec incluido en el archivo. nupkg correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="d7e6f-205">El archivo. nuspec es un documento XML.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="d7e6f-206">Si el paquete no existe en el origen del paquete, se devuelve un código de estado 404.</span><span class="sxs-lookup"><span data-stu-id="d7e6f-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d7e6f-207">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d7e6f-207">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a><span data-ttu-id="d7e6f-208">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="d7e6f-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
