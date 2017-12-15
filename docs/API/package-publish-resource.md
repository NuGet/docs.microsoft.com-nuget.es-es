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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "El servicio de publicación permite a los clientes publicar nuevos paquetes y ocultar o eliminar los paquetes existentes."
keywords: "Paquete de inserción de API de NuGet, API de NuGet eliminar paquete, API de NuGet ocultar paquete, paquete de carga de la API de NuGet, API de NuGet crear paquete"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="d6ab2-104">Insertar y eliminar</span><span class="sxs-lookup"><span data-stu-id="d6ab2-104">Push and Delete</span></span>

<span data-ttu-id="d6ab2-105">Es posible insertar y eliminar elementos (u ocultar, dependiendo de la implementación de servidor) paquetes mediante la API V3 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="d6ab2-106">Ambas operaciones se basan en el `PackagePublish` recurso se encuentra en la [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d6ab2-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d6ab2-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="d6ab2-107">Versioning</span></span>

<span data-ttu-id="d6ab2-108">El siguiente `@type` valor se utiliza:</span><span class="sxs-lookup"><span data-stu-id="d6ab2-108">The following `@type` value is used:</span></span>

<span data-ttu-id="d6ab2-109">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="d6ab2-109">@type value</span></span>          | <span data-ttu-id="d6ab2-110">Notas</span><span class="sxs-lookup"><span data-stu-id="d6ab2-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="d6ab2-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="d6ab2-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="d6ab2-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="d6ab2-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d6ab2-113">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="d6ab2-113">Base URL</span></span>

<span data-ttu-id="d6ab2-114">La dirección URL base para las API siguientes es el valor de la `@id` propiedad de la `PackagePublish/2.0.0` recursos en el origen de paquete [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d6ab2-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="d6ab2-115">Para obtener la documentación siguiente, se utiliza la dirección URL de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="d6ab2-116">Considere la posibilidad de `https://www.nuget.org/api/v2/package` como un marcador de posición para el `@id` valor se encuentra en el índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="d6ab2-117">Tenga en cuenta que esta dirección URL señala a la misma ubicación que el extremo de inserción V2 heredado como el protocolo es el mismo.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d6ab2-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="d6ab2-118">HTTP methods</span></span>

<span data-ttu-id="d6ab2-119">El `PUT` y `DELETE` métodos HTTP son compatibles con este recurso.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="d6ab2-120">Para los métodos que se admiten en cada punto de conexión, consulte a continuación.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="d6ab2-121">Insertar un paquete</span><span class="sxs-lookup"><span data-stu-id="d6ab2-121">Push a package</span></span>

<span data-ttu-id="d6ab2-122">NuGet.org admite la inserción de nuevos paquetes mediante la siguiente API.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="d6ab2-123">Si ya existe el paquete con el identificador y la versión proporcionada, nuget.org rechazará la inserción.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="d6ab2-124">Otros orígenes de paquetes pueden admitir reemplazando un paquete existente.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="d6ab2-125">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="d6ab2-125">Request parameters</span></span>

<span data-ttu-id="d6ab2-126">Name</span><span class="sxs-lookup"><span data-stu-id="d6ab2-126">Name</span></span>           | <span data-ttu-id="d6ab2-127">En</span><span class="sxs-lookup"><span data-stu-id="d6ab2-127">In</span></span>     | <span data-ttu-id="d6ab2-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ab2-128">Type</span></span>   | <span data-ttu-id="d6ab2-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ab2-129">Required</span></span> | <span data-ttu-id="d6ab2-130">Notas</span><span class="sxs-lookup"><span data-stu-id="d6ab2-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d6ab2-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d6ab2-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d6ab2-132">Header</span><span class="sxs-lookup"><span data-stu-id="d6ab2-132">Header</span></span> | <span data-ttu-id="d6ab2-133">string</span><span class="sxs-lookup"><span data-stu-id="d6ab2-133">string</span></span> | <span data-ttu-id="d6ab2-134">sí</span><span class="sxs-lookup"><span data-stu-id="d6ab2-134">yes</span></span>      | <span data-ttu-id="d6ab2-135">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="d6ab2-136">La clave de API es una cadena opaca recibido desde el origen del paquete por el usuario y configurado en el cliente.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="d6ab2-137">Ningún formato de cadena determinada es obligatoria, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores de encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="d6ab2-138">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="d6ab2-138">Request body</span></span>

<span data-ttu-id="d6ab2-139">El cuerpo de solicitud debe proceder de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="d6ab2-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="d6ab2-140">Datos de formulario de varias partes</span><span class="sxs-lookup"><span data-stu-id="d6ab2-140">Multipart form data</span></span>

<span data-ttu-id="d6ab2-141">El encabezado de solicitud `Content-Type` es `multipart/form-data` y el primer elemento en el cuerpo de solicitud es los bytes sin formato de la .nupkg que se va a insertar.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="d6ab2-142">Se omiten los elementos siguientes en el cuerpo de varias partes.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="d6ab2-143">Se omite el nombre de archivo o cualquier otro encabezado de los elementos de varias partes.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="d6ab2-144">Respuesta</span><span class="sxs-lookup"><span data-stu-id="d6ab2-144">Response</span></span>

<span data-ttu-id="d6ab2-145">Código de estado</span><span class="sxs-lookup"><span data-stu-id="d6ab2-145">Status Code</span></span> | <span data-ttu-id="d6ab2-146">Significado</span><span class="sxs-lookup"><span data-stu-id="d6ab2-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="d6ab2-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="d6ab2-147">201, 202</span></span>    | <span data-ttu-id="d6ab2-148">El paquete se ha insertado correctamente</span><span class="sxs-lookup"><span data-stu-id="d6ab2-148">The package was successfully pushed</span></span>
<span data-ttu-id="d6ab2-149">400</span><span class="sxs-lookup"><span data-stu-id="d6ab2-149">400</span></span>         | <span data-ttu-id="d6ab2-150">El paquete proporcionado no es válido</span><span class="sxs-lookup"><span data-stu-id="d6ab2-150">The provided package is invalid</span></span>
<span data-ttu-id="d6ab2-151">409</span><span class="sxs-lookup"><span data-stu-id="d6ab2-151">409</span></span>         | <span data-ttu-id="d6ab2-152">Ya existe un paquete con el identificador proporcionado y la versión</span><span class="sxs-lookup"><span data-stu-id="d6ab2-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="d6ab2-153">Las implementaciones de servidor varían en el código de estado correcto devuelto cuando un paquete se envíe correctamente.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="d6ab2-154">Eliminar un paquete</span><span class="sxs-lookup"><span data-stu-id="d6ab2-154">Delete a package</span></span>

<span data-ttu-id="d6ab2-155">NuGet.org interpreta la solicitud de eliminación de paquete como un "Ocultar".</span><span class="sxs-lookup"><span data-stu-id="d6ab2-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="d6ab2-156">Esto significa que el paquete sigue estando disponible para los usuarios existentes del paquete, pero el paquete ya no aparece en los resultados de la búsqueda o en la interfaz web.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="d6ab2-157">Para obtener más información acerca de este procedimiento, consulte la [eliminar paquetes](../policies/deleting-packages.md) directiva.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="d6ab2-158">Otras implementaciones del servidor son gratuitos para interpretar esta señal como una eliminación de disco duro, eliminar temporalmente u ocultar.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="d6ab2-159">Por ejemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (una implementación de servidor sólo admite la API V2 anteriores) es compatible con esta solicitud de control como un unlist o una eliminación de disco duro en función de una opción de configuración.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="d6ab2-160">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="d6ab2-160">Request parameters</span></span>

<span data-ttu-id="d6ab2-161">Name</span><span class="sxs-lookup"><span data-stu-id="d6ab2-161">Name</span></span>           | <span data-ttu-id="d6ab2-162">En</span><span class="sxs-lookup"><span data-stu-id="d6ab2-162">In</span></span>     | <span data-ttu-id="d6ab2-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ab2-163">Type</span></span>   | <span data-ttu-id="d6ab2-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ab2-164">Required</span></span> | <span data-ttu-id="d6ab2-165">Notas</span><span class="sxs-lookup"><span data-stu-id="d6ab2-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d6ab2-166">Id.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-166">ID</span></span>             | <span data-ttu-id="d6ab2-167">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="d6ab2-167">URL</span></span>    | <span data-ttu-id="d6ab2-168">string</span><span class="sxs-lookup"><span data-stu-id="d6ab2-168">string</span></span> | <span data-ttu-id="d6ab2-169">sí</span><span class="sxs-lookup"><span data-stu-id="d6ab2-169">yes</span></span>      | <span data-ttu-id="d6ab2-170">El identificador del paquete para eliminar</span><span class="sxs-lookup"><span data-stu-id="d6ab2-170">The ID of the package to delete</span></span>
<span data-ttu-id="d6ab2-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="d6ab2-171">VERSION</span></span>        | <span data-ttu-id="d6ab2-172">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="d6ab2-172">URL</span></span>    | <span data-ttu-id="d6ab2-173">string</span><span class="sxs-lookup"><span data-stu-id="d6ab2-173">string</span></span> | <span data-ttu-id="d6ab2-174">sí</span><span class="sxs-lookup"><span data-stu-id="d6ab2-174">yes</span></span>      | <span data-ttu-id="d6ab2-175">La versión del paquete que se va a eliminar</span><span class="sxs-lookup"><span data-stu-id="d6ab2-175">The version of the package to delete</span></span>
<span data-ttu-id="d6ab2-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d6ab2-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d6ab2-177">Header</span><span class="sxs-lookup"><span data-stu-id="d6ab2-177">Header</span></span> | <span data-ttu-id="d6ab2-178">string</span><span class="sxs-lookup"><span data-stu-id="d6ab2-178">string</span></span> | <span data-ttu-id="d6ab2-179">sí</span><span class="sxs-lookup"><span data-stu-id="d6ab2-179">yes</span></span>      | <span data-ttu-id="d6ab2-180">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="d6ab2-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="d6ab2-181">Respuesta</span><span class="sxs-lookup"><span data-stu-id="d6ab2-181">Response</span></span>

<span data-ttu-id="d6ab2-182">Código de estado</span><span class="sxs-lookup"><span data-stu-id="d6ab2-182">Status Code</span></span> | <span data-ttu-id="d6ab2-183">Significado</span><span class="sxs-lookup"><span data-stu-id="d6ab2-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="d6ab2-184">204</span><span class="sxs-lookup"><span data-stu-id="d6ab2-184">204</span></span>         | <span data-ttu-id="d6ab2-185">Se eliminó el paquete</span><span class="sxs-lookup"><span data-stu-id="d6ab2-185">The package was deleted</span></span>
<span data-ttu-id="d6ab2-186">404</span><span class="sxs-lookup"><span data-stu-id="d6ab2-186">404</span></span>         | <span data-ttu-id="d6ab2-187">Ningún paquete con proporcionado `ID` y `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="d6ab2-187">No package with the provided `ID` and `VERSION` exists</span></span>
