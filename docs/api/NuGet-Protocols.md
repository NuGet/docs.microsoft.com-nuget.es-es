---
title: Protocolos de NuGet.org
description: Los protocolos de nuget.org en constante evolución para interactuar con los clientes de NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547278"
---
# <a name="nugetorg-protocols"></a>protocolos de NuGet.org

Para interactuar con nuget.org, los clientes deben seguir ciertos protocolos. Dado que estos protocolos mantengan evolucionando, los clientes deben identificar la versión del protocolo que se usan cuando se llama a nuget.org específica API. Esto permite nuget.org introducir cambios de forma que no son importantes para los clientes anteriores.

> [!Note]
> Las API documentadas en esta página son específicas de nuget.org y no hay ninguna expectativa para otras implementaciones del servidor de NuGet introducir estas API. 

Para obtener información acerca de la API de NuGet ampliamente implementado en el ecosistema de NuGet, vea el [Introducción a la API](overview.md).

En este tema se enumera varios protocolos como y cuando le pidan existencia.

## <a name="nuget-protocol-version-410"></a>Versión de protocolo de NuGet 4.1.0

La 4.1.0 protocolo especifica el uso de claves de comprobar el ámbito para interactuar con los servicios que no sean de nuget.org, para validar un paquete en una cuenta de nuget.org. Tenga en cuenta que el `4.1.0` versión número es una cadena opaca pero ocurre para que coincida con la primera versión del cliente NuGet oficial que admiten este protocolo.

La validación garantiza que las claves de API creados por el usuario solo se usan con nuget.org, y esa otra comprobación o la validación de un servicio de terceros se controla a través de un claves de comprobar el ámbito de un solo uso. Estas claves de comprobar el ámbito pueden usarse para validar que el paquete pertenece a un usuario determinado (cuenta) en nuget.org.

### <a name="client-requirement"></a>Requisito de cliente

Los clientes tienen que pasar el encabezado siguiente cuando realicen llamadas de API **inserción** paquetes en nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Tenga en cuenta que el `X-NuGet-Client-Version` encabezado tiene una semántica similar pero está reservado para su uso por el cliente NuGet oficial. Los clientes de terceros deben usar el `X-NuGet-Protocol-Version` encabezado y valor.

El **inserción** propio protocolo se describe en la documentación de la [ `PackagePublish` recursos](package-publish-resource.md).

Si un cliente interactúa con los servicios externos y necesidades para validar si un paquete pertenece a un usuario determinado (cuenta), debe usar el protocolo siguiente y utilizar las teclas de comprobar el ámbito y no las claves de API de nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API para solicitar una clave de comprobación dentro del ámbito

Esta API se usa para obtener una clave de comprobar el ámbito de un autor de nuget.org validar un paquete en la propiedad por él mismo.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parámetros de solicitud

nombre           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
Id.             | Resolución    | cadena | sí      | Para el que se solicita la clave de ámbito de comprobar la identidier de paquete
VERSION        | Resolución    | cadena | No       | La versión del paquete
X-NuGet-ApiKey | Header | cadena | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.

#### <a name="response"></a>Respuesta

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API para comprobar la clave de ámbito Compruebe

Esta API se usa para validar una clave de comprobar el ámbito de paquete propiedad por el autor de nuget.org.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parámetros de solicitud

nombre           | En     | Tipo   | Obligatorio | Notas
-------------  | ------ | ------ | -------- | -----
Id.             | Resolución    | cadena | sí      | El identificador del paquete para el que se solicita la clave de ámbito de verify
VERSION        | Resolución    | cadena | No       | La versión del paquete
X-NuGet-ApiKey | Header | cadena | sí      | Por ejemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Esta clave de API de ámbito Compruebe expira en un momento del día o en el primer uso, lo que ocurra primero.

#### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
200         | La clave de API es válida
403         | La clave de API no es válido o no está autorizado a insertar en el paquete
404         | El paquete al que hace referencia `ID` y `VERSION` (opcional) no existe
