---
title: Insertar paquetes de símbolos, API de NuGet | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: El servicio de publicación permite a los clientes publicar nuevos paquetes de símbolos.
keywords: Paquete de símbolos de inserción de API de NuGet
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580418"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="48dca-104">Paquetes de símbolos de inserción</span><span class="sxs-lookup"><span data-stu-id="48dca-104">Push Symbol Packages</span></span>

<span data-ttu-id="48dca-105">Es posible insertar paquetes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mediante la API de NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="48dca-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="48dca-106">Estas operaciones se basa en el `SymbolPackagePublish` encontrar el recurso en el [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="48dca-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="48dca-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="48dca-107">Versioning</span></span>

<span data-ttu-id="48dca-108">La siguiente `@type` se usa el valor:</span><span class="sxs-lookup"><span data-stu-id="48dca-108">The following `@type` value is used:</span></span>

<span data-ttu-id="48dca-109">Valor de@type </span><span class="sxs-lookup"><span data-stu-id="48dca-109">@type value</span></span>                 | <span data-ttu-id="48dca-110">Notas</span><span class="sxs-lookup"><span data-stu-id="48dca-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="48dca-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="48dca-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="48dca-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="48dca-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="48dca-113">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="48dca-113">Base URL</span></span>

<span data-ttu-id="48dca-114">La dirección URL base para las siguientes API es el valor de la `@id` propiedad de la `SymbolPackagePublish/4.9.0` recursos en el origen de paquete [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="48dca-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="48dca-115">Para obtener la documentación a continuación, se usa la dirección URL de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="48dca-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="48dca-116">Considere la posibilidad de `https://www.nuget.org/api/v2/symbolpackage` como marcador de posición para el `@id` valor se encuentra en el índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="48dca-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="48dca-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="48dca-117">HTTP methods</span></span>

<span data-ttu-id="48dca-118">El `PUT` método HTTP es compatible con este recurso.</span><span class="sxs-lookup"><span data-stu-id="48dca-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="48dca-119">Insertar un paquete de símbolos</span><span class="sxs-lookup"><span data-stu-id="48dca-119">Push a symbol package</span></span>

<span data-ttu-id="48dca-120">NuGet.org admite Insertar nuevo formato de paquetes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mediante la API siguiente.</span><span class="sxs-lookup"><span data-stu-id="48dca-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="48dca-121">Paquetes de símbolos con el mismo identificador y versión se pueden enviar varias veces.</span><span class="sxs-lookup"><span data-stu-id="48dca-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="48dca-122">En los casos siguientes, se rechazarán un paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="48dca-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="48dca-123">No existe un paquete con el mismo identificador y versión.</span><span class="sxs-lookup"><span data-stu-id="48dca-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="48dca-124">Un paquete de símbolos con el mismo identificador y versión se ha insertado, pero no se ha publicado.</span><span class="sxs-lookup"><span data-stu-id="48dca-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="48dca-125">El paquete de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) no es válido (consulte [restricciones del paquete de símbolos](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="48dca-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="48dca-126">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="48dca-126">Request parameters</span></span>

<span data-ttu-id="48dca-127">nombre</span><span class="sxs-lookup"><span data-stu-id="48dca-127">Name</span></span>           | <span data-ttu-id="48dca-128">En</span><span class="sxs-lookup"><span data-stu-id="48dca-128">In</span></span>     | <span data-ttu-id="48dca-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="48dca-129">Type</span></span>   | <span data-ttu-id="48dca-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="48dca-130">Required</span></span> | <span data-ttu-id="48dca-131">Notas</span><span class="sxs-lookup"><span data-stu-id="48dca-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="48dca-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="48dca-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="48dca-133">Header</span><span class="sxs-lookup"><span data-stu-id="48dca-133">Header</span></span> | <span data-ttu-id="48dca-134">cadena</span><span class="sxs-lookup"><span data-stu-id="48dca-134">string</span></span> | <span data-ttu-id="48dca-135">sí</span><span class="sxs-lookup"><span data-stu-id="48dca-135">yes</span></span>      | <span data-ttu-id="48dca-136">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="48dca-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="48dca-137">La clave de API es una cadena opaca llegado desde el origen del paquete por el usuario y configurado en el cliente.</span><span class="sxs-lookup"><span data-stu-id="48dca-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="48dca-138">Ningún formato de cadena concreta está asignada, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores de encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="48dca-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="48dca-139">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="48dca-139">Request body</span></span>

<span data-ttu-id="48dca-140">El cuerpo de solicitud para la inserción de símbolos es igual que con el cuerpo de solicitud de una solicitud de inserción del paquete (consulte [empaquetar la inserción y eliminación](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="48dca-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="48dca-141">Respuesta</span><span class="sxs-lookup"><span data-stu-id="48dca-141">Response</span></span>

<span data-ttu-id="48dca-142">Código de estado</span><span class="sxs-lookup"><span data-stu-id="48dca-142">Status Code</span></span> | <span data-ttu-id="48dca-143">Significado</span><span class="sxs-lookup"><span data-stu-id="48dca-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="48dca-144">201</span><span class="sxs-lookup"><span data-stu-id="48dca-144">201</span></span>         | <span data-ttu-id="48dca-145">El paquete de símbolos se ha insertado correctamente.</span><span class="sxs-lookup"><span data-stu-id="48dca-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="48dca-146">400</span><span class="sxs-lookup"><span data-stu-id="48dca-146">400</span></span>         | <span data-ttu-id="48dca-147">El paquete de símbolos proporcionado no es válido.</span><span class="sxs-lookup"><span data-stu-id="48dca-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="48dca-148">401</span><span class="sxs-lookup"><span data-stu-id="48dca-148">401</span></span>         | <span data-ttu-id="48dca-149">El usuario no está autorizado para realizar esta acción.</span><span class="sxs-lookup"><span data-stu-id="48dca-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="48dca-150">404</span><span class="sxs-lookup"><span data-stu-id="48dca-150">404</span></span>         | <span data-ttu-id="48dca-151">No existe un paquete con el identificador proporcionado y la versión correspondiente.</span><span class="sxs-lookup"><span data-stu-id="48dca-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="48dca-152">409</span><span class="sxs-lookup"><span data-stu-id="48dca-152">409</span></span>         | <span data-ttu-id="48dca-153">Se ha insertado un paquete de símbolos con el identificador proporcionado y la versión, pero aún no está disponible.</span><span class="sxs-lookup"><span data-stu-id="48dca-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="48dca-154">413</span><span class="sxs-lookup"><span data-stu-id="48dca-154">413</span></span>         | <span data-ttu-id="48dca-155">El paquete es demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="48dca-155">The package is too large.</span></span>

