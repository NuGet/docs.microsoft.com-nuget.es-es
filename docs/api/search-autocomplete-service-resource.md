---
title: Autocompletar, API de NuGet
description: El servicio de búsqueda de Autocompletar es compatible con las versiones y la detección interactiva de los identificadores de paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911054"
---
# <a name="autocomplete"></a><span data-ttu-id="ff5b1-103">Autocompletar</span><span class="sxs-lookup"><span data-stu-id="ff5b1-103">Autocomplete</span></span>

<span data-ttu-id="ff5b1-104">Es posible crear una experiencia paquete ID y version Autocompletar mediante la API de V3.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="ff5b1-105">El recurso que se usa para realizar consultas de Autocompletar es el `SearchAutocompleteService` encontrar el recurso en el [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ff5b1-106">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="ff5b1-106">Versioning</span></span>

<span data-ttu-id="ff5b1-107">La siguiente `@type` se usan los valores:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-107">The following `@type` values are used:</span></span>

<span data-ttu-id="ff5b1-108">Valor de@type </span><span class="sxs-lookup"><span data-stu-id="ff5b1-108">@type value</span></span>                          | <span data-ttu-id="ff5b1-109">Notas</span><span class="sxs-lookup"><span data-stu-id="ff5b1-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="ff5b1-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="ff5b1-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="ff5b1-111">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="ff5b1-111">The initial release</span></span>
<span data-ttu-id="ff5b1-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="ff5b1-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="ff5b1-113">Alias de</span><span class="sxs-lookup"><span data-stu-id="ff5b1-113">Alias of</span></span> `SearchAutocompleteService`
<span data-ttu-id="ff5b1-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="ff5b1-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="ff5b1-115">Alias de</span><span class="sxs-lookup"><span data-stu-id="ff5b1-115">Alias of</span></span> `SearchAutocompleteService`

## <a name="base-url"></a><span data-ttu-id="ff5b1-116">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="ff5b1-116">Base URL</span></span>

<span data-ttu-id="ff5b1-117">La dirección URL base para las siguientes API es el valor de la `@id` propiedad asociada con uno de los recursos mencionados anteriormente `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="ff5b1-118">En el siguiente documento, la dirección URL base del marcador de posición `{@id}` se usará.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ff5b1-119">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="ff5b1-119">HTTP Methods</span></span>

<span data-ttu-id="ff5b1-120">Todas las direcciones URL se encuentra en la compatibilidad con recursos de registro de los métodos HTTP `GET` y `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="ff5b1-121">Busque los identificadores de paquete</span><span class="sxs-lookup"><span data-stu-id="ff5b1-121">Search for package IDs</span></span>

<span data-ttu-id="ff5b1-122">La primera API de Autocompletar admite la búsqueda de la parte de una cadena de identificador de paquete.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="ff5b1-123">Esto es fantástico cuando desee proporcionar una característica de escritura anticipada del paquete en una interfaz de usuario integrada con un origen del paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="ff5b1-124">Un paquete con solo las versiones no enumeradas no aparecerán en los resultados.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="ff5b1-125">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="ff5b1-125">Request parameters</span></span>

<span data-ttu-id="ff5b1-126">Name</span><span class="sxs-lookup"><span data-stu-id="ff5b1-126">Name</span></span>        | <span data-ttu-id="ff5b1-127">En</span><span class="sxs-lookup"><span data-stu-id="ff5b1-127">In</span></span>     | <span data-ttu-id="ff5b1-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff5b1-128">Type</span></span>    | <span data-ttu-id="ff5b1-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ff5b1-129">Required</span></span> | <span data-ttu-id="ff5b1-130">Notas</span><span class="sxs-lookup"><span data-stu-id="ff5b1-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ff5b1-131">q</span><span class="sxs-lookup"><span data-stu-id="ff5b1-131">q</span></span>           | <span data-ttu-id="ff5b1-132">Resolución</span><span class="sxs-lookup"><span data-stu-id="ff5b1-132">URL</span></span>    | <span data-ttu-id="ff5b1-133">cadena</span><span class="sxs-lookup"><span data-stu-id="ff5b1-133">string</span></span>  | <span data-ttu-id="ff5b1-134">No</span><span class="sxs-lookup"><span data-stu-id="ff5b1-134">no</span></span>       | <span data-ttu-id="ff5b1-135">La cadena para comparar los identificadores de paquete</span><span class="sxs-lookup"><span data-stu-id="ff5b1-135">The string to compare against package IDs</span></span>
<span data-ttu-id="ff5b1-136">skip</span><span class="sxs-lookup"><span data-stu-id="ff5b1-136">skip</span></span>        | <span data-ttu-id="ff5b1-137">Resolución</span><span class="sxs-lookup"><span data-stu-id="ff5b1-137">URL</span></span>    | <span data-ttu-id="ff5b1-138">enteros</span><span class="sxs-lookup"><span data-stu-id="ff5b1-138">integer</span></span> | <span data-ttu-id="ff5b1-139">No</span><span class="sxs-lookup"><span data-stu-id="ff5b1-139">no</span></span>       | <span data-ttu-id="ff5b1-140">El número de resultados que se omitirán para la paginación</span><span class="sxs-lookup"><span data-stu-id="ff5b1-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="ff5b1-141">Take</span><span class="sxs-lookup"><span data-stu-id="ff5b1-141">take</span></span>        | <span data-ttu-id="ff5b1-142">Resolución</span><span class="sxs-lookup"><span data-stu-id="ff5b1-142">URL</span></span>    | <span data-ttu-id="ff5b1-143">enteros</span><span class="sxs-lookup"><span data-stu-id="ff5b1-143">integer</span></span> | <span data-ttu-id="ff5b1-144">No</span><span class="sxs-lookup"><span data-stu-id="ff5b1-144">no</span></span>       | <span data-ttu-id="ff5b1-145">El número de resultados que se va a devolver para la paginación</span><span class="sxs-lookup"><span data-stu-id="ff5b1-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="ff5b1-146">versión preliminar</span><span class="sxs-lookup"><span data-stu-id="ff5b1-146">prerelease</span></span>  | <span data-ttu-id="ff5b1-147">Resolución</span><span class="sxs-lookup"><span data-stu-id="ff5b1-147">URL</span></span>    | <span data-ttu-id="ff5b1-148">booleano</span><span class="sxs-lookup"><span data-stu-id="ff5b1-148">boolean</span></span> | <span data-ttu-id="ff5b1-149">No</span><span class="sxs-lookup"><span data-stu-id="ff5b1-149">no</span></span>       | `true` <span data-ttu-id="ff5b1-150">o `false` determinar si se debe incluir [paquetes de versión preliminar](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-150">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ff5b1-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ff5b1-151">semVerLevel</span></span> | <span data-ttu-id="ff5b1-152">Resolución</span><span class="sxs-lookup"><span data-stu-id="ff5b1-152">URL</span></span>    | <span data-ttu-id="ff5b1-153">cadena</span><span class="sxs-lookup"><span data-stu-id="ff5b1-153">string</span></span>  | <span data-ttu-id="ff5b1-154">No</span><span class="sxs-lookup"><span data-stu-id="ff5b1-154">no</span></span>       | <span data-ttu-id="ff5b1-155">Una cadena de versión 1.0.0 de SemVer</span><span class="sxs-lookup"><span data-stu-id="ff5b1-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="ff5b1-156">La consulta de Autocompletar `q` se analiza de manera que se define mediante la implementación del servidor.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="ff5b1-157">NuGet.org admite las consultas para el prefijo de los tokens de identificador de paquete, que son partes de identificador generados por división original por caracteres camel de caso y símbolos.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="ff5b1-158">El `skip` parámetro el valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="ff5b1-159">El `take` parámetro debe ser un entero mayor que cero.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="ff5b1-160">La implementación del servidor puede imponer un valor máximo.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="ff5b1-161">Si `prerelease` no es siempre se excluyen los paquetes de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ff5b1-162">El `semVerLevel` parámetro de consulta se utiliza para participar en [SemVer 2.0.0 paquetes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="ff5b1-163">Si se excluye de este parámetro de consulta, se devolverán solo los identificadores de paquete con las versiones compatibles de SemVer 1.0.0 (con el [control de versiones de NuGet estándar](../reference/package-versioning.md) advertencias, tales como las cadenas de versión con 4 partes entero).</span><span class="sxs-lookup"><span data-stu-id="ff5b1-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="ff5b1-164">Si `semVerLevel=2.0.0` es siempre se devolverá SemVer 1.0.0 y 2.0.0 de SemVer compatibles paquetes.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="ff5b1-165">Consulte la [compatibilidad con SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="ff5b1-166">Respuesta</span><span class="sxs-lookup"><span data-stu-id="ff5b1-166">Response</span></span>

<span data-ttu-id="ff5b1-167">La respuesta es un documento JSON que contiene hasta `take` Autocompletar resultados.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="ff5b1-168">El objeto JSON de raíz tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="ff5b1-169">Name</span><span class="sxs-lookup"><span data-stu-id="ff5b1-169">Name</span></span>      | <span data-ttu-id="ff5b1-170">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff5b1-170">Type</span></span>             | <span data-ttu-id="ff5b1-171">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ff5b1-171">Required</span></span> | <span data-ttu-id="ff5b1-172">Notas</span><span class="sxs-lookup"><span data-stu-id="ff5b1-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ff5b1-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="ff5b1-173">totalHits</span></span> | <span data-ttu-id="ff5b1-174">enteros</span><span class="sxs-lookup"><span data-stu-id="ff5b1-174">integer</span></span>          | <span data-ttu-id="ff5b1-175">sí</span><span class="sxs-lookup"><span data-stu-id="ff5b1-175">yes</span></span>      | <span data-ttu-id="ff5b1-176">El número total de coincidencias, omitiendo `skip` y</span><span class="sxs-lookup"><span data-stu-id="ff5b1-176">The total number of matches, disregarding `skip` and</span></span> `take`
<span data-ttu-id="ff5b1-177">datos</span><span class="sxs-lookup"><span data-stu-id="ff5b1-177">data</span></span>      | <span data-ttu-id="ff5b1-178">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="ff5b1-178">array of strings</span></span> | <span data-ttu-id="ff5b1-179">sí</span><span class="sxs-lookup"><span data-stu-id="ff5b1-179">yes</span></span>      | <span data-ttu-id="ff5b1-180">El paquete de identificadores que coinciden con la solicitud</span><span class="sxs-lookup"><span data-stu-id="ff5b1-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="ff5b1-181">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ff5b1-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="ff5b1-182">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ff5b1-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="ff5b1-183">Enumerar versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="ff5b1-183">Enumerate package versions</span></span>

<span data-ttu-id="ff5b1-184">Una vez que se detecta un identificador de paquete mediante la API anterior, un cliente puede utilizar la API de Autocompletar para enumerar las versiones del paquete para un identificador de paquete proporcionado.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="ff5b1-185">No aparecerá en los resultados de una versión del paquete que se da de baja.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="ff5b1-186">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="ff5b1-186">Request parameters</span></span>

<span data-ttu-id="ff5b1-187">Name</span><span class="sxs-lookup"><span data-stu-id="ff5b1-187">Name</span></span>        | <span data-ttu-id="ff5b1-188">En</span><span class="sxs-lookup"><span data-stu-id="ff5b1-188">In</span></span>     | <span data-ttu-id="ff5b1-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff5b1-189">Type</span></span>    | <span data-ttu-id="ff5b1-190">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ff5b1-190">Required</span></span> | <span data-ttu-id="ff5b1-191">Notas</span><span class="sxs-lookup"><span data-stu-id="ff5b1-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ff5b1-192">id</span><span class="sxs-lookup"><span data-stu-id="ff5b1-192">id</span></span>          | <span data-ttu-id="ff5b1-193">Resolución</span><span class="sxs-lookup"><span data-stu-id="ff5b1-193">URL</span></span>    | <span data-ttu-id="ff5b1-194">cadena</span><span class="sxs-lookup"><span data-stu-id="ff5b1-194">string</span></span>  | <span data-ttu-id="ff5b1-195">sí</span><span class="sxs-lookup"><span data-stu-id="ff5b1-195">yes</span></span>      | <span data-ttu-id="ff5b1-196">El identificador del paquete para capturar las versiones de</span><span class="sxs-lookup"><span data-stu-id="ff5b1-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="ff5b1-197">versión preliminar</span><span class="sxs-lookup"><span data-stu-id="ff5b1-197">prerelease</span></span>  | <span data-ttu-id="ff5b1-198">Resolución</span><span class="sxs-lookup"><span data-stu-id="ff5b1-198">URL</span></span>    | <span data-ttu-id="ff5b1-199">booleano</span><span class="sxs-lookup"><span data-stu-id="ff5b1-199">boolean</span></span> | <span data-ttu-id="ff5b1-200">No</span><span class="sxs-lookup"><span data-stu-id="ff5b1-200">no</span></span>       | `true` <span data-ttu-id="ff5b1-201">o `false` determinar si se debe incluir [paquetes de versión preliminar](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ff5b1-201">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ff5b1-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ff5b1-202">semVerLevel</span></span> | <span data-ttu-id="ff5b1-203">Resolución</span><span class="sxs-lookup"><span data-stu-id="ff5b1-203">URL</span></span>    | <span data-ttu-id="ff5b1-204">cadena</span><span class="sxs-lookup"><span data-stu-id="ff5b1-204">string</span></span>  | <span data-ttu-id="ff5b1-205">No</span><span class="sxs-lookup"><span data-stu-id="ff5b1-205">no</span></span>       | <span data-ttu-id="ff5b1-206">Una cadena de versión 2.0.0 de SemVer</span><span class="sxs-lookup"><span data-stu-id="ff5b1-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="ff5b1-207">Si `prerelease` no es siempre se excluyen los paquetes de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ff5b1-208">El `semVerLevel` parámetro de consulta se utiliza para participar en los paquetes de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="ff5b1-209">Si se excluye de este parámetro de consulta, se devolverá solo las versiones de SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="ff5b1-210">Si `semVerLevel=2.0.0` es siempre SemVer 1.0.0 y 2.0.0 de SemVer versiones se devolverá.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="ff5b1-211">Consulte la [compatibilidad con SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="ff5b1-212">Respuesta</span><span class="sxs-lookup"><span data-stu-id="ff5b1-212">Response</span></span>

<span data-ttu-id="ff5b1-213">La respuesta es el documento JSON que contiene todas las versiones de paquete del identificador del paquete proporcionado, filtrado por los parámetros de consulta determinada.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="ff5b1-214">El objeto JSON de raíz tiene la siguiente propiedad:</span><span class="sxs-lookup"><span data-stu-id="ff5b1-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="ff5b1-215">Name</span><span class="sxs-lookup"><span data-stu-id="ff5b1-215">Name</span></span>      | <span data-ttu-id="ff5b1-216">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff5b1-216">Type</span></span>             | <span data-ttu-id="ff5b1-217">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ff5b1-217">Required</span></span> | <span data-ttu-id="ff5b1-218">Notas</span><span class="sxs-lookup"><span data-stu-id="ff5b1-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ff5b1-219">datos</span><span class="sxs-lookup"><span data-stu-id="ff5b1-219">data</span></span>      | <span data-ttu-id="ff5b1-220">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="ff5b1-220">array of strings</span></span> | <span data-ttu-id="ff5b1-221">sí</span><span class="sxs-lookup"><span data-stu-id="ff5b1-221">yes</span></span>      | <span data-ttu-id="ff5b1-222">Las versiones del paquete coincide con la solicitud</span><span class="sxs-lookup"><span data-stu-id="ff5b1-222">The package versions matched by the request</span></span>

<span data-ttu-id="ff5b1-223">Las versiones del paquete en el `data` matriz puede contener metadatos de la compilación de SemVer 2.0.0 (por ejemplo, `1.0.0+metadata`) si el `semVerLevel=2.0.0` se proporciona en la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="ff5b1-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ff5b1-224">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ff5b1-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="ff5b1-225">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ff5b1-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
