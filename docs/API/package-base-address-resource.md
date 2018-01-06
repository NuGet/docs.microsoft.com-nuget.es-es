---
title: Paquete de contenido, NuGet API | Documentos de Microsoft
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
ms.assetid: ec68b5d1-a684-4995-b1a6-6210dbb24875
description: "La dirección base del paquete es una interfaz sencilla para capturar el propio paquete."
keywords: "NuGet planos contenedor, la dirección base del paquete de NuGet, NuGet nupkg API, las versiones de paquetes de NuGet API, API de NuGet que no figuran en paquetes, nuspec de descarga de API de NuGet"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: a581f9854410bc1a84d65310b38928a1d889ece2
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="package-content"></a><span data-ttu-id="8bf52-104">Contenido del paquete</span><span class="sxs-lookup"><span data-stu-id="8bf52-104">Package Content</span></span>

<span data-ttu-id="8bf52-105">Es posible generar una dirección URL para recuperar contenido de un paquete arbitrario (el archivo .nupkg) mediante la API V3.</span><span class="sxs-lookup"><span data-stu-id="8bf52-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="8bf52-106">El recurso que se utiliza para capturar el contenido del paquete es el `PackageBaseAddress` recurso se encuentra en la [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="8bf52-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="8bf52-107">Este recurso también habilita la detección de todas las versiones de un paquete, que se indica o dados de baja.</span><span class="sxs-lookup"><span data-stu-id="8bf52-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="8bf52-108">Este recurso se conoce normalmente como la "paquete base dirección" o "contenedor sin formato".</span><span class="sxs-lookup"><span data-stu-id="8bf52-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="8bf52-109">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="8bf52-109">Versioning</span></span>

<span data-ttu-id="8bf52-110">El siguiente `@type` valor se utiliza:</span><span class="sxs-lookup"><span data-stu-id="8bf52-110">The following `@type` value is used:</span></span>

<span data-ttu-id="8bf52-111">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="8bf52-111">@type value</span></span>              | <span data-ttu-id="8bf52-112">Notas</span><span class="sxs-lookup"><span data-stu-id="8bf52-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="8bf52-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="8bf52-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="8bf52-114">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="8bf52-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="8bf52-115">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="8bf52-115">Base URL</span></span>

<span data-ttu-id="8bf52-116">La dirección URL base para las API siguientes es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="8bf52-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="8bf52-117">En el siguiente documento, el marcador de posición de la dirección URL base `{@id}` se usará.</span><span class="sxs-lookup"><span data-stu-id="8bf52-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8bf52-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="8bf52-118">HTTP methods</span></span>

<span data-ttu-id="8bf52-119">Todas las direcciones URL se encuentra en el soporte de registro del recurso los métodos HTTP `GET` y `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="8bf52-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="8bf52-120">Enumerar las versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="8bf52-120">Enumerate package versions</span></span>

<span data-ttu-id="8bf52-121">Si el cliente sabe que un identificador de paquete y desea descubrir que versiones del paquete el paquete de origen tiene disponible, el cliente puede construir una dirección URL de predicción para enumerar todas las versiones de paquete.</span><span class="sxs-lookup"><span data-stu-id="8bf52-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="8bf52-122">Esta lista se ha diseñado para ser una "lista de directorios" para la API de contenido de paquete que se mencionan más abajo.</span><span class="sxs-lookup"><span data-stu-id="8bf52-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="8bf52-123">Esta lista contiene ambas versiones de la lista y que no figuran en el paquete.</span><span class="sxs-lookup"><span data-stu-id="8bf52-123">This list contains both listed and unlisted package versions.</span></span>

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a><span data-ttu-id="8bf52-124">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="8bf52-124">Request parameters</span></span>

<span data-ttu-id="8bf52-125">nombre</span><span class="sxs-lookup"><span data-stu-id="8bf52-125">Name</span></span>     | <span data-ttu-id="8bf52-126">En</span><span class="sxs-lookup"><span data-stu-id="8bf52-126">In</span></span>     | <span data-ttu-id="8bf52-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="8bf52-127">Type</span></span>    | <span data-ttu-id="8bf52-128">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8bf52-128">Required</span></span> | <span data-ttu-id="8bf52-129">Notas</span><span class="sxs-lookup"><span data-stu-id="8bf52-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="8bf52-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="8bf52-130">LOWER_ID</span></span> | <span data-ttu-id="8bf52-131">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="8bf52-131">URL</span></span>    | <span data-ttu-id="8bf52-132">cadena</span><span class="sxs-lookup"><span data-stu-id="8bf52-132">string</span></span>  | <span data-ttu-id="8bf52-133">sí</span><span class="sxs-lookup"><span data-stu-id="8bf52-133">yes</span></span>      | <span data-ttu-id="8bf52-134">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="8bf52-134">The package ID, lowercase</span></span>

<span data-ttu-id="8bf52-135">El `LOWER_ID` valor es el identificador de paquete deseado en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="8bf52-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="8bf52-136">Respuesta</span><span class="sxs-lookup"><span data-stu-id="8bf52-136">Response</span></span>

<span data-ttu-id="8bf52-137">Si el origen del paquete no tiene ninguna versión del identificador del paquete suministrado, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="8bf52-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="8bf52-138">Si el origen del paquete tiene una o varias versiones, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="8bf52-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="8bf52-139">El cuerpo de respuesta es un objeto JSON con la siguiente propiedad:</span><span class="sxs-lookup"><span data-stu-id="8bf52-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="8bf52-140">nombre</span><span class="sxs-lookup"><span data-stu-id="8bf52-140">Name</span></span>     | <span data-ttu-id="8bf52-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="8bf52-141">Type</span></span>             | <span data-ttu-id="8bf52-142">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8bf52-142">Required</span></span> | <span data-ttu-id="8bf52-143">Notas</span><span class="sxs-lookup"><span data-stu-id="8bf52-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="8bf52-144">versiones</span><span class="sxs-lookup"><span data-stu-id="8bf52-144">versions</span></span> | <span data-ttu-id="8bf52-145">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="8bf52-145">array of strings</span></span> | <span data-ttu-id="8bf52-146">sí</span><span class="sxs-lookup"><span data-stu-id="8bf52-146">yes</span></span>      | <span data-ttu-id="8bf52-147">El paquete identificadores disponibles</span><span class="sxs-lookup"><span data-stu-id="8bf52-147">The package IDs available</span></span>

<span data-ttu-id="8bf52-148">Las cadenas en el `versions` matriz todos minúscula, [normalizar las cadenas de versión de NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="8bf52-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="8bf52-149">Las cadenas de versión no contienen ningún metadato de compilación SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="8bf52-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="8bf52-150">La intención es que las cadenas de versión que se encuentra en esta matriz pueden utilizarse literalmente para el `LOWER_VERSION` tokens ubicados en los siguientes extremos.</span><span class="sxs-lookup"><span data-stu-id="8bf52-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8bf52-151">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8bf52-151">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a><span data-ttu-id="8bf52-152">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8bf52-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="8bf52-153">Descargar contenido de paquete (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="8bf52-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="8bf52-154">Si el cliente sabe que un identificador de paquete y la versión y desea descargar el contenido del paquete, solo tiene construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="8bf52-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a><span data-ttu-id="8bf52-155">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="8bf52-155">Request parameters</span></span>

<span data-ttu-id="8bf52-156">nombre</span><span class="sxs-lookup"><span data-stu-id="8bf52-156">Name</span></span>          | <span data-ttu-id="8bf52-157">En</span><span class="sxs-lookup"><span data-stu-id="8bf52-157">In</span></span>     | <span data-ttu-id="8bf52-158">Tipo</span><span class="sxs-lookup"><span data-stu-id="8bf52-158">Type</span></span>   | <span data-ttu-id="8bf52-159">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8bf52-159">Required</span></span> | <span data-ttu-id="8bf52-160">Notas</span><span class="sxs-lookup"><span data-stu-id="8bf52-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="8bf52-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="8bf52-161">LOWER_ID</span></span>      | <span data-ttu-id="8bf52-162">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="8bf52-162">URL</span></span>    | <span data-ttu-id="8bf52-163">cadena</span><span class="sxs-lookup"><span data-stu-id="8bf52-163">string</span></span> | <span data-ttu-id="8bf52-164">sí</span><span class="sxs-lookup"><span data-stu-id="8bf52-164">yes</span></span>      | <span data-ttu-id="8bf52-165">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="8bf52-165">The package ID, lowercase</span></span>
<span data-ttu-id="8bf52-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="8bf52-166">LOWER_VERSION</span></span> | <span data-ttu-id="8bf52-167">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="8bf52-167">URL</span></span>    | <span data-ttu-id="8bf52-168">cadena</span><span class="sxs-lookup"><span data-stu-id="8bf52-168">string</span></span> | <span data-ttu-id="8bf52-169">sí</span><span class="sxs-lookup"><span data-stu-id="8bf52-169">yes</span></span>      | <span data-ttu-id="8bf52-170">La versión del paquete, normalizar y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="8bf52-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="8bf52-171">Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="8bf52-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="8bf52-172">El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [las reglas de normalización](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="8bf52-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="8bf52-173">Esto significa que los metadatos de compilación está permitido por la especificación de SemVer 2.0.0 se deben excluir en este caso.</span><span class="sxs-lookup"><span data-stu-id="8bf52-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="8bf52-174">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="8bf52-174">Response body</span></span>

<span data-ttu-id="8bf52-175">Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="8bf52-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="8bf52-176">El cuerpo de respuesta será el contenido del paquete.</span><span class="sxs-lookup"><span data-stu-id="8bf52-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="8bf52-177">Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="8bf52-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8bf52-178">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8bf52-178">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a><span data-ttu-id="8bf52-179">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8bf52-179">Sample response</span></span>

<span data-ttu-id="8bf52-180">La secuencia binaria que sea el .nupkg para Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="8bf52-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="8bf52-181">Descargue el manifiesto del paquete (NuSpec)</span><span class="sxs-lookup"><span data-stu-id="8bf52-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="8bf52-182">Si el cliente sabe que un identificador de paquete y la versión y desea descargar el manifiesto del paquete, solo tiene construir la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="8bf52-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a><span data-ttu-id="8bf52-183">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="8bf52-183">Request parameters</span></span>

<span data-ttu-id="8bf52-184">nombre</span><span class="sxs-lookup"><span data-stu-id="8bf52-184">Name</span></span>          | <span data-ttu-id="8bf52-185">En</span><span class="sxs-lookup"><span data-stu-id="8bf52-185">In</span></span>     | <span data-ttu-id="8bf52-186">Tipo</span><span class="sxs-lookup"><span data-stu-id="8bf52-186">Type</span></span>    | <span data-ttu-id="8bf52-187">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8bf52-187">Required</span></span> | <span data-ttu-id="8bf52-188">Notas</span><span class="sxs-lookup"><span data-stu-id="8bf52-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="8bf52-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="8bf52-189">LOWER_ID</span></span>      | <span data-ttu-id="8bf52-190">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="8bf52-190">URL</span></span>    | <span data-ttu-id="8bf52-191">cadena</span><span class="sxs-lookup"><span data-stu-id="8bf52-191">string</span></span>  | <span data-ttu-id="8bf52-192">sí</span><span class="sxs-lookup"><span data-stu-id="8bf52-192">yes</span></span>      | <span data-ttu-id="8bf52-193">El identificador del paquete, en minúsculas</span><span class="sxs-lookup"><span data-stu-id="8bf52-193">The package ID, lowercase</span></span>
<span data-ttu-id="8bf52-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="8bf52-194">LOWER_VERSION</span></span> | <span data-ttu-id="8bf52-195">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="8bf52-195">URL</span></span>    | <span data-ttu-id="8bf52-196">enteros</span><span class="sxs-lookup"><span data-stu-id="8bf52-196">integer</span></span> | <span data-ttu-id="8bf52-197">sí</span><span class="sxs-lookup"><span data-stu-id="8bf52-197">yes</span></span>      | <span data-ttu-id="8bf52-198">La versión del paquete, normalizar y en minúsculas</span><span class="sxs-lookup"><span data-stu-id="8bf52-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="8bf52-199">Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="8bf52-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="8bf52-200">El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [las reglas de normalización](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="8bf52-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="8bf52-201">Esto significa que los metadatos de compilación está permitido por la especificación de SemVer 2.0.0 se deben excluir en este caso.</span><span class="sxs-lookup"><span data-stu-id="8bf52-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="8bf52-202">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="8bf52-202">Response body</span></span>

<span data-ttu-id="8bf52-203">Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="8bf52-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="8bf52-204">El cuerpo de respuesta será el manifiesto del paquete, que es el NuSpec contenidos en el .nupkg correspondiente.</span><span class="sxs-lookup"><span data-stu-id="8bf52-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="8bf52-205">El NuSpec es un documento XML.</span><span class="sxs-lookup"><span data-stu-id="8bf52-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="8bf52-206">Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.</span><span class="sxs-lookup"><span data-stu-id="8bf52-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8bf52-207">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8bf52-207">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a><span data-ttu-id="8bf52-208">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8bf52-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
