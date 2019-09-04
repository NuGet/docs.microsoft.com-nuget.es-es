---
title: Paquetes de símbolos de envío, API de NuGet | Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: El servicio de publicación permite a los clientes publicar paquetes de símbolos nuevos.
keywords: Paquete de símbolos de la API de NuGet
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235107"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="2221b-104">Paquetes de símbolos de envío</span><span class="sxs-lookup"><span data-stu-id="2221b-104">Push Symbol Packages</span></span>

<span data-ttu-id="2221b-105">Es posible insertar paquetes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mediante la API de NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="2221b-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="2221b-106">Estas operaciones se basan en el recurso `SymbolPackagePublish` que se encuentra en el [Índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="2221b-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2221b-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="2221b-107">Versioning</span></span>

<span data-ttu-id="2221b-108">Se usa `@type` el siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="2221b-108">The following `@type` value is used:</span></span>

<span data-ttu-id="2221b-109">Valor de@type</span><span class="sxs-lookup"><span data-stu-id="2221b-109">@type value</span></span>                 | <span data-ttu-id="2221b-110">Notas</span><span class="sxs-lookup"><span data-stu-id="2221b-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="2221b-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="2221b-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="2221b-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="2221b-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="2221b-113">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="2221b-113">Base URL</span></span>

<span data-ttu-id="2221b-114">La dirección URL base para las siguientes API es el valor de `@id` la propiedad `SymbolPackagePublish/4.9.0` del recurso en el [Índice de servicio](service-index.md)del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="2221b-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="2221b-115">En la documentación siguiente, se usa la dirección URL de Nuget. org.</span><span class="sxs-lookup"><span data-stu-id="2221b-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="2221b-116">Considere `https://www.nuget.org/api/v2/symbolpackage` como un marcador de posición `@id` para el valor que se encuentra en el índice de servicio.</span><span class="sxs-lookup"><span data-stu-id="2221b-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2221b-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="2221b-117">HTTP methods</span></span>

<span data-ttu-id="2221b-118">Este `PUT` recurso admite el método http.</span><span class="sxs-lookup"><span data-stu-id="2221b-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="2221b-119">Inserte un paquete de símbolos</span><span class="sxs-lookup"><span data-stu-id="2221b-119">Push a symbol package</span></span>

<span data-ttu-id="2221b-120">nuget.org admite la inserción del nuevo formato de paquetes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mediante la siguiente API.</span><span class="sxs-lookup"><span data-stu-id="2221b-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="2221b-121">Los paquetes de símbolos con el mismo identificador y versión se pueden enviar varias veces.</span><span class="sxs-lookup"><span data-stu-id="2221b-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="2221b-122">Un paquete de símbolos se rechazará en los casos siguientes.</span><span class="sxs-lookup"><span data-stu-id="2221b-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="2221b-123">No existe un paquete con el mismo identificador y versión.</span><span class="sxs-lookup"><span data-stu-id="2221b-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="2221b-124">Se insertó un paquete de símbolos con el mismo identificador y versión, pero aún no se ha publicado.</span><span class="sxs-lookup"><span data-stu-id="2221b-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="2221b-125">El paquete de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) no es válido (vea [restricciones de paquetes de símbolos](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="2221b-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="2221b-126">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="2221b-126">Request parameters</span></span>

<span data-ttu-id="2221b-127">NOMBRE</span><span class="sxs-lookup"><span data-stu-id="2221b-127">Name</span></span>           | <span data-ttu-id="2221b-128">En</span><span class="sxs-lookup"><span data-stu-id="2221b-128">In</span></span>     | <span data-ttu-id="2221b-129">Type</span><span class="sxs-lookup"><span data-stu-id="2221b-129">Type</span></span>   | <span data-ttu-id="2221b-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2221b-130">Required</span></span> | <span data-ttu-id="2221b-131">Notas</span><span class="sxs-lookup"><span data-stu-id="2221b-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2221b-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2221b-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2221b-133">Encabezado</span><span class="sxs-lookup"><span data-stu-id="2221b-133">Header</span></span> | <span data-ttu-id="2221b-134">string</span><span class="sxs-lookup"><span data-stu-id="2221b-134">string</span></span> | <span data-ttu-id="2221b-135">sí</span><span class="sxs-lookup"><span data-stu-id="2221b-135">yes</span></span>      | <span data-ttu-id="2221b-136">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2221b-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="2221b-137">La clave de API es una cadena opaca procedente del origen del paquete por el usuario y configurada en el cliente.</span><span class="sxs-lookup"><span data-stu-id="2221b-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="2221b-138">No se asigna ningún formato de cadena determinado, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores del encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="2221b-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="2221b-139">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2221b-139">Request body</span></span>

<span data-ttu-id="2221b-140">El cuerpo de la solicitud para la inserciones de símbolos es igual que con el cuerpo de la solicitud de una solicitud de envío de paquete (consulte la [Introducción y eliminación de paquetes](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="2221b-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="2221b-141">Respuesta</span><span class="sxs-lookup"><span data-stu-id="2221b-141">Response</span></span>

<span data-ttu-id="2221b-142">Código de estado</span><span class="sxs-lookup"><span data-stu-id="2221b-142">Status Code</span></span> | <span data-ttu-id="2221b-143">Significado</span><span class="sxs-lookup"><span data-stu-id="2221b-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="2221b-144">201</span><span class="sxs-lookup"><span data-stu-id="2221b-144">201</span></span>         | <span data-ttu-id="2221b-145">El paquete de símbolos se insertó correctamente.</span><span class="sxs-lookup"><span data-stu-id="2221b-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="2221b-146">400</span><span class="sxs-lookup"><span data-stu-id="2221b-146">400</span></span>         | <span data-ttu-id="2221b-147">El paquete de símbolos proporcionado no es válido.</span><span class="sxs-lookup"><span data-stu-id="2221b-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="2221b-148">401</span><span class="sxs-lookup"><span data-stu-id="2221b-148">401</span></span>         | <span data-ttu-id="2221b-149">El usuario no está autorizado para realizar esta acción.</span><span class="sxs-lookup"><span data-stu-id="2221b-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="2221b-150">404</span><span class="sxs-lookup"><span data-stu-id="2221b-150">404</span></span>         | <span data-ttu-id="2221b-151">No existe un paquete correspondiente con el identificador y la versión proporcionados.</span><span class="sxs-lookup"><span data-stu-id="2221b-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="2221b-152">409</span><span class="sxs-lookup"><span data-stu-id="2221b-152">409</span></span>         | <span data-ttu-id="2221b-153">Se insertó un paquete de símbolos con el identificador y la versión proporcionados, pero aún no está disponible.</span><span class="sxs-lookup"><span data-stu-id="2221b-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="2221b-154">413</span><span class="sxs-lookup"><span data-stu-id="2221b-154">413</span></span>         | <span data-ttu-id="2221b-155">El paquete es demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="2221b-155">The package is too large.</span></span>

