---
title: Protocolos de NuGet.org | Documentos de Microsoft
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "Los protocolos de nuget.org en constante evolución para interactuar con los clientes de NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="19f8d-103">Protocolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="19f8d-103">nuget.org Protocols</span></span>

<span data-ttu-id="19f8d-104">Para interactuar con nuget.org, los clientes deben seguir ciertas protocolos.</span><span class="sxs-lookup"><span data-stu-id="19f8d-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="19f8d-105">Dado que estos protocolos mantengan evolucionando, los clientes deben identificar la versión de protocolo que se usan cuando se llama a nuget.org específico API.</span><span class="sxs-lookup"><span data-stu-id="19f8d-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="19f8d-106">Esto permite nuget.org introducir cambios de una manera poco problemático para los clientes anteriores.</span><span class="sxs-lookup"><span data-stu-id="19f8d-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="19f8d-107">Las API documentadas en esta página son específicas de nuget.org y no hay ninguna expectativa para otras implementaciones del servidor de NuGet introducir estas API.</span><span class="sxs-lookup"><span data-stu-id="19f8d-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="19f8d-108">Para obtener información acerca de la API de NuGet implementan ampliamente en el ecosistema de NuGet, consulte el [Introducción a la API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="19f8d-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="19f8d-109">Este tema enumeran varios protocolos como y cuando descubren a su existencia.</span><span class="sxs-lookup"><span data-stu-id="19f8d-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="19f8d-110">Versión de protocolo de NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="19f8d-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="19f8d-111">La 4.1.0 protocolo especifica el uso de claves de comprobar el ámbito para interactuar con los servicios que no sea nuget.org, para validar un paquete con una cuenta de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="19f8d-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="19f8d-112">Tenga en cuenta que el `4.1.0` versión número es una cadena opaca, pero no ocurre para que coincida con la primera versión del cliente NuGet oficial que admiten este protocolo.</span><span class="sxs-lookup"><span data-stu-id="19f8d-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="19f8d-113">La validación garantiza que las claves de API creados por el usuario sólo se utilizan con nuget.org, y que otros comprobación o validación de un servicio de terceros se controla mediante una clave de comprobar el ámbito de un solo uso.</span><span class="sxs-lookup"><span data-stu-id="19f8d-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="19f8d-114">Estas claves de comprobar el ámbito pueden usarse para validar que el paquete pertenece a un usuario determinado (cuenta) en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="19f8d-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="19f8d-115">Requisitos de cliente</span><span class="sxs-lookup"><span data-stu-id="19f8d-115">Client requirement</span></span>

<span data-ttu-id="19f8d-116">Los clientes tienen que pasar el encabezado siguiente cuando realicen llamadas de API a **inserción** paquetes en nuget.org:</span><span class="sxs-lookup"><span data-stu-id="19f8d-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="19f8d-117">Tenga en cuenta que la preexistente `X-NuGet-Client-Version` encabezado tiene el mismo propósito, pero está en desuso y ya no debe usarse.</span><span class="sxs-lookup"><span data-stu-id="19f8d-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="19f8d-118">El **inserción** protocolo en sí se describe en la documentación de la [ `PackagePublish` recursos](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="19f8d-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="19f8d-119">Si un cliente interactúa con servicios externos y necesidades para validar si un paquete pertenece a un usuario determinado (cuenta), debe usar el siguiente protocolo y utilizar las teclas de comprobar el ámbito y no las claves de API de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="19f8d-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="19f8d-120">API para solicitar una clave de comprobar el ámbito</span><span class="sxs-lookup"><span data-stu-id="19f8d-120">API to request a verify-scope key</span></span>

<span data-ttu-id="19f8d-121">Esta API se utiliza para obtener una clave de comprobar el ámbito de un autor nuget.org validar un paquete de la propiedad por él mismo.</span><span class="sxs-lookup"><span data-stu-id="19f8d-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="19f8d-122">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="19f8d-122">Request parameters</span></span>

<span data-ttu-id="19f8d-123">Name</span><span class="sxs-lookup"><span data-stu-id="19f8d-123">Name</span></span>           | <span data-ttu-id="19f8d-124">En</span><span class="sxs-lookup"><span data-stu-id="19f8d-124">In</span></span>     | <span data-ttu-id="19f8d-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="19f8d-125">Type</span></span>   | <span data-ttu-id="19f8d-126">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19f8d-126">Required</span></span> | <span data-ttu-id="19f8d-127">Notas</span><span class="sxs-lookup"><span data-stu-id="19f8d-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="19f8d-128">Id.</span><span class="sxs-lookup"><span data-stu-id="19f8d-128">ID</span></span>             | <span data-ttu-id="19f8d-129">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="19f8d-129">URL</span></span>    | <span data-ttu-id="19f8d-130">string</span><span class="sxs-lookup"><span data-stu-id="19f8d-130">string</span></span> | <span data-ttu-id="19f8d-131">sí</span><span class="sxs-lookup"><span data-stu-id="19f8d-131">yes</span></span>      | <span data-ttu-id="19f8d-132">El identidier de paquete para el que se solicita la clave de ámbito Compruebe</span><span class="sxs-lookup"><span data-stu-id="19f8d-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="19f8d-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="19f8d-133">VERSION</span></span>        | <span data-ttu-id="19f8d-134">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="19f8d-134">URL</span></span>    | <span data-ttu-id="19f8d-135">string</span><span class="sxs-lookup"><span data-stu-id="19f8d-135">string</span></span> | <span data-ttu-id="19f8d-136">No</span><span class="sxs-lookup"><span data-stu-id="19f8d-136">no</span></span>       | <span data-ttu-id="19f8d-137">La versión del paquete</span><span class="sxs-lookup"><span data-stu-id="19f8d-137">The package version</span></span>
<span data-ttu-id="19f8d-138">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="19f8d-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="19f8d-139">Header</span><span class="sxs-lookup"><span data-stu-id="19f8d-139">Header</span></span> | <span data-ttu-id="19f8d-140">string</span><span class="sxs-lookup"><span data-stu-id="19f8d-140">string</span></span> | <span data-ttu-id="19f8d-141">sí</span><span class="sxs-lookup"><span data-stu-id="19f8d-141">yes</span></span>      | <span data-ttu-id="19f8d-142">Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="19f8d-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="19f8d-143">Respuesta</span><span class="sxs-lookup"><span data-stu-id="19f8d-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="19f8d-144">API para comprobar la clave de ámbito Compruebe</span><span class="sxs-lookup"><span data-stu-id="19f8d-144">API to verify the verify scope key</span></span>

<span data-ttu-id="19f8d-145">Esta API se utiliza para validar una clave de comprobar el ámbito de paquete propiedad por el autor de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="19f8d-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="19f8d-146">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="19f8d-146">Request parameters</span></span>

<span data-ttu-id="19f8d-147">Name</span><span class="sxs-lookup"><span data-stu-id="19f8d-147">Name</span></span>           | <span data-ttu-id="19f8d-148">En</span><span class="sxs-lookup"><span data-stu-id="19f8d-148">In</span></span>     | <span data-ttu-id="19f8d-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="19f8d-149">Type</span></span>   | <span data-ttu-id="19f8d-150">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19f8d-150">Required</span></span> | <span data-ttu-id="19f8d-151">Notas</span><span class="sxs-lookup"><span data-stu-id="19f8d-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="19f8d-152">Id.</span><span class="sxs-lookup"><span data-stu-id="19f8d-152">ID</span></span>             | <span data-ttu-id="19f8d-153">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="19f8d-153">URL</span></span>    | <span data-ttu-id="19f8d-154">string</span><span class="sxs-lookup"><span data-stu-id="19f8d-154">string</span></span> | <span data-ttu-id="19f8d-155">sí</span><span class="sxs-lookup"><span data-stu-id="19f8d-155">yes</span></span>      | <span data-ttu-id="19f8d-156">El identificador de paquete para el que se solicita la clave de ámbito Compruebe</span><span class="sxs-lookup"><span data-stu-id="19f8d-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="19f8d-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="19f8d-157">VERSION</span></span>        | <span data-ttu-id="19f8d-158">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="19f8d-158">URL</span></span>    | <span data-ttu-id="19f8d-159">string</span><span class="sxs-lookup"><span data-stu-id="19f8d-159">string</span></span> | <span data-ttu-id="19f8d-160">No</span><span class="sxs-lookup"><span data-stu-id="19f8d-160">no</span></span>       | <span data-ttu-id="19f8d-161">La versión del paquete</span><span class="sxs-lookup"><span data-stu-id="19f8d-161">The package version</span></span>
<span data-ttu-id="19f8d-162">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="19f8d-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="19f8d-163">Header</span><span class="sxs-lookup"><span data-stu-id="19f8d-163">Header</span></span> | <span data-ttu-id="19f8d-164">string</span><span class="sxs-lookup"><span data-stu-id="19f8d-164">string</span></span> | <span data-ttu-id="19f8d-165">sí</span><span class="sxs-lookup"><span data-stu-id="19f8d-165">yes</span></span>      | <span data-ttu-id="19f8d-166">Por ejemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="19f8d-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="19f8d-167">Esta clave de API de ámbito Compruebe expira en un momento del día o use por primera vez, lo que ocurra primero.</span><span class="sxs-lookup"><span data-stu-id="19f8d-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="19f8d-168">Respuesta</span><span class="sxs-lookup"><span data-stu-id="19f8d-168">Response</span></span>

<span data-ttu-id="19f8d-169">Código de estado</span><span class="sxs-lookup"><span data-stu-id="19f8d-169">Status Code</span></span> | <span data-ttu-id="19f8d-170">Significado</span><span class="sxs-lookup"><span data-stu-id="19f8d-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="19f8d-171">200</span><span class="sxs-lookup"><span data-stu-id="19f8d-171">200</span></span>         | <span data-ttu-id="19f8d-172">La clave de API es válida</span><span class="sxs-lookup"><span data-stu-id="19f8d-172">The API key is valid</span></span>
<span data-ttu-id="19f8d-173">403</span><span class="sxs-lookup"><span data-stu-id="19f8d-173">403</span></span>         | <span data-ttu-id="19f8d-174">La clave de API no es válido o no autorizados para insertar en el paquete</span><span class="sxs-lookup"><span data-stu-id="19f8d-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="19f8d-175">404</span><span class="sxs-lookup"><span data-stu-id="19f8d-175">404</span></span>         | <span data-ttu-id="19f8d-176">El paquete al que hace referencia `ID` y `VERSION` (opcional) no existe</span><span class="sxs-lookup"><span data-stu-id="19f8d-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
