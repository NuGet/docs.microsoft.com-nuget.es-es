---
title: Plantilla de URL de notificación de abuso, API de NuGet
description: La plantilla notificar dirección URL de abuso permite a los clientes mostrar un vínculo notificar abuso en la interfaz de usuario.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775231"
---
# <a name="report-abuse-url-template"></a>Plantilla de URL de notificación de abuso

Un cliente puede crear una dirección URL que el usuario pueda usar para notificar el abuso de un paquete específico. Esto resulta útil cuando un origen de paquete desea habilitar todas las experiencias de cliente (incluso terceros) para delegar informes de abuso en el origen del paquete.

El recurso que se usa para generar esta dirección URL es el `ReportAbuseUriTemplate` recurso que se encuentra en el [Índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

`@type`Se usan los siguientes valores:

Valor de @type                       | Notas
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | La versión inicial
ReportAbuseUriTemplate/3.0.0-RC   | Alias de `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL template

La dirección URL de la siguiente API es el valor de la `@id` propiedad asociada a uno de los valores de recursos mencionados anteriormente `@type` .

## <a name="http-methods"></a>Métodos HTTP

Aunque el cliente no está diseñado para realizar solicitudes a la dirección URL del informe de abuso en nombre del usuario, la página web debe admitir el `GET` método para permitir que se pueda abrir fácilmente una dirección URL en un explorador Web.

## <a name="construct-the-url"></a>Construir la dirección URL

Dado un identificador de paquete conocido y una versión, la implementación del cliente puede construir una dirección URL que se usa para tener acceso a una interfaz Web. La implementación del cliente debe mostrar esta dirección URL construida (o vínculo en el que se pueda hacer clic) al usuario, lo que le permite abrir un explorador Web en la dirección URL y hacer cualquier informe de abuso necesario. La implementación del formulario de informe de abuso viene determinada por la implementación del servidor.

El valor de `@id` es una cadena de dirección URL que contiene cualquiera de los siguientes tokens de marcador de posición:

### <a name="url-placeholders"></a>Marcadores de posición de dirección URL

Nombre        | Tipo    | Obligatorio | Notas
----------- | ------- | -------- | -----
`{id}`      | string  | no       | IDENTIFICADOR del paquete del que se va a notificar abuso
`{version}` | string  | no       | La versión del paquete para notificar abuso

Los `{id}` `{version}` valores y interpretados por la implementación del servidor deben distinguir entre mayúsculas y minúsculas y no distinguir si la versión está normalizada.

Por ejemplo, la plantilla de abuso de informes de Nuget. org tiene el siguiente aspecto:

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

Si la implementación del cliente necesita mostrar un vínculo al formulario de abuso de informes para NuGet. control de versiones 4.3.0, generaría la siguiente dirección URL y la proporcionará al usuario:

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
