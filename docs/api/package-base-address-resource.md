---
title: Contenido del paquete, NuGet API
description: La dirección base del paquete es una interfaz sencilla para capturar el propio paquete.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426764"
---
# <a name="package-content"></a>Contenido del paquete

Es posible generar una dirección URL para capturar el contenido de un paquete arbitrario (el archivo .nupkg) mediante la API de V3. El recurso usado para recuperar el contenido del paquete es el `PackageBaseAddress` encontrar el recurso en el [índice de servicio](service-index.md). Este recurso también permite la detección de todas las versiones de un paquete, aparece o no enumerado.

Este recurso se conoce comúnmente como el "paquete base dirección" o como contenedor"plano".

## <a name="versioning"></a>Control de versiones

La siguiente `@type` se usa el valor:

Valor de@type              | Notas
------------------------ | -----
PackageBaseAddress/3.0.0 | La versión inicial

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las siguientes API es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valor. En el siguiente documento, la dirección URL base del marcador de posición `{@id}` se usará.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL se encuentra en la compatibilidad con recursos de registro de los métodos HTTP `GET` y `HEAD`.

## <a name="enumerate-package-versions"></a>Enumerar versiones de paquetes

Si el cliente sabe que un identificador de paquete y desea descubrir que las versiones del paquete el paquete de código fuente disponible, el cliente puede construir una dirección URL de predicción para enumerar todas las versiones de paquete. Esta lista está pensada para ser una "lista de directorios" para la API de contenido de paquete que se mencionan a continuación.

> [!Note]
> Esta lista contiene ambas versiones del paquete figuran.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parámetros de solicitud

Name     | En     | Tipo    | Obligatorio | Notas
-------- | ------ | ------- | -------- | -----
LOWER_ID | Resolución    | cadena  | sí      | El identificador del paquete, en minúsculas

El `LOWER_ID` valor es el identificador de paquete deseado utilizando las reglas implementadas por en minúsculas. La red [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

### <a name="response"></a>Respuesta

Si el origen del paquete no tiene que no hay ninguna versión del identificador del paquete suministrado, se devuelve un código de 404 estado.

Si el origen del paquete tiene una o varias versiones, se devuelve un código de 200 estado. El cuerpo de respuesta es un objeto JSON con la siguiente propiedad:

Name     | Tipo             | Obligatorio | Notas
-------- | ---------------- | -------- | -----
versiones | matriz de cadenas | sí      | El paquete Id. disponibles

Las cadenas en el `versions` matriz todos minúscula, [normalizar las cadenas de versión de NuGet](../reference/package-versioning.md#normalized-version-numbers). Las cadenas de versión no contienen los metadatos de la compilación de SemVer 2.0.0.

La intención es que las cadenas de versión que se encuentra en esta matriz se pueden usar literalmente para el `LOWER_VERSION` tokens que se encuentra en los siguientes puntos de conexión.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Descargar contenido de paquete (archivo .nupkg)

Si el cliente sabe que un identificador de paquete y la versión y desea descargar el contenido del paquete, solo deberá construir la dirección URL siguiente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parámetros de solicitud

Name          | En     | Tipo   | Obligatorio | Notas
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Resolución    | cadena | sí      | El identificador del paquete, en minúsculas
LOWER_VERSION | Resolución    | cadena | sí      | La versión del paquete, normalizar y en minúsculas

Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. La red [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
.

El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [reglas de normalización](../reference/package-versioning.md#normalized-version-numbers). Esto significa que los metadatos de compilación que se permiten la especificación de SemVer 2.0.0 en este caso se deben excluir.

### <a name="response-body"></a>Cuerpo de la respuesta

Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado. El cuerpo de respuesta será el contenido del paquete.

Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Respuesta de ejemplo

El flujo binario que es el archivo .nupkg para Newtonsoft.Json 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Descargue el manifiesto del paquete (.nuspec)

Si el cliente sabe que un identificador de paquete y la versión y desea descargar el manifiesto del paquete, solo deberá construir la dirección URL siguiente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parámetros de solicitud

Name          | En     | Tipo   | Obligatorio | Notas
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Resolución    | cadena | sí      | El identificador del paquete, en minúsculas
LOWER_VERSION | Resolución    | cadena | sí      | La versión del paquete, normalizar y en minúsculas

Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. La red [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [reglas de normalización](../reference/package-versioning.md#normalized-version-numbers). Esto significa que los metadatos de compilación que se permiten la especificación de SemVer 2.0.0 en este caso se deben excluir.

### <a name="response-body"></a>Cuerpo de la respuesta

Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado. El cuerpo de respuesta será el manifiesto del paquete, que es el archivo .nuspec contenidos en los archivos .nupkg correspondiente. El archivo .nuspec es un documento XML.

Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
