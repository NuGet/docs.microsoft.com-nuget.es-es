---
title: Paquetes de símbolos de envío, API de NuGet | Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: El servicio de publicación permite a los clientes publicar paquetes de símbolos nuevos.
keywords: Paquete de símbolos de la API de NuGet
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235107"
---
# <a name="push-symbol-packages"></a>Paquetes de símbolos de envío

Es posible insertar paquetes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mediante la API de NuGet V3.
Estas operaciones se basan en el recurso `SymbolPackagePublish` que se encuentra en el [Índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

Se usa `@type` el siguiente valor:

Valor de@type                 | Notas
--------------------        | -----
SymbolPackagePublish/4.9.0  | La versión inicial

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las siguientes API es el valor de `@id` la propiedad `SymbolPackagePublish/4.9.0` del recurso en el [Índice de servicio](service-index.md)del origen del paquete. En la documentación siguiente, se usa la dirección URL de Nuget. org. Considere `https://www.nuget.org/api/v2/symbolpackage` como un marcador de posición `@id` para el valor que se encuentra en el índice de servicio.

## <a name="http-methods"></a>Métodos HTTP

Este `PUT` recurso admite el método http. 

## <a name="push-a-symbol-package"></a>Inserte un paquete de símbolos

nuget.org admite la inserción del nuevo formato de paquetes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mediante la siguiente API. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Los paquetes de símbolos con el mismo identificador y versión se pueden enviar varias veces. Un paquete de símbolos se rechazará en los casos siguientes.
- No existe un paquete con el mismo identificador y versión.
- Se insertó un paquete de símbolos con el mismo identificador y versión, pero aún no se ha publicado.
- El paquete de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) no es válido (vea [restricciones de paquetes de símbolos](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parámetros de solicitud

NOMBRE           | En     | Type   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Encabezado | string | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

La clave de API es una cadena opaca procedente del origen del paquete por el usuario y configurada en el cliente. No se asigna ningún formato de cadena determinado, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores del encabezado HTTP.

### <a name="request-body"></a>Cuerpo de la solicitud

El cuerpo de la solicitud para la inserciones de símbolos es igual que con el cuerpo de la solicitud de una solicitud de envío de paquete (consulte la [Introducción y eliminación de paquetes](package-publish-resource.md)). 

### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
201         | El paquete de símbolos se insertó correctamente.
400         | El paquete de símbolos proporcionado no es válido.
401         | El usuario no está autorizado para realizar esta acción.
404         | No existe un paquete correspondiente con el identificador y la versión proporcionados.
409         | Se insertó un paquete de símbolos con el identificador y la versión proporcionados, pero aún no está disponible.
413         | El paquete es demasiado grande.

