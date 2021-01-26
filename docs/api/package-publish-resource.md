---
title: Extracción y eliminación, API de NuGet
description: El servicio de publicación permite a los clientes publicar paquetes nuevos y quitar de la lista o eliminar los paquetes existentes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773928"
---
# <a name="push-and-delete"></a><span data-ttu-id="bafd9-103">Enviar y eliminar</span><span class="sxs-lookup"><span data-stu-id="bafd9-103">Push and Delete</span></span>

<span data-ttu-id="bafd9-104">Es posible insertar, eliminar (o quitar de la lista, en función de la implementación del servidor) y volver a enumerar los paquetes mediante la API de NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="bafd9-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="bafd9-105">Estas operaciones se basan `PackagePublish` en el recurso que se encuentra en el [Índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="bafd9-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="bafd9-106">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="bafd9-106">Versioning</span></span>

<span data-ttu-id="bafd9-107">`@type`Se usa el siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="bafd9-107">The following `@type` value is used:</span></span>

<span data-ttu-id="bafd9-108">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="bafd9-108">@type value</span></span>          | <span data-ttu-id="bafd9-109">Notas</span><span class="sxs-lookup"><span data-stu-id="bafd9-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="bafd9-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="bafd9-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="bafd9-111">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="bafd9-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="bafd9-112">URL base</span><span class="sxs-lookup"><span data-stu-id="bafd9-112">Base URL</span></span>

<span data-ttu-id="bafd9-113">La dirección URL base para las siguientes API es el valor de la `@id` propiedad del `PackagePublish/2.0.0` recurso en el [Índice de servicio](service-index.md)del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="bafd9-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="bafd9-114">En la documentación siguiente, se usa la dirección URL de Nuget. org.</span><span class="sxs-lookup"><span data-stu-id="bafd9-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="bafd9-115">Considere `https://www.nuget.org/api/v2/package` como un marcador de posición para el `@id` valor que se encuentra en el índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="bafd9-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="bafd9-116">Tenga en cuenta que esta dirección URL señala a la misma ubicación que el punto de conexión de inserciones V2 heredado, ya que el protocolo es el mismo.</span><span class="sxs-lookup"><span data-stu-id="bafd9-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="bafd9-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="bafd9-117">HTTP methods</span></span>

<span data-ttu-id="bafd9-118">`PUT` `POST` `DELETE` Este recurso admite los métodos http y.</span><span class="sxs-lookup"><span data-stu-id="bafd9-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="bafd9-119">Para saber qué métodos se admiten en cada punto de conexión, vea a continuación.</span><span class="sxs-lookup"><span data-stu-id="bafd9-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="bafd9-120">Inserte un paquete</span><span class="sxs-lookup"><span data-stu-id="bafd9-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="bafd9-121">nuget.org tiene [requisitos adicionales](NuGet-Protocols.md) para interactuar con el punto de conexión de la inserciones.</span><span class="sxs-lookup"><span data-stu-id="bafd9-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="bafd9-122">nuget.org admite la inserción de nuevos paquetes mediante la siguiente API.</span><span class="sxs-lookup"><span data-stu-id="bafd9-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="bafd9-123">Si ya existe el paquete con el identificador y la versión proporcionados, nuget.org rechazará la inserciones.</span><span class="sxs-lookup"><span data-stu-id="bafd9-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="bafd9-124">Otros orígenes de paquetes pueden admitir el reemplazo de un paquete existente.</span><span class="sxs-lookup"><span data-stu-id="bafd9-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="bafd9-125">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="bafd9-125">Request parameters</span></span>

<span data-ttu-id="bafd9-126">Nombre</span><span class="sxs-lookup"><span data-stu-id="bafd9-126">Name</span></span>           | <span data-ttu-id="bafd9-127">En</span><span class="sxs-lookup"><span data-stu-id="bafd9-127">In</span></span>     | <span data-ttu-id="bafd9-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="bafd9-128">Type</span></span>   | <span data-ttu-id="bafd9-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="bafd9-129">Required</span></span> | <span data-ttu-id="bafd9-130">Notas</span><span class="sxs-lookup"><span data-stu-id="bafd9-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="bafd9-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="bafd9-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="bafd9-132">Encabezado</span><span class="sxs-lookup"><span data-stu-id="bafd9-132">Header</span></span> | <span data-ttu-id="bafd9-133">string</span><span class="sxs-lookup"><span data-stu-id="bafd9-133">string</span></span> | <span data-ttu-id="bafd9-134">sí</span><span class="sxs-lookup"><span data-stu-id="bafd9-134">yes</span></span>      | <span data-ttu-id="bafd9-135">Por ejemplo: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="bafd9-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="bafd9-136">La clave de API es una cadena opaca procedente del origen del paquete por el usuario y configurada en el cliente.</span><span class="sxs-lookup"><span data-stu-id="bafd9-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="bafd9-137">No se asigna ningún formato de cadena determinado, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores del encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="bafd9-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="bafd9-138">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="bafd9-138">Request body</span></span>

<span data-ttu-id="bafd9-139">El cuerpo de la solicitud debe tener el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="bafd9-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="bafd9-140">Datos de formulario de varias partes</span><span class="sxs-lookup"><span data-stu-id="bafd9-140">Multipart form data</span></span>

<span data-ttu-id="bafd9-141">El encabezado de solicitud `Content-Type` es `multipart/form-data` y el primer elemento del cuerpo de la solicitud son los bytes sin formato del. nupkg que se va a insertar.</span><span class="sxs-lookup"><span data-stu-id="bafd9-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="bafd9-142">Los elementos subsiguientes del cuerpo de varias partes se omiten.</span><span class="sxs-lookup"><span data-stu-id="bafd9-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="bafd9-143">Se omiten el nombre de archivo o cualquier otro encabezado de los elementos de varias partes.</span><span class="sxs-lookup"><span data-stu-id="bafd9-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="bafd9-144">Response</span><span class="sxs-lookup"><span data-stu-id="bafd9-144">Response</span></span>

<span data-ttu-id="bafd9-145">Código de estado</span><span class="sxs-lookup"><span data-stu-id="bafd9-145">Status Code</span></span> | <span data-ttu-id="bafd9-146">Significado</span><span class="sxs-lookup"><span data-stu-id="bafd9-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="bafd9-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="bafd9-147">201, 202</span></span>    | <span data-ttu-id="bafd9-148">El paquete se insertó correctamente</span><span class="sxs-lookup"><span data-stu-id="bafd9-148">The package was successfully pushed</span></span>
<span data-ttu-id="bafd9-149">400</span><span class="sxs-lookup"><span data-stu-id="bafd9-149">400</span></span>         | <span data-ttu-id="bafd9-150">El paquete proporcionado no es válido</span><span class="sxs-lookup"><span data-stu-id="bafd9-150">The provided package is invalid</span></span>
<span data-ttu-id="bafd9-151">409</span><span class="sxs-lookup"><span data-stu-id="bafd9-151">409</span></span>         | <span data-ttu-id="bafd9-152">Ya existe un paquete con el identificador y la versión proporcionados</span><span class="sxs-lookup"><span data-stu-id="bafd9-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="bafd9-153">Las implementaciones de servidor varían en el código de estado correcto que se devuelve cuando se inserta un paquete correctamente.</span><span class="sxs-lookup"><span data-stu-id="bafd9-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="bafd9-154">Eliminación de un paquete</span><span class="sxs-lookup"><span data-stu-id="bafd9-154">Delete a package</span></span>

<span data-ttu-id="bafd9-155">nuget.org interpreta la solicitud de eliminación de paquetes como una "unlist".</span><span class="sxs-lookup"><span data-stu-id="bafd9-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="bafd9-156">Esto significa que el paquete sigue estando disponible para los consumidores existentes del paquete, pero el paquete ya no aparece en los resultados de la búsqueda o en la interfaz Web.</span><span class="sxs-lookup"><span data-stu-id="bafd9-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="bafd9-157">Para obtener más información acerca de esta práctica, vea la Directiva de [paquetes eliminados](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="bafd9-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="bafd9-158">Otras implementaciones de servidor son gratuitas para interpretar esta señal como una eliminación temporal, una eliminación temporal o una lista desenumerada.</span><span class="sxs-lookup"><span data-stu-id="bafd9-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="bafd9-159">Por ejemplo, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (una implementación de servidor que solo admite la API V2 anterior) permite administrar esta solicitud como una lista desactiva o como una eliminación de hardware basada en una opción de configuración.</span><span class="sxs-lookup"><span data-stu-id="bafd9-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="bafd9-160">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="bafd9-160">Request parameters</span></span>

<span data-ttu-id="bafd9-161">Nombre</span><span class="sxs-lookup"><span data-stu-id="bafd9-161">Name</span></span>           | <span data-ttu-id="bafd9-162">En</span><span class="sxs-lookup"><span data-stu-id="bafd9-162">In</span></span>     | <span data-ttu-id="bafd9-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="bafd9-163">Type</span></span>   | <span data-ttu-id="bafd9-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="bafd9-164">Required</span></span> | <span data-ttu-id="bafd9-165">Notas</span><span class="sxs-lookup"><span data-stu-id="bafd9-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="bafd9-166">ID</span><span class="sxs-lookup"><span data-stu-id="bafd9-166">ID</span></span>             | <span data-ttu-id="bafd9-167">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="bafd9-167">URL</span></span>    | <span data-ttu-id="bafd9-168">string</span><span class="sxs-lookup"><span data-stu-id="bafd9-168">string</span></span> | <span data-ttu-id="bafd9-169">sí</span><span class="sxs-lookup"><span data-stu-id="bafd9-169">yes</span></span>      | <span data-ttu-id="bafd9-170">Identificador del paquete que se va a eliminar.</span><span class="sxs-lookup"><span data-stu-id="bafd9-170">The ID of the package to delete</span></span>
<span data-ttu-id="bafd9-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="bafd9-171">VERSION</span></span>        | <span data-ttu-id="bafd9-172">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="bafd9-172">URL</span></span>    | <span data-ttu-id="bafd9-173">string</span><span class="sxs-lookup"><span data-stu-id="bafd9-173">string</span></span> | <span data-ttu-id="bafd9-174">sí</span><span class="sxs-lookup"><span data-stu-id="bafd9-174">yes</span></span>      | <span data-ttu-id="bafd9-175">Versión del paquete que se va a eliminar.</span><span class="sxs-lookup"><span data-stu-id="bafd9-175">The version of the package to delete</span></span>
<span data-ttu-id="bafd9-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="bafd9-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="bafd9-177">Encabezado</span><span class="sxs-lookup"><span data-stu-id="bafd9-177">Header</span></span> | <span data-ttu-id="bafd9-178">string</span><span class="sxs-lookup"><span data-stu-id="bafd9-178">string</span></span> | <span data-ttu-id="bafd9-179">sí</span><span class="sxs-lookup"><span data-stu-id="bafd9-179">yes</span></span>      | <span data-ttu-id="bafd9-180">Por ejemplo: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="bafd9-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="bafd9-181">Response</span><span class="sxs-lookup"><span data-stu-id="bafd9-181">Response</span></span>

<span data-ttu-id="bafd9-182">Código de estado</span><span class="sxs-lookup"><span data-stu-id="bafd9-182">Status Code</span></span> | <span data-ttu-id="bafd9-183">Significado</span><span class="sxs-lookup"><span data-stu-id="bafd9-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="bafd9-184">204</span><span class="sxs-lookup"><span data-stu-id="bafd9-184">204</span></span>         | <span data-ttu-id="bafd9-185">El paquete se ha eliminado</span><span class="sxs-lookup"><span data-stu-id="bafd9-185">The package was deleted</span></span>
<span data-ttu-id="bafd9-186">404</span><span class="sxs-lookup"><span data-stu-id="bafd9-186">404</span></span>         | <span data-ttu-id="bafd9-187">No hay ningún paquete con el proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="bafd9-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="bafd9-188">Volver a enumerar un paquete</span><span class="sxs-lookup"><span data-stu-id="bafd9-188">Relist a package</span></span>

<span data-ttu-id="bafd9-189">Si un paquete no está en la lista, es posible que el paquete vuelva a estar visible en los resultados de la búsqueda mediante el punto de conexión "volver a mostrar".</span><span class="sxs-lookup"><span data-stu-id="bafd9-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="bafd9-190">Este extremo tiene la misma forma que el [punto de conexión Delete (unlist)](#delete-a-package) , pero usa el `POST` método http en lugar del `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="bafd9-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="bafd9-191">Si el paquete ya aparece en la lista, la solicitud se realizará correctamente.</span><span class="sxs-lookup"><span data-stu-id="bafd9-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="bafd9-192">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="bafd9-192">Request parameters</span></span>

<span data-ttu-id="bafd9-193">Nombre</span><span class="sxs-lookup"><span data-stu-id="bafd9-193">Name</span></span>           | <span data-ttu-id="bafd9-194">En</span><span class="sxs-lookup"><span data-stu-id="bafd9-194">In</span></span>     | <span data-ttu-id="bafd9-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="bafd9-195">Type</span></span>   | <span data-ttu-id="bafd9-196">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="bafd9-196">Required</span></span> | <span data-ttu-id="bafd9-197">Notas</span><span class="sxs-lookup"><span data-stu-id="bafd9-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="bafd9-198">ID</span><span class="sxs-lookup"><span data-stu-id="bafd9-198">ID</span></span>             | <span data-ttu-id="bafd9-199">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="bafd9-199">URL</span></span>    | <span data-ttu-id="bafd9-200">string</span><span class="sxs-lookup"><span data-stu-id="bafd9-200">string</span></span> | <span data-ttu-id="bafd9-201">sí</span><span class="sxs-lookup"><span data-stu-id="bafd9-201">yes</span></span>      | <span data-ttu-id="bafd9-202">IDENTIFICADOR del paquete que se va a volver a enumerar</span><span class="sxs-lookup"><span data-stu-id="bafd9-202">The ID of the package to relist</span></span>
<span data-ttu-id="bafd9-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="bafd9-203">VERSION</span></span>        | <span data-ttu-id="bafd9-204">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="bafd9-204">URL</span></span>    | <span data-ttu-id="bafd9-205">string</span><span class="sxs-lookup"><span data-stu-id="bafd9-205">string</span></span> | <span data-ttu-id="bafd9-206">sí</span><span class="sxs-lookup"><span data-stu-id="bafd9-206">yes</span></span>      | <span data-ttu-id="bafd9-207">Versión del paquete que se va a volver a enumerar</span><span class="sxs-lookup"><span data-stu-id="bafd9-207">The version of the package to relist</span></span>
<span data-ttu-id="bafd9-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="bafd9-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="bafd9-209">Encabezado</span><span class="sxs-lookup"><span data-stu-id="bafd9-209">Header</span></span> | <span data-ttu-id="bafd9-210">string</span><span class="sxs-lookup"><span data-stu-id="bafd9-210">string</span></span> | <span data-ttu-id="bafd9-211">sí</span><span class="sxs-lookup"><span data-stu-id="bafd9-211">yes</span></span>      | <span data-ttu-id="bafd9-212">Por ejemplo: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="bafd9-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="bafd9-213">Response</span><span class="sxs-lookup"><span data-stu-id="bafd9-213">Response</span></span>

<span data-ttu-id="bafd9-214">Código de estado</span><span class="sxs-lookup"><span data-stu-id="bafd9-214">Status Code</span></span> | <span data-ttu-id="bafd9-215">Significado</span><span class="sxs-lookup"><span data-stu-id="bafd9-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="bafd9-216">200</span><span class="sxs-lookup"><span data-stu-id="bafd9-216">200</span></span>         | <span data-ttu-id="bafd9-217">El paquete aparece ahora</span><span class="sxs-lookup"><span data-stu-id="bafd9-217">The package is now listed</span></span>
<span data-ttu-id="bafd9-218">404</span><span class="sxs-lookup"><span data-stu-id="bafd9-218">404</span></span>         | <span data-ttu-id="bafd9-219">No hay ningún paquete con el proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="bafd9-219">No package with the provided `ID` and `VERSION` exists</span></span>
