---
title: Contenido del paquete, API de NuGet
description: La dirección base del paquete es una interfaz sencilla para capturar el propio paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094119"
---
# <a name="package-content"></a>Contenido del paquete

Es posible generar una dirección URL para capturar el contenido de un paquete arbitrario (el archivo. nupkg) mediante la API V3. El recurso que se usa para obtener el contenido del `PackageBaseAddress` paquete es el recurso que se encuentra en el [Índice de servicio](service-index.md). Este recurso también habilita la detección de todas las versiones de un paquete, enumeradas o no enumeradas.

Este recurso se conoce comúnmente como "dirección base del paquete" o como "contenedor plano".

## <a name="versioning"></a>Control de versiones

Se usa `@type` el siguiente valor:

Valor de@type              | Notas
------------------------ | -----
PackageBaseAddress/3.0.0 | La versión inicial

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las siguientes API es el valor de `@id` la propiedad asociada al valor de `@type` recurso mencionado anteriormente. En el siguiente documento, se usará la dirección `{@id}` URL base del marcador de posición.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL encontradas en el recurso de registro admiten `HEAD`los métodos `GET` http y.

## <a name="enumerate-package-versions"></a>Enumerar versiones de paquetes

Si el cliente conoce un identificador de paquete y desea detectar qué versiones de paquete tiene el origen del paquete, el cliente puede crear una dirección URL de predicción para enumerar todas las versiones del paquete. Esta lista está pensada como una "lista de directorios" para la API de contenido de paquete que se menciona a continuación.

> [!Note]
> Esta lista contiene las versiones de paquetes que se muestran y que no figuran en la lista.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parámetros de solicitud

NOMBRE     | En     | Type    | Obligatorio | Notas
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | sí      | El identificador del paquete, en minúsculas

El `LOWER_ID` valor es el identificador de paquete deseado en minúsculas mediante las reglas implementadas por. Método de [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) la red.

### <a name="response"></a>Respuesta

Si el origen del paquete no tiene ninguna versión del identificador de paquete proporcionado, se devuelve un código de estado 404.

Si el origen del paquete tiene una o más versiones, se devuelve un código de estado 200. El cuerpo de la respuesta es un objeto JSON con la siguiente propiedad:

NOMBRE     | Type             | Obligatorio | Notas
-------- | ---------------- | -------- | -----
versiones | Matriz de cadenas | sí      | Las versiones disponibles

Las cadenas de la `versions` matriz están todas en minúsculas, con las [cadenas de versión de NuGet normalizadas](../concepts/package-versioning.md#normalized-version-numbers). Las cadenas de versión no contienen metadatos de compilación de SemVer 2.0.0.

La intención es que las cadenas de versión encontradas en esta matriz se puedan usar literalmente para `LOWER_VERSION` los tokens que se encuentran en los puntos de conexión siguientes.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Descargar contenido de paquete (. nupkg)

Si el cliente conoce un identificador y una versión del paquete y desea descargar el contenido del paquete, solo necesita construir la dirección URL siguiente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parámetros de solicitud

NOMBRE          | En     | Type   | Obligatorio | Notas
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | sí      | El identificador del paquete, en minúsculas
LOWER_VERSION | URL    | string | sí      | Versión del paquete, normalizado y en minúsculas

`LOWER_ID` Y`LOWER_VERSION` están en minúsculas mediante las reglas implementadas por. De la red[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
.

Es la versión del paquete deseada normalizada con [las reglas de normalización](../concepts/package-versioning.md#normalized-version-numbers)de la versión de NuGet. `LOWER_VERSION` Esto significa que los metadatos de compilación permitidos por la especificación SemVer 2.0.0 deben excluirse en este caso.

### <a name="response-body"></a>Cuerpo de la respuesta

Si el paquete existe en el origen del paquete, se devuelve un código de estado 200. El cuerpo de la respuesta será el contenido del paquete.

Si el paquete no existe en el origen del paquete, se devuelve un código de estado 404.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Respuesta de ejemplo

El flujo binario que es el archivo. nupkg para Newtonsoft. JSON 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Descargar el manifiesto del paquete (. nuspec)

Si el cliente conoce un identificador y una versión del paquete y desea descargar el manifiesto del paquete, solo necesita construir la dirección URL siguiente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parámetros de solicitud

NOMBRE          | En     | Type   | Obligatorio | Notas
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | sí      | El identificador del paquete, en minúsculas
LOWER_VERSION | URL    | string | sí      | Versión del paquete, normalizado y en minúsculas

`LOWER_ID` Y`LOWER_VERSION` están en minúsculas mediante las reglas implementadas por. Método de [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) la red.

Es la versión del paquete deseada normalizada con [las reglas de normalización](../concepts/package-versioning.md#normalized-version-numbers)de la versión de NuGet. `LOWER_VERSION` Esto significa que los metadatos de compilación permitidos por la especificación SemVer 2.0.0 deben excluirse en este caso.

### <a name="response-body"></a>Cuerpo de la respuesta

Si el paquete existe en el origen del paquete, se devuelve un código de estado 200. El cuerpo de la respuesta será el manifiesto del paquete, que es el archivo. nuspec incluido en el archivo. nupkg correspondiente. El archivo. nuspec es un documento XML.

Si el paquete no existe en el origen del paquete, se devuelve un código de estado 404.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
