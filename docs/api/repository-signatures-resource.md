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
# <a name="repository-signatures"></a>Firmas de repositorio

Si un origen de paquete permite agregar firmas de repositorio a paquetes publicados, es posible que un cliente determine los certificados de firma utilizados por el origen del paquete. Este recurso permite a los clientes detectar si un paquete firmado con el repositorio se ha manipulado o tiene un certificado de firma inesperado.

El recurso que se usa para obtener la información de la firma del repositorio es el `RepositorySignatures` recurso que se encuentra en el [Índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

`@type`Se usa el siguiente valor:

Valor de @type                | Notas
-------------------------- | -----
RepositorySignatures/4.7.0 | La versión inicial
RepositorySignatures/4.9.0 | Compatible con los clientes de NuGet v 4.9 +
RepositorySignatures/5.0.0 | Permite habilitar `allRepositorySigned` . Compatible con clientes de NuGet v 5.0 +

## <a name="base-url"></a>URL base

La dirección URL del punto de entrada para las siguientes API es el valor de la `@id` propiedad asociada al valor de recurso mencionado anteriormente `@type` . En este tema se utiliza la dirección URL del marcador de posición `{@id}` .

Tenga en cuenta que, a diferencia de otros recursos, `{@id}` se requiere que la dirección URL se atienda a través de HTTPS.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL encontradas en el recurso de firmas de repositorio solo admiten los métodos HTTP `GET` y `HEAD` .

## <a name="repository-signatures-index"></a>Índice de firmas de repositorio

El índice de firmas de repositorio contiene dos fragmentos de información:

1. Indica si todos los paquetes que se encuentran en el origen están firmados por este origen del paquete.
1. Lista de certificados utilizados por el origen del paquete para firmar paquetes.

En la mayoría de los casos, la lista de certificados solo se anexará a. Los nuevos certificados se agregan a la lista cuando el certificado de firma anterior ha expirado y el origen del paquete debe empezar a usar un nuevo certificado de firma. Si se quita un certificado de la lista, eso significa que todas las firmas de paquete creadas con el certificado de firma quitado ya no deben considerarse válidas para el cliente. En este caso, la firma del paquete (pero no necesariamente el paquete) no es válida. Una directiva de cliente puede permitir la instalación del paquete como sin firmar.

En el caso de la revocación de certificados (por ejemplo, peligro de clave), se espera que el origen del paquete vuelva a firmar todos los paquetes firmados por el certificado afectado. Además, el origen del paquete debe quitar el certificado afectado de la lista certificado de firma.

La solicitud siguiente captura el índice de firmas del repositorio.

```
GET {@id}
```

El índice de la firma del repositorio es un documento JSON que contiene un objeto con las siguientes propiedades:

Nombre                | Tipo             | Obligatorio | Notas
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | sí      | Debe estar `false` en los recursos 4.7.0 y 4.9.0
signingCertificates | matriz de objetos | sí      | 

El `allRepositorySigned` valor booleano se establece en false si el origen del paquete tiene algunos paquetes que no tienen ninguna firma de repositorio. Si el valor booleano se establece en true, todos los paquetes disponibles en el origen deben tener una firma de repositorio generada por uno de los certificados de firma mencionados en `signingCertificates` .

> [!Warning]
> El `allRepositorySigned` valor booleano debe ser false en los recursos 4.7.0 y 4.9.0. Los clientes de NuGet v 4.7, v 4.8 y v 4.9 no pueden instalar paquetes de orígenes que tengan `allRepositorySigned` establecido en true.

Debe haber uno o más certificados de firma en la `signingCertificates` matriz si el `allRepositorySigned` valor booleano se establece en true. Si la matriz está vacía y `allRepositorySigned` está establecida en true, todos los paquetes del origen se deben considerar no válidos, aunque una directiva de cliente puede seguir permitiendo el consumo de paquetes. Cada elemento de esta matriz es un objeto JSON con las siguientes propiedades.

Nombre         | Tipo   | Obligatorio | Notas
------------ | ------ | -------- | -----
contentUrl   | string | sí      | Dirección URL absoluta al certificado público con codificación DER
las huellas digitales | object | sí      |
subject      | string | sí      | Nombre distintivo del sujeto del certificado.
issuer       | string | sí      | Nombre distintivo del emisor del certificado.
notBefore    | string | sí      | Marca de tiempo de inicio del período de validez del certificado
notAfter     | string | sí      | Marca de tiempo de finalización del período de validez del certificado

Tenga en cuenta que `contentUrl` es necesario que se atienda a través de HTTPS. Esta dirección URL no tiene ningún patrón de URL específico y se debe detectar de forma dinámica mediante este documento de índice de firmas de repositorio. 

Todas las propiedades de este objeto (aparte de `contentUrl` ) deben derivarse del certificado que se encuentra en `contentUrl` .
Estas propiedades que se pueden derivar se proporcionan por comodidad para minimizar los recorridos de ida y vuelta.

El objeto `fingerprints` tiene las siguientes propiedades:

Nombre                   | Tipo   | Obligatorio | Notas
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | sí      | La huella digital SHA-256

El nombre `2.16.840.1.101.3.4.2.1` de clave es el OID del algoritmo hash SHA-256.

Todos los valores hash deben ser minúsculas y codificadas en hexadecimal las representaciones de cadena de la síntesis hash.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
