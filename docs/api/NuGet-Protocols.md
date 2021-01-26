---
title: Protocolos de nuget.org
description: Los protocolos nuget.org en evolución para interactuar con los clientes de NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773970"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="7243b-103">Protocolos de nuget.org</span><span class="sxs-lookup"><span data-stu-id="7243b-103">nuget.org protocols</span></span>

<span data-ttu-id="7243b-104">Para interactuar con nuget.org, los clientes deben seguir determinados protocolos.</span><span class="sxs-lookup"><span data-stu-id="7243b-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="7243b-105">Dado que estos protocolos siguen evolucionando, los clientes deben identificar la versión del protocolo que usan al llamar a determinadas API de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7243b-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="7243b-106">Esto permite a nuget.org introducir cambios en una forma ininterrumpida para los clientes anteriores.</span><span class="sxs-lookup"><span data-stu-id="7243b-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="7243b-107">Las API documentadas en esta página son específicas de nuget.org y no se espera que otras implementaciones de servidor NuGet presenten estas API.</span><span class="sxs-lookup"><span data-stu-id="7243b-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="7243b-108">Para obtener información sobre la API de NuGet implementada en general en el ecosistema de NuGet, consulte la [Introducción a la API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="7243b-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="7243b-109">En este tema se enumeran varios protocolos como y cuando llegan a su existencia.</span><span class="sxs-lookup"><span data-stu-id="7243b-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="7243b-110">Versión del protocolo NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="7243b-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="7243b-111">El protocolo 4.1.0 especifica el uso de claves Verify-Scope para interactuar con servicios distintos de nuget.org, para validar un paquete con una cuenta nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7243b-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="7243b-112">Tenga en cuenta que el `4.1.0` número de versión es una cadena opaca pero que coincide con la primera versión del cliente de NuGet oficial que admitía este protocolo.</span><span class="sxs-lookup"><span data-stu-id="7243b-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="7243b-113">La validación garantiza que las claves de API creadas por el usuario solo se usan con nuget.org y que otras comprobaciones o validaciones de un servicio de terceros se controlan a través de las claves Verify-Scope de un solo uso.</span><span class="sxs-lookup"><span data-stu-id="7243b-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="7243b-114">Estas claves Verify-Scope se pueden usar para validar que el paquete pertenece a un usuario determinado (cuenta) en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7243b-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="7243b-115">Requisitos del cliente</span><span class="sxs-lookup"><span data-stu-id="7243b-115">Client requirement</span></span>

<span data-ttu-id="7243b-116">Los clientes deben pasar el encabezado siguiente cuando realizan llamadas API para **enviar paquetes a** Nuget.org:</span><span class="sxs-lookup"><span data-stu-id="7243b-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="7243b-117">Tenga en cuenta que el `X-NuGet-Client-Version` encabezado tiene una semántica similar pero que se reserva para que solo lo use el cliente de NuGet oficial.</span><span class="sxs-lookup"><span data-stu-id="7243b-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="7243b-118">Los clientes de terceros deben usar el `X-NuGet-Protocol-Version` encabezado y el valor.</span><span class="sxs-lookup"><span data-stu-id="7243b-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="7243b-119">El protocolo de **extracción** en sí se describe en la documentación del [ `PackagePublish` recurso](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7243b-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="7243b-120">Si un cliente interactúa con servicios externos y necesita validar si un paquete pertenece a un usuario determinado (cuenta), debe usar el protocolo siguiente y usar las claves Verify-Scope y no las claves de API de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7243b-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="7243b-121">API para solicitar una clave Verify-Scope</span><span class="sxs-lookup"><span data-stu-id="7243b-121">API to request a verify-scope key</span></span>

<span data-ttu-id="7243b-122">Esta API se usa para obtener una clave Verify-Scope para que un autor de nuget.org valide un paquete propiedad de él.</span><span class="sxs-lookup"><span data-stu-id="7243b-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="7243b-123">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="7243b-123">Request parameters</span></span>

<span data-ttu-id="7243b-124">Nombre</span><span class="sxs-lookup"><span data-stu-id="7243b-124">Name</span></span>           | <span data-ttu-id="7243b-125">En</span><span class="sxs-lookup"><span data-stu-id="7243b-125">In</span></span>     | <span data-ttu-id="7243b-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="7243b-126">Type</span></span>   | <span data-ttu-id="7243b-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7243b-127">Required</span></span> | <span data-ttu-id="7243b-128">Notas</span><span class="sxs-lookup"><span data-stu-id="7243b-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7243b-129">ID</span><span class="sxs-lookup"><span data-stu-id="7243b-129">ID</span></span>             | <span data-ttu-id="7243b-130">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="7243b-130">URL</span></span>    | <span data-ttu-id="7243b-131">string</span><span class="sxs-lookup"><span data-stu-id="7243b-131">string</span></span> | <span data-ttu-id="7243b-132">sí</span><span class="sxs-lookup"><span data-stu-id="7243b-132">yes</span></span>      | <span data-ttu-id="7243b-133">El paquete identidier para el que se solicita la clave de ámbito de comprobación.</span><span class="sxs-lookup"><span data-stu-id="7243b-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="7243b-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="7243b-134">VERSION</span></span>        | <span data-ttu-id="7243b-135">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="7243b-135">URL</span></span>    | <span data-ttu-id="7243b-136">string</span><span class="sxs-lookup"><span data-stu-id="7243b-136">string</span></span> | <span data-ttu-id="7243b-137">no</span><span class="sxs-lookup"><span data-stu-id="7243b-137">no</span></span>       | <span data-ttu-id="7243b-138">La versión del paquete</span><span class="sxs-lookup"><span data-stu-id="7243b-138">The package version</span></span>
<span data-ttu-id="7243b-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7243b-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7243b-140">Encabezado</span><span class="sxs-lookup"><span data-stu-id="7243b-140">Header</span></span> | <span data-ttu-id="7243b-141">string</span><span class="sxs-lookup"><span data-stu-id="7243b-141">string</span></span> | <span data-ttu-id="7243b-142">sí</span><span class="sxs-lookup"><span data-stu-id="7243b-142">yes</span></span>      | <span data-ttu-id="7243b-143">Por ejemplo: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="7243b-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="7243b-144">Response</span><span class="sxs-lookup"><span data-stu-id="7243b-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="7243b-145">API para comprobar la clave de ámbito de comprobación</span><span class="sxs-lookup"><span data-stu-id="7243b-145">API to verify the verify scope key</span></span>

<span data-ttu-id="7243b-146">Esta API se usa para validar una clave Verify-Scope para el paquete propiedad del autor de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7243b-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="7243b-147">Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="7243b-147">Request parameters</span></span>

<span data-ttu-id="7243b-148">Nombre</span><span class="sxs-lookup"><span data-stu-id="7243b-148">Name</span></span>           | <span data-ttu-id="7243b-149">En</span><span class="sxs-lookup"><span data-stu-id="7243b-149">In</span></span>     | <span data-ttu-id="7243b-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="7243b-150">Type</span></span>   | <span data-ttu-id="7243b-151">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7243b-151">Required</span></span> | <span data-ttu-id="7243b-152">Notas</span><span class="sxs-lookup"><span data-stu-id="7243b-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="7243b-153">ID</span><span class="sxs-lookup"><span data-stu-id="7243b-153">ID</span></span>             | <span data-ttu-id="7243b-154">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="7243b-154">URL</span></span>    | <span data-ttu-id="7243b-155">string</span><span class="sxs-lookup"><span data-stu-id="7243b-155">string</span></span> | <span data-ttu-id="7243b-156">sí</span><span class="sxs-lookup"><span data-stu-id="7243b-156">yes</span></span>      | <span data-ttu-id="7243b-157">Identificador del paquete para el que se solicita la clave de ámbito de comprobación.</span><span class="sxs-lookup"><span data-stu-id="7243b-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="7243b-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="7243b-158">VERSION</span></span>        | <span data-ttu-id="7243b-159">Dirección URL</span><span class="sxs-lookup"><span data-stu-id="7243b-159">URL</span></span>    | <span data-ttu-id="7243b-160">string</span><span class="sxs-lookup"><span data-stu-id="7243b-160">string</span></span> | <span data-ttu-id="7243b-161">no</span><span class="sxs-lookup"><span data-stu-id="7243b-161">no</span></span>       | <span data-ttu-id="7243b-162">La versión del paquete</span><span class="sxs-lookup"><span data-stu-id="7243b-162">The package version</span></span>
<span data-ttu-id="7243b-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7243b-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7243b-164">Encabezado</span><span class="sxs-lookup"><span data-stu-id="7243b-164">Header</span></span> | <span data-ttu-id="7243b-165">string</span><span class="sxs-lookup"><span data-stu-id="7243b-165">string</span></span> | <span data-ttu-id="7243b-166">sí</span><span class="sxs-lookup"><span data-stu-id="7243b-166">yes</span></span>      | <span data-ttu-id="7243b-167">Por ejemplo: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="7243b-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="7243b-168">Esto comprueba que la clave de API de ámbito expire en el momento del día o en el primer uso, lo que ocurra primero.</span><span class="sxs-lookup"><span data-stu-id="7243b-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="7243b-169">Response</span><span class="sxs-lookup"><span data-stu-id="7243b-169">Response</span></span>

<span data-ttu-id="7243b-170">Código de estado</span><span class="sxs-lookup"><span data-stu-id="7243b-170">Status Code</span></span> | <span data-ttu-id="7243b-171">Significado</span><span class="sxs-lookup"><span data-stu-id="7243b-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="7243b-172">200</span><span class="sxs-lookup"><span data-stu-id="7243b-172">200</span></span>         | <span data-ttu-id="7243b-173">La clave de API es válida</span><span class="sxs-lookup"><span data-stu-id="7243b-173">The API key is valid</span></span>
<span data-ttu-id="7243b-174">403</span><span class="sxs-lookup"><span data-stu-id="7243b-174">403</span></span>         | <span data-ttu-id="7243b-175">La clave de API no es válida o no está autorizada para la inserciones en el paquete</span><span class="sxs-lookup"><span data-stu-id="7243b-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="7243b-176">404</span><span class="sxs-lookup"><span data-stu-id="7243b-176">404</span></span>         | <span data-ttu-id="7243b-177">El paquete al que hace referencia `ID` y `VERSION` (opcional) no existe.</span><span class="sxs-lookup"><span data-stu-id="7243b-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
