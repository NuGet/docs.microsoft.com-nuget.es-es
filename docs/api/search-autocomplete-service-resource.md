---
title: Autocompletar, API de NuGet
description: El servicio de búsqueda de autocompletar admite la detección interactiva de identificadores y versiones de paquetes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488304"
---
# <a name="autocomplete"></a>Autocompletar

Es posible crear un identificador de paquete y una experiencia de autocompletar de versión mediante la API V3. El recurso que se usa para realizar consultas de autocompletar es el recurso que `SearchAutocompleteService` se encuentra en el índice de [servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

Se usan `@type` los siguientes valores:

Valor de@type                          | Notas
------------------------------------ | -----
SearchAutocompleteService            | La versión inicial
SearchAutocompleteService/3.0.0-beta | Alias de`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Alias de`SearchAutocompleteService`

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las siguientes API es el valor de `@id` la propiedad asociada a uno de los valores `@type` de recursos mencionados anteriormente. En el siguiente documento, se usará la dirección `{@id}` URL base del marcador de posición.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL encontradas en el recurso de registro admiten `HEAD`los métodos `GET` http y.

## <a name="search-for-package-ids"></a>Buscar identificadores de paquete

La primera API de autocompletar admite la búsqueda de una parte de una cadena de identificador de paquete. Esto es genial cuando desea proporcionar una característica de escritura anticipada de paquete en una interfaz de usuario integrada con un origen de paquete NuGet.

Un paquete con solo versiones que no figuran en la lista no aparecerá en los resultados.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parámetros de solicitud

NOMBRE        | En     | Type    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | No       | Cadena que se va a comparar con los identificadores de paquete.
skip        | URL    | integer | No       | Número de resultados que se van a omitir para la paginación.
echar        | URL    | integer | No       | Número de resultados que se van a devolver, para la paginación
versión preliminar  | URL    | boolean | No       | `true`o `false` determinar si se deben incluir los [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | No       | Una cadena de versión de SemVer 1.0.0 

La consulta `q` de autocompletar se analiza de la manera definida por la implementación del servidor. nuget.org admite la consulta del prefijo de tokens de identificador de paquete, que son partes del identificador que se producen dividiendo el original por caracteres de mayúsculas y minúsculas Camel.

El `skip` valor predeterminado del parámetro es 0.

El `take` parámetro debe ser un entero mayor que cero. La implementación del servidor puede imponer un valor máximo.

Si `prerelease` no se proporciona, se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se usa para participar en los [paquetes de SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si se excluye este parámetro de consulta, solo se devolverán los identificadores de paquete con versiones compatibles con SemVer 1.0.0 (con las advertencias de [control de versiones de NuGet estándar](../concepts/package-versioning.md) , como las cadenas de versión con 4 partes enteras).
Si `semVerLevel=2.0.0` se proporciona, se devolverán los paquetes compatibles con SemVer 1.0.0 y SemVer 2.0.0. Para obtener más información, consulte la [compatibilidad con SemVer 2.0.0 para Nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Respuesta

La respuesta es un documento JSON que contiene `take` resultados de rellenado de forma completa.

El objeto JSON raíz tiene las siguientes propiedades:

NOMBRE      | Type             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
totalHits | integer          | sí      | El número total de coincidencias, que `skip` no se tienen en cuenta y`take`
data      | matriz de cadenas | sí      | Los identificadores de paquete que coinciden con la solicitud

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumerar versiones de paquetes

Una vez que se detecta un identificador de paquete mediante la API anterior, un cliente puede usar la API de Autocompletar para enumerar las versiones de paquete para un identificador de paquete proporcionado.

Una versión del paquete que se ha quitado de la lista no aparecerá en los resultados.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parámetros de solicitud

NOMBRE        | En     | Type    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | sí      | IDENTIFICADOR de paquete para el que se van a capturar versiones
versión preliminar  | URL    | boolean | No       | `true`o `false` determinar si se deben incluir los [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | No       | Una cadena de versión de SemVer 2.0.0 

Si `prerelease` no se proporciona, se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se usa para participar en los paquetes de SemVer 2.0.0. Si se excluye este parámetro de consulta, solo se devolverán las versiones de SemVer 1.0.0. Si `semVerLevel=2.0.0` se proporciona, se devolverán las versiones SemVer 1.0.0 y SemVer 2.0.0. Para obtener más información, consulte la [compatibilidad con SemVer 2.0.0 para Nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Respuesta

La respuesta es un documento JSON que contiene todas las versiones de paquete del identificador de paquete proporcionado, filtrando por los parámetros de consulta especificados.

El objeto JSON raíz tiene la siguiente propiedad:

NOMBRE      | Type             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
data      | matriz de cadenas | sí      | Las versiones del paquete que coinciden con la solicitud

Las versiones de paquete de `data` la matriz pueden contener metadatos de compilación de SemVer `1.0.0+metadata`2.0.0 (por `semVerLevel=2.0.0` ejemplo,) si se proporciona en la cadena de consulta.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
