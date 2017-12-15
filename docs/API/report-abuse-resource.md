---
title: "Plantilla de dirección URL de abuso, NuGet API de informes | Documentos de Microsoft"
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
ms.assetid: 148d743a-09e5-4539-8454-675be11902db
description: "La plantilla de dirección URL de abuso de informes permite a los clientes mostrar un vínculo de abuso del informe en su interfaz de usuario."
keywords: "Informar de abuso de API de NuGet, queja de archivo de API de NuGet, plantilla de dirección URL de informe NuGet.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7b3413297f5a7fcf0e2c7757036b1f240ed0058a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="report-abuse-url-template"></a>Plantilla de dirección URL de informe abuso

Es posible que un cliente generar una dirección URL que puede usarse por el usuario para notificar un abuso sobre un paquete específico. Esto es útil cuando desea que un origen de paquete habilitar todas las experiencias de cliente (incluso 3ª parte) delegar abuso informes al origen del paquete.

El recurso que se utiliza para capturar el contenido del paquete es el `ReportAbuseUriTemplate` recurso se encuentra en la [índice servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

Los siguientes `@type` se usan valores:

Valor de @type                       | Notas
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | La versión inicial
ReportAbuseUriTemplate/3.0.0-rc   | Alias de`ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Plantilla de dirección URL

La dirección URL de la siguiente API es el valor de la `@id` propiedad asociado a uno de los recursos mencionados anteriormente `@type` valores.

## <a name="http-methods"></a>Métodos HTTP

Aunque el cliente no está diseñado para realizar solicitudes a la dirección URL de abuso de informes en nombre del usuario, la página web debe admitir la `GET` método para permitir una dirección URL hace clic en abrir fácilmente en un explorador web.

## <a name="construct-the-url"></a>Construir la dirección URL

Dado un identificador de paquete conocidos y la versión, la implementación del cliente puede construir una dirección URL utilizada para tener acceso a una interfaz web. La implementación del cliente debería mostrar esta dirección URL construida (o hacer clic en ella) para el usuario que les permite abra un explorador web para la dirección URL y realice cualquier informe de abuso necesarios. La implementación del formulario de informe de abuso se determina mediante la implementación del servidor.

El valor de la `@id` es una cadena de dirección URL que contengan cualquiera de los tokens de marcador de posición siguientes:

### <a name="url-placeholders"></a>Marcadores de posición de la dirección URL

Name        | Tipo    | Obligatorio | Notas
----------- | ------- | -------- | -----
`{id}`      | string  | No       | El identificador del paquete para notificar un abuso para
`{version}` | string  | No       | La versión del paquete para notificar un abuso para

El `{id}` y `{version}` valores interpretados la implementación de servidor deben ser sin distinción de mayúsculas y no sensibles a si se normaliza la versión.

Por ejemplo, plantilla de abuso de nuget.org informe tiene un aspecto similar al siguiente:

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

Si la implementación del cliente debe mostrar un vínculo a la forma de controlar el abuso de informe para NuGet.Versioning 4.3.0, se podría producir la siguiente dirección URL y proporcionar al usuario:

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```