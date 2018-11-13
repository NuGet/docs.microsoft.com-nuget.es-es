---
title: Insertar paquetes de símbolos, API de NuGet | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: El servicio de publicación permite a los clientes publicar nuevos paquetes de símbolos.
keywords: Paquete de símbolos de inserción de API de NuGet
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580418"
---
# <a name="push-symbol-packages"></a>Paquetes de símbolos de inserción

Es posible insertar paquetes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mediante la API de NuGet V3.
Estas operaciones se basa en el `SymbolPackagePublish` encontrar el recurso en el [índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

La siguiente `@type` se usa el valor:

Valor de@type                  | Notas
--------------------        | -----
SymbolPackagePublish/4.9.0  | La versión inicial

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las siguientes API es el valor de la `@id` propiedad de la `SymbolPackagePublish/4.9.0` recursos en el origen de paquete [índice de servicio](service-index.md). Para obtener la documentación a continuación, se usa la dirección URL de nuget.org. Considere la posibilidad de `https://www.nuget.org/api/v2/symbolpackage` como marcador de posición para el `@id` valor se encuentra en el índice de servicio.

## <a name="http-methods"></a>Métodos HTTP

El `PUT` método HTTP es compatible con este recurso. 

## <a name="push-a-symbol-package"></a>Insertar un paquete de símbolos

NuGet.org admite Insertar nuevo formato de paquetes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mediante la API siguiente. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Paquetes de símbolos con el mismo identificador y versión se pueden enviar varias veces. En los casos siguientes, se rechazarán un paquete de símbolos.
- No existe un paquete con el mismo identificador y versión.
- Un paquete de símbolos con el mismo identificador y versión se ha insertado, pero no se ha publicado.
- El paquete de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) no es válido (consulte [restricciones del paquete de símbolos](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parámetros de solicitud

nombre           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | cadena | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.

La clave de API es una cadena opaca llegado desde el origen del paquete por el usuario y configurado en el cliente. Ningún formato de cadena concreta está asignada, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores de encabezado HTTP.

### <a name="request-body"></a>Cuerpo de la solicitud

El cuerpo de solicitud para la inserción de símbolos es igual que con el cuerpo de solicitud de una solicitud de inserción del paquete (consulte [empaquetar la inserción y eliminación](package-publish-resource.md)). 

### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
201         | El paquete de símbolos se ha insertado correctamente.
400         | El paquete de símbolos proporcionado no es válido.
401         | El usuario no está autorizado para realizar esta acción.
404         | No existe un paquete con el identificador proporcionado y la versión correspondiente.
409         | Se ha insertado un paquete de símbolos con el identificador proporcionado y la versión, pero aún no está disponible.
413         | El paquete es demasiado grande.

