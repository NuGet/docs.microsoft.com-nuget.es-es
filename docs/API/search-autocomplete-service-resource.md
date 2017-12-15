---
title: Autocompletar, NuGet API | Documentos de Microsoft
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
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: "El servicio de búsqueda Autocompletar admite las versiones y descubrimiento interactivo de identificadores de paquete."
keywords: "API de Autocompletar de NuGet, Id. de paquete de búsqueda de NuGet, Id. de paquete de subcadena"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a>Autocompletar

Es posible crear una experiencia paquete identificador y la versión Autocompletar mediante la API V3. El recurso que se utiliza para realizar consultas de Autocompletar es el `SearchAutocompleteService` recurso se encuentra en la [índice servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

Los siguientes `@type` se usan valores:

Valor de @type                          | Notas
------------------------------------ | -----
SearchAutocompleteService            | La versión inicial
SearchAutocompleteService/3.0.0-beta | Alias de`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias de`SearchAutocompleteService`

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las API siguientes es el valor de la `@id` propiedad asociado a uno de los recursos mencionados anteriormente `@type` valores. En el siguiente documento, el marcador de posición de la dirección URL base `{@id}` se usará.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL se encuentra en el soporte de registro del recurso los métodos HTTP `GET` y `HEAD`.

## <a name="search-for-package-ids"></a>Busque los identificadores de paquete

La primera Autocompletar API admite las búsquedas de parte de una cadena de identificador de paquete. Esto es excelente cuando desea proporcionar una característica de escritura anticipada de paquete en una interfaz de usuario integrada con un origen de paquete de NuGet.

Un paquete con solo las versiones que no figuran en no aparecerán en los resultados.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>Parámetros de solicitud

Name        | En     | Tipo    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
q           | Dirección URL    | string  | No       | La cadena para comparar identificadores de paquete
skip        | Dirección URL    | enteros | No       | El número de resultados que se va a omitir, para la paginación
Take        | Dirección URL    | enteros | No       | El número de resultados que se va a devolver para la paginación
versión preliminar  | Dirección URL    | booleano | No       | `true`o `false` determinar si se debe incluir [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | Dirección URL    | string  | No       | Una cadena de versión SemVer 1.0.0 

La consulta de Autocompletar `q` se analiza de forma que se define mediante la implementación del servidor. NuGet.org admite las consultas para el prefijo de tokens de Id. de paquete, que son partes del identificador generado por spliting original, caracteres camel de caso y símbolos.

El `skip` parámetro el valor predeterminado es 0.

El `take` parámetro debe ser un entero mayor que cero. La implementación del servidor puede imponer un valor máximo.

Si `prerelease` no es siempre, se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se utiliza para participar en [SemVer 2.0.0 paquetes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si se excluye de este parámetro de consulta, se devolverán los identificadores de paquete solo con las versiones compatibles de SemVer 1.0.0 (con la [control de versiones de NuGet estándar](../reference/package-versioning.md) advertencias, como las cadenas de versión con 4 partes entero).
Si `semVerLevel=2.0.0` es siempre devolverán SemVer 1.0.0 y paquetes de SemVer 2.0.0 compatibles. Consulte la [SemVer 2.0.0 compatibilidad con nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obtener más información.

### <a name="response"></a>Respuesta

La respuesta es documento JSON que contiene hasta `take` resultados de Autocompletar.

El objeto JSON raíz tiene las siguientes propiedades:

Name      | Tipo             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
totalHits | enteros          | sí      | El número total de coincidencias, sin tener en cuenta `skip` y`take`
datos      | Matriz de cadenas | sí      | El paquete coincidentes con la solicitud de identificadores

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumerar las versiones del paquete

Una vez que se detecta un identificador de paquete mediante la API anterior, un cliente puede utilizar la API de Autocompletar para enumerar las versiones del paquete para un identificador de paquete proporcionado.

Una versión de paquete que no figuran en no aparecerán en los resultados.

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>Parámetros de solicitud

Name        | En     | Tipo    | Obligatorio | Notas
----------- | ------ | ------- | -------- | -----
id          | Dirección URL    | string  | sí      | El identificador del paquete para capturar las versiones de
versión preliminar  | Dirección URL    | booleano | No       | `true`o `false` determinar si se debe incluir [paquetes de versión preliminar](../create-packages/prerelease-packages.md)
semVerLevel | Dirección URL    | string  | No       | Una cadena de versión SemVer 2.0.0 

Si `prerelease` no es siempre, se excluyen los paquetes de versión preliminar.

El `semVerLevel` parámetro de consulta se utiliza para participar en paquetes SemVer 2.0.0. Si se excluye de este parámetro de consulta, se devolverá solo las versiones de SemVer 1.0.0. Si `semVerLevel=2.0.0` es siempre devolverán SemVer 1.0.0 y SemVer 2.0.0 versiones. Consulte la [SemVer 2.0.0 compatibilidad con nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obtener más información.

### <a name="response"></a>Respuesta

La respuesta es documento JSON que contiene todas las versiones de paquete del identificador de paquete suministrado, filtrado por los parámetros de consulta determinada.

El objeto JSON raíz tiene la propiedad siguiente:

Name      | Tipo             | Obligatorio | Notas
--------- | ---------------- | -------- | -----
datos      | Matriz de cadenas | sí      | Las versiones del paquete coincidentes con la solicitud

Las versiones del paquete en el `data` matriz podría contener metadatos de compilación SemVer 2.0.0 (p. ej. `1.0.0+metadata`) si el `semVerLevel=2.0.0` se proporcionó en la cadena de consulta.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
