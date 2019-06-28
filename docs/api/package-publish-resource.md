---
title: Inserción y eliminación, la API de NuGet
description: El servicio de publicación permite a los clientes publicar nuevos paquetes y quitar de la lista o elimine los paquetes existentes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426724"
---
# <a name="push-and-delete"></a><span data-ttu-id="ee125-103">Inserción y eliminación</span><span class="sxs-lookup"><span data-stu-id="ee125-103">Push and Delete</span></span>

<span data-ttu-id="ee125-104">Es posible insertar, eliminar (o quitar de la lista, dependiendo de la implementación de servidor) y poner los paquetes mediante la API de NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="ee125-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="ee125-105">Estas operaciones se basa en el `PackagePublish` encontrar el recurso en el [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ee125-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ee125-106">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="ee125-106">Versioning</span></span>

<span data-ttu-id="ee125-107">La siguiente `@type` se usa el valor:</span><span class="sxs-lookup"><span data-stu-id="ee125-107">The following `@type` value is used:</span></span>

<span data-ttu-id="ee125-108">Valor de@type</span><span class="sxs-lookup"><span data-stu-id="ee125-108">@type value</span></span>          | <span data-ttu-id="ee125-109">Notas</span><span class="sxs-lookup"><span data-stu-id="ee125-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="ee125-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="ee125-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="ee125-111">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="ee125-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="ee125-112">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="ee125-112">Base URL</span></span>

<span data-ttu-id="ee125-113">La dirección URL base para las siguientes API es el valor de la `@id` propiedad de la `PackagePublish/2.0.0` recursos en el origen de paquete [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ee125-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="ee125-114">Para obtener la documentación a continuación, se usa la dirección URL de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ee125-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="ee125-115">Considere la posibilidad de `https://www.nuget.org/api/v2/package` como marcador de posición para el `@id` valor se encuentra en el índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="ee125-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="ee125-116">Tenga en cuenta que esta dirección URL señala a la misma ubicación que el punto de conexión de inserción heredada de V2, dado que el protocolo es el mismo.</span><span class="sxs-lookup"><span data-stu-id="ee125-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ee125-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="ee125-117">HTTP methods</span></span>

<span data-ttu-id="ee125-118">El `PUT`, `POST` y `DELETE` métodos HTTP son compatibles con este recurso.</span><span class="sxs-lookup"><span data-stu-id="ee125-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="ee125-119">Para los métodos que se admiten en cada punto de conexión, consulte a continuación.</span><span class="sxs-lookup"><span data-stu-id="ee125-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="ee125-120">Inserte un paquete</span><span class="sxs-lookup"><span data-stu-id="ee125-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="ee125-121">NuGet.org tiene [requisitos adicionales](NuGet-Protocols.md) para interactuar con el punto de conexión de inserción.</span><span class="sxs-lookup"><span data-stu-id="ee125-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="ee125-122">NuGet.org admite insertar nuevos paquetes mediante la API siguiente.</span><span class="sxs-lookup"><span data-stu-id="ee125-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="ee125-123">Si ya existe el paquete con el identificador proporcionado y la versión, nuget.org rechazará la inserción.</span><span class="sxs-lookup"><span data-stu-id="ee125-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="ee125-124">Otros orígenes de paquetes pueden admitir reemplazando un paquete existente.</span><span class="sxs-lookup"><span data-stu-id="ee125-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="ee125-125">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="ee125-125">Request parameters</span></span>

<span data-ttu-id="ee125-126">Name</span><span class="sxs-lookup"><span data-stu-id="ee125-126">Name</span></span>           | <span data-ttu-id="ee125-127">En</span><span class="sxs-lookup"><span data-stu-id="ee125-127">In</span></span>     | <span data-ttu-id="ee125-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee125-128">Type</span></span>   | <span data-ttu-id="ee125-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ee125-129">Required</span></span> | <span data-ttu-id="ee125-130">Notas</span><span class="sxs-lookup"><span data-stu-id="ee125-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ee125-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ee125-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ee125-132">Header</span><span class="sxs-lookup"><span data-stu-id="ee125-132">Header</span></span> | <span data-ttu-id="ee125-133">cadena</span><span class="sxs-lookup"><span data-stu-id="ee125-133">string</span></span> | <span data-ttu-id="ee125-134">sí</span><span class="sxs-lookup"><span data-stu-id="ee125-134">yes</span></span>      | <span data-ttu-id="ee125-135">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="ee125-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="ee125-136">La clave de API es una cadena opaca llegado desde el origen del paquete por el usuario y configurado en el cliente.</span><span class="sxs-lookup"><span data-stu-id="ee125-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="ee125-137">Ningún formato de cadena concreta está asignada, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores de encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="ee125-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="ee125-138">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="ee125-138">Request body</span></span>

<span data-ttu-id="ee125-139">El cuerpo de solicitud debe proceder de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="ee125-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="ee125-140">Datos de formulario de varias partes</span><span class="sxs-lookup"><span data-stu-id="ee125-140">Multipart form data</span></span>

<span data-ttu-id="ee125-141">El encabezado de solicitud `Content-Type` es `multipart/form-data` y el primer elemento en el cuerpo de solicitud es los bytes sin formato de los archivos .nupkg que se va a insertar.</span><span class="sxs-lookup"><span data-stu-id="ee125-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="ee125-142">Se omiten los elementos siguientes en el cuerpo de varias partes.</span><span class="sxs-lookup"><span data-stu-id="ee125-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="ee125-143">El nombre de archivo o cualquier otro encabezado de los elementos de varias partes se omite.</span><span class="sxs-lookup"><span data-stu-id="ee125-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="ee125-144">Respuesta</span><span class="sxs-lookup"><span data-stu-id="ee125-144">Response</span></span>

<span data-ttu-id="ee125-145">Código de estado</span><span class="sxs-lookup"><span data-stu-id="ee125-145">Status Code</span></span> | <span data-ttu-id="ee125-146">Significado</span><span class="sxs-lookup"><span data-stu-id="ee125-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="ee125-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="ee125-147">201, 202</span></span>    | <span data-ttu-id="ee125-148">El paquete se ha insertado correctamente</span><span class="sxs-lookup"><span data-stu-id="ee125-148">The package was successfully pushed</span></span>
<span data-ttu-id="ee125-149">400</span><span class="sxs-lookup"><span data-stu-id="ee125-149">400</span></span>         | <span data-ttu-id="ee125-150">El paquete proporcionado no es válido</span><span class="sxs-lookup"><span data-stu-id="ee125-150">The provided package is invalid</span></span>
<span data-ttu-id="ee125-151">409</span><span class="sxs-lookup"><span data-stu-id="ee125-151">409</span></span>         | <span data-ttu-id="ee125-152">Ya existe un paquete con el identificador proporcionado y la versión</span><span class="sxs-lookup"><span data-stu-id="ee125-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="ee125-153">Las implementaciones de servidor varían en el código de estado correcto, devuelve cuando se insertó correctamente un paquete.</span><span class="sxs-lookup"><span data-stu-id="ee125-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="ee125-154">Eliminar un paquete</span><span class="sxs-lookup"><span data-stu-id="ee125-154">Delete a package</span></span>

<span data-ttu-id="ee125-155">NuGet.org interpreta la solicitud de eliminación de paquete como un "quitar de la lista".</span><span class="sxs-lookup"><span data-stu-id="ee125-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="ee125-156">Esto significa que el paquete sigue estando disponible para los usuarios existentes del paquete, pero el paquete ya no aparece en los resultados de búsqueda o en la interfaz web.</span><span class="sxs-lookup"><span data-stu-id="ee125-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="ee125-157">Para obtener más información acerca de esta práctica, consulte el [paquetes eliminados](../nuget-org/policies/deleting-packages.md) directiva.</span><span class="sxs-lookup"><span data-stu-id="ee125-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="ee125-158">Otras implementaciones del servidor son gratis para interpretar esta señal como una eliminación de disco dura, eliminación temporal o quitar de la lista.</span><span class="sxs-lookup"><span data-stu-id="ee125-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="ee125-159">Por ejemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (una implementación de servidor solo admite la API V2 anterior) es compatible con esta solicitud de control como una eliminación de la lista o una eliminación de disco dura basada en una opción de configuración.</span><span class="sxs-lookup"><span data-stu-id="ee125-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="ee125-160">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="ee125-160">Request parameters</span></span>

<span data-ttu-id="ee125-161">Name</span><span class="sxs-lookup"><span data-stu-id="ee125-161">Name</span></span>           | <span data-ttu-id="ee125-162">En</span><span class="sxs-lookup"><span data-stu-id="ee125-162">In</span></span>     | <span data-ttu-id="ee125-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee125-163">Type</span></span>   | <span data-ttu-id="ee125-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ee125-164">Required</span></span> | <span data-ttu-id="ee125-165">Notas</span><span class="sxs-lookup"><span data-stu-id="ee125-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ee125-166">ID</span><span class="sxs-lookup"><span data-stu-id="ee125-166">ID</span></span>             | <span data-ttu-id="ee125-167">Resolución</span><span class="sxs-lookup"><span data-stu-id="ee125-167">URL</span></span>    | <span data-ttu-id="ee125-168">cadena</span><span class="sxs-lookup"><span data-stu-id="ee125-168">string</span></span> | <span data-ttu-id="ee125-169">sí</span><span class="sxs-lookup"><span data-stu-id="ee125-169">yes</span></span>      | <span data-ttu-id="ee125-170">El identificador del paquete va a eliminar</span><span class="sxs-lookup"><span data-stu-id="ee125-170">The ID of the package to delete</span></span>
<span data-ttu-id="ee125-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="ee125-171">VERSION</span></span>        | <span data-ttu-id="ee125-172">Resolución</span><span class="sxs-lookup"><span data-stu-id="ee125-172">URL</span></span>    | <span data-ttu-id="ee125-173">cadena</span><span class="sxs-lookup"><span data-stu-id="ee125-173">string</span></span> | <span data-ttu-id="ee125-174">sí</span><span class="sxs-lookup"><span data-stu-id="ee125-174">yes</span></span>      | <span data-ttu-id="ee125-175">La versión del paquete para eliminar</span><span class="sxs-lookup"><span data-stu-id="ee125-175">The version of the package to delete</span></span>
<span data-ttu-id="ee125-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ee125-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ee125-177">Header</span><span class="sxs-lookup"><span data-stu-id="ee125-177">Header</span></span> | <span data-ttu-id="ee125-178">cadena</span><span class="sxs-lookup"><span data-stu-id="ee125-178">string</span></span> | <span data-ttu-id="ee125-179">sí</span><span class="sxs-lookup"><span data-stu-id="ee125-179">yes</span></span>      | <span data-ttu-id="ee125-180">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="ee125-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="ee125-181">Respuesta</span><span class="sxs-lookup"><span data-stu-id="ee125-181">Response</span></span>

<span data-ttu-id="ee125-182">Código de estado</span><span class="sxs-lookup"><span data-stu-id="ee125-182">Status Code</span></span> | <span data-ttu-id="ee125-183">Significado</span><span class="sxs-lookup"><span data-stu-id="ee125-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="ee125-184">204</span><span class="sxs-lookup"><span data-stu-id="ee125-184">204</span></span>         | <span data-ttu-id="ee125-185">Se eliminó el paquete</span><span class="sxs-lookup"><span data-stu-id="ee125-185">The package was deleted</span></span>
<span data-ttu-id="ee125-186">404</span><span class="sxs-lookup"><span data-stu-id="ee125-186">404</span></span>         | <span data-ttu-id="ee125-187">Ningún paquete con el proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="ee125-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="ee125-188">Poner un paquete</span><span class="sxs-lookup"><span data-stu-id="ee125-188">Relist a package</span></span>

<span data-ttu-id="ee125-189">Si un paquete se da de baja, es posible que ese paquete una vez más visible en los resultados de búsqueda mediante el punto de conexión de "poner en".</span><span class="sxs-lookup"><span data-stu-id="ee125-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="ee125-190">Este punto de conexión tiene la misma forma que el [eliminar (quitar de la lista) punto de conexión](#delete-a-package) , pero usa el `POST` método HTTP en lugar de la `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="ee125-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="ee125-191">Si el paquete ya aparece, la solicitud se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="ee125-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="ee125-192">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="ee125-192">Request parameters</span></span>

<span data-ttu-id="ee125-193">Name</span><span class="sxs-lookup"><span data-stu-id="ee125-193">Name</span></span>           | <span data-ttu-id="ee125-194">En</span><span class="sxs-lookup"><span data-stu-id="ee125-194">In</span></span>     | <span data-ttu-id="ee125-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee125-195">Type</span></span>   | <span data-ttu-id="ee125-196">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ee125-196">Required</span></span> | <span data-ttu-id="ee125-197">Notas</span><span class="sxs-lookup"><span data-stu-id="ee125-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ee125-198">ID</span><span class="sxs-lookup"><span data-stu-id="ee125-198">ID</span></span>             | <span data-ttu-id="ee125-199">Resolución</span><span class="sxs-lookup"><span data-stu-id="ee125-199">URL</span></span>    | <span data-ttu-id="ee125-200">cadena</span><span class="sxs-lookup"><span data-stu-id="ee125-200">string</span></span> | <span data-ttu-id="ee125-201">sí</span><span class="sxs-lookup"><span data-stu-id="ee125-201">yes</span></span>      | <span data-ttu-id="ee125-202">El identificador del paquete para volver a</span><span class="sxs-lookup"><span data-stu-id="ee125-202">The ID of the package to relist</span></span>
<span data-ttu-id="ee125-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="ee125-203">VERSION</span></span>        | <span data-ttu-id="ee125-204">Resolución</span><span class="sxs-lookup"><span data-stu-id="ee125-204">URL</span></span>    | <span data-ttu-id="ee125-205">cadena</span><span class="sxs-lookup"><span data-stu-id="ee125-205">string</span></span> | <span data-ttu-id="ee125-206">sí</span><span class="sxs-lookup"><span data-stu-id="ee125-206">yes</span></span>      | <span data-ttu-id="ee125-207">La versión del paquete para volver a</span><span class="sxs-lookup"><span data-stu-id="ee125-207">The version of the package to relist</span></span>
<span data-ttu-id="ee125-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ee125-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ee125-209">Header</span><span class="sxs-lookup"><span data-stu-id="ee125-209">Header</span></span> | <span data-ttu-id="ee125-210">cadena</span><span class="sxs-lookup"><span data-stu-id="ee125-210">string</span></span> | <span data-ttu-id="ee125-211">sí</span><span class="sxs-lookup"><span data-stu-id="ee125-211">yes</span></span>      | <span data-ttu-id="ee125-212">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="ee125-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="ee125-213">Respuesta</span><span class="sxs-lookup"><span data-stu-id="ee125-213">Response</span></span>

<span data-ttu-id="ee125-214">Código de estado</span><span class="sxs-lookup"><span data-stu-id="ee125-214">Status Code</span></span> | <span data-ttu-id="ee125-215">Significado</span><span class="sxs-lookup"><span data-stu-id="ee125-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="ee125-216">200</span><span class="sxs-lookup"><span data-stu-id="ee125-216">200</span></span>         | <span data-ttu-id="ee125-217">El paquete aparece ahora</span><span class="sxs-lookup"><span data-stu-id="ee125-217">The package is now listed</span></span>
<span data-ttu-id="ee125-218">404</span><span class="sxs-lookup"><span data-stu-id="ee125-218">404</span></span>         | <span data-ttu-id="ee125-219">Ningún paquete con el proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="ee125-219">No package with the provided `ID` and `VERSION` exists</span></span>
