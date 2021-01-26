---
title: Búsqueda, API de NuGet
description: El servicio de búsqueda permite que los clientes consulten los paquetes por palabra clave y filtren los resultados en determinados campos de paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7047dfd48b7f93756bbb1491de1b7e65da2c12b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775414"
---
# <a name="search"></a>Search

Es posible buscar paquetes disponibles en un origen de paquete mediante la API V3. El recurso que se usa para buscar es el `SearchQueryService` recurso que se encuentra en el [Índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

`@type`Se usan los siguientes valores:

Valor de @type                   | Notas
----------------------------- | -----
SearchQueryService            | La versión inicial
SearchQueryService/3.0.0-beta | Alias de `SearchQueryService`
SearchQueryService/3.0.0-RC   | Alias de `SearchQueryService`
SearchQueryService/3.5.0      | Incluye compatibilidad con el `packageType` parámetro de consulta

### <a name="searchqueryservice350"></a>SearchQueryService/3.5.0
Esta versión introduce la compatibilidad con el `packageType` parámetro de consulta y la `packageTypes` propiedad de respuesta, lo que permite filtrar por tipos de paquetes definidos por el autor. Es totalmente compatible con las consultas a `SearchQueryService` .

## <a name="base-url"></a>URL base

La dirección URL base para la siguiente API es el valor de la `@id` propiedad asociada a uno de los valores de recursos mencionados anteriormente `@type` . En el siguiente documento, se usará la dirección URL base del marcador de posición `{@id}` .

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL encontradas en el recurso de registro admiten los métodos HTTP `GET` y `HEAD` .

## <a name="search-for-packages"></a>Buscar paquetes

La API de búsqueda permite a un cliente consultar una página de paquetes que coinciden con una consulta de búsqueda especificada. La interpretación de la consulta de búsqueda (por ejemplo, la tokenización de los términos de búsqueda) viene determinada por la implementación del servidor, pero la expectativa general es que la consulta de búsqueda se usa para buscar coincidencias con los identificadores de paquete, los títulos, las descripciones y las etiquetas. También se pueden considerar otros campos de metadatos de paquetes.

Un paquete que no aparece en la lista nunca debe aparecer en los resultados de la búsqueda.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a>Parámetros de solicitud

Nombre        | En     | Tipo    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
q           | Dirección URL    | string  | no       | Términos de búsqueda que se usan para filtrar paquetes
skip        | Dirección URL    | integer | no       | Número de resultados que se van a omitir para la paginación.
take        | Dirección URL    | integer | no       | Número de resultados que se van a devolver, para la paginación
prerelease  | Dirección URL    | boolean | no       | `true` o `false` determinar si se deben incluir los [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | Dirección URL    | string  | no       | Una cadena de versión de SemVer 1.0.0 
packageType | Dirección URL    | string  | no       | El tipo de paquete que se va a usar para filtrar paquetes (agregados en `SearchQueryService/3.5.0` )

La consulta `q` de búsqueda se analiza de una manera definida por la implementación del servidor. nuget.org admite el filtrado básico en [diversos campos](../consume-packages/finding-and-choosing-packages.md#search-syntax). Si no `q` se proporciona ningún paquete, se deben devolver todos los paquetes, dentro de los límites impuestos por SKIP y Take. Esto habilita la pestaña "examinar" en la experiencia de Visual Studio de NuGet.

El `skip` valor predeterminado del parámetro es 0.

El `take` parámetro debe ser un entero mayor que cero. La implementación del servidor puede imponer un valor máximo.

Si `prerelease` no se proporciona, se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se usa para participar en los [paquetes de SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si se excluye este parámetro de consulta, solo se devolverán los paquetes con versiones compatibles con SemVer 1.0.0 (con las advertencias de [control de versiones de NuGet estándar](../concepts/package-versioning.md) , como las cadenas de versión con 4 partes enteras).
Si `semVerLevel=2.0.0` se proporciona, se devolverán los paquetes compatibles con SemVer 1.0.0 y SemVer 2.0.0. Para obtener más información, consulte la [compatibilidad con SemVer 2.0.0 para Nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

El `packageType` parámetro se usa para filtrar aún más los resultados de la búsqueda a los paquetes que tienen al menos un tipo de paquete que coincide con el nombre del tipo de paquete.
Si el tipo de paquete proporcionado no es un tipo de paquete válido, tal y como se define en el [documento de tipo de paquete](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), se devolverá un resultado vacío.
Si el tipo de paquete proporcionado está vacío, no se aplicará ningún filtro. En otras palabras, si no se pasa ningún valor al parámetro packageType, se comportará como si no se hubiera pasado el parámetro.

### <a name="response"></a>Response

La respuesta es un documento JSON que contiene `take` los resultados de la búsqueda. Los resultados de la búsqueda se agrupan por identificador de paquete.

El objeto JSON raíz tiene las siguientes propiedades:

Nombre      | Tipo             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
totalHits | integer          | sí      | El número total de coincidencias, que no se tienen en cuenta `skip` y `take`
datos      | matriz de objetos | sí      | Resultados de la búsqueda que coinciden con la solicitud

### <a name="search-result"></a>Resultado de la búsqueda

Cada elemento de la `data` matriz es un objeto JSON que consta de un grupo de versiones de paquete que comparten el mismo identificador de paquete.
El objeto tiene las siguientes propiedades:

Nombre           | Tipo                       | Obligatorio | Notas
-------------- | -------------------------- | -------- | -----
id             | string                     | sí      | Identificador del paquete coincidente.
version        | string                     | sí      | La cadena de versión de SemVer 2.0.0 completa del paquete (podría contener metadatos de compilación)
description    | string                     | no       | 
versions       | matriz de objetos           | sí      | Todas las versiones del paquete que coinciden con el `prerelease` parámetro
authors        | cadena o matriz de cadenas | no       | 
iconUrl        | string                     | no       | 
licenseUrl     | string                     | no       | 
owners         | cadena o matriz de cadenas | no       | 
projectUrl     | string                     | no       | 
registro   | string                     | no       | La dirección URL absoluta al [Índice de registro](registration-base-url-resource.md#registration-index) asociado
Resumen        | string                     | no       | 
etiquetas           | cadena o matriz de cadenas | no       | 
title          | string                     | no       | 
totalDownloads | integer                    | no       | Este valor se puede inferir por la suma de descargas de la `versions` matriz.
demasiado       | boolean                    | no       | Un valor booleano JSON que indica si se [comprueba](../nuget-org/id-prefix-reservation.md) el paquete
packageTypes   | matriz de objetos           | sí      | Los tipos de paquetes definidos por el autor del paquete (agregado en `SearchQueryService/3.5.0` )

En nuget.org, un paquete comprobado es aquél que tiene un identificador de paquete que coincide con un prefijo de identificador reservado y es propiedad de uno de los propietarios del prefijo reservado. Para obtener más información, consulte la [documentación sobre la reserva de prefijos de identificador](../nuget-org/id-prefix-reservation.md).

Los metadatos contenidos en el objeto de resultado de la búsqueda se toman de la versión más reciente del paquete. Cada elemento de la `versions` matriz es un objeto JSON con las siguientes propiedades:

Nombre      | Tipo    | Obligatorio | Notas
--------- | ------- | -------- | -----
@id       | string  | sí      | La dirección URL absoluta de la [hoja de registro](registration-base-url-resource.md#registration-leaf) asociada
version   | string  | sí      | La cadena de versión de SemVer 2.0.0 completa del paquete (podría contener metadatos de compilación)
descargas | integer | sí      | El número de descargas para esta versión de paquete específica

La `packageTypes` matriz siempre contendrá al menos un (1) elemento. El tipo de paquete para un identificador de paquete determinado se considera como los tipos de paquetes definidos por la versión más reciente del paquete con respecto a los demás parámetros de búsqueda. Cada elemento de la `packageTypes` matriz es un objeto JSON con las siguientes propiedades:

Nombre      | Tipo    | Obligatorio | Notas
--------- | ------- | -------- | -----
name      | string  | sí      | Nombre del tipo de paquete.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0
```

### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [search-result.json](./_data/search-result.json)]