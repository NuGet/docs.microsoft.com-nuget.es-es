---
title: Insertar y eliminar, NuGet API | Documentos de Microsoft
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
description: "El servicio de publicación permite a los clientes publicar nuevos paquetes y ocultar o eliminar los paquetes existentes."
keywords: "Paquete de inserción de API de NuGet, API de NuGet eliminar paquete, API de NuGet ocultar paquete, paquete de carga de la API de NuGet, API de NuGet crear paquete"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: f8051ca57fccae77917567d8c9f2f8a120a8d884
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="0d6db-104">Insertar y eliminar</span><span class="sxs-lookup"><span data-stu-id="0d6db-104">Push and Delete</span></span>

<span data-ttu-id="0d6db-105">Es posible insertar, eliminar (ni ocultar, dependiendo de la implementación de servidor) y poner los paquetes mediante la API V3 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="0d6db-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="0d6db-106">Estas operaciones se basan en el `PackagePublish` recurso se encuentra en la [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="0d6db-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="0d6db-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="0d6db-107">Versioning</span></span>

<span data-ttu-id="0d6db-108">El siguiente `@type` valor se utiliza:</span><span class="sxs-lookup"><span data-stu-id="0d6db-108">The following `@type` value is used:</span></span>

<span data-ttu-id="0d6db-109">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="0d6db-109">@type value</span></span>          | <span data-ttu-id="0d6db-110">Notas</span><span class="sxs-lookup"><span data-stu-id="0d6db-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="0d6db-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="0d6db-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="0d6db-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="0d6db-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="0d6db-113">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="0d6db-113">Base URL</span></span>

<span data-ttu-id="0d6db-114">La dirección URL base para las API siguientes es el valor de la `@id` propiedad de la `PackagePublish/2.0.0` recursos en el origen de paquete [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="0d6db-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="0d6db-115">Para obtener la documentación siguiente, se utiliza la dirección URL de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0d6db-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="0d6db-116">Considere la posibilidad de `https://www.nuget.org/api/v2/package` como un marcador de posición para el `@id` valor se encuentra en el índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="0d6db-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="0d6db-117">Tenga en cuenta que esta dirección URL señala a la misma ubicación que el extremo de inserción V2 heredado como el protocolo es el mismo.</span><span class="sxs-lookup"><span data-stu-id="0d6db-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0d6db-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="0d6db-118">HTTP methods</span></span>

<span data-ttu-id="0d6db-119">El `PUT`, `POST` y `DELETE` métodos HTTP son compatibles con este recurso.</span><span class="sxs-lookup"><span data-stu-id="0d6db-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="0d6db-120">Para los métodos que se admiten en cada punto de conexión, consulte a continuación.</span><span class="sxs-lookup"><span data-stu-id="0d6db-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="0d6db-121">Insertar un paquete</span><span class="sxs-lookup"><span data-stu-id="0d6db-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="0d6db-122">tiene NuGet.org [requisitos adicionales](NuGet-Protocols.md) para interactuar con el punto de conexión de inserción.</span><span class="sxs-lookup"><span data-stu-id="0d6db-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="0d6db-123">NuGet.org admite la inserción de nuevos paquetes mediante la siguiente API.</span><span class="sxs-lookup"><span data-stu-id="0d6db-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="0d6db-124">Si ya existe el paquete con el identificador y la versión proporcionada, nuget.org rechazará la inserción.</span><span class="sxs-lookup"><span data-stu-id="0d6db-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="0d6db-125">Otros orígenes de paquetes pueden admitir reemplazando un paquete existente.</span><span class="sxs-lookup"><span data-stu-id="0d6db-125">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="0d6db-126">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="0d6db-126">Request parameters</span></span>

<span data-ttu-id="0d6db-127">nombre</span><span class="sxs-lookup"><span data-stu-id="0d6db-127">Name</span></span>           | <span data-ttu-id="0d6db-128">En</span><span class="sxs-lookup"><span data-stu-id="0d6db-128">In</span></span>     | <span data-ttu-id="0d6db-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d6db-129">Type</span></span>   | <span data-ttu-id="0d6db-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0d6db-130">Required</span></span> | <span data-ttu-id="0d6db-131">Notas</span><span class="sxs-lookup"><span data-stu-id="0d6db-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="0d6db-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="0d6db-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="0d6db-133">Header</span><span class="sxs-lookup"><span data-stu-id="0d6db-133">Header</span></span> | <span data-ttu-id="0d6db-134">cadena</span><span class="sxs-lookup"><span data-stu-id="0d6db-134">string</span></span> | <span data-ttu-id="0d6db-135">sí</span><span class="sxs-lookup"><span data-stu-id="0d6db-135">yes</span></span>      | <span data-ttu-id="0d6db-136">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="0d6db-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="0d6db-137">La clave de API es una cadena opaca recibido desde el origen del paquete por el usuario y configurado en el cliente.</span><span class="sxs-lookup"><span data-stu-id="0d6db-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="0d6db-138">Ningún formato de cadena determinada es obligatoria, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores de encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="0d6db-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="0d6db-139">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="0d6db-139">Request body</span></span>

<span data-ttu-id="0d6db-140">El cuerpo de solicitud debe proceder de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="0d6db-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="0d6db-141">Datos de formulario de varias partes</span><span class="sxs-lookup"><span data-stu-id="0d6db-141">Multipart form data</span></span>

<span data-ttu-id="0d6db-142">El encabezado de solicitud `Content-Type` es `multipart/form-data` y el primer elemento en el cuerpo de solicitud es los bytes sin formato de la .nupkg que se va a insertar.</span><span class="sxs-lookup"><span data-stu-id="0d6db-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="0d6db-143">Se omiten los elementos siguientes en el cuerpo de varias partes.</span><span class="sxs-lookup"><span data-stu-id="0d6db-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="0d6db-144">Se omite el nombre de archivo o cualquier otro encabezado de los elementos de varias partes.</span><span class="sxs-lookup"><span data-stu-id="0d6db-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="0d6db-145">Respuesta</span><span class="sxs-lookup"><span data-stu-id="0d6db-145">Response</span></span>

<span data-ttu-id="0d6db-146">Código de estado</span><span class="sxs-lookup"><span data-stu-id="0d6db-146">Status Code</span></span> | <span data-ttu-id="0d6db-147">Significado</span><span class="sxs-lookup"><span data-stu-id="0d6db-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="0d6db-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="0d6db-148">201, 202</span></span>    | <span data-ttu-id="0d6db-149">El paquete se ha insertado correctamente</span><span class="sxs-lookup"><span data-stu-id="0d6db-149">The package was successfully pushed</span></span>
<span data-ttu-id="0d6db-150">400</span><span class="sxs-lookup"><span data-stu-id="0d6db-150">400</span></span>         | <span data-ttu-id="0d6db-151">El paquete proporcionado no es válido</span><span class="sxs-lookup"><span data-stu-id="0d6db-151">The provided package is invalid</span></span>
<span data-ttu-id="0d6db-152">409</span><span class="sxs-lookup"><span data-stu-id="0d6db-152">409</span></span>         | <span data-ttu-id="0d6db-153">Ya existe un paquete con el identificador proporcionado y la versión</span><span class="sxs-lookup"><span data-stu-id="0d6db-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="0d6db-154">Las implementaciones de servidor varían en el código de estado correcto devuelto cuando un paquete se envíe correctamente.</span><span class="sxs-lookup"><span data-stu-id="0d6db-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="0d6db-155">Eliminar un paquete</span><span class="sxs-lookup"><span data-stu-id="0d6db-155">Delete a package</span></span>

<span data-ttu-id="0d6db-156">NuGet.org interpreta la solicitud de eliminación de paquete como un "Ocultar".</span><span class="sxs-lookup"><span data-stu-id="0d6db-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="0d6db-157">Esto significa que el paquete sigue estando disponible para los usuarios existentes del paquete, pero el paquete ya no aparece en los resultados de la búsqueda o en la interfaz web.</span><span class="sxs-lookup"><span data-stu-id="0d6db-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="0d6db-158">Para obtener más información acerca de este procedimiento, consulte la [eliminar paquetes](../policies/deleting-packages.md) directiva.</span><span class="sxs-lookup"><span data-stu-id="0d6db-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="0d6db-159">Otras implementaciones del servidor son gratuitos para interpretar esta señal como una eliminación de disco duro, eliminar temporalmente u ocultar.</span><span class="sxs-lookup"><span data-stu-id="0d6db-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="0d6db-160">Por ejemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (una implementación de servidor sólo admite la API V2 anteriores) es compatible con esta solicitud de control como un unlist o una eliminación de disco duro en función de una opción de configuración.</span><span class="sxs-lookup"><span data-stu-id="0d6db-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="0d6db-161">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="0d6db-161">Request parameters</span></span>

<span data-ttu-id="0d6db-162">nombre</span><span class="sxs-lookup"><span data-stu-id="0d6db-162">Name</span></span>           | <span data-ttu-id="0d6db-163">En</span><span class="sxs-lookup"><span data-stu-id="0d6db-163">In</span></span>     | <span data-ttu-id="0d6db-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d6db-164">Type</span></span>   | <span data-ttu-id="0d6db-165">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0d6db-165">Required</span></span> | <span data-ttu-id="0d6db-166">Notas</span><span class="sxs-lookup"><span data-stu-id="0d6db-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="0d6db-167">Id.</span><span class="sxs-lookup"><span data-stu-id="0d6db-167">ID</span></span>             | <span data-ttu-id="0d6db-168">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="0d6db-168">URL</span></span>    | <span data-ttu-id="0d6db-169">cadena</span><span class="sxs-lookup"><span data-stu-id="0d6db-169">string</span></span> | <span data-ttu-id="0d6db-170">sí</span><span class="sxs-lookup"><span data-stu-id="0d6db-170">yes</span></span>      | <span data-ttu-id="0d6db-171">El identificador del paquete para eliminar</span><span class="sxs-lookup"><span data-stu-id="0d6db-171">The ID of the package to delete</span></span>
<span data-ttu-id="0d6db-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="0d6db-172">VERSION</span></span>        | <span data-ttu-id="0d6db-173">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="0d6db-173">URL</span></span>    | <span data-ttu-id="0d6db-174">cadena</span><span class="sxs-lookup"><span data-stu-id="0d6db-174">string</span></span> | <span data-ttu-id="0d6db-175">sí</span><span class="sxs-lookup"><span data-stu-id="0d6db-175">yes</span></span>      | <span data-ttu-id="0d6db-176">La versión del paquete que se va a eliminar</span><span class="sxs-lookup"><span data-stu-id="0d6db-176">The version of the package to delete</span></span>
<span data-ttu-id="0d6db-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="0d6db-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="0d6db-178">Header</span><span class="sxs-lookup"><span data-stu-id="0d6db-178">Header</span></span> | <span data-ttu-id="0d6db-179">cadena</span><span class="sxs-lookup"><span data-stu-id="0d6db-179">string</span></span> | <span data-ttu-id="0d6db-180">sí</span><span class="sxs-lookup"><span data-stu-id="0d6db-180">yes</span></span>      | <span data-ttu-id="0d6db-181">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="0d6db-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="0d6db-182">Respuesta</span><span class="sxs-lookup"><span data-stu-id="0d6db-182">Response</span></span>

<span data-ttu-id="0d6db-183">Código de estado</span><span class="sxs-lookup"><span data-stu-id="0d6db-183">Status Code</span></span> | <span data-ttu-id="0d6db-184">Significado</span><span class="sxs-lookup"><span data-stu-id="0d6db-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="0d6db-185">204</span><span class="sxs-lookup"><span data-stu-id="0d6db-185">204</span></span>         | <span data-ttu-id="0d6db-186">Se eliminó el paquete</span><span class="sxs-lookup"><span data-stu-id="0d6db-186">The package was deleted</span></span>
<span data-ttu-id="0d6db-187">404</span><span class="sxs-lookup"><span data-stu-id="0d6db-187">404</span></span>         | <span data-ttu-id="0d6db-188">Ningún paquete con proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="0d6db-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="0d6db-189">Poner un paquete</span><span class="sxs-lookup"><span data-stu-id="0d6db-189">Relist a package</span></span>

<span data-ttu-id="0d6db-190">Si un paquete se dados de baja, es posible hacer que el paquete una vez más visible en los resultados de búsqueda con el punto de conexión de "poner en".</span><span class="sxs-lookup"><span data-stu-id="0d6db-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="0d6db-191">Este punto de conexión tiene la misma forma que la [eliminar (ocultar) extremo](#delete-a-package) pero usa el `POST` método HTTP en lugar de la `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="0d6db-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="0d6db-192">Si el paquete ya está disponible, la solicitud se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="0d6db-192">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="0d6db-193">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="0d6db-193">Request parameters</span></span>

<span data-ttu-id="0d6db-194">nombre</span><span class="sxs-lookup"><span data-stu-id="0d6db-194">Name</span></span>           | <span data-ttu-id="0d6db-195">En</span><span class="sxs-lookup"><span data-stu-id="0d6db-195">In</span></span>     | <span data-ttu-id="0d6db-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d6db-196">Type</span></span>   | <span data-ttu-id="0d6db-197">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0d6db-197">Required</span></span> | <span data-ttu-id="0d6db-198">Notas</span><span class="sxs-lookup"><span data-stu-id="0d6db-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="0d6db-199">Id.</span><span class="sxs-lookup"><span data-stu-id="0d6db-199">ID</span></span>             | <span data-ttu-id="0d6db-200">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="0d6db-200">URL</span></span>    | <span data-ttu-id="0d6db-201">cadena</span><span class="sxs-lookup"><span data-stu-id="0d6db-201">string</span></span> | <span data-ttu-id="0d6db-202">sí</span><span class="sxs-lookup"><span data-stu-id="0d6db-202">yes</span></span>      | <span data-ttu-id="0d6db-203">El identificador del paquete a poner en venta</span><span class="sxs-lookup"><span data-stu-id="0d6db-203">The ID of the package to relist</span></span>
<span data-ttu-id="0d6db-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="0d6db-204">VERSION</span></span>        | <span data-ttu-id="0d6db-205">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="0d6db-205">URL</span></span>    | <span data-ttu-id="0d6db-206">cadena</span><span class="sxs-lookup"><span data-stu-id="0d6db-206">string</span></span> | <span data-ttu-id="0d6db-207">sí</span><span class="sxs-lookup"><span data-stu-id="0d6db-207">yes</span></span>      | <span data-ttu-id="0d6db-208">La versión del paquete que se va a poner en venta</span><span class="sxs-lookup"><span data-stu-id="0d6db-208">The version of the package to relist</span></span>
<span data-ttu-id="0d6db-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="0d6db-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="0d6db-210">Header</span><span class="sxs-lookup"><span data-stu-id="0d6db-210">Header</span></span> | <span data-ttu-id="0d6db-211">cadena</span><span class="sxs-lookup"><span data-stu-id="0d6db-211">string</span></span> | <span data-ttu-id="0d6db-212">sí</span><span class="sxs-lookup"><span data-stu-id="0d6db-212">yes</span></span>      | <span data-ttu-id="0d6db-213">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="0d6db-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="0d6db-214">Respuesta</span><span class="sxs-lookup"><span data-stu-id="0d6db-214">Response</span></span>

<span data-ttu-id="0d6db-215">Código de estado</span><span class="sxs-lookup"><span data-stu-id="0d6db-215">Status Code</span></span> | <span data-ttu-id="0d6db-216">Significado</span><span class="sxs-lookup"><span data-stu-id="0d6db-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="0d6db-217">200</span><span class="sxs-lookup"><span data-stu-id="0d6db-217">200</span></span>         | <span data-ttu-id="0d6db-218">El paquete aparece ahora</span><span class="sxs-lookup"><span data-stu-id="0d6db-218">The package is now listed</span></span>
<span data-ttu-id="0d6db-219">404</span><span class="sxs-lookup"><span data-stu-id="0d6db-219">404</span></span>         | <span data-ttu-id="0d6db-220">Ningún paquete con proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="0d6db-220">No package with the provided `ID` and `VERSION` exists</span></span>
