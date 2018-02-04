---
title: Autocompletar, NuGet API | Documentos de Microsoft
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
description: "El servicio de búsqueda Autocompletar admite las versiones y descubrimiento interactivo de identificadores de paquete."
keywords: "API de Autocompletar de NuGet, Id. de paquete de búsqueda de NuGet, Id. de paquete de subcadena"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a><span data-ttu-id="b3828-104">Autocompletar</span><span class="sxs-lookup"><span data-stu-id="b3828-104">Autocomplete</span></span>

<span data-ttu-id="b3828-105">Es posible crear una experiencia paquete identificador y la versión Autocompletar mediante la API V3.</span><span class="sxs-lookup"><span data-stu-id="b3828-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="b3828-106">El recurso que se utiliza para realizar consultas de Autocompletar es el `SearchAutocompleteService` recurso se encuentra en la [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="b3828-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b3828-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="b3828-107">Versioning</span></span>

<span data-ttu-id="b3828-108">Los siguientes `@type` se usan valores:</span><span class="sxs-lookup"><span data-stu-id="b3828-108">The following `@type` values are used:</span></span>

<span data-ttu-id="b3828-109">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="b3828-109">@type value</span></span>                          | <span data-ttu-id="b3828-110">Notas</span><span class="sxs-lookup"><span data-stu-id="b3828-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="b3828-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="b3828-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="b3828-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="b3828-112">The initial release</span></span>
<span data-ttu-id="b3828-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="b3828-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="b3828-114">Alias de`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="b3828-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="b3828-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="b3828-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="b3828-116">Alias de`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="b3828-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="b3828-117">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="b3828-117">Base URL</span></span>

<span data-ttu-id="b3828-118">La dirección URL base para las API siguientes es el valor de la `@id` propiedad asociado a uno de los recursos mencionados anteriormente `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="b3828-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="b3828-119">En el siguiente documento, el marcador de posición de la dirección URL base `{@id}` se usará.</span><span class="sxs-lookup"><span data-stu-id="b3828-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b3828-120">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="b3828-120">HTTP Methods</span></span>

<span data-ttu-id="b3828-121">Todas las direcciones URL se encuentra en el soporte de registro del recurso los métodos HTTP `GET` y `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="b3828-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="b3828-122">Busque los identificadores de paquete</span><span class="sxs-lookup"><span data-stu-id="b3828-122">Search for package IDs</span></span>

<span data-ttu-id="b3828-123">La primera Autocompletar API admite las búsquedas de parte de una cadena de identificador de paquete.</span><span class="sxs-lookup"><span data-stu-id="b3828-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="b3828-124">Esto es excelente cuando desea proporcionar una característica de escritura anticipada de paquete en una interfaz de usuario integrada con un origen de paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="b3828-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="b3828-125">Un paquete con solo las versiones que no figuran en no aparecerán en los resultados.</span><span class="sxs-lookup"><span data-stu-id="b3828-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="b3828-126">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="b3828-126">Request parameters</span></span>

<span data-ttu-id="b3828-127">nombre</span><span class="sxs-lookup"><span data-stu-id="b3828-127">Name</span></span>        | <span data-ttu-id="b3828-128">En</span><span class="sxs-lookup"><span data-stu-id="b3828-128">In</span></span>     | <span data-ttu-id="b3828-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="b3828-129">Type</span></span>    | <span data-ttu-id="b3828-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b3828-130">Required</span></span> | <span data-ttu-id="b3828-131">Notas</span><span class="sxs-lookup"><span data-stu-id="b3828-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="b3828-132">q</span><span class="sxs-lookup"><span data-stu-id="b3828-132">q</span></span>           | <span data-ttu-id="b3828-133">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="b3828-133">URL</span></span>    | <span data-ttu-id="b3828-134">cadena</span><span class="sxs-lookup"><span data-stu-id="b3828-134">string</span></span>  | <span data-ttu-id="b3828-135">No</span><span class="sxs-lookup"><span data-stu-id="b3828-135">no</span></span>       | <span data-ttu-id="b3828-136">La cadena para comparar identificadores de paquete</span><span class="sxs-lookup"><span data-stu-id="b3828-136">The string to compare against package IDs</span></span>
<span data-ttu-id="b3828-137">skip</span><span class="sxs-lookup"><span data-stu-id="b3828-137">skip</span></span>        | <span data-ttu-id="b3828-138">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="b3828-138">URL</span></span>    | <span data-ttu-id="b3828-139">enteros</span><span class="sxs-lookup"><span data-stu-id="b3828-139">integer</span></span> | <span data-ttu-id="b3828-140">No</span><span class="sxs-lookup"><span data-stu-id="b3828-140">no</span></span>       | <span data-ttu-id="b3828-141">El número de resultados que se va a omitir, para la paginación</span><span class="sxs-lookup"><span data-stu-id="b3828-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="b3828-142">Take</span><span class="sxs-lookup"><span data-stu-id="b3828-142">take</span></span>        | <span data-ttu-id="b3828-143">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="b3828-143">URL</span></span>    | <span data-ttu-id="b3828-144">enteros</span><span class="sxs-lookup"><span data-stu-id="b3828-144">integer</span></span> | <span data-ttu-id="b3828-145">No</span><span class="sxs-lookup"><span data-stu-id="b3828-145">no</span></span>       | <span data-ttu-id="b3828-146">El número de resultados que se va a devolver para la paginación</span><span class="sxs-lookup"><span data-stu-id="b3828-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="b3828-147">versión preliminar</span><span class="sxs-lookup"><span data-stu-id="b3828-147">prerelease</span></span>  | <span data-ttu-id="b3828-148">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="b3828-148">URL</span></span>    | <span data-ttu-id="b3828-149">booleano</span><span class="sxs-lookup"><span data-stu-id="b3828-149">boolean</span></span> | <span data-ttu-id="b3828-150">No</span><span class="sxs-lookup"><span data-stu-id="b3828-150">no</span></span>       | <span data-ttu-id="b3828-151">`true`o `false` determinar si se debe incluir [paquetes de versión preliminar](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="b3828-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="b3828-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="b3828-152">semVerLevel</span></span> | <span data-ttu-id="b3828-153">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="b3828-153">URL</span></span>    | <span data-ttu-id="b3828-154">cadena</span><span class="sxs-lookup"><span data-stu-id="b3828-154">string</span></span>  | <span data-ttu-id="b3828-155">No</span><span class="sxs-lookup"><span data-stu-id="b3828-155">no</span></span>       | <span data-ttu-id="b3828-156">Una cadena de versión SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="b3828-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="b3828-157">La consulta de Autocompletar `q` se analiza de forma que se define mediante la implementación del servidor.</span><span class="sxs-lookup"><span data-stu-id="b3828-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="b3828-158">NuGet.org admite las consultas para el prefijo de tokens de Id. de paquete, que son partes del identificador generado por spliting original, caracteres camel de caso y símbolos.</span><span class="sxs-lookup"><span data-stu-id="b3828-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="b3828-159">El `skip` parámetro el valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="b3828-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="b3828-160">El `take` parámetro debe ser un entero mayor que cero.</span><span class="sxs-lookup"><span data-stu-id="b3828-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="b3828-161">La implementación del servidor puede imponer un valor máximo.</span><span class="sxs-lookup"><span data-stu-id="b3828-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="b3828-162">Si `prerelease` no es siempre, se excluyen los paquetes de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="b3828-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="b3828-163">El `semVerLevel` parámetro de consulta se utiliza para participar en [SemVer 2.0.0 paquetes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="b3828-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="b3828-164">Si se excluye de este parámetro de consulta, se devolverán los identificadores de paquete solo con las versiones compatibles de SemVer 1.0.0 (con la [control de versiones de NuGet estándar](../reference/package-versioning.md) advertencias, como las cadenas de versión con 4 partes entero).</span><span class="sxs-lookup"><span data-stu-id="b3828-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="b3828-165">Si `semVerLevel=2.0.0` es siempre devolverán SemVer 1.0.0 y paquetes de SemVer 2.0.0 compatibles.</span><span class="sxs-lookup"><span data-stu-id="b3828-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="b3828-166">Consulte la [SemVer 2.0.0 compatibilidad con nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b3828-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="b3828-167">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b3828-167">Response</span></span>

<span data-ttu-id="b3828-168">La respuesta es documento JSON que contiene hasta `take` resultados de Autocompletar.</span><span class="sxs-lookup"><span data-stu-id="b3828-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="b3828-169">El objeto JSON raíz tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="b3828-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="b3828-170">nombre</span><span class="sxs-lookup"><span data-stu-id="b3828-170">Name</span></span>      | <span data-ttu-id="b3828-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="b3828-171">Type</span></span>             | <span data-ttu-id="b3828-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b3828-172">Required</span></span> | <span data-ttu-id="b3828-173">Notas</span><span class="sxs-lookup"><span data-stu-id="b3828-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="b3828-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="b3828-174">totalHits</span></span> | <span data-ttu-id="b3828-175">enteros</span><span class="sxs-lookup"><span data-stu-id="b3828-175">integer</span></span>          | <span data-ttu-id="b3828-176">sí</span><span class="sxs-lookup"><span data-stu-id="b3828-176">yes</span></span>      | <span data-ttu-id="b3828-177">El número total de coincidencias, sin tener en cuenta `skip` y`take`</span><span class="sxs-lookup"><span data-stu-id="b3828-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="b3828-178">datos</span><span class="sxs-lookup"><span data-stu-id="b3828-178">data</span></span>      | <span data-ttu-id="b3828-179">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="b3828-179">array of strings</span></span> | <span data-ttu-id="b3828-180">sí</span><span class="sxs-lookup"><span data-stu-id="b3828-180">yes</span></span>      | <span data-ttu-id="b3828-181">El paquete coincidentes con la solicitud de identificadores</span><span class="sxs-lookup"><span data-stu-id="b3828-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="b3828-182">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b3828-182">Sample request</span></span>

<span data-ttu-id="b3828-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="b3828-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="b3828-184">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b3828-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="b3828-185">Enumerar las versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="b3828-185">Enumerate package versions</span></span>

<span data-ttu-id="b3828-186">Una vez que se detecta un identificador de paquete mediante la API anterior, un cliente puede utilizar la API de Autocompletar para enumerar las versiones del paquete para un identificador de paquete proporcionado.</span><span class="sxs-lookup"><span data-stu-id="b3828-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="b3828-187">Una versión de paquete que no figuran en no aparecerán en los resultados.</span><span class="sxs-lookup"><span data-stu-id="b3828-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="b3828-188">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="b3828-188">Request parameters</span></span>

<span data-ttu-id="b3828-189">nombre</span><span class="sxs-lookup"><span data-stu-id="b3828-189">Name</span></span>        | <span data-ttu-id="b3828-190">En</span><span class="sxs-lookup"><span data-stu-id="b3828-190">In</span></span>     | <span data-ttu-id="b3828-191">Tipo</span><span class="sxs-lookup"><span data-stu-id="b3828-191">Type</span></span>    | <span data-ttu-id="b3828-192">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b3828-192">Required</span></span> | <span data-ttu-id="b3828-193">Notas</span><span class="sxs-lookup"><span data-stu-id="b3828-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="b3828-194">id</span><span class="sxs-lookup"><span data-stu-id="b3828-194">id</span></span>          | <span data-ttu-id="b3828-195">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="b3828-195">URL</span></span>    | <span data-ttu-id="b3828-196">cadena</span><span class="sxs-lookup"><span data-stu-id="b3828-196">string</span></span>  | <span data-ttu-id="b3828-197">sí</span><span class="sxs-lookup"><span data-stu-id="b3828-197">yes</span></span>      | <span data-ttu-id="b3828-198">El identificador del paquete para capturar las versiones de</span><span class="sxs-lookup"><span data-stu-id="b3828-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="b3828-199">versión preliminar</span><span class="sxs-lookup"><span data-stu-id="b3828-199">prerelease</span></span>  | <span data-ttu-id="b3828-200">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="b3828-200">URL</span></span>    | <span data-ttu-id="b3828-201">booleano</span><span class="sxs-lookup"><span data-stu-id="b3828-201">boolean</span></span> | <span data-ttu-id="b3828-202">No</span><span class="sxs-lookup"><span data-stu-id="b3828-202">no</span></span>       | <span data-ttu-id="b3828-203">`true`o `false` determinar si se debe incluir [paquetes de versión preliminar](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="b3828-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="b3828-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="b3828-204">semVerLevel</span></span> | <span data-ttu-id="b3828-205">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="b3828-205">URL</span></span>    | <span data-ttu-id="b3828-206">cadena</span><span class="sxs-lookup"><span data-stu-id="b3828-206">string</span></span>  | <span data-ttu-id="b3828-207">No</span><span class="sxs-lookup"><span data-stu-id="b3828-207">no</span></span>       | <span data-ttu-id="b3828-208">Una cadena de versión SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b3828-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="b3828-209">Si `prerelease` no es siempre, se excluyen los paquetes de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="b3828-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="b3828-210">El `semVerLevel` parámetro de consulta se utiliza para participar en paquetes SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="b3828-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="b3828-211">Si se excluye de este parámetro de consulta, se devolverá solo las versiones de SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="b3828-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="b3828-212">Si `semVerLevel=2.0.0` es siempre devolverán SemVer 1.0.0 y SemVer 2.0.0 versiones.</span><span class="sxs-lookup"><span data-stu-id="b3828-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="b3828-213">Consulte la [SemVer 2.0.0 compatibilidad con nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b3828-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="b3828-214">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b3828-214">Response</span></span>

<span data-ttu-id="b3828-215">La respuesta es documento JSON que contiene todas las versiones de paquete del identificador de paquete suministrado, filtrado por los parámetros de consulta determinada.</span><span class="sxs-lookup"><span data-stu-id="b3828-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="b3828-216">El objeto JSON raíz tiene la propiedad siguiente:</span><span class="sxs-lookup"><span data-stu-id="b3828-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="b3828-217">nombre</span><span class="sxs-lookup"><span data-stu-id="b3828-217">Name</span></span>      | <span data-ttu-id="b3828-218">Tipo</span><span class="sxs-lookup"><span data-stu-id="b3828-218">Type</span></span>             | <span data-ttu-id="b3828-219">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b3828-219">Required</span></span> | <span data-ttu-id="b3828-220">Notas</span><span class="sxs-lookup"><span data-stu-id="b3828-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="b3828-221">datos</span><span class="sxs-lookup"><span data-stu-id="b3828-221">data</span></span>      | <span data-ttu-id="b3828-222">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="b3828-222">array of strings</span></span> | <span data-ttu-id="b3828-223">sí</span><span class="sxs-lookup"><span data-stu-id="b3828-223">yes</span></span>      | <span data-ttu-id="b3828-224">Las versiones del paquete coincidentes con la solicitud</span><span class="sxs-lookup"><span data-stu-id="b3828-224">The package versions matched by the request</span></span>

<span data-ttu-id="b3828-225">Las versiones del paquete en el `data` matriz podría contener metadatos de compilación SemVer 2.0.0 (p. ej. `1.0.0+metadata`) si el `semVerLevel=2.0.0` se proporcionó en la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="b3828-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="b3828-226">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b3828-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="b3828-227">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b3828-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
