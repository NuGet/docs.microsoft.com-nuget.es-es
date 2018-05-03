---
title: Contenido del paquete, NuGet API
description: La dirección base del paquete es una interfaz sencilla para capturar el propio paquete.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="package-content"></a>Contenido del paquete

Es posible generar una dirección URL para recuperar contenido de un paquete arbitrario (el archivo .nupkg) mediante la API V3. El recurso que se utiliza para capturar el contenido del paquete es el `PackageBaseAddress` recurso se encuentra en la [índice servicio](service-index.md). Este recurso también habilita la detección de todas las versiones de un paquete, que se indica o dados de baja.

Este recurso se conoce normalmente como la "paquete base dirección" o "contenedor sin formato".

## <a name="versioning"></a>Control de versiones

El siguiente `@type` valor se utiliza:

Valor de @type              | Notas
------------------------ | -----
PackageBaseAddress/3.0.0 | La versión inicial

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las API siguientes es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valor. En el siguiente documento, el marcador de posición de la dirección URL base `{@id}` se usará.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL se encuentra en el soporte de registro del recurso los métodos HTTP `GET` y `HEAD`.

## <a name="enumerate-package-versions"></a>Enumerar las versiones del paquete

Si el cliente sabe que un identificador de paquete y desea descubrir que versiones del paquete el paquete de origen tiene disponible, el cliente puede construir una dirección URL de predicción para enumerar todas las versiones de paquete. Esta lista se ha diseñado para ser una "lista de directorios" para la API de contenido de paquete que se mencionan más abajo.

> [!Note]
> Esta lista contiene ambas versiones de la lista y que no figuran en el paquete.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parámetros de solicitud

nombre     | En     | Tipo    | Obligatorio | Notas
-------- | ------ | ------- | -------- | -----
LOWER_ID | Resolución    | cadena  | sí      | El identificador del paquete, en minúsculas

El `LOWER_ID` valor es el identificador de paquete deseado en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

### <a name="response"></a>Respuesta

Si el origen del paquete no tiene ninguna versión del identificador del paquete suministrado, se devuelve un código de 404 estado.

Si el origen del paquete tiene una o varias versiones, se devuelve un código de 200 estado. El cuerpo de respuesta es un objeto JSON con la siguiente propiedad:

nombre     | Tipo             | Obligatorio | Notas
-------- | ---------------- | -------- | -----
versiones | Matriz de cadenas | sí      | El paquete identificadores disponibles

Las cadenas en el `versions` matriz todos minúscula, [normalizar las cadenas de versión de NuGet](../reference/package-versioning.md#normalized-version-numbers). Las cadenas de versión no contienen ningún metadato de compilación SemVer 2.0.0.

La intención es que las cadenas de versión que se encuentra en esta matriz pueden utilizarse literalmente para el `LOWER_VERSION` tokens ubicados en los siguientes extremos.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Descargar contenido de paquete (.nupkg)

Si el cliente sabe que un identificador de paquete y la versión y desea descargar el contenido del paquete, solo tiene construir la dirección URL siguiente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parámetros de solicitud

nombre          | En     | Tipo   | Obligatorio | Notas
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Resolución    | cadena | sí      | El identificador del paquete, en minúsculas
LOWER_VERSION | Resolución    | cadena | sí      | La versión del paquete, normalizar y en minúsculas

Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [las reglas de normalización](../reference/package-versioning.md#normalized-version-numbers). Esto significa que los metadatos de compilación está permitido por la especificación de SemVer 2.0.0 se deben excluir en este caso.

### <a name="response-body"></a>Cuerpo de la respuesta

Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado. El cuerpo de respuesta será el contenido del paquete.

Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Respuesta de ejemplo

La secuencia binaria que sea el .nupkg para Newtonsoft.Json 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Descargue el manifiesto del paquete (NuSpec)

Si el cliente sabe que un identificador de paquete y la versión y desea descargar el manifiesto del paquete, solo tiene construir la dirección URL siguiente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parámetros de solicitud

nombre          | En     | Tipo    | Obligatorio | Notas
------------- | ------ | ------- | -------- | -----
LOWER_ID      | Resolución    | cadena  | sí      | El identificador del paquete, en minúsculas
LOWER_VERSION | Resolución    | enteros | sí      | La versión del paquete, normalizar y en minúsculas

Ambos `LOWER_ID` y `LOWER_VERSION` están en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

El `LOWER_VERSION` se normaliza la versión del paquete deseado mediante la versión de NuGet [las reglas de normalización](../reference/package-versioning.md#normalized-version-numbers). Esto significa que los metadatos de compilación está permitido por la especificación de SemVer 2.0.0 se deben excluir en este caso.

### <a name="response-body"></a>Cuerpo de la respuesta

Si el paquete existe en el origen del paquete, se devuelve un código de 200 estado. El cuerpo de respuesta será el manifiesto del paquete, que es el NuSpec contenidos en el .nupkg correspondiente. El NuSpec es un documento XML.

Si el paquete no existe en el origen del paquete, se devuelve un código de 404 estado.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
