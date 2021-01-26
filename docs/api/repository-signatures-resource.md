---
title: Firmas del repositorio, API de NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: El recurso firmas de repositorio permite a los clientes empaquetar orígenes para anunciar sus capacidades de firma de repositorios.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775335"
---
# <a name="repository-signatures"></a><span data-ttu-id="c2305-103">Firmas de repositorio</span><span class="sxs-lookup"><span data-stu-id="c2305-103">Repository signatures</span></span>

<span data-ttu-id="c2305-104">Si un origen de paquete permite agregar firmas de repositorio a paquetes publicados, es posible que un cliente determine los certificados de firma utilizados por el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="c2305-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="c2305-105">Este recurso permite a los clientes detectar si un paquete firmado con el repositorio se ha manipulado o tiene un certificado de firma inesperado.</span><span class="sxs-lookup"><span data-stu-id="c2305-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="c2305-106">El recurso que se usa para obtener la información de la firma del repositorio es el `RepositorySignatures` recurso que se encuentra en el [Índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c2305-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c2305-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="c2305-107">Versioning</span></span>

<span data-ttu-id="c2305-108">`@type`Se usa el siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="c2305-108">The following `@type` value is used:</span></span>

<span data-ttu-id="c2305-109">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="c2305-109">@type value</span></span>                | <span data-ttu-id="c2305-110">Notas</span><span class="sxs-lookup"><span data-stu-id="c2305-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="c2305-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="c2305-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="c2305-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="c2305-112">The initial release</span></span>
<span data-ttu-id="c2305-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="c2305-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="c2305-114">Compatible con los clientes de NuGet v 4.9 +</span><span class="sxs-lookup"><span data-stu-id="c2305-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="c2305-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="c2305-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="c2305-116">Permite habilitar `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="c2305-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="c2305-117">Compatible con clientes de NuGet v 5.0 +</span><span class="sxs-lookup"><span data-stu-id="c2305-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="c2305-118">URL base</span><span class="sxs-lookup"><span data-stu-id="c2305-118">Base URL</span></span>

<span data-ttu-id="c2305-119">La dirección URL del punto de entrada para las siguientes API es el valor de la `@id` propiedad asociada al valor de recurso mencionado anteriormente `@type` .</span><span class="sxs-lookup"><span data-stu-id="c2305-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="c2305-120">En este tema se utiliza la dirección URL del marcador de posición `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="c2305-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="c2305-121">Tenga en cuenta que, a diferencia de otros recursos, `{@id}` se requiere que la dirección URL se atienda a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c2305-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c2305-122">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="c2305-122">HTTP methods</span></span>

<span data-ttu-id="c2305-123">Todas las direcciones URL encontradas en el recurso de firmas de repositorio solo admiten los métodos HTTP `GET` y `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="c2305-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="c2305-124">Índice de firmas de repositorio</span><span class="sxs-lookup"><span data-stu-id="c2305-124">Repository signatures index</span></span>

<span data-ttu-id="c2305-125">El índice de firmas de repositorio contiene dos fragmentos de información:</span><span class="sxs-lookup"><span data-stu-id="c2305-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="c2305-126">Indica si todos los paquetes que se encuentran en el origen están firmados por este origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="c2305-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="c2305-127">Lista de certificados utilizados por el origen del paquete para firmar paquetes.</span><span class="sxs-lookup"><span data-stu-id="c2305-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="c2305-128">En la mayoría de los casos, la lista de certificados solo se anexará a.</span><span class="sxs-lookup"><span data-stu-id="c2305-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="c2305-129">Los nuevos certificados se agregan a la lista cuando el certificado de firma anterior ha expirado y el origen del paquete debe empezar a usar un nuevo certificado de firma.</span><span class="sxs-lookup"><span data-stu-id="c2305-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="c2305-130">Si se quita un certificado de la lista, eso significa que todas las firmas de paquete creadas con el certificado de firma quitado ya no deben considerarse válidas para el cliente.</span><span class="sxs-lookup"><span data-stu-id="c2305-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="c2305-131">En este caso, la firma del paquete (pero no necesariamente el paquete) no es válida.</span><span class="sxs-lookup"><span data-stu-id="c2305-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="c2305-132">Una directiva de cliente puede permitir la instalación del paquete como sin firmar.</span><span class="sxs-lookup"><span data-stu-id="c2305-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="c2305-133">En el caso de la revocación de certificados (por ejemplo, peligro de clave), se espera que el origen del paquete vuelva a firmar todos los paquetes firmados por el certificado afectado.</span><span class="sxs-lookup"><span data-stu-id="c2305-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="c2305-134">Además, el origen del paquete debe quitar el certificado afectado de la lista certificado de firma.</span><span class="sxs-lookup"><span data-stu-id="c2305-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="c2305-135">La solicitud siguiente captura el índice de firmas del repositorio.</span><span class="sxs-lookup"><span data-stu-id="c2305-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="c2305-136">El índice de la firma del repositorio es un documento JSON que contiene un objeto con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="c2305-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="c2305-137">Nombre</span><span class="sxs-lookup"><span data-stu-id="c2305-137">Name</span></span>                | <span data-ttu-id="c2305-138">Tipo</span><span class="sxs-lookup"><span data-stu-id="c2305-138">Type</span></span>             | <span data-ttu-id="c2305-139">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c2305-139">Required</span></span> | <span data-ttu-id="c2305-140">Notas</span><span class="sxs-lookup"><span data-stu-id="c2305-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="c2305-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="c2305-141">allRepositorySigned</span></span> | <span data-ttu-id="c2305-142">boolean</span><span class="sxs-lookup"><span data-stu-id="c2305-142">boolean</span></span>          | <span data-ttu-id="c2305-143">sí</span><span class="sxs-lookup"><span data-stu-id="c2305-143">yes</span></span>      | <span data-ttu-id="c2305-144">Debe estar `false` en los recursos 4.7.0 y 4.9.0</span><span class="sxs-lookup"><span data-stu-id="c2305-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="c2305-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="c2305-145">signingCertificates</span></span> | <span data-ttu-id="c2305-146">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="c2305-146">array of objects</span></span> | <span data-ttu-id="c2305-147">sí</span><span class="sxs-lookup"><span data-stu-id="c2305-147">yes</span></span>      | 

<span data-ttu-id="c2305-148">El `allRepositorySigned` valor booleano se establece en false si el origen del paquete tiene algunos paquetes que no tienen ninguna firma de repositorio.</span><span class="sxs-lookup"><span data-stu-id="c2305-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="c2305-149">Si el valor booleano se establece en true, todos los paquetes disponibles en el origen deben tener una firma de repositorio generada por uno de los certificados de firma mencionados en `signingCertificates` .</span><span class="sxs-lookup"><span data-stu-id="c2305-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="c2305-150">El `allRepositorySigned` valor booleano debe ser false en los recursos 4.7.0 y 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="c2305-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="c2305-151">Los clientes de NuGet v 4.7, v 4.8 y v 4.9 no pueden instalar paquetes de orígenes que tengan `allRepositorySigned` establecido en true.</span><span class="sxs-lookup"><span data-stu-id="c2305-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="c2305-152">Debe haber uno o más certificados de firma en la `signingCertificates` matriz si el `allRepositorySigned` valor booleano se establece en true.</span><span class="sxs-lookup"><span data-stu-id="c2305-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="c2305-153">Si la matriz está vacía y `allRepositorySigned` está establecida en true, todos los paquetes del origen se deben considerar no válidos, aunque una directiva de cliente puede seguir permitiendo el consumo de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c2305-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="c2305-154">Cada elemento de esta matriz es un objeto JSON con las siguientes propiedades.</span><span class="sxs-lookup"><span data-stu-id="c2305-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="c2305-155">Nombre</span><span class="sxs-lookup"><span data-stu-id="c2305-155">Name</span></span>         | <span data-ttu-id="c2305-156">Tipo</span><span class="sxs-lookup"><span data-stu-id="c2305-156">Type</span></span>   | <span data-ttu-id="c2305-157">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c2305-157">Required</span></span> | <span data-ttu-id="c2305-158">Notas</span><span class="sxs-lookup"><span data-stu-id="c2305-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="c2305-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="c2305-159">contentUrl</span></span>   | <span data-ttu-id="c2305-160">string</span><span class="sxs-lookup"><span data-stu-id="c2305-160">string</span></span> | <span data-ttu-id="c2305-161">sí</span><span class="sxs-lookup"><span data-stu-id="c2305-161">yes</span></span>      | <span data-ttu-id="c2305-162">Dirección URL absoluta al certificado público con codificación DER</span><span class="sxs-lookup"><span data-stu-id="c2305-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="c2305-163">las huellas digitales</span><span class="sxs-lookup"><span data-stu-id="c2305-163">fingerprints</span></span> | <span data-ttu-id="c2305-164">object</span><span class="sxs-lookup"><span data-stu-id="c2305-164">object</span></span> | <span data-ttu-id="c2305-165">sí</span><span class="sxs-lookup"><span data-stu-id="c2305-165">yes</span></span>      |
<span data-ttu-id="c2305-166">subject</span><span class="sxs-lookup"><span data-stu-id="c2305-166">subject</span></span>      | <span data-ttu-id="c2305-167">string</span><span class="sxs-lookup"><span data-stu-id="c2305-167">string</span></span> | <span data-ttu-id="c2305-168">sí</span><span class="sxs-lookup"><span data-stu-id="c2305-168">yes</span></span>      | <span data-ttu-id="c2305-169">Nombre distintivo del sujeto del certificado.</span><span class="sxs-lookup"><span data-stu-id="c2305-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="c2305-170">issuer</span><span class="sxs-lookup"><span data-stu-id="c2305-170">issuer</span></span>       | <span data-ttu-id="c2305-171">string</span><span class="sxs-lookup"><span data-stu-id="c2305-171">string</span></span> | <span data-ttu-id="c2305-172">sí</span><span class="sxs-lookup"><span data-stu-id="c2305-172">yes</span></span>      | <span data-ttu-id="c2305-173">Nombre distintivo del emisor del certificado.</span><span class="sxs-lookup"><span data-stu-id="c2305-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="c2305-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="c2305-174">notBefore</span></span>    | <span data-ttu-id="c2305-175">string</span><span class="sxs-lookup"><span data-stu-id="c2305-175">string</span></span> | <span data-ttu-id="c2305-176">sí</span><span class="sxs-lookup"><span data-stu-id="c2305-176">yes</span></span>      | <span data-ttu-id="c2305-177">Marca de tiempo de inicio del período de validez del certificado</span><span class="sxs-lookup"><span data-stu-id="c2305-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="c2305-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="c2305-178">notAfter</span></span>     | <span data-ttu-id="c2305-179">string</span><span class="sxs-lookup"><span data-stu-id="c2305-179">string</span></span> | <span data-ttu-id="c2305-180">sí</span><span class="sxs-lookup"><span data-stu-id="c2305-180">yes</span></span>      | <span data-ttu-id="c2305-181">Marca de tiempo de finalización del período de validez del certificado</span><span class="sxs-lookup"><span data-stu-id="c2305-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="c2305-182">Tenga en cuenta que `contentUrl` es necesario que se atienda a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c2305-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="c2305-183">Esta dirección URL no tiene ningún patrón de URL específico y se debe detectar de forma dinámica mediante este documento de índice de firmas de repositorio.</span><span class="sxs-lookup"><span data-stu-id="c2305-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="c2305-184">Todas las propiedades de este objeto (aparte de `contentUrl` ) deben derivarse del certificado que se encuentra en `contentUrl` .</span><span class="sxs-lookup"><span data-stu-id="c2305-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="c2305-185">Estas propiedades que se pueden derivar se proporcionan por comodidad para minimizar los recorridos de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="c2305-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="c2305-186">El objeto `fingerprints` tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="c2305-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="c2305-187">Nombre</span><span class="sxs-lookup"><span data-stu-id="c2305-187">Name</span></span>                   | <span data-ttu-id="c2305-188">Tipo</span><span class="sxs-lookup"><span data-stu-id="c2305-188">Type</span></span>   | <span data-ttu-id="c2305-189">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c2305-189">Required</span></span> | <span data-ttu-id="c2305-190">Notas</span><span class="sxs-lookup"><span data-stu-id="c2305-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="c2305-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="c2305-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="c2305-192">string</span><span class="sxs-lookup"><span data-stu-id="c2305-192">string</span></span> | <span data-ttu-id="c2305-193">sí</span><span class="sxs-lookup"><span data-stu-id="c2305-193">yes</span></span>      | <span data-ttu-id="c2305-194">La huella digital SHA-256</span><span class="sxs-lookup"><span data-stu-id="c2305-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="c2305-195">El nombre `2.16.840.1.101.3.4.2.1` de clave es el OID del algoritmo hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="c2305-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="c2305-196">Todos los valores hash deben ser minúsculas y codificadas en hexadecimal las representaciones de cadena de la síntesis hash.</span><span class="sxs-lookup"><span data-stu-id="c2305-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c2305-197">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c2305-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="c2305-198">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="c2305-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
