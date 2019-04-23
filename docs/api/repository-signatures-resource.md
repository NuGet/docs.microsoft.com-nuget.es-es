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
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931857"
---
# <a name="repository-signatures"></a>Firmas de repositorio

Si un origen de paquete admite agregar firmas de repositorio para los paquetes publicados, es posible que un cliente determinar los certificados de firma utilizados por el origen del paquete. Este recurso permite a los clientes a detectar si la firma de un repositorio de paquetes ha sido alterado o tiene un certificado de firma inesperado.

El recurso usado para recuperar la información de firma de este repositorio es el `RepositorySignatures` encontrar el recurso en el [índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

La siguiente `@type` se usa el valor:

Valor de@type                 | Notas
-------------------------- | -----
RepositorySignatures/4.7.0 | La versión inicial
RepositorySignatures/4.9.0 | Compatible con clientes de NuGet v4.9 +
RepositorySignatures/5.0.0 | Permite habilitar `allRepositorySigned`. Compatible con clientes de NuGet v5.0 +

## <a name="base-url"></a>Dirección URL base

La dirección URL de punto de entrada para las siguientes API es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valor. Este tema usa la dirección URL del marcador de posición `{@id}`.

Tenga en cuenta que a diferencia de otros recursos, el `{@id}` URL es necesaria para proporcionarse a través de HTTPS.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL se encuentra en los métodos de soporte técnico solo HTTP repositorio firmas recursos `GET` y `HEAD`.

## <a name="repository-signatures-index"></a>Índice de las firmas del repositorio

El índice de firmas de repositorio contiene dos fragmentos de información:

1. Si no todos los paquetes que se encuentran en el origen son repositorio firmada por este origen de paquete.
1. La lista de los certificados usados por el origen del paquete para firmar paquetes.

En la mayoría de los casos, solo se anexará a la lista de certificados. Se debe agregar los nuevos certificados a la lista cuando ha expirado el certificado de firma anterior y el origen del paquete debe empezar a usar un certificado de firma. Si se quita un certificado de la lista, significa que todas las firmas de paquete creadas con el certificado de firma quitado ya no se deben considerar válidas por el cliente. En este caso, la firma del paquete (pero no necesariamente el paquete) no es válido. Una directiva de cliente puede permitir la instalación del paquete como unsigned.

En el caso de revocación de certificados (compromiso de clave p. ej.), el origen del paquete debe volver a firmar todos los paquetes firmados por el certificado afectado. Además, el origen del paquete debe quitar el certificado afectado en la lista de certificados de firma.

La siguiente solicitud recupera el índice de las firmas del repositorio.

    GET {@id}

El índice de la firma de repositorio es un documento JSON que contiene un objeto con las siguientes propiedades:

Name                | Tipo             | Obligatorio | Notas
------------------- | ---------------- | -------- | -----
allRepositorySigned | booleano          | sí      | Debe ser `false` en recursos 4.7.0 y 4.9.0
signingCertificates | matriz de objetos | sí      | 

El `allRepositorySigned` booleano se establece en false si el origen del paquete tiene algunos paquetes que no tengan ninguna firma de repositorio. Si el valor booleano se establece en true, todos los paquetes disponibles en el origen debe tener una firma de repositorio producida por uno de los certificados de firma se ha mencionado en `signingCertificates`.

> [!Warning]
> El `allRepositorySigned` booleano debe ser false en los recursos 4.7.0 y 4.9.0. Los clientes de NuGet v4.7, v4.8 y v4.9 no pueden instalar los paquetes de orígenes que tienen `allRepositorySigned` establecido en true.

Debe haber uno o varios certificados de firma en el `signingCertificates` matriz si la `allRepositorySigned` booleano se establece en true. Si la matriz está vacía y `allRepositorySigned` se establece en true, todos los paquetes desde el origen deben considerarse válidos, aunque una directiva de cliente todavía puede permitir el consumo de paquetes. Cada elemento de esta matriz es un objeto JSON con las siguientes propiedades.

Name         | Tipo   | Obligatorio | Notas
------------ | ------ | -------- | -----
contentUrl   | cadena | sí      | Dirección URL absoluta para el certificado público con codificación DER
fingerprints | objeto | sí      |
subject      | cadena | sí      | El nombre distintivo del sujeto del certificado
issuer       | cadena | sí      | El nombre distintivo del emisor del certificado
notBefore    | cadena | sí      | La marca de tiempo de inicio del período de validez del certificado
notAfter     | cadena | sí      | La marca de tiempo final del período de validez del certificado

Tenga en cuenta que el `contentUrl` debe proporcionarse a través de HTTPS. Esta dirección URL no tiene ningún patrón de URL específico y debe detectarse dinámicamente con este documento de índice de las firmas de repositorio. 

Todas las propiedades de este objeto (además del `contentUrl`) deben derivar desde el certificado encontrado en `contentUrl`.
Estas propiedades derivar se proporcionan por comodidad para minimizar la ida y vuelta.

La `fingerprints` objeto tiene las siguientes propiedades:

Name                   | Tipo   | Obligatorio | Notas
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | cadena | sí      | La huella digital de SHA-256

El nombre de clave `2.16.840.1.101.3.4.2.1` es el OID del algoritmo hash SHA-256.

Todos los valores de hash deben ser representaciones de cadena en minúsculas, con codificación hexadecimal de la síntesis de hash.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
