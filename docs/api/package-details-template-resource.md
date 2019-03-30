---
title: Plantilla de dirección URL de los detalles de paquete, NuGet API
description: La plantilla de dirección URL de detalles de paquete permite a los clientes que se mostrará en su vínculo de un sitio web para obtener más detalles del paquete de interfaz de usuario
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638082"
---
# <a name="package-details-url-template"></a>Plantilla de dirección URL de los detalles de paquete

Es posible que un cliente generar una dirección URL que el usuario puede utilizar para ver más detalles de paquete en su explorador web. Esto es útil cuando un origen del paquete que desea mostrar información adicional sobre un paquete que no cabrá dentro del ámbito de lo que se muestra la aplicación de cliente de NuGet.

El recurso se usa para compilar esta dirección URL es la `PackageDetailsUriTemplate` encontrar el recurso en el [índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

La siguiente `@type` se usan los valores:

Valor de@type                      | Notas
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | La versión inicial

## <a name="url-template"></a>Plantilla de dirección URL

La dirección URL de la siguiente API es el valor de la `@id` propiedad asociada con uno de los recursos mencionados anteriormente `@type` valores.

## <a name="http-methods"></a>Métodos HTTP

Aunque el cliente no está diseñado para realizar solicitudes a la dirección URL de los detalles de paquete en nombre del usuario, la página web debe admitir la `GET` método para permitir que una dirección URL hace clic en él se puede abrir fácilmente en un explorador web.

## <a name="construct-the-url"></a>Construir la dirección URL

Dado un identificador de paquete conocidos y la versión, la implementación del cliente puede construir una dirección URL utilizada para tener acceso a una interfaz web. La implementación del cliente debería mostrar esta dirección URL construida (o vínculo interactivo) para el usuario lo que les permite abrir un explorador web a la dirección URL y para obtener más información sobre el paquete. El contenido de la página de detalles del paquete viene determinada por la implementación del servidor.

La dirección URL debe ser una dirección URL absoluta y el esquema (protocolo) debe ser HTTPS.

El valor de la `@id` en el servicio de índice es una cadena de dirección URL que contiene cualquiera de los tokens de marcador de posición siguientes:

### <a name="url-placeholders"></a>Marcadores de posición de dirección URL

Name        | Tipo    | Obligatorio | Notas
----------- | ------- | -------- | -----
`{id}`      | cadena  | No       | Para obtener detalles para el identificador del paquete
`{version}` | cadena  | No       | Para obtener los detalles de la versión del paquete

El servidor debe aceptar `{id}` y `{version}` valores con cualquier uso de mayúsculas y minúsculas. Además, el servidor no debe ser sensible a si es la versión [normalizado](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers). En otras palabras, el servidor debe aceptar también aceptan versiones no normalizado.

Por ejemplo, plantilla de detalles del paquete de nuget.org tiene este aspecto:

    https://www.nuget.org/packages/{id}/{version}

Si la implementación del cliente debe mostrar un vínculo a los detalles del paquete para NuGet.Versioning 4.3.0, se podría producir la siguiente dirección URL y proporcionar al usuario:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
