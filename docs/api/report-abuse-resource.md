---
title: Plantilla de dirección URL de informe abuso, API de NuGet
description: La plantilla de dirección URL de abuso de informes permite a los clientes mostrar un vínculo de abuso de informe en su interfaz de usuario.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549344"
---
# <a name="report-abuse-url-template"></a>Plantilla de dirección URL de abuso de informe

Es posible que un cliente generar una dirección URL que se puede usar por el usuario para notificar un abuso sobre un paquete específico. Esto es útil cuando un origen del paquete que desea habilitar todas las experiencias de cliente (incluso 3ª parte) delegar el abuso de informes para el origen del paquete.

El recurso se usa para compilar esta dirección URL es la `ReportAbuseUriTemplate` encontrar el recurso en el [índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

La siguiente `@type` se usan los valores:

Valor de @type                       | Notas
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | La versión inicial
ReportAbuseUriTemplate/3.0.0-rc   | Alias de `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Plantilla de dirección URL

La dirección URL de la siguiente API es el valor de la `@id` propiedad asociada con uno de los recursos mencionados anteriormente `@type` valores.

## <a name="http-methods"></a>Métodos HTTP

Aunque el cliente no está diseñado para realizar solicitudes a la dirección URL de abuso de informes en nombre del usuario, la página web debe admitir la `GET` método para permitir que una dirección URL hace clic en él se puede abrir fácilmente en un explorador web.

## <a name="construct-the-url"></a>Construir la dirección URL

Dado un identificador de paquete conocidos y la versión, la implementación del cliente puede construir una dirección URL utilizada para tener acceso a una interfaz web. La implementación del cliente debería mostrar esta dirección URL construida (o vínculo interactivo) para el usuario lo que les permite abrir un explorador web a la dirección URL y realizar cualquier informe abuso necesarios. La implementación del formulario de informe de abuso viene determinada por la implementación del servidor.

El valor de la `@id` es una cadena de dirección URL que contiene cualquiera de los tokens de marcador de posición siguientes:

### <a name="url-placeholders"></a>Marcadores de posición de dirección URL

nombre        | Tipo    | Obligatorio | Notas
----------- | ------- | -------- | -----
`{id}`      | cadena  | No       | El identificador del paquete para notificar abuso para
`{version}` | cadena  | No       | Para notificar un abuso de la versión del paquete

El `{id}` y `{version}` valores interpretados la implementación del servidor deben ser entre mayúsculas y minúsculas y no sensibles a si se normaliza la versión.

Por ejemplo, plantilla de abuso de informe de nuget.org tiene este aspecto:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Si la implementación del cliente debe mostrar un vínculo a la forma de abuso de informe para NuGet.Versioning 4.3.0, se podría producir la siguiente dirección URL y proporcionar al usuario:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
