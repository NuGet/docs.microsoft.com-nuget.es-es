---
title: Índice de servicio, API de NuGet
description: El índice de servicio es el punto de entrada de la API de HTTP de NuGet y enumera las funciones del servidor.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324726"
---
# <a name="service-index"></a>Índice de servicio

El índice de servicio es un documento JSON que es el punto de entrada para un origen de paquete de NuGet y permite que una implementación de cliente detectar las capacidades del origen del paquete. El índice de servicio es un objeto JSON con dos propiedades necesarias: `version` (la versión de esquema del índice de servicio) y `resources` (puntos de conexión o las capacidades del origen del paquete).

índice del servicio de NuGet.org se encuentra en `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Control de versiones

El `version` valor es una cadena de versión analizable SemVer 2.0.0 que indica la versión del esquema del índice de servicio. La API exige que la cadena de versión tiene un número de versión principal `3`. Cuando se realizan cambios no importantes en el esquema de índice de servicio, aumentará la versión secundaria de la cadena de versión.

Cada recurso en el índice de servicio tiene versiones independientemente de la versión de esquema de índice de servicio.

La versión de esquema actual es `3.0.0`. El `3.0.0` es funcionalmente equivalente a la antigua versión `3.0.0-beta.1` versión pero debe preferirse tal como se comunica con mayor claridad el esquema estable, que se define.

## <a name="http-methods"></a>Métodos HTTP

El índice de servicio es accesible mediante los métodos HTTP `GET` y `HEAD`.

## <a name="resources"></a>Recursos

El `resources` propiedad contiene una matriz de recursos admitidos por este origen de paquete.

### <a name="resource"></a>Recurso

Un recurso es un objeto en el `resources` matriz. Representa una funcionalidad con control de versiones de un origen del paquete. Un recurso tiene las siguientes propiedades:

nombre          | Tipo   | Obligatorio | Notas
------------- | ------ | -------- | -----
@id           | cadena | sí      | La dirección URL del recurso
@type         | cadena | sí      | Una constante de cadena que representa el tipo de recurso
comentario       | cadena | No       | Una descripción legible del recurso

El `@id` es una dirección URL que debe ser absoluto y debe tener el esquema HTTP o HTTPS.

El `@type` se usa para identificar el protocolo específico a usar al interactuar con recursos. El tipo del recurso es una cadena opaca, pero normalmente tiene el formato:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Se esperan que los clientes a codificar de forma rígida la `@type` valores que se comprenden y buscarlos en el índice de un origen paquete de servicio. Exactamente `@type` valores en la actualidad se enumeran en los documentos de referencia de recurso individual enumerados en el [Introducción a la API](overview.md#resources-and-schema).

Por motivos de esta documentación, la documentación sobre los distintos recursos básicamente se agruparán por el `{RESOURCE_NAME}` se encuentra en el índice de servicio que es análogo a la agrupación por escenario. 

No es necesario que cada recurso tiene un único `@id` o `@type`. Es la implementación del cliente para determinar qué recursos se deben preferir otro. Una posible implementación es que los recursos de la misma o compatible `@type` puede usarse en un modo round-robin en caso de error de servidor o error de conexión.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [service-index.json](./_data/service-index.json)]
