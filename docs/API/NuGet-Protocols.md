---
title: Protocolos de NuGet.org | Documentos de Microsoft
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Los protocolos de nuget.org en constante evolución para interactuar con los clientes de NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 488a86a36a6bc83c91f0182bf437ddb83e707e31
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="0a234-103">protocolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="0a234-103">nuget.org protocols</span></span>

<span data-ttu-id="0a234-104">Para interactuar con nuget.org, los clientes deben seguir ciertas protocolos.</span><span class="sxs-lookup"><span data-stu-id="0a234-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="0a234-105">Dado que estos protocolos mantengan evolucionando, los clientes deben identificar la versión de protocolo que se usan cuando se llama a nuget.org específico API.</span><span class="sxs-lookup"><span data-stu-id="0a234-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="0a234-106">Esto permite nuget.org introducir cambios de una manera poco problemático para los clientes anteriores.</span><span class="sxs-lookup"><span data-stu-id="0a234-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="0a234-107">Las API documentadas en esta página son específicas de nuget.org y no hay ninguna expectativa para otras implementaciones del servidor de NuGet introducir estas API.</span><span class="sxs-lookup"><span data-stu-id="0a234-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="0a234-108">Para obtener información acerca de la API de NuGet implementan ampliamente en el ecosistema de NuGet, consulte el [Introducción a la API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a234-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="0a234-109">Este tema enumeran varios protocolos como y cuando descubren a su existencia.</span><span class="sxs-lookup"><span data-stu-id="0a234-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="0a234-110">Versión de protocolo de NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="0a234-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="0a234-111">La 4.1.0 protocolo especifica el uso de claves de comprobar el ámbito para interactuar con los servicios que no sea nuget.org, para validar un paquete con una cuenta de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0a234-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="0a234-112">Tenga en cuenta que el `4.1.0` versión número es una cadena opaca, pero no ocurre para que coincida con la primera versión del cliente NuGet oficial que admiten este protocolo.</span><span class="sxs-lookup"><span data-stu-id="0a234-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="0a234-113">La validación garantiza que las claves de API creados por el usuario sólo se utilizan con nuget.org, y que otros comprobación o validación de un servicio de terceros se controla mediante una clave de comprobar el ámbito de un solo uso.</span><span class="sxs-lookup"><span data-stu-id="0a234-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="0a234-114">Estas claves de comprobar el ámbito pueden usarse para validar que el paquete pertenece a un usuario determinado (cuenta) en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0a234-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="0a234-115">Requisitos de cliente</span><span class="sxs-lookup"><span data-stu-id="0a234-115">Client requirement</span></span>

<span data-ttu-id="0a234-116">Los clientes tienen que pasar el encabezado siguiente cuando realicen llamadas de API a **inserción** paquetes en nuget.org:</span><span class="sxs-lookup"><span data-stu-id="0a234-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="0a234-117">Tenga en cuenta que el `X-NuGet-Client-Version` encabezado tiene una semántica similar pero está reservado solo se puede usar el cliente de NuGet oficial.</span><span class="sxs-lookup"><span data-stu-id="0a234-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="0a234-118">Los clientes de otros fabricantes deben usar el `X-NuGet-Protocol-Version` encabezado y valor.</span><span class="sxs-lookup"><span data-stu-id="0a234-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="0a234-119">El **inserción** protocolo en sí se describe en la documentación de la [ `PackagePublish` recursos](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="0a234-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="0a234-120">Si un cliente interactúa con servicios externos y necesidades para validar si un paquete pertenece a un usuario determinado (cuenta), debe usar el siguiente protocolo y utilizar las teclas de comprobar el ámbito y no las claves de API de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0a234-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="0a234-121">API para solicitar una clave de comprobar el ámbito</span><span class="sxs-lookup"><span data-stu-id="0a234-121">API to request a verify-scope key</span></span>

<span data-ttu-id="0a234-122">Esta API se utiliza para obtener una clave de comprobar el ámbito de un autor nuget.org validar un paquete de la propiedad por él mismo.</span><span class="sxs-lookup"><span data-stu-id="0a234-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="0a234-123">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="0a234-123">Request parameters</span></span>

<span data-ttu-id="0a234-124">nombre</span><span class="sxs-lookup"><span data-stu-id="0a234-124">Name</span></span>           | <span data-ttu-id="0a234-125">En</span><span class="sxs-lookup"><span data-stu-id="0a234-125">In</span></span>     | <span data-ttu-id="0a234-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="0a234-126">Type</span></span>   | <span data-ttu-id="0a234-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0a234-127">Required</span></span> | <span data-ttu-id="0a234-128">Notas</span><span class="sxs-lookup"><span data-stu-id="0a234-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="0a234-129">Id.</span><span class="sxs-lookup"><span data-stu-id="0a234-129">ID</span></span>             | <span data-ttu-id="0a234-130">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="0a234-130">URL</span></span>    | <span data-ttu-id="0a234-131">cadena</span><span class="sxs-lookup"><span data-stu-id="0a234-131">string</span></span> | <span data-ttu-id="0a234-132">sí</span><span class="sxs-lookup"><span data-stu-id="0a234-132">yes</span></span>      | <span data-ttu-id="0a234-133">El identidier de paquete para el que se solicita la clave de ámbito Compruebe</span><span class="sxs-lookup"><span data-stu-id="0a234-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="0a234-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="0a234-134">VERSION</span></span>        | <span data-ttu-id="0a234-135">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="0a234-135">URL</span></span>    | <span data-ttu-id="0a234-136">cadena</span><span class="sxs-lookup"><span data-stu-id="0a234-136">string</span></span> | <span data-ttu-id="0a234-137">No</span><span class="sxs-lookup"><span data-stu-id="0a234-137">no</span></span>       | <span data-ttu-id="0a234-138">La versión del paquete</span><span class="sxs-lookup"><span data-stu-id="0a234-138">The package version</span></span>
<span data-ttu-id="0a234-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="0a234-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="0a234-140">Header</span><span class="sxs-lookup"><span data-stu-id="0a234-140">Header</span></span> | <span data-ttu-id="0a234-141">cadena</span><span class="sxs-lookup"><span data-stu-id="0a234-141">string</span></span> | <span data-ttu-id="0a234-142">sí</span><span class="sxs-lookup"><span data-stu-id="0a234-142">yes</span></span>      | <span data-ttu-id="0a234-143">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="0a234-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="0a234-144">Respuesta</span><span class="sxs-lookup"><span data-stu-id="0a234-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="0a234-145">API para comprobar la clave de ámbito Compruebe</span><span class="sxs-lookup"><span data-stu-id="0a234-145">API to verify the verify scope key</span></span>

<span data-ttu-id="0a234-146">Esta API se utiliza para validar una clave de comprobar el ámbito de paquete propiedad por el autor de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0a234-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="0a234-147">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="0a234-147">Request parameters</span></span>

<span data-ttu-id="0a234-148">nombre</span><span class="sxs-lookup"><span data-stu-id="0a234-148">Name</span></span>           | <span data-ttu-id="0a234-149">En</span><span class="sxs-lookup"><span data-stu-id="0a234-149">In</span></span>     | <span data-ttu-id="0a234-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="0a234-150">Type</span></span>   | <span data-ttu-id="0a234-151">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0a234-151">Required</span></span> | <span data-ttu-id="0a234-152">Notas</span><span class="sxs-lookup"><span data-stu-id="0a234-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="0a234-153">Id.</span><span class="sxs-lookup"><span data-stu-id="0a234-153">ID</span></span>             | <span data-ttu-id="0a234-154">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="0a234-154">URL</span></span>    | <span data-ttu-id="0a234-155">cadena</span><span class="sxs-lookup"><span data-stu-id="0a234-155">string</span></span> | <span data-ttu-id="0a234-156">sí</span><span class="sxs-lookup"><span data-stu-id="0a234-156">yes</span></span>      | <span data-ttu-id="0a234-157">El identificador de paquete para el que se solicita la clave de ámbito Compruebe</span><span class="sxs-lookup"><span data-stu-id="0a234-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="0a234-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="0a234-158">VERSION</span></span>        | <span data-ttu-id="0a234-159">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="0a234-159">URL</span></span>    | <span data-ttu-id="0a234-160">cadena</span><span class="sxs-lookup"><span data-stu-id="0a234-160">string</span></span> | <span data-ttu-id="0a234-161">No</span><span class="sxs-lookup"><span data-stu-id="0a234-161">no</span></span>       | <span data-ttu-id="0a234-162">La versión del paquete</span><span class="sxs-lookup"><span data-stu-id="0a234-162">The package version</span></span>
<span data-ttu-id="0a234-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="0a234-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="0a234-164">Header</span><span class="sxs-lookup"><span data-stu-id="0a234-164">Header</span></span> | <span data-ttu-id="0a234-165">cadena</span><span class="sxs-lookup"><span data-stu-id="0a234-165">string</span></span> | <span data-ttu-id="0a234-166">sí</span><span class="sxs-lookup"><span data-stu-id="0a234-166">yes</span></span>      | <span data-ttu-id="0a234-167">Por ejemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="0a234-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="0a234-168">Esta clave de API de ámbito Compruebe expira en un momento del día o use por primera vez, lo que ocurra primero.</span><span class="sxs-lookup"><span data-stu-id="0a234-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="0a234-169">Respuesta</span><span class="sxs-lookup"><span data-stu-id="0a234-169">Response</span></span>

<span data-ttu-id="0a234-170">Código de estado</span><span class="sxs-lookup"><span data-stu-id="0a234-170">Status Code</span></span> | <span data-ttu-id="0a234-171">Significado</span><span class="sxs-lookup"><span data-stu-id="0a234-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="0a234-172">200</span><span class="sxs-lookup"><span data-stu-id="0a234-172">200</span></span>         | <span data-ttu-id="0a234-173">La clave de API es válida</span><span class="sxs-lookup"><span data-stu-id="0a234-173">The API key is valid</span></span>
<span data-ttu-id="0a234-174">403</span><span class="sxs-lookup"><span data-stu-id="0a234-174">403</span></span>         | <span data-ttu-id="0a234-175">La clave de API no es válido o no autorizados para insertar en el paquete</span><span class="sxs-lookup"><span data-stu-id="0a234-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="0a234-176">404</span><span class="sxs-lookup"><span data-stu-id="0a234-176">404</span></span>         | <span data-ttu-id="0a234-177">El paquete al que hace referencia `ID` y `VERSION` (opcional) no existe</span><span class="sxs-lookup"><span data-stu-id="0a234-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
