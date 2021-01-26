---
title: Protocolos de nuget.org
description: Los protocolos nuget.org en evolución para interactuar con los clientes de NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773970"
---
# <a name="nugetorg-protocols"></a>Protocolos de nuget.org

Para interactuar con nuget.org, los clientes deben seguir determinados protocolos. Dado que estos protocolos siguen evolucionando, los clientes deben identificar la versión del protocolo que usan al llamar a determinadas API de nuget.org. Esto permite a nuget.org introducir cambios en una forma ininterrumpida para los clientes anteriores.

> [!Note]
> Las API documentadas en esta página son específicas de nuget.org y no se espera que otras implementaciones de servidor NuGet presenten estas API. 

Para obtener información sobre la API de NuGet implementada en general en el ecosistema de NuGet, consulte la [Introducción a la API](overview.md).

En este tema se enumeran varios protocolos como y cuando llegan a su existencia.

## <a name="nuget-protocol-version-410"></a>Versión del protocolo NuGet 4.1.0

El protocolo 4.1.0 especifica el uso de claves Verify-Scope para interactuar con servicios distintos de nuget.org, para validar un paquete con una cuenta nuget.org. Tenga en cuenta que el `4.1.0` número de versión es una cadena opaca pero que coincide con la primera versión del cliente de NuGet oficial que admitía este protocolo.

La validación garantiza que las claves de API creadas por el usuario solo se usan con nuget.org y que otras comprobaciones o validaciones de un servicio de terceros se controlan a través de las claves Verify-Scope de un solo uso. Estas claves Verify-Scope se pueden usar para validar que el paquete pertenece a un usuario determinado (cuenta) en nuget.org.

### <a name="client-requirement"></a>Requisitos del cliente

Los clientes deben pasar el encabezado siguiente cuando realizan llamadas API para **enviar paquetes a** Nuget.org:

```
X-NuGet-Protocol-Version: 4.1.0
```

Tenga en cuenta que el `X-NuGet-Client-Version` encabezado tiene una semántica similar pero que se reserva para que solo lo use el cliente de NuGet oficial. Los clientes de terceros deben usar el `X-NuGet-Protocol-Version` encabezado y el valor.

El protocolo de **extracción** en sí se describe en la documentación del [ `PackagePublish` recurso](package-publish-resource.md).

Si un cliente interactúa con servicios externos y necesita validar si un paquete pertenece a un usuario determinado (cuenta), debe usar el protocolo siguiente y usar las claves Verify-Scope y no las claves de API de nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API para solicitar una clave Verify-Scope

Esta API se usa para obtener una clave Verify-Scope para que un autor de nuget.org valide un paquete propiedad de él.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parámetros de solicitud

Nombre           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
ID             | Dirección URL    | string | sí      | El paquete identidier para el que se solicita la clave de ámbito de comprobación.
VERSION        | Dirección URL    | string | no       | La versión del paquete
X-NuGet-ApiKey | Encabezado | string | sí      | Por ejemplo: `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Response

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API para comprobar la clave de ámbito de comprobación

Esta API se usa para validar una clave Verify-Scope para el paquete propiedad del autor de nuget.org.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parámetros de solicitud

Nombre           | En     | Tipo   | Obligatorio | Notas
-------------  | ------ | ------ | -------- | -----
ID             | Dirección URL    | string | sí      | Identificador del paquete para el que se solicita la clave de ámbito de comprobación.
VERSION        | Dirección URL    | string | no       | La versión del paquete
X-NuGet-ApiKey | Encabezado | string | sí      | Por ejemplo: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Esto comprueba que la clave de API de ámbito expire en el momento del día o en el primer uso, lo que ocurra primero.

#### <a name="response"></a>Response

Código de estado | Significado
----------- | -------
200         | La clave de API es válida
403         | La clave de API no es válida o no está autorizada para la inserciones en el paquete
404         | El paquete al que hace referencia `ID` y `VERSION` (opcional) no existe.
