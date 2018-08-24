---
title: Las firmas de repositorio, API de NuGet | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: El recurso de firmas de repositorio permite a los clientes los orígenes de paquetes anunciar su repositorio de funciones de firma.
keywords: Las firmas de repositorio de API de NuGet, nuget.org firma de certificados, la firma del paquete de nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 32dd2ee19261488a2b1b92724095a11ced69ae68
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793209"
---
# <a name="repository-signatures"></a><span data-ttu-id="f5b2d-104">Firmas de repositorio</span><span class="sxs-lookup"><span data-stu-id="f5b2d-104">Repository signatures</span></span>

<span data-ttu-id="f5b2d-105">Si un origen de paquete admite agregar firmas de repositorio para los paquetes publicados, es posible que un cliente determinar los certificados de firma utilizados por el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="f5b2d-106">Este recurso permite a los clientes a detectar si la firma de un repositorio de paquetes ha sido alterado o tiene un certificado de firma inesperado.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="f5b2d-107">El recurso usado para recuperar la información de firma de este repositorio es el `RepositorySignatures` encontrar el recurso en el [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="f5b2d-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="f5b2d-108">NuGet.org se iniciará el anuncio de la `RepositorySignatures` recursos en un futuro próximo.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="f5b2d-109">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="f5b2d-109">Versioning</span></span>

<span data-ttu-id="f5b2d-110">La siguiente `@type` se usa el valor:</span><span class="sxs-lookup"><span data-stu-id="f5b2d-110">The following `@type` value is used:</span></span>

<span data-ttu-id="f5b2d-111">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="f5b2d-111">@type value</span></span>                | <span data-ttu-id="f5b2d-112">Notas</span><span class="sxs-lookup"><span data-stu-id="f5b2d-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="f5b2d-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="f5b2d-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="f5b2d-114">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="f5b2d-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="f5b2d-115">Dirección URL base</span><span class="sxs-lookup"><span data-stu-id="f5b2d-115">Base URL</span></span>

<span data-ttu-id="f5b2d-116">La dirección URL de punto de entrada para las siguientes API es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="f5b2d-117">Este tema usa la dirección URL del marcador de posición `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="f5b2d-118">Tenga en cuenta que a diferencia de otros recursos, el `{@id}` URL es necesaria para proporcionarse a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f5b2d-119">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="f5b2d-119">HTTP methods</span></span>

<span data-ttu-id="f5b2d-120">Todas las direcciones URL se encuentra en los métodos de soporte técnico solo HTTP repositorio firmas recursos `GET` y `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="f5b2d-121">Índice de las firmas del repositorio</span><span class="sxs-lookup"><span data-stu-id="f5b2d-121">Repository signatures index</span></span>

<span data-ttu-id="f5b2d-122">El índice de firmas de repositorio contiene dos fragmentos de información:</span><span class="sxs-lookup"><span data-stu-id="f5b2d-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="f5b2d-123">Si no todos los paquetes que se encuentran en el origen son repositorio firmada por este origen de paquete.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="f5b2d-124">La lista de los certificados usados por el origen del paquete para firmar paquetes.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="f5b2d-125">En la mayoría de los casos, solo se anexará a la lista de certificados.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="f5b2d-126">Se debe agregar los nuevos certificados a la lista cuando ha expirado el certificado de firma anterior y el origen del paquete debe empezar a usar un certificado de firma.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="f5b2d-127">Si se quita un certificado de la lista, significa que todas las firmas de paquete creadas con el certificado de firma quitado ya no se deben considerar válidas por el cliente.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="f5b2d-128">En este caso, la firma del paquete (pero no necesariamente el paquete) no es válido.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="f5b2d-129">Una directiva de cliente puede permitir la instalación del paquete como unsigned.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="f5b2d-130">En el caso de revocación de certificados (compromiso de clave p. ej.), el origen del paquete debe volver a firmar todos los paquetes firmados por el certificado afectado.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="f5b2d-131">Además, el origen del paquete debe quitar el certificado afectado en la lista de certificados de firma.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="f5b2d-132">La siguiente solicitud recupera el índice de las firmas del repositorio.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="f5b2d-133">El índice de la firma de repositorio es un documento JSON que contiene un objeto con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="f5b2d-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="f5b2d-134">nombre</span><span class="sxs-lookup"><span data-stu-id="f5b2d-134">Name</span></span>                | <span data-ttu-id="f5b2d-135">Tipo</span><span class="sxs-lookup"><span data-stu-id="f5b2d-135">Type</span></span>             | <span data-ttu-id="f5b2d-136">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f5b2d-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="f5b2d-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="f5b2d-137">allRepositorySigned</span></span> | <span data-ttu-id="f5b2d-138">booleano</span><span class="sxs-lookup"><span data-stu-id="f5b2d-138">boolean</span></span>          | <span data-ttu-id="f5b2d-139">sí</span><span class="sxs-lookup"><span data-stu-id="f5b2d-139">yes</span></span>
<span data-ttu-id="f5b2d-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="f5b2d-140">signingCertificates</span></span> | <span data-ttu-id="f5b2d-141">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="f5b2d-141">array of objects</span></span> | <span data-ttu-id="f5b2d-142">sí</span><span class="sxs-lookup"><span data-stu-id="f5b2d-142">yes</span></span>

<span data-ttu-id="f5b2d-143">El `allRepositorySigned` booleano se establece en false si el origen del paquete tiene algunos paquetes que no tengan ninguna firma de repositorio.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="f5b2d-144">Si el valor booleano se establece en true, todos los paquetes disponibles en el origen debe tener una firma de repositorio producida por uno de los certificados de firma se ha mencionado en `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="f5b2d-145">Debe haber uno o varios certificados de firma en el `signingCertificates` matriz si la `allRepositorySigned` booleano se establece en true.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="f5b2d-146">Si la matriz está vacía y `allRepositorySigned` se establece en true, todos los paquetes desde el origen deben considerarse válidos, aunque una directiva de cliente todavía puede permitir el consumo de paquetes.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="f5b2d-147">Cada elemento de esta matriz es un objeto JSON con las siguientes propiedades.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="f5b2d-148">nombre</span><span class="sxs-lookup"><span data-stu-id="f5b2d-148">Name</span></span>         | <span data-ttu-id="f5b2d-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="f5b2d-149">Type</span></span>   | <span data-ttu-id="f5b2d-150">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f5b2d-150">Required</span></span> | <span data-ttu-id="f5b2d-151">Notas</span><span class="sxs-lookup"><span data-stu-id="f5b2d-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="f5b2d-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="f5b2d-152">contentUrl</span></span>   | <span data-ttu-id="f5b2d-153">cadena</span><span class="sxs-lookup"><span data-stu-id="f5b2d-153">string</span></span> | <span data-ttu-id="f5b2d-154">sí</span><span class="sxs-lookup"><span data-stu-id="f5b2d-154">yes</span></span>      | <span data-ttu-id="f5b2d-155">Dirección URL absoluta para el certificado público con codificación DER</span><span class="sxs-lookup"><span data-stu-id="f5b2d-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="f5b2d-156">huellas digitales</span><span class="sxs-lookup"><span data-stu-id="f5b2d-156">fingerprints</span></span> | <span data-ttu-id="f5b2d-157">objeto</span><span class="sxs-lookup"><span data-stu-id="f5b2d-157">object</span></span> | <span data-ttu-id="f5b2d-158">sí</span><span class="sxs-lookup"><span data-stu-id="f5b2d-158">yes</span></span>      |
<span data-ttu-id="f5b2d-159">Asunto</span><span class="sxs-lookup"><span data-stu-id="f5b2d-159">subject</span></span>      | <span data-ttu-id="f5b2d-160">cadena</span><span class="sxs-lookup"><span data-stu-id="f5b2d-160">string</span></span> | <span data-ttu-id="f5b2d-161">sí</span><span class="sxs-lookup"><span data-stu-id="f5b2d-161">yes</span></span>      | <span data-ttu-id="f5b2d-162">El nombre distintivo del sujeto del certificado</span><span class="sxs-lookup"><span data-stu-id="f5b2d-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="f5b2d-163">issuer</span><span class="sxs-lookup"><span data-stu-id="f5b2d-163">issuer</span></span>       | <span data-ttu-id="f5b2d-164">cadena</span><span class="sxs-lookup"><span data-stu-id="f5b2d-164">string</span></span> | <span data-ttu-id="f5b2d-165">sí</span><span class="sxs-lookup"><span data-stu-id="f5b2d-165">yes</span></span>      | <span data-ttu-id="f5b2d-166">El nombre distintivo del emisor del certificado</span><span class="sxs-lookup"><span data-stu-id="f5b2d-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="f5b2d-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="f5b2d-167">notBefore</span></span>    | <span data-ttu-id="f5b2d-168">cadena</span><span class="sxs-lookup"><span data-stu-id="f5b2d-168">string</span></span> | <span data-ttu-id="f5b2d-169">sí</span><span class="sxs-lookup"><span data-stu-id="f5b2d-169">yes</span></span>      | <span data-ttu-id="f5b2d-170">La marca de tiempo de inicio del período de validez del certificado</span><span class="sxs-lookup"><span data-stu-id="f5b2d-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="f5b2d-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="f5b2d-171">notAfter</span></span>     | <span data-ttu-id="f5b2d-172">cadena</span><span class="sxs-lookup"><span data-stu-id="f5b2d-172">string</span></span> | <span data-ttu-id="f5b2d-173">sí</span><span class="sxs-lookup"><span data-stu-id="f5b2d-173">yes</span></span>      | <span data-ttu-id="f5b2d-174">La marca de tiempo final del período de validez del certificado</span><span class="sxs-lookup"><span data-stu-id="f5b2d-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="f5b2d-175">Tenga en cuenta que el `contentUrl` debe proporcionarse a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="f5b2d-176">Esta dirección URL no tiene ningún patrón de URL específico y debe detectarse dinámicamente con este documento de índice de las firmas de repositorio.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="f5b2d-177">Todas las propiedades de este objeto (además del `contentUrl`) deben derivar desde el certificado encontrado en `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="f5b2d-178">Estas propiedades derivar se proporcionan por comodidad para minimizar la ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="f5b2d-179">La `fingerprints` objeto tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="f5b2d-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="f5b2d-180">nombre</span><span class="sxs-lookup"><span data-stu-id="f5b2d-180">Name</span></span>                   | <span data-ttu-id="f5b2d-181">Tipo</span><span class="sxs-lookup"><span data-stu-id="f5b2d-181">Type</span></span>   | <span data-ttu-id="f5b2d-182">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f5b2d-182">Required</span></span> | <span data-ttu-id="f5b2d-183">Notas</span><span class="sxs-lookup"><span data-stu-id="f5b2d-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="f5b2d-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="f5b2d-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="f5b2d-185">cadena</span><span class="sxs-lookup"><span data-stu-id="f5b2d-185">string</span></span> | <span data-ttu-id="f5b2d-186">sí</span><span class="sxs-lookup"><span data-stu-id="f5b2d-186">yes</span></span>      | <span data-ttu-id="f5b2d-187">La huella digital de SHA-256</span><span class="sxs-lookup"><span data-stu-id="f5b2d-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="f5b2d-188">El nombre de clave `2.16.840.1.101.3.4.2.1` es el OID del algoritmo hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="f5b2d-189">Todos los valores de hash deben ser representaciones de cadena en minúsculas, con codificación hexadecimal de la síntesis de hash.</span><span class="sxs-lookup"><span data-stu-id="f5b2d-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="f5b2d-190">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f5b2d-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="f5b2d-191">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f5b2d-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
