---
title: Autocompletar, API de NuGet
description: El servicio de búsqueda de autocompletar admite la detección interactiva de identificadores y versiones de paquetes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: f574849bf99cd4da4eefd55c3dd5a0648042f0c1
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292298"
---
# <a name="autocomplete"></a>Autocompletar

Es posible crear un identificador de paquete y una experiencia de autocompletar de versión mediante la API V3. El recurso que se usa para realizar consultas de autocompletar es el `SearchAutocompleteService` recurso que se encuentra en el [Índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

`@type`Se usan los siguientes valores:

Valor de@type                          | Notas
------------------------------------ | -----
SearchAutocompleteService            | La versión inicial
SearchAutocompleteService/3.0.0-beta | Alias de`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Alias de`SearchAutocompleteService`
SearchAutocompleteService/3.5.0      | Incluye compatibilidad con el `packageType` parámetro de consulta

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5.0
Esta versión introduce la compatibilidad con el `packageType` parámetro de consulta, lo que permite filtrar por tipos de paquetes definidos por el autor. Es totalmente compatible con las consultas a `SearchAutocompleteService` .

## <a name="base-url"></a>URL base

La dirección URL base para las siguientes API es el valor de la `@id` propiedad asociada a uno de los valores de recursos mencionados anteriormente `@type` . En el siguiente documento, se usará la dirección URL base del marcador de posición `{@id}` .

## <a name="http-methods"></a>HTTP Methods

Todas las direcciones URL encontradas en el recurso de registro admiten los métodos HTTP `GET` y `HEAD` .

## <a name="search-for-package-ids"></a>Buscar identificadores de paquete

La primera API de autocompletar admite la búsqueda de una parte de una cadena de identificador de paquete. Esto es genial cuando desea proporcionar una característica de escritura anticipada de paquete en una interfaz de usuario integrada con un origen de paquete NuGet.

Un paquete con solo versiones que no figuran en la lista no aparecerá en los resultados.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>Parámetros de solicitud

Nombre        | En     | Tipo    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | Cadena que se va a comparar con los identificadores de paquete.
skip        | URL    | integer | no       | Número de resultados que se van a omitir para la paginación.
take        | URL    | integer | no       | Número de resultados que se van a devolver, para la paginación
prerelease  | URL    | boolean | no       | `true`o `false` determinar si se deben incluir los [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | Una cadena de versión de SemVer 1.0.0 
packageType | URL    | string  | no       | El tipo de paquete que se va a usar para filtrar paquetes (agregados en `SearchAutocompleteService/3.5.0` )

La consulta de autocompletar `q` se analiza de la manera definida por la implementación del servidor. nuget.org admite la consulta del prefijo de tokens de identificador de paquete, que son partes del identificador que se producen dividiendo el original por caracteres de mayúsculas y minúsculas Camel.

El `skip` valor predeterminado del parámetro es 0.

El `take` parámetro debe ser un entero mayor que cero. La implementación del servidor puede imponer un valor máximo.

Si `prerelease` no se proporciona, se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se usa para participar en los [paquetes de SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si se excluye este parámetro de consulta, solo se devolverán los identificadores de paquete con versiones compatibles con SemVer 1.0.0 (con las advertencias de [control de versiones de NuGet estándar](../concepts/package-versioning.md) , como las cadenas de versión con 4 partes enteras).
Si `semVerLevel=2.0.0` se proporciona, se devolverán los paquetes compatibles con SemVer 1.0.0 y SemVer 2.0.0. Para obtener más información, consulte la [compatibilidad con SemVer 2.0.0 para Nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

El `packageType` parámetro se usa para filtrar aún más los resultados de autocompletar a los paquetes que tengan al menos un tipo de paquete que coincida con el nombre del tipo de paquete.
Si el tipo de paquete proporcionado no es un tipo de paquete válido, tal y como se define en el [documento de tipo de paquete](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), se devolverá un resultado vacío.
Si el tipo de paquete proporcionado está vacío, no se aplicará ningún filtro. En otras palabras, si no se pasa ningún valor al `packageType` parámetro, se comportará como si no se hubiera pasado el parámetro.

### <a name="response"></a>Respuesta

La respuesta es un documento JSON que contiene `take` resultados de rellenado de forma completa.

El objeto JSON raíz tiene las siguientes propiedades:

Nombre      | Tipo             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
totalHits | integer          | sí      | El número total de coincidencias, que no se tienen en cuenta `skip` y`take`
datos      | Matriz de cadenas | sí      | Los identificadores de paquete que coinciden con la solicitud

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumerar versiones de paquetes

Una vez que se detecta un identificador de paquete mediante la API anterior, un cliente puede usar la API de Autocompletar para enumerar las versiones de paquete para un identificador de paquete proporcionado.

Una versión del paquete que se ha quitado de la lista no aparecerá en los resultados.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parámetros de solicitud

Nombre        | En     | Tipo    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | sí      | IDENTIFICADOR de paquete para el que se van a capturar versiones
prerelease  | URL    | boolean | no       | `true`o `false` determinar si se deben incluir los [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | Una cadena de versión de SemVer 2.0.0 

Si `prerelease` no se proporciona, se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se usa para participar en los paquetes de SemVer 2.0.0. Si se excluye este parámetro de consulta, solo se devolverán las versiones de SemVer 1.0.0. Si `semVerLevel=2.0.0` se proporciona, se devolverán las versiones SemVer 1.0.0 y SemVer 2.0.0. Para obtener más información, consulte la [compatibilidad con SemVer 2.0.0 para Nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Respuesta

La respuesta es un documento JSON que contiene todas las versiones de paquete del identificador de paquete proporcionado, filtrando por los parámetros de consulta especificados.

El objeto JSON raíz tiene la siguiente propiedad:

Nombre      | Tipo             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
datos      | Matriz de cadenas | sí      | Las versiones del paquete que coinciden con la solicitud

Las versiones de paquete de la `data` matriz pueden contener metadatos de compilación de SemVer 2.0.0 (por ejemplo, `1.0.0+metadata` ) si `semVerLevel=2.0.0` se proporciona en la cadena de consulta.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
