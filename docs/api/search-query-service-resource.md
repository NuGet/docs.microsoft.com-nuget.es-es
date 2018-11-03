---
title: Search, API de NuGet
description: El servicio de búsqueda permite a los clientes para consultar los paquetes mediante la palabra clave y para filtrar los resultados en determinados campos del paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: cfcb52ba7689f1b392c782b4ad42ba820a76c8bf
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981137"
---
# <a name="search"></a>Buscar

Es posible buscar paquetes disponibles en un origen de paquete mediante la API de V3. Es el recurso utilizado para buscar el `SearchQueryService` encontrar el recurso en el [índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

La siguiente `@type` se usan los valores:

Valor de@type                    | Notas
----------------------------- | -----
SearchQueryService            | La versión inicial
SearchQueryService/3.0.0-beta | Alias de `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias de `SearchQueryService`

## <a name="base-url"></a>Dirección URL base

La dirección URL base para la siguiente API es el valor de la `@id` propiedad asociada con uno de los recursos mencionados anteriormente `@type` valores. En el siguiente documento, la dirección URL base del marcador de posición `{@id}` se usará.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL se encuentra en la compatibilidad con recursos de registro de los métodos HTTP `GET` y `HEAD`.

## <a name="search-for-packages"></a>Buscar paquetes

La API de búsqueda permite que un cliente a la consulta para una página de los paquetes que coinciden con una consulta de búsqueda especificado. La interpretación de la consulta de búsqueda (por ejemplo, la tokenización de los términos de búsqueda) viene determinada por la implementación del servidor, pero la expectativa general es que la consulta de búsqueda se usa para la coincidencia de Id. de paquete, títulos, descripciones y etiquetas. También se pueden considerar otros campos de metadatos de paquete.

Un paquete de dados de baja nunca debe aparecer en los resultados de búsqueda.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parámetros de solicitud

nombre        | En     | Tipo    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
q           | Resolución    | cadena  | No       | Términos de búsqueda usados para filtrar paquetes
skip        | Resolución    | enteros | No       | El número de resultados que se omitirán para la paginación
Take        | Resolución    | enteros | No       | El número de resultados que se va a devolver para la paginación
versión preliminar  | Resolución    | booleano | No       | `true` o `false` determinar si se debe incluir [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | Resolución    | cadena  | No       | Una cadena de versión 1.0.0 de SemVer 

La consulta de búsqueda `q` se analiza de manera que se define mediante la implementación del servidor. NuGet.org admite el filtrado básico en un [diversos campos](../consume-packages/finding-and-choosing-packages.md#search-syntax). Si no hay ningún `q` es siempre deben devolver todos los paquetes y dentro de los límites impuestos por skip y take. Esto permite que la pestaña "Examinar" en la experiencia de NuGet de Visual Studio.

El `skip` parámetro el valor predeterminado es 0.

El `take` parámetro debe ser un entero mayor que cero. La implementación del servidor puede imponer un valor máximo.

Si `prerelease` no es siempre se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se utiliza para participar en [SemVer 2.0.0 paquetes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si se excluye de este parámetro de consulta, se devolverán solo los paquetes con las versiones compatibles de SemVer 1.0.0 (con el [control de versiones de NuGet estándar](../reference/package-versioning.md) advertencias, tales como las cadenas de versión con 4 partes entero).
Si `semVerLevel=2.0.0` es siempre se devolverá SemVer 1.0.0 y 2.0.0 de SemVer compatibles paquetes. Consulte la [compatibilidad con SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obtener más información.

### <a name="response"></a>Respuesta

La respuesta es un documento JSON que contiene hasta `take` los resultados de búsqueda. Los resultados de búsqueda se agrupan por el identificador del paquete.

El objeto JSON de raíz tiene las siguientes propiedades:

nombre      | Tipo             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
totalHits | enteros          | sí      | El número total de coincidencias, omitiendo `skip` y `take`
datos      | matriz de objetos | sí      | Los resultados de búsqueda coincide con la solicitud

### <a name="search-result"></a>Resultado de la búsqueda

Cada elemento de la `data` matriz es un objeto JSON que consta de un grupo de versiones del paquete compartir el mismo identificador de paquete.
El objeto tiene las siguientes propiedades:

nombre           | Tipo                       | Obligatorio | Notas
-------------- | -------------------------- | -------- | -----
id             | cadena                     | sí      | El identificador del paquete coincidente
version        | cadena                     | sí      | La cadena de versión completa de SemVer 2.0.0 del paquete (podría contener metadatos de la compilación)
Descripción    | cadena                     | No       | 
versiones       | matriz de objetos           | sí      | Todas las versiones de paquete que coincidan los `prerelease` parámetro
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
comprobar       | booleano                    | No       | Un valor booleano JSON que indica si el paquete es [comprobado](../reference/id-prefix-reservation.md)

En nuget.org, un paquete verificado es uno que tiene un identificador de paquete que coincide con un prefijo de identificador reservado y que pertenecen a uno de los propietarios del prefijo reservado. Para obtener más información, consulte el [documentación acerca de la reserva de prefijo de identificador](../reference/id-prefix-reservation.md).

Los metadatos contenidos en el objeto de resultado de búsqueda se toman de la versión más reciente del paquete. Cada elemento de la `versions` matriz es un objeto JSON con las siguientes propiedades:

nombre      | Tipo    | Obligatorio | Notas
--------- | ------- | -------- | -----
@id       | cadena  | sí      | La dirección URL absoluta a la categoría asociada [hoja de registro](registration-base-url-resource.md#registration-leaf)
version   | cadena  | sí      | La cadena de versión completa de SemVer 2.0.0 del paquete (podría contener metadatos de la compilación)
Descargas | enteros | sí      | El número de descargas para esta versión de paquete específico

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [search-result.json](./_data/search-result.json)]
