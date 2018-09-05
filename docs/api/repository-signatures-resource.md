---
title: Las firmas de repositorio, API de NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: El recurso de firmas de repositorio permite a los clientes los orígenes de paquetes anunciar su repositorio de funciones de firma.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547986"
---
# <a name="repository-signatures"></a><span data-ttu-id="d64a7-103">Firmas de repositorio</span><span class="sxs-lookup"><span data-stu-id="d64a7-103">Repository signatures</span></span>

<span data-ttu-id="d64a7-104">Si un origen de paquete admite agregar firmas de repositorio para los paquetes publicados, es posible que un cliente determinar los certificados de firma utilizados por el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="d64a7-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="d64a7-105">Este recurso permite a los clientes a detectar si la firma de un repositorio de paquetes ha sido alterado o tiene un certificado de firma inesperado.</span><span class="sxs-lookup"><span data-stu-id="d64a7-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="d64a7-106">El recurso usado para recuperar la información de firma de este repositorio es el `RepositorySignatures` encontrar el recurso en el [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d64a7-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="d64a7-107">NuGet.org se iniciará el anuncio de la `RepositorySignatures` recursos en un futuro próximo.</span><span class="sxs-lookup"><span data-stu-id="d64a7-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="d64a7-108">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="d64a7-108">Versioning</span></span>

<span data-ttu-id="d64a7-109">La siguiente `@type` se usa el valor:</span><span class="sxs-lookup"><span data-stu-id="d64a7-109">The following `@type` value is used:</span></span>

<span data-ttu-id="d64a7-110">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="d64a7-110">@type value</span></span>                | <span data-ttu-id="d64a7-111">Notas</span><span class="sxs-lookup"><span data-stu-id="d64a7-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="d64a7-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="d64a7-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="d64a7-113">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="d64a7-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d64a7-114">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="d64a7-114">Base URL</span></span>

<span data-ttu-id="d64a7-115">La dirección URL de punto de entrada para las siguientes API es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="d64a7-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="d64a7-116">Este tema usa la dirección URL del marcador de posición `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="d64a7-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="d64a7-117">Tenga en cuenta que a diferencia de otros recursos, el `{@id}` URL es necesaria para proporcionarse a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d64a7-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d64a7-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="d64a7-118">HTTP methods</span></span>

<span data-ttu-id="d64a7-119">Todas las direcciones URL se encuentra en los métodos de soporte técnico solo HTTP repositorio firmas recursos `GET` y `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="d64a7-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="d64a7-120">Índice de las firmas del repositorio</span><span class="sxs-lookup"><span data-stu-id="d64a7-120">Repository signatures index</span></span>

<span data-ttu-id="d64a7-121">El índice de firmas de repositorio contiene dos fragmentos de información:</span><span class="sxs-lookup"><span data-stu-id="d64a7-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="d64a7-122">Si no todos los paquetes que se encuentran en el origen son repositorio firmada por este origen de paquete.</span><span class="sxs-lookup"><span data-stu-id="d64a7-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="d64a7-123">La lista de los certificados usados por el origen del paquete para firmar paquetes.</span><span class="sxs-lookup"><span data-stu-id="d64a7-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="d64a7-124">En la mayoría de los casos, solo se anexará a la lista de certificados.</span><span class="sxs-lookup"><span data-stu-id="d64a7-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="d64a7-125">Se debe agregar los nuevos certificados a la lista cuando ha expirado el certificado de firma anterior y el origen del paquete debe empezar a usar un certificado de firma.</span><span class="sxs-lookup"><span data-stu-id="d64a7-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="d64a7-126">Si se quita un certificado de la lista, significa que todas las firmas de paquete creadas con el certificado de firma quitado ya no se deben considerar válidas por el cliente.</span><span class="sxs-lookup"><span data-stu-id="d64a7-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="d64a7-127">En este caso, la firma del paquete (pero no necesariamente el paquete) no es válido.</span><span class="sxs-lookup"><span data-stu-id="d64a7-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="d64a7-128">Una directiva de cliente puede permitir la instalación del paquete como unsigned.</span><span class="sxs-lookup"><span data-stu-id="d64a7-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="d64a7-129">En el caso de revocación de certificados (compromiso de clave p. ej.), el origen del paquete debe volver a firmar todos los paquetes firmados por el certificado afectado.</span><span class="sxs-lookup"><span data-stu-id="d64a7-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="d64a7-130">Además, el origen del paquete debe quitar el certificado afectado en la lista de certificados de firma.</span><span class="sxs-lookup"><span data-stu-id="d64a7-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="d64a7-131">La siguiente solicitud recupera el índice de las firmas del repositorio.</span><span class="sxs-lookup"><span data-stu-id="d64a7-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="d64a7-132">El índice de la firma de repositorio es un documento JSON que contiene un objeto con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="d64a7-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="d64a7-133">nombre</span><span class="sxs-lookup"><span data-stu-id="d64a7-133">Name</span></span>                | <span data-ttu-id="d64a7-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="d64a7-134">Type</span></span>             | <span data-ttu-id="d64a7-135">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d64a7-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="d64a7-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="d64a7-136">allRepositorySigned</span></span> | <span data-ttu-id="d64a7-137">booleano</span><span class="sxs-lookup"><span data-stu-id="d64a7-137">boolean</span></span>          | <span data-ttu-id="d64a7-138">sí</span><span class="sxs-lookup"><span data-stu-id="d64a7-138">yes</span></span>
<span data-ttu-id="d64a7-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="d64a7-139">signingCertificates</span></span> | <span data-ttu-id="d64a7-140">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="d64a7-140">array of objects</span></span> | <span data-ttu-id="d64a7-141">sí</span><span class="sxs-lookup"><span data-stu-id="d64a7-141">yes</span></span>

<span data-ttu-id="d64a7-142">El `allRepositorySigned` booleano se establece en false si el origen del paquete tiene algunos paquetes que no tengan ninguna firma de repositorio.</span><span class="sxs-lookup"><span data-stu-id="d64a7-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="d64a7-143">Si el valor booleano se establece en true, todos los paquetes disponibles en el origen debe tener una firma de repositorio producida por uno de los certificados de firma se ha mencionado en `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="d64a7-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="d64a7-144">Debe haber uno o varios certificados de firma en el `signingCertificates` matriz si la `allRepositorySigned` booleano se establece en true.</span><span class="sxs-lookup"><span data-stu-id="d64a7-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="d64a7-145">Si la matriz está vacía y `allRepositorySigned` se establece en true, todos los paquetes desde el origen deben considerarse válidos, aunque una directiva de cliente todavía puede permitir el consumo de paquetes.</span><span class="sxs-lookup"><span data-stu-id="d64a7-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="d64a7-146">Cada elemento de esta matriz es un objeto JSON con las siguientes propiedades.</span><span class="sxs-lookup"><span data-stu-id="d64a7-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="d64a7-147">nombre</span><span class="sxs-lookup"><span data-stu-id="d64a7-147">Name</span></span>         | <span data-ttu-id="d64a7-148">Tipo</span><span class="sxs-lookup"><span data-stu-id="d64a7-148">Type</span></span>   | <span data-ttu-id="d64a7-149">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d64a7-149">Required</span></span> | <span data-ttu-id="d64a7-150">Notas</span><span class="sxs-lookup"><span data-stu-id="d64a7-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="d64a7-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="d64a7-151">contentUrl</span></span>   | <span data-ttu-id="d64a7-152">cadena</span><span class="sxs-lookup"><span data-stu-id="d64a7-152">string</span></span> | <span data-ttu-id="d64a7-153">sí</span><span class="sxs-lookup"><span data-stu-id="d64a7-153">yes</span></span>      | <span data-ttu-id="d64a7-154">Dirección URL absoluta para el certificado público con codificación DER</span><span class="sxs-lookup"><span data-stu-id="d64a7-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="d64a7-155">huellas digitales</span><span class="sxs-lookup"><span data-stu-id="d64a7-155">fingerprints</span></span> | <span data-ttu-id="d64a7-156">objeto</span><span class="sxs-lookup"><span data-stu-id="d64a7-156">object</span></span> | <span data-ttu-id="d64a7-157">sí</span><span class="sxs-lookup"><span data-stu-id="d64a7-157">yes</span></span>      |
<span data-ttu-id="d64a7-158">Asunto</span><span class="sxs-lookup"><span data-stu-id="d64a7-158">subject</span></span>      | <span data-ttu-id="d64a7-159">cadena</span><span class="sxs-lookup"><span data-stu-id="d64a7-159">string</span></span> | <span data-ttu-id="d64a7-160">sí</span><span class="sxs-lookup"><span data-stu-id="d64a7-160">yes</span></span>      | <span data-ttu-id="d64a7-161">El nombre distintivo del sujeto del certificado</span><span class="sxs-lookup"><span data-stu-id="d64a7-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="d64a7-162">issuer</span><span class="sxs-lookup"><span data-stu-id="d64a7-162">issuer</span></span>       | <span data-ttu-id="d64a7-163">cadena</span><span class="sxs-lookup"><span data-stu-id="d64a7-163">string</span></span> | <span data-ttu-id="d64a7-164">sí</span><span class="sxs-lookup"><span data-stu-id="d64a7-164">yes</span></span>      | <span data-ttu-id="d64a7-165">El nombre distintivo del emisor del certificado</span><span class="sxs-lookup"><span data-stu-id="d64a7-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="d64a7-166">notBefore</span><span class="sxs-lookup"><span data-stu-id="d64a7-166">notBefore</span></span>    | <span data-ttu-id="d64a7-167">cadena</span><span class="sxs-lookup"><span data-stu-id="d64a7-167">string</span></span> | <span data-ttu-id="d64a7-168">sí</span><span class="sxs-lookup"><span data-stu-id="d64a7-168">yes</span></span>      | <span data-ttu-id="d64a7-169">La marca de tiempo de inicio del período de validez del certificado</span><span class="sxs-lookup"><span data-stu-id="d64a7-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="d64a7-170">notAfter</span><span class="sxs-lookup"><span data-stu-id="d64a7-170">notAfter</span></span>     | <span data-ttu-id="d64a7-171">cadena</span><span class="sxs-lookup"><span data-stu-id="d64a7-171">string</span></span> | <span data-ttu-id="d64a7-172">sí</span><span class="sxs-lookup"><span data-stu-id="d64a7-172">yes</span></span>      | <span data-ttu-id="d64a7-173">La marca de tiempo final del período de validez del certificado</span><span class="sxs-lookup"><span data-stu-id="d64a7-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="d64a7-174">Tenga en cuenta que el `contentUrl` debe proporcionarse a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d64a7-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="d64a7-175">Esta dirección URL no tiene ningún patrón de URL específico y debe detectarse dinámicamente con este documento de índice de las firmas de repositorio.</span><span class="sxs-lookup"><span data-stu-id="d64a7-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="d64a7-176">Todas las propiedades de este objeto (además del `contentUrl`) deben derivar desde el certificado encontrado en `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="d64a7-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="d64a7-177">Estas propiedades derivar se proporcionan por comodidad para minimizar la ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="d64a7-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="d64a7-178">La `fingerprints` objeto tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="d64a7-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="d64a7-179">nombre</span><span class="sxs-lookup"><span data-stu-id="d64a7-179">Name</span></span>                   | <span data-ttu-id="d64a7-180">Tipo</span><span class="sxs-lookup"><span data-stu-id="d64a7-180">Type</span></span>   | <span data-ttu-id="d64a7-181">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d64a7-181">Required</span></span> | <span data-ttu-id="d64a7-182">Notas</span><span class="sxs-lookup"><span data-stu-id="d64a7-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="d64a7-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="d64a7-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="d64a7-184">cadena</span><span class="sxs-lookup"><span data-stu-id="d64a7-184">string</span></span> | <span data-ttu-id="d64a7-185">sí</span><span class="sxs-lookup"><span data-stu-id="d64a7-185">yes</span></span>      | <span data-ttu-id="d64a7-186">La huella digital de SHA-256</span><span class="sxs-lookup"><span data-stu-id="d64a7-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="d64a7-187">El nombre de clave `2.16.840.1.101.3.4.2.1` es el OID del algoritmo hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="d64a7-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="d64a7-188">Todos los valores de hash deben ser representaciones de cadena en minúsculas, con codificación hexadecimal de la síntesis de hash.</span><span class="sxs-lookup"><span data-stu-id="d64a7-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d64a7-189">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d64a7-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="d64a7-190">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d64a7-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
