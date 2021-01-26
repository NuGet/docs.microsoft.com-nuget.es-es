---
title: Contenido del paquete, API de NuGet
description: La dirección base del paquete es una interfaz sencilla para capturar el propio paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773930"
---
# <a name="package-content"></a>Contenido de un paquete

Es posible generar una dirección URL para capturar el contenido de un paquete arbitrario (el archivo. nupkg) mediante la API V3. El recurso que se usa para obtener el contenido del paquete es el `PackageBaseAddress` recurso que se encuentra en el [Índice de servicio](service-index.md). Este recurso también habilita la detección de todas las versiones de un paquete, enumeradas o no enumeradas.

Este recurso se conoce comúnmente como "dirección base del paquete" o como "contenedor plano".

## <a name="versioning"></a>Control de versiones

`@type`Se usa el siguiente valor:

Valor de @type              | Notas
------------------------ | -----
PackageBaseAddress/3.0.0 | La versión inicial

## <a name="base-url"></a>URL base

La dirección URL base para las siguientes API es el valor de la `@id` propiedad asociada al valor de recurso mencionado anteriormente `@type` . En el siguiente documento, se usará la dirección URL base del marcador de posición `{@id}` .

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL encontradas en el recurso de registro admiten los métodos HTTP `GET` y `HEAD` .

## <a name="enumerate-package-versions"></a>Enumerar versiones de paquetes

Si el cliente conoce un identificador de paquete y desea detectar qué versiones de paquete tiene el origen del paquete, el cliente puede crear una dirección URL de predicción para enumerar todas las versiones del paquete. Esta lista está pensada como una "lista de directorios" para la API de contenido de paquete que se menciona a continuación.

> [!Note]
> Esta lista contiene las versiones de paquetes que se muestran y que no figuran en la lista.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Parámetros de solicitud

Nombre     | En     | Tipo    | Obligatorio | Notas
-------- | ------ | ------- | -------- | -----
LOWER_ID | Dirección URL    | string  | sí      | El identificador del paquete, en minúsculas

El `LOWER_ID` valor es el identificador de paquete deseado en minúsculas mediante las reglas implementadas por. Método de la red [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .

### <a name="response"></a>Response

Si el origen del paquete no tiene ninguna versión del identificador de paquete proporcionado, se devuelve un código de estado 404.

Si el origen del paquete tiene una o más versiones, se devuelve un código de estado 200. El cuerpo de la respuesta es un objeto JSON con la siguiente propiedad:

Nombre     | Tipo             | Obligatorio | Notas
-------- | ---------------- | -------- | -----
versions | Matriz de cadenas | sí      | Las versiones disponibles

Las cadenas de la `versions` matriz están todas en minúsculas, con las [cadenas de versión de NuGet normalizadas](../concepts/package-versioning.md#normalized-version-numbers). Las cadenas de versión no contienen metadatos de compilación de SemVer 2.0.0.

La intención es que las cadenas de versión encontradas en esta matriz se puedan usar literalmente para los `LOWER_VERSION` tokens que se encuentran en los puntos de conexión siguientes.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Descargar contenido de paquete (. nupkg)

Si el cliente conoce un identificador y una versión del paquete y desea descargar el contenido del paquete, solo necesita construir la dirección URL siguiente:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>Parámetros de solicitud

Nombre          | En     | Tipo   | Obligatorio | Notas
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Dirección URL    | string | sí      | El identificador del paquete, en minúsculas
LOWER_VERSION | Dirección URL    | string | sí      | Versión del paquete, normalizado y en minúsculas

`LOWER_ID`Y `LOWER_VERSION` están en minúsculas mediante las reglas implementadas por. De la red[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)
.

`LOWER_VERSION`Es la versión del paquete deseada normalizada con [las reglas de normalización](../concepts/package-versioning.md#normalized-version-numbers)de la versión de NuGet. Esto significa que los metadatos de compilación permitidos por la especificación SemVer 2.0.0 deben excluirse en este caso.

### <a name="response-body"></a>Response body

Si el paquete existe en el origen del paquete, se devuelve un código de estado 200. El cuerpo de la respuesta será el contenido del paquete.

Si el paquete no existe en el origen del paquete, se devuelve un código de estado 404.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>Respuesta de muestra

Secuencia binaria que es. nupkg para Newtonsoft.Jsen 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Descargar el manifiesto del paquete (. nuspec)

Si el cliente conoce un identificador y una versión del paquete y desea descargar el manifiesto del paquete, solo necesita construir la dirección URL siguiente:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>Parámetros de solicitud

Nombre          | En     | Tipo   | Obligatorio | Notas
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Dirección URL    | string | sí      | El identificador del paquete, en minúsculas
LOWER_VERSION | Dirección URL    | string | sí      | Versión del paquete, normalizado y en minúsculas

`LOWER_ID`Y `LOWER_VERSION` están en minúsculas mediante las reglas implementadas por. Método de la red [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .

`LOWER_VERSION`Es la versión del paquete deseada normalizada con [las reglas de normalización](../concepts/package-versioning.md#normalized-version-numbers)de la versión de NuGet. Esto significa que los metadatos de compilación permitidos por la especificación SemVer 2.0.0 deben excluirse en este caso.

### <a name="response-body"></a>Response body

Si el paquete existe en el origen del paquete, se devuelve un código de estado 200. El cuerpo de la respuesta será el manifiesto del paquete, que es el archivo. nuspec incluido en el archivo. nupkg correspondiente. El archivo. nuspec es un documento XML.

Si el paquete no existe en el origen del paquete, se devuelve un código de estado 404.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>Respuesta de muestra

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
