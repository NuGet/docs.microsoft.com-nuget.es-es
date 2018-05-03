---
title: Insertar y eliminar, NuGet API
description: El servicio de publicación permite a los clientes publicar nuevos paquetes y ocultar o eliminar los paquetes existentes.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="34a2f-103">Insertar y eliminar</span><span class="sxs-lookup"><span data-stu-id="34a2f-103">Push and Delete</span></span>

<span data-ttu-id="34a2f-104">Es posible insertar, eliminar (ni ocultar, dependiendo de la implementación de servidor) y poner los paquetes mediante la API V3 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="34a2f-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="34a2f-105">Estas operaciones se basan en el `PackagePublish` recurso se encuentra en la [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="34a2f-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="34a2f-106">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="34a2f-106">Versioning</span></span>

<span data-ttu-id="34a2f-107">El siguiente `@type` valor se utiliza:</span><span class="sxs-lookup"><span data-stu-id="34a2f-107">The following `@type` value is used:</span></span>

<span data-ttu-id="34a2f-108">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="34a2f-108">@type value</span></span>          | <span data-ttu-id="34a2f-109">Notas</span><span class="sxs-lookup"><span data-stu-id="34a2f-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="34a2f-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="34a2f-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="34a2f-111">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="34a2f-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="34a2f-112">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="34a2f-112">Base URL</span></span>

<span data-ttu-id="34a2f-113">La dirección URL base para las API siguientes es el valor de la `@id` propiedad de la `PackagePublish/2.0.0` recursos en el origen de paquete [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="34a2f-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="34a2f-114">Para obtener la documentación siguiente, se utiliza la dirección URL de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="34a2f-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="34a2f-115">Considere la posibilidad de `https://www.nuget.org/api/v2/package` como un marcador de posición para el `@id` valor se encuentra en el índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="34a2f-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="34a2f-116">Tenga en cuenta que esta dirección URL señala a la misma ubicación que el extremo de inserción V2 heredado como el protocolo es el mismo.</span><span class="sxs-lookup"><span data-stu-id="34a2f-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="34a2f-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="34a2f-117">HTTP methods</span></span>

<span data-ttu-id="34a2f-118">El `PUT`, `POST` y `DELETE` métodos HTTP son compatibles con este recurso.</span><span class="sxs-lookup"><span data-stu-id="34a2f-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="34a2f-119">Para los métodos que se admiten en cada punto de conexión, consulte a continuación.</span><span class="sxs-lookup"><span data-stu-id="34a2f-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="34a2f-120">Insertar un paquete</span><span class="sxs-lookup"><span data-stu-id="34a2f-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="34a2f-121">tiene NuGet.org [requisitos adicionales](NuGet-Protocols.md) para interactuar con el punto de conexión de inserción.</span><span class="sxs-lookup"><span data-stu-id="34a2f-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="34a2f-122">NuGet.org admite la inserción de nuevos paquetes mediante la siguiente API.</span><span class="sxs-lookup"><span data-stu-id="34a2f-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="34a2f-123">Si ya existe el paquete con el identificador y la versión proporcionada, nuget.org rechazará la inserción.</span><span class="sxs-lookup"><span data-stu-id="34a2f-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="34a2f-124">Otros orígenes de paquetes pueden admitir reemplazando un paquete existente.</span><span class="sxs-lookup"><span data-stu-id="34a2f-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="34a2f-125">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="34a2f-125">Request parameters</span></span>

<span data-ttu-id="34a2f-126">nombre</span><span class="sxs-lookup"><span data-stu-id="34a2f-126">Name</span></span>           | <span data-ttu-id="34a2f-127">En</span><span class="sxs-lookup"><span data-stu-id="34a2f-127">In</span></span>     | <span data-ttu-id="34a2f-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="34a2f-128">Type</span></span>   | <span data-ttu-id="34a2f-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="34a2f-129">Required</span></span> | <span data-ttu-id="34a2f-130">Notas</span><span class="sxs-lookup"><span data-stu-id="34a2f-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="34a2f-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="34a2f-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="34a2f-132">Header</span><span class="sxs-lookup"><span data-stu-id="34a2f-132">Header</span></span> | <span data-ttu-id="34a2f-133">cadena</span><span class="sxs-lookup"><span data-stu-id="34a2f-133">string</span></span> | <span data-ttu-id="34a2f-134">sí</span><span class="sxs-lookup"><span data-stu-id="34a2f-134">yes</span></span>      | <span data-ttu-id="34a2f-135">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="34a2f-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="34a2f-136">La clave de API es una cadena opaca recibido desde el origen del paquete por el usuario y configurado en el cliente.</span><span class="sxs-lookup"><span data-stu-id="34a2f-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="34a2f-137">Ningún formato de cadena determinada es obligatoria, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores de encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="34a2f-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="34a2f-138">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="34a2f-138">Request body</span></span>

<span data-ttu-id="34a2f-139">El cuerpo de solicitud debe proceder de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="34a2f-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="34a2f-140">Datos de formulario de varias partes</span><span class="sxs-lookup"><span data-stu-id="34a2f-140">Multipart form data</span></span>

<span data-ttu-id="34a2f-141">El encabezado de solicitud `Content-Type` es `multipart/form-data` y el primer elemento en el cuerpo de solicitud es los bytes sin formato de la .nupkg que se va a insertar.</span><span class="sxs-lookup"><span data-stu-id="34a2f-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="34a2f-142">Se omiten los elementos siguientes en el cuerpo de varias partes.</span><span class="sxs-lookup"><span data-stu-id="34a2f-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="34a2f-143">Se omite el nombre de archivo o cualquier otro encabezado de los elementos de varias partes.</span><span class="sxs-lookup"><span data-stu-id="34a2f-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="34a2f-144">Respuesta</span><span class="sxs-lookup"><span data-stu-id="34a2f-144">Response</span></span>

<span data-ttu-id="34a2f-145">Código de estado</span><span class="sxs-lookup"><span data-stu-id="34a2f-145">Status Code</span></span> | <span data-ttu-id="34a2f-146">Significado</span><span class="sxs-lookup"><span data-stu-id="34a2f-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="34a2f-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="34a2f-147">201, 202</span></span>    | <span data-ttu-id="34a2f-148">El paquete se ha insertado correctamente</span><span class="sxs-lookup"><span data-stu-id="34a2f-148">The package was successfully pushed</span></span>
<span data-ttu-id="34a2f-149">400</span><span class="sxs-lookup"><span data-stu-id="34a2f-149">400</span></span>         | <span data-ttu-id="34a2f-150">El paquete proporcionado no es válido</span><span class="sxs-lookup"><span data-stu-id="34a2f-150">The provided package is invalid</span></span>
<span data-ttu-id="34a2f-151">409</span><span class="sxs-lookup"><span data-stu-id="34a2f-151">409</span></span>         | <span data-ttu-id="34a2f-152">Ya existe un paquete con el identificador proporcionado y la versión</span><span class="sxs-lookup"><span data-stu-id="34a2f-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="34a2f-153">Las implementaciones de servidor varían en el código de estado correcto devuelto cuando un paquete se envíe correctamente.</span><span class="sxs-lookup"><span data-stu-id="34a2f-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="34a2f-154">Eliminar un paquete</span><span class="sxs-lookup"><span data-stu-id="34a2f-154">Delete a package</span></span>

<span data-ttu-id="34a2f-155">NuGet.org interpreta la solicitud de eliminación de paquete como un "Ocultar".</span><span class="sxs-lookup"><span data-stu-id="34a2f-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="34a2f-156">Esto significa que el paquete sigue estando disponible para los usuarios existentes del paquete, pero el paquete ya no aparece en los resultados de la búsqueda o en la interfaz web.</span><span class="sxs-lookup"><span data-stu-id="34a2f-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="34a2f-157">Para obtener más información acerca de este procedimiento, consulte la [eliminar paquetes](../policies/deleting-packages.md) directiva.</span><span class="sxs-lookup"><span data-stu-id="34a2f-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="34a2f-158">Otras implementaciones del servidor son gratuitos para interpretar esta señal como una eliminación de disco duro, eliminar temporalmente u ocultar.</span><span class="sxs-lookup"><span data-stu-id="34a2f-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="34a2f-159">Por ejemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (una implementación de servidor sólo admite la API V2 anteriores) es compatible con esta solicitud de control como un unlist o una eliminación de disco duro en función de una opción de configuración.</span><span class="sxs-lookup"><span data-stu-id="34a2f-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="34a2f-160">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="34a2f-160">Request parameters</span></span>

<span data-ttu-id="34a2f-161">nombre</span><span class="sxs-lookup"><span data-stu-id="34a2f-161">Name</span></span>           | <span data-ttu-id="34a2f-162">En</span><span class="sxs-lookup"><span data-stu-id="34a2f-162">In</span></span>     | <span data-ttu-id="34a2f-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="34a2f-163">Type</span></span>   | <span data-ttu-id="34a2f-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="34a2f-164">Required</span></span> | <span data-ttu-id="34a2f-165">Notas</span><span class="sxs-lookup"><span data-stu-id="34a2f-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="34a2f-166">Id.</span><span class="sxs-lookup"><span data-stu-id="34a2f-166">ID</span></span>             | <span data-ttu-id="34a2f-167">Resolución</span><span class="sxs-lookup"><span data-stu-id="34a2f-167">URL</span></span>    | <span data-ttu-id="34a2f-168">cadena</span><span class="sxs-lookup"><span data-stu-id="34a2f-168">string</span></span> | <span data-ttu-id="34a2f-169">sí</span><span class="sxs-lookup"><span data-stu-id="34a2f-169">yes</span></span>      | <span data-ttu-id="34a2f-170">El identificador del paquete para eliminar</span><span class="sxs-lookup"><span data-stu-id="34a2f-170">The ID of the package to delete</span></span>
<span data-ttu-id="34a2f-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="34a2f-171">VERSION</span></span>        | <span data-ttu-id="34a2f-172">Resolución</span><span class="sxs-lookup"><span data-stu-id="34a2f-172">URL</span></span>    | <span data-ttu-id="34a2f-173">cadena</span><span class="sxs-lookup"><span data-stu-id="34a2f-173">string</span></span> | <span data-ttu-id="34a2f-174">sí</span><span class="sxs-lookup"><span data-stu-id="34a2f-174">yes</span></span>      | <span data-ttu-id="34a2f-175">La versión del paquete que se va a eliminar</span><span class="sxs-lookup"><span data-stu-id="34a2f-175">The version of the package to delete</span></span>
<span data-ttu-id="34a2f-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="34a2f-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="34a2f-177">Header</span><span class="sxs-lookup"><span data-stu-id="34a2f-177">Header</span></span> | <span data-ttu-id="34a2f-178">cadena</span><span class="sxs-lookup"><span data-stu-id="34a2f-178">string</span></span> | <span data-ttu-id="34a2f-179">sí</span><span class="sxs-lookup"><span data-stu-id="34a2f-179">yes</span></span>      | <span data-ttu-id="34a2f-180">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="34a2f-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="34a2f-181">Respuesta</span><span class="sxs-lookup"><span data-stu-id="34a2f-181">Response</span></span>

<span data-ttu-id="34a2f-182">Código de estado</span><span class="sxs-lookup"><span data-stu-id="34a2f-182">Status Code</span></span> | <span data-ttu-id="34a2f-183">Significado</span><span class="sxs-lookup"><span data-stu-id="34a2f-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="34a2f-184">204</span><span class="sxs-lookup"><span data-stu-id="34a2f-184">204</span></span>         | <span data-ttu-id="34a2f-185">Se eliminó el paquete</span><span class="sxs-lookup"><span data-stu-id="34a2f-185">The package was deleted</span></span>
<span data-ttu-id="34a2f-186">404</span><span class="sxs-lookup"><span data-stu-id="34a2f-186">404</span></span>         | <span data-ttu-id="34a2f-187">Ningún paquete con proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="34a2f-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="34a2f-188">Poner un paquete</span><span class="sxs-lookup"><span data-stu-id="34a2f-188">Relist a package</span></span>

<span data-ttu-id="34a2f-189">Si un paquete se dados de baja, es posible hacer que el paquete una vez más visible en los resultados de búsqueda con el punto de conexión de "poner en".</span><span class="sxs-lookup"><span data-stu-id="34a2f-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="34a2f-190">Este punto de conexión tiene la misma forma que la [eliminar (ocultar) extremo](#delete-a-package) pero usa el `POST` método HTTP en lugar de la `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="34a2f-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="34a2f-191">Si el paquete ya está disponible, la solicitud se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="34a2f-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="34a2f-192">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="34a2f-192">Request parameters</span></span>

<span data-ttu-id="34a2f-193">nombre</span><span class="sxs-lookup"><span data-stu-id="34a2f-193">Name</span></span>           | <span data-ttu-id="34a2f-194">En</span><span class="sxs-lookup"><span data-stu-id="34a2f-194">In</span></span>     | <span data-ttu-id="34a2f-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="34a2f-195">Type</span></span>   | <span data-ttu-id="34a2f-196">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="34a2f-196">Required</span></span> | <span data-ttu-id="34a2f-197">Notas</span><span class="sxs-lookup"><span data-stu-id="34a2f-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="34a2f-198">Id.</span><span class="sxs-lookup"><span data-stu-id="34a2f-198">ID</span></span>             | <span data-ttu-id="34a2f-199">Resolución</span><span class="sxs-lookup"><span data-stu-id="34a2f-199">URL</span></span>    | <span data-ttu-id="34a2f-200">cadena</span><span class="sxs-lookup"><span data-stu-id="34a2f-200">string</span></span> | <span data-ttu-id="34a2f-201">sí</span><span class="sxs-lookup"><span data-stu-id="34a2f-201">yes</span></span>      | <span data-ttu-id="34a2f-202">El identificador del paquete a poner en venta</span><span class="sxs-lookup"><span data-stu-id="34a2f-202">The ID of the package to relist</span></span>
<span data-ttu-id="34a2f-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="34a2f-203">VERSION</span></span>        | <span data-ttu-id="34a2f-204">Resolución</span><span class="sxs-lookup"><span data-stu-id="34a2f-204">URL</span></span>    | <span data-ttu-id="34a2f-205">cadena</span><span class="sxs-lookup"><span data-stu-id="34a2f-205">string</span></span> | <span data-ttu-id="34a2f-206">sí</span><span class="sxs-lookup"><span data-stu-id="34a2f-206">yes</span></span>      | <span data-ttu-id="34a2f-207">La versión del paquete que se va a poner en venta</span><span class="sxs-lookup"><span data-stu-id="34a2f-207">The version of the package to relist</span></span>
<span data-ttu-id="34a2f-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="34a2f-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="34a2f-209">Header</span><span class="sxs-lookup"><span data-stu-id="34a2f-209">Header</span></span> | <span data-ttu-id="34a2f-210">cadena</span><span class="sxs-lookup"><span data-stu-id="34a2f-210">string</span></span> | <span data-ttu-id="34a2f-211">sí</span><span class="sxs-lookup"><span data-stu-id="34a2f-211">yes</span></span>      | <span data-ttu-id="34a2f-212">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="34a2f-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="34a2f-213">Respuesta</span><span class="sxs-lookup"><span data-stu-id="34a2f-213">Response</span></span>

<span data-ttu-id="34a2f-214">Código de estado</span><span class="sxs-lookup"><span data-stu-id="34a2f-214">Status Code</span></span> | <span data-ttu-id="34a2f-215">Significado</span><span class="sxs-lookup"><span data-stu-id="34a2f-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="34a2f-216">200</span><span class="sxs-lookup"><span data-stu-id="34a2f-216">200</span></span>         | <span data-ttu-id="34a2f-217">El paquete aparece ahora</span><span class="sxs-lookup"><span data-stu-id="34a2f-217">The package is now listed</span></span>
<span data-ttu-id="34a2f-218">404</span><span class="sxs-lookup"><span data-stu-id="34a2f-218">404</span></span>         | <span data-ttu-id="34a2f-219">Ningún paquete con proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="34a2f-219">No package with the provided `ID` and `VERSION` exists</span></span>
