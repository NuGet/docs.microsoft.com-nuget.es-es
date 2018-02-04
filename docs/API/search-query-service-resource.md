---
title: "Búsqueda, NuGet API | Documentos de Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "El servicio de búsqueda permite a los clientes para consultar los paquetes por palabra clave y a los resultados del filtro en determinados campos de paquete."
keywords: "API de búsqueda de NuGet, NuGet detectar los paquetes, API a los paquetes de NuGet de consulta, API para examinar paquetes de NuGet"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 612ce0f46b654335a29bb36a64b27525994162ed
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="search"></a>Buscar

Es posible buscar paquetes disponibles en un origen de paquete mediante la API V3. El recurso que se usa para realizar búsquedas es el `SearchQueryService` recurso se encuentra en la [índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

Los siguientes `@type` se usan valores:

Valor de @type                   | Notas
----------------------------- | -----
SearchQueryService            | La versión inicial
SearchQueryService/3.0.0-beta | Alias de`SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias de`SearchQueryService`

## <a name="base-url"></a>Dirección URL base

La dirección URL base para la siguiente API es el valor de la `@id` propiedad asociado a uno de los recursos mencionados anteriormente `@type` valores. En el siguiente documento, el marcador de posición de la dirección URL base `{@id}` se usará.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL se encuentra en el soporte de registro del recurso los métodos HTTP `GET` y `HEAD`.

## <a name="search-for-packages"></a>Buscar paquetes

La API de búsqueda permite que un cliente a la consulta para una página de los paquetes que coinciden con una consulta de búsqueda especificado. La interpretación de la consulta de búsqueda (por ejemplo, la división en tokens de los términos de búsqueda) viene determinada por la implementación del servidor, pero la expectativa general es que la consulta de búsqueda se utiliza para la coincidencia de Id. de paquete, títulos, descripciones y etiquetas. También pueden considerar otros campos de metadatos de paquete.

Un paquete que no figuran en nunca debe aparecer en los resultados de búsqueda.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parámetros de solicitud

nombre        | En     | Tipo    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
q           | Dirección URL    | cadena  | No       | Términos de búsqueda usados para filtrar los paquetes
skip        | Dirección URL    | enteros | No       | El número de resultados que se va a omitir, para la paginación
Take        | Dirección URL    | enteros | No       | El número de resultados que se va a devolver para la paginación
versión preliminar  | Dirección URL    | booleano | No       | `true`o `false` determinar si se debe incluir [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | Dirección URL    | cadena  | No       | Una cadena de versión SemVer 1.0.0 

La consulta de búsqueda `q` se analiza de forma que se define mediante la implementación del servidor. NuGet.org admite el filtrado básico en una [serie de campos](../consume-packages/finding-and-choosing-packages.md#search-syntax). Si no hay ningún `q` es siempre se deben devolver todos los paquetes, dentro de los límites impuestos por skip y take. Esto permite que la ficha "Buscar" en la experiencia de NuGet Visual Studio.

El `skip` parámetro el valor predeterminado es 0.

El `take` parámetro debe ser un entero mayor que cero. La implementación del servidor puede imponer un valor máximo.

Si `prerelease` no es siempre, se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se utiliza para participar en [SemVer 2.0.0 paquetes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si se excluye de este parámetro de consulta, se devolverán los paquetes que solo con las versiones compatibles de SemVer 1.0.0 (con la [control de versiones de NuGet estándar](../reference/package-versioning.md) advertencias, como las cadenas de versión con 4 partes entero).
Si `semVerLevel=2.0.0` es siempre devolverán SemVer 1.0.0 y paquetes de SemVer 2.0.0 compatibles. Consulte la [SemVer 2.0.0 compatibilidad con nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obtener más información.

### <a name="response"></a>Respuesta

La respuesta es documento JSON que contiene hasta `take` resultados de búsqueda. Resultados de la búsqueda se agrupan por el identificador del paquete.

El objeto JSON raíz tiene las siguientes propiedades:

nombre      | Tipo             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
totalHits | enteros          | sí      | El número total de coincidencias, sin tener en cuenta `skip` y`take`
datos      | Matriz de objetos | sí      | Los resultados de búsqueda coincidentes con la solicitud

### <a name="search-result"></a>resultado de la búsqueda

Cada elemento de la `data` matriz es un objeto JSON que consta de un grupo de versiones del paquete compartir el mismo identificador de paquete.
El objeto tiene las siguientes propiedades:

nombre           | Tipo                       | Obligatorio | Notas
-------------- | -------------------------- | -------- | -----
id             | cadena                     | sí      | El identificador del paquete coincidente
version        | cadena                     | sí      | La cadena de versión SemVer 2.0.0 completa del paquete (podría contener metadatos de compilación)
Descripción    | cadena                     | No       | 
versiones       | Matriz de objetos           | sí      | Todas las versiones de la coincidencia del paquete el `prerelease` parámetro
authors        | cadena o matriz de cadenas | No       | 
iconUrl        | cadena                     | No       | 
licenseUrl     | cadena                     | No       | 
owners         | cadena o matriz de cadenas | No       | 
projectUrl     | cadena                     | No       | 
registro   | cadena                     | No       | La dirección URL absoluta a la categoría asociada [índice de registro](registration-base-url-resource.md#registration-index)
resumen        | cadena                     | No       | 
etiquetas           | cadena o matriz de cadenas | No       | 
título          | cadena                     | No       | 
totalDownloads | enteros                    | No       | Este valor se puede inferir por la suma de las descargas en el `versions` matriz
Comprobar       | booleano                    | No       | Un valor booleano JSON que indica si el paquete está [comprobado](../reference/id-prefix-reservation.md)

En nuget.org, un paquete comprobado es uno que tiene un identificador de paquete que coincide con un prefijo de identificador reservado y que pertenecen a uno de los propietarios del espacio de nombres reservado. Para obtener más información, consulte el [documentación acerca de la reserva de prefijo de identificador](../reference/id-prefix-reservation.md).

Los metadatos contenidos en el objeto de resultado de la búsqueda se realiza desde la versión más reciente del paquete. Cada elemento de la `versions` matriz es un objeto JSON con las siguientes propiedades:

nombre      | Tipo    | Obligatorio | Notas
--------- | ------- | -------- | -----
@id       | cadena  | sí      | La dirección URL absoluta a la categoría asociada [hoja de registro](registration-base-url-resource.md#registration-leaf)
version   | cadena  | sí      | La cadena de versión SemVer 2.0.0 completa del paquete (podría contener metadatos de compilación)
Descargas | enteros | sí      | El número de descargas para esta versión de paquete específico

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [search-result.json](./_data/search-result.json)]
