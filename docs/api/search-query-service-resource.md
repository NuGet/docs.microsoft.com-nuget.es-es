---
title: Búsqueda, API de NuGet
description: El servicio de búsqueda permite que los clientes consulten los paquetes por palabra clave y filtren los resultados en determinados campos de paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: be25e9bf72b9115de8ae55f6296195fed3152f10
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235118"
---
# <a name="search"></a>Buscar

Es posible buscar paquetes disponibles en un origen de paquete mediante la API V3. El recurso que se usa para buscar `SearchQueryService` es el recurso que se encuentra en el [Índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

Se usan `@type` los siguientes valores:

Valor de@type                   | Notas
----------------------------- | -----
SearchQueryService            | La versión inicial
SearchQueryService/3.0.0-beta | Alias de`SearchQueryService`
SearchQueryService/3.0.0-RC   | Alias de`SearchQueryService`

## <a name="base-url"></a>Dirección URL base

La dirección URL base para la siguiente API es el valor de `@id` la propiedad asociada a uno de los valores `@type` de recursos mencionados anteriormente. En el siguiente documento, se usará la dirección `{@id}` URL base del marcador de posición.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL encontradas en el recurso de registro admiten `HEAD`los métodos `GET` http y.

## <a name="search-for-packages"></a>Buscar paquetes

La API de búsqueda permite a un cliente consultar una página de paquetes que coinciden con una consulta de búsqueda especificada. La interpretación de la consulta de búsqueda (por ejemplo, la tokenización de los términos de búsqueda) viene determinada por la implementación del servidor, pero la expectativa general es que la consulta de búsqueda se usa para buscar coincidencias con los identificadores de paquete, los títulos, las descripciones y las etiquetas. También se pueden considerar otros campos de metadatos de paquetes.

Un paquete que no aparece en la lista nunca debe aparecer en los resultados de la búsqueda.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parámetros de solicitud

NOMBRE        | En     | Type    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | No       | Términos de búsqueda que se usan para filtrar paquetes
skip        | URL    | integer | No       | Número de resultados que se van a omitir para la paginación.
echar        | URL    | integer | No       | Número de resultados que se van a devolver, para la paginación
versión preliminar  | URL    | boolean | No       | `true`o `false` determinar si se deben incluir los [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | No       | Una cadena de versión de SemVer 1.0.0 

La consulta `q` de búsqueda se analiza de una manera definida por la implementación del servidor. nuget.org admite el filtrado básico en [diversos campos](../consume-packages/finding-and-choosing-packages.md#search-syntax). Si no `q` se proporciona ningún paquete, se deben devolver todos los paquetes, dentro de los límites impuestos por SKIP y Take. Esto habilita la pestaña "examinar" en la experiencia de Visual Studio de NuGet.

El `skip` valor predeterminado del parámetro es 0.

El `take` parámetro debe ser un entero mayor que cero. La implementación del servidor puede imponer un valor máximo.

Si `prerelease` no se proporciona, se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se usa para participar en los [paquetes de SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si se excluye este parámetro de consulta, solo se devolverán los paquetes con versiones compatibles con SemVer 1.0.0 (con las advertencias de [control de versiones de NuGet estándar](../concepts/package-versioning.md) , como las cadenas de versión con 4 partes enteras).
Si `semVerLevel=2.0.0` se proporciona, se devolverán los paquetes compatibles con SemVer 1.0.0 y SemVer 2.0.0. Para obtener más información, consulte la [compatibilidad con SemVer 2.0.0 para Nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Respuesta

La respuesta es un documento JSON que contiene `take` los resultados de la búsqueda. Los resultados de la búsqueda se agrupan por identificador de paquete.

El objeto JSON raíz tiene las siguientes propiedades:

NOMBRE      | Type             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
totalHits | integer          | sí      | El número total de coincidencias, que `skip` no se tienen en cuenta y`take`
data      | matriz de objetos | sí      | Resultados de la búsqueda que coinciden con la solicitud

### <a name="search-result"></a>Resultado de la búsqueda

Cada elemento de la `data` matriz es un objeto JSON que consta de un grupo de versiones de paquete que comparten el mismo identificador de paquete.
El objeto tiene las siguientes propiedades:

NOMBRE           | Type                       | Obligatorio | Notas
-------------- | -------------------------- | -------- | -----
id             | string                     | sí      | Identificador del paquete coincidente.
version        | string                     | sí      | La cadena de versión de SemVer 2.0.0 completa del paquete (podría contener metadatos de compilación)
description    | string                     | No       | 
versiones       | matriz de objetos           | sí      | Todas las versiones del paquete que coinciden con `prerelease` el parámetro
authors        | cadena o matriz de cadenas | No       | 
iconUrl        | string                     | No       | 
licenseUrl     | string                     | No       | 
owners         | cadena o matriz de cadenas | No       | 
projectUrl     | string                     | No       | 
registro   | string                     | No       | La dirección URL absoluta al [Índice de registro](registration-base-url-resource.md#registration-index) asociado
resumen        | string                     | No       | 
tags           | cadena o matriz de cadenas | No       | 
title          | string                     | No       | 
totalDownloads | integer                    | No       | Este valor se puede inferir por la suma de descargas de la `versions` matriz.
demasiado       | boolean                    | No       | Un valor booleano JSON que indica si se [comprueba](../nuget-org/id-prefix-reservation.md) el paquete

En nuget.org, un paquete comprobado es aquél que tiene un identificador de paquete que coincide con un prefijo de identificador reservado y es propiedad de uno de los propietarios del prefijo reservado. Para obtener más información, consulte la [documentación sobre la reserva de prefijos de identificador](../reference/id-prefix-reservation.md).

Los metadatos contenidos en el objeto de resultado de la búsqueda se toman de la versión más reciente del paquete. Cada elemento de la `versions` matriz es un objeto JSON con las siguientes propiedades:

NOMBRE      | Type    | Obligatorio | Notas
--------- | ------- | -------- | -----
@id       | string  | sí      | La dirección URL absoluta de la [hoja de registro](registration-base-url-resource.md#registration-leaf) asociada
version   | string  | sí      | La cadena de versión de SemVer 2.0.0 completa del paquete (podría contener metadatos de compilación)
carga | integer | sí      | El número de descargas para esta versión de paquete específica

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [search-result.json](./_data/search-result.json)]
