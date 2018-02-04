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
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="5fbac-104">Insertar y eliminar</span><span class="sxs-lookup"><span data-stu-id="5fbac-104">Push and Delete</span></span>

<span data-ttu-id="5fbac-105">Es posible insertar, eliminar (ni ocultar, dependiendo de la implementación de servidor) y poner los paquetes mediante la API V3 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="5fbac-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="5fbac-106">Estas operaciones se basan en el `PackagePublish` recurso se encuentra en la [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5fbac-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5fbac-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="5fbac-107">Versioning</span></span>

<span data-ttu-id="5fbac-108">El siguiente `@type` valor se utiliza:</span><span class="sxs-lookup"><span data-stu-id="5fbac-108">The following `@type` value is used:</span></span>

<span data-ttu-id="5fbac-109">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="5fbac-109">@type value</span></span>          | <span data-ttu-id="5fbac-110">Notas</span><span class="sxs-lookup"><span data-stu-id="5fbac-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="5fbac-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="5fbac-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="5fbac-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="5fbac-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="5fbac-113">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="5fbac-113">Base URL</span></span>

<span data-ttu-id="5fbac-114">La dirección URL base para las API siguientes es el valor de la `@id` propiedad de la `PackagePublish/2.0.0` recursos en el origen de paquete [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5fbac-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="5fbac-115">Para obtener la documentación siguiente, se utiliza la dirección URL de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5fbac-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="5fbac-116">Considere la posibilidad de `https://www.nuget.org/api/v2/package` como un marcador de posición para el `@id` valor se encuentra en el índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="5fbac-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="5fbac-117">Tenga en cuenta que esta dirección URL señala a la misma ubicación que el extremo de inserción V2 heredado como el protocolo es el mismo.</span><span class="sxs-lookup"><span data-stu-id="5fbac-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5fbac-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="5fbac-118">HTTP methods</span></span>

<span data-ttu-id="5fbac-119">El `PUT`, `POST` y `DELETE` métodos HTTP son compatibles con este recurso.</span><span class="sxs-lookup"><span data-stu-id="5fbac-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="5fbac-120">Para los métodos que se admiten en cada punto de conexión, consulte a continuación.</span><span class="sxs-lookup"><span data-stu-id="5fbac-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="5fbac-121">Insertar un paquete</span><span class="sxs-lookup"><span data-stu-id="5fbac-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="5fbac-122">tiene NuGet.org [requisitos adicionales](NuGet-Protocols.md) para interactuar con el punto de conexión de inserción.</span><span class="sxs-lookup"><span data-stu-id="5fbac-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="5fbac-123">NuGet.org admite la inserción de nuevos paquetes mediante la siguiente API.</span><span class="sxs-lookup"><span data-stu-id="5fbac-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="5fbac-124">Si ya existe el paquete con el identificador y la versión proporcionada, nuget.org rechazará la inserción.</span><span class="sxs-lookup"><span data-stu-id="5fbac-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="5fbac-125">Otros orígenes de paquetes pueden admitir reemplazando un paquete existente.</span><span class="sxs-lookup"><span data-stu-id="5fbac-125">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="5fbac-126">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="5fbac-126">Request parameters</span></span>

<span data-ttu-id="5fbac-127">nombre</span><span class="sxs-lookup"><span data-stu-id="5fbac-127">Name</span></span>           | <span data-ttu-id="5fbac-128">En</span><span class="sxs-lookup"><span data-stu-id="5fbac-128">In</span></span>     | <span data-ttu-id="5fbac-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="5fbac-129">Type</span></span>   | <span data-ttu-id="5fbac-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5fbac-130">Required</span></span> | <span data-ttu-id="5fbac-131">Notas</span><span class="sxs-lookup"><span data-stu-id="5fbac-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5fbac-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5fbac-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5fbac-133">Header</span><span class="sxs-lookup"><span data-stu-id="5fbac-133">Header</span></span> | <span data-ttu-id="5fbac-134">cadena</span><span class="sxs-lookup"><span data-stu-id="5fbac-134">string</span></span> | <span data-ttu-id="5fbac-135">sí</span><span class="sxs-lookup"><span data-stu-id="5fbac-135">yes</span></span>      | <span data-ttu-id="5fbac-136">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="5fbac-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="5fbac-137">La clave de API es una cadena opaca recibido desde el origen del paquete por el usuario y configurado en el cliente.</span><span class="sxs-lookup"><span data-stu-id="5fbac-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="5fbac-138">Ningún formato de cadena determinada es obligatoria, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores de encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="5fbac-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="5fbac-139">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="5fbac-139">Request body</span></span>

<span data-ttu-id="5fbac-140">El cuerpo de solicitud debe proceder de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="5fbac-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="5fbac-141">Datos de formulario de varias partes</span><span class="sxs-lookup"><span data-stu-id="5fbac-141">Multipart form data</span></span>

<span data-ttu-id="5fbac-142">El encabezado de solicitud `Content-Type` es `multipart/form-data` y el primer elemento en el cuerpo de solicitud es los bytes sin formato de la .nupkg que se va a insertar.</span><span class="sxs-lookup"><span data-stu-id="5fbac-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="5fbac-143">Se omiten los elementos siguientes en el cuerpo de varias partes.</span><span class="sxs-lookup"><span data-stu-id="5fbac-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="5fbac-144">Se omite el nombre de archivo o cualquier otro encabezado de los elementos de varias partes.</span><span class="sxs-lookup"><span data-stu-id="5fbac-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="5fbac-145">Respuesta</span><span class="sxs-lookup"><span data-stu-id="5fbac-145">Response</span></span>

<span data-ttu-id="5fbac-146">Código de estado</span><span class="sxs-lookup"><span data-stu-id="5fbac-146">Status Code</span></span> | <span data-ttu-id="5fbac-147">Significado</span><span class="sxs-lookup"><span data-stu-id="5fbac-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="5fbac-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="5fbac-148">201, 202</span></span>    | <span data-ttu-id="5fbac-149">El paquete se ha insertado correctamente</span><span class="sxs-lookup"><span data-stu-id="5fbac-149">The package was successfully pushed</span></span>
<span data-ttu-id="5fbac-150">400</span><span class="sxs-lookup"><span data-stu-id="5fbac-150">400</span></span>         | <span data-ttu-id="5fbac-151">El paquete proporcionado no es válido</span><span class="sxs-lookup"><span data-stu-id="5fbac-151">The provided package is invalid</span></span>
<span data-ttu-id="5fbac-152">409</span><span class="sxs-lookup"><span data-stu-id="5fbac-152">409</span></span>         | <span data-ttu-id="5fbac-153">Ya existe un paquete con el identificador proporcionado y la versión</span><span class="sxs-lookup"><span data-stu-id="5fbac-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="5fbac-154">Las implementaciones de servidor varían en el código de estado correcto devuelto cuando un paquete se envíe correctamente.</span><span class="sxs-lookup"><span data-stu-id="5fbac-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="5fbac-155">Eliminar un paquete</span><span class="sxs-lookup"><span data-stu-id="5fbac-155">Delete a package</span></span>

<span data-ttu-id="5fbac-156">NuGet.org interpreta la solicitud de eliminación de paquete como un "Ocultar".</span><span class="sxs-lookup"><span data-stu-id="5fbac-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="5fbac-157">Esto significa que el paquete sigue estando disponible para los usuarios existentes del paquete, pero el paquete ya no aparece en los resultados de la búsqueda o en la interfaz web.</span><span class="sxs-lookup"><span data-stu-id="5fbac-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="5fbac-158">Para obtener más información acerca de este procedimiento, consulte la [eliminar paquetes](../policies/deleting-packages.md) directiva.</span><span class="sxs-lookup"><span data-stu-id="5fbac-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="5fbac-159">Otras implementaciones del servidor son gratuitos para interpretar esta señal como una eliminación de disco duro, eliminar temporalmente u ocultar.</span><span class="sxs-lookup"><span data-stu-id="5fbac-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="5fbac-160">Por ejemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (una implementación de servidor sólo admite la API V2 anteriores) es compatible con esta solicitud de control como un unlist o una eliminación de disco duro en función de una opción de configuración.</span><span class="sxs-lookup"><span data-stu-id="5fbac-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="5fbac-161">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="5fbac-161">Request parameters</span></span>

<span data-ttu-id="5fbac-162">nombre</span><span class="sxs-lookup"><span data-stu-id="5fbac-162">Name</span></span>           | <span data-ttu-id="5fbac-163">En</span><span class="sxs-lookup"><span data-stu-id="5fbac-163">In</span></span>     | <span data-ttu-id="5fbac-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="5fbac-164">Type</span></span>   | <span data-ttu-id="5fbac-165">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5fbac-165">Required</span></span> | <span data-ttu-id="5fbac-166">Notas</span><span class="sxs-lookup"><span data-stu-id="5fbac-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5fbac-167">Id.</span><span class="sxs-lookup"><span data-stu-id="5fbac-167">ID</span></span>             | <span data-ttu-id="5fbac-168">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="5fbac-168">URL</span></span>    | <span data-ttu-id="5fbac-169">cadena</span><span class="sxs-lookup"><span data-stu-id="5fbac-169">string</span></span> | <span data-ttu-id="5fbac-170">sí</span><span class="sxs-lookup"><span data-stu-id="5fbac-170">yes</span></span>      | <span data-ttu-id="5fbac-171">El identificador del paquete para eliminar</span><span class="sxs-lookup"><span data-stu-id="5fbac-171">The ID of the package to delete</span></span>
<span data-ttu-id="5fbac-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="5fbac-172">VERSION</span></span>        | <span data-ttu-id="5fbac-173">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="5fbac-173">URL</span></span>    | <span data-ttu-id="5fbac-174">cadena</span><span class="sxs-lookup"><span data-stu-id="5fbac-174">string</span></span> | <span data-ttu-id="5fbac-175">sí</span><span class="sxs-lookup"><span data-stu-id="5fbac-175">yes</span></span>      | <span data-ttu-id="5fbac-176">La versión del paquete que se va a eliminar</span><span class="sxs-lookup"><span data-stu-id="5fbac-176">The version of the package to delete</span></span>
<span data-ttu-id="5fbac-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5fbac-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5fbac-178">Header</span><span class="sxs-lookup"><span data-stu-id="5fbac-178">Header</span></span> | <span data-ttu-id="5fbac-179">cadena</span><span class="sxs-lookup"><span data-stu-id="5fbac-179">string</span></span> | <span data-ttu-id="5fbac-180">sí</span><span class="sxs-lookup"><span data-stu-id="5fbac-180">yes</span></span>      | <span data-ttu-id="5fbac-181">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="5fbac-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="5fbac-182">Respuesta</span><span class="sxs-lookup"><span data-stu-id="5fbac-182">Response</span></span>

<span data-ttu-id="5fbac-183">Código de estado</span><span class="sxs-lookup"><span data-stu-id="5fbac-183">Status Code</span></span> | <span data-ttu-id="5fbac-184">Significado</span><span class="sxs-lookup"><span data-stu-id="5fbac-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="5fbac-185">204</span><span class="sxs-lookup"><span data-stu-id="5fbac-185">204</span></span>         | <span data-ttu-id="5fbac-186">Se eliminó el paquete</span><span class="sxs-lookup"><span data-stu-id="5fbac-186">The package was deleted</span></span>
<span data-ttu-id="5fbac-187">404</span><span class="sxs-lookup"><span data-stu-id="5fbac-187">404</span></span>         | <span data-ttu-id="5fbac-188">Ningún paquete con proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="5fbac-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="5fbac-189">Poner un paquete</span><span class="sxs-lookup"><span data-stu-id="5fbac-189">Relist a package</span></span>

<span data-ttu-id="5fbac-190">Si un paquete se dados de baja, es posible hacer que el paquete una vez más visible en los resultados de búsqueda con el punto de conexión de "poner en".</span><span class="sxs-lookup"><span data-stu-id="5fbac-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="5fbac-191">Este punto de conexión tiene la misma forma que la [eliminar (ocultar) extremo](#delete-a-package) pero usa el `POST` método HTTP en lugar de la `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="5fbac-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="5fbac-192">Si el paquete ya está disponible, la solicitud se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="5fbac-192">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="5fbac-193">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="5fbac-193">Request parameters</span></span>

<span data-ttu-id="5fbac-194">nombre</span><span class="sxs-lookup"><span data-stu-id="5fbac-194">Name</span></span>           | <span data-ttu-id="5fbac-195">En</span><span class="sxs-lookup"><span data-stu-id="5fbac-195">In</span></span>     | <span data-ttu-id="5fbac-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="5fbac-196">Type</span></span>   | <span data-ttu-id="5fbac-197">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5fbac-197">Required</span></span> | <span data-ttu-id="5fbac-198">Notas</span><span class="sxs-lookup"><span data-stu-id="5fbac-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5fbac-199">Id.</span><span class="sxs-lookup"><span data-stu-id="5fbac-199">ID</span></span>             | <span data-ttu-id="5fbac-200">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="5fbac-200">URL</span></span>    | <span data-ttu-id="5fbac-201">cadena</span><span class="sxs-lookup"><span data-stu-id="5fbac-201">string</span></span> | <span data-ttu-id="5fbac-202">sí</span><span class="sxs-lookup"><span data-stu-id="5fbac-202">yes</span></span>      | <span data-ttu-id="5fbac-203">El identificador del paquete a poner en venta</span><span class="sxs-lookup"><span data-stu-id="5fbac-203">The ID of the package to relist</span></span>
<span data-ttu-id="5fbac-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="5fbac-204">VERSION</span></span>        | <span data-ttu-id="5fbac-205">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="5fbac-205">URL</span></span>    | <span data-ttu-id="5fbac-206">cadena</span><span class="sxs-lookup"><span data-stu-id="5fbac-206">string</span></span> | <span data-ttu-id="5fbac-207">sí</span><span class="sxs-lookup"><span data-stu-id="5fbac-207">yes</span></span>      | <span data-ttu-id="5fbac-208">La versión del paquete que se va a poner en venta</span><span class="sxs-lookup"><span data-stu-id="5fbac-208">The version of the package to relist</span></span>
<span data-ttu-id="5fbac-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5fbac-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5fbac-210">Header</span><span class="sxs-lookup"><span data-stu-id="5fbac-210">Header</span></span> | <span data-ttu-id="5fbac-211">cadena</span><span class="sxs-lookup"><span data-stu-id="5fbac-211">string</span></span> | <span data-ttu-id="5fbac-212">sí</span><span class="sxs-lookup"><span data-stu-id="5fbac-212">yes</span></span>      | <span data-ttu-id="5fbac-213">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="5fbac-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="5fbac-214">Respuesta</span><span class="sxs-lookup"><span data-stu-id="5fbac-214">Response</span></span>

<span data-ttu-id="5fbac-215">Código de estado</span><span class="sxs-lookup"><span data-stu-id="5fbac-215">Status Code</span></span> | <span data-ttu-id="5fbac-216">Significado</span><span class="sxs-lookup"><span data-stu-id="5fbac-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="5fbac-217">200</span><span class="sxs-lookup"><span data-stu-id="5fbac-217">200</span></span>         | <span data-ttu-id="5fbac-218">El paquete aparece ahora</span><span class="sxs-lookup"><span data-stu-id="5fbac-218">The package is now listed</span></span>
<span data-ttu-id="5fbac-219">404</span><span class="sxs-lookup"><span data-stu-id="5fbac-219">404</span></span>         | <span data-ttu-id="5fbac-220">Ningún paquete con proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="5fbac-220">No package with the provided `ID` and `VERSION` exists</span></span>
