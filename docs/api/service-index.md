---
title: Índice de servicio, API de NuGet
description: El índice de servicio es el punto de entrada de la API HTTP de NuGet y enumera las funciones del servidor.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775354"
---
# <a name="service-index"></a>Índice de servicio

El índice de servicio es un documento JSON que es el punto de entrada de un origen de paquete NuGet y permite a una implementación de cliente detectar las capacidades del origen del paquete. El índice de servicio es un objeto JSON con dos propiedades obligatorias: `version` (la versión del esquema del índice del servicio) y `resources`  (los puntos de conexión o capacidades del origen del paquete).

el índice de servicio de Nuget. org se encuentra en `https://api.nuget.org/v3/index.json` .

## <a name="versioning"></a>Control de versiones

El `version` valor es una cadena de versión de SemVer 2.0.0 que indica la versión de esquema del índice de servicio. La API asigna que la cadena de versión tiene un número de versión principal de `3` . A medida que se realizan cambios no importantes en el esquema de índice de servicio, se aumentará la versión secundaria de la cadena de versión.

Cada recurso del índice de servicio tiene versiones independientes de la versión del esquema de índice de servicio.

La versión de esquema actual es `3.0.0` . La `3.0.0` versión es funcionalmente equivalente a la `3.0.0-beta.1` versión anterior, pero debe ser preferible a medida que comunica con mayor claridad el esquema definido y estable.

## <a name="http-methods"></a>Métodos HTTP

Se puede tener acceso al índice de servicio mediante métodos HTTP `GET` y `HEAD` .

## <a name="resources"></a>Recursos

La `resources` propiedad contiene una matriz de recursos admitidos por este origen del paquete.

### <a name="resource"></a>Recurso

Un recurso es un objeto de la `resources` matriz. Representa una funcionalidad con versión de un origen de paquete. Un recurso tiene las siguientes propiedades:

Nombre          | Tipo   | Obligatorio | Notas
------------- | ------ | -------- | -----
@id           | string | sí      | Dirección URL del recurso.
@type         | string | sí      | Una constante de cadena que representa el tipo de recurso
comment       | string | no       | Una descripción inteligible del recurso

`@id`Es una dirección URL que debe ser absoluta y debe tener el esquema http o https.

`@type`Se utiliza para identificar el protocolo específico que se va a utilizar al interactuar con el recurso. El tipo del recurso es una cadena opaca pero generalmente tiene el formato:

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

Se espera que los clientes codifiquen de forma rígida los `@type` valores que entienden y los examinan en el índice de servicio del origen del paquete. Los valores exactos que `@type` se usan hoy en día se enumeran en los documentos de referencia de recursos individuales que se enumeran en la [información general](overview.md#resources-and-schema)de la API.

En esta documentación, la documentación sobre los distintos recursos se agrupará básicamente por el `{RESOURCE_NAME}` que se encuentra en el índice del servicio, que es análogo a agrupar por escenario. 

No es necesario que cada recurso tenga un único `@id` o `@type` . Depende de la implementación del cliente determinar qué recurso prefiere sobre otro. Una posible implementación es que se pueden usar recursos del mismo o compatible `@type` en un modo Round Robin en caso de error de conexión o de servidor.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [service-index.json](./_data/service-index.json)]
