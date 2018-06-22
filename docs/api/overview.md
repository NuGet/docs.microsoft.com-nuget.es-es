---
title: Información general de la API de NuGet
description: La API de NuGet es un conjunto de extremos HTTP que puede usarse para descargar los paquetes, capturar metadatos, publicar nuevos paquetes, etcetera.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a638dba005c14bff4b2e668e2d6ca527a67b94a9
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820006"
---
# <a name="nuget-api"></a>API de NuGet

La API de NuGet es un conjunto de extremos HTTP que puede usarse para descargar los paquetes, capturar metadatos, publicar nuevos paquetes y realizar otras operaciones disponibles en los clientes de NuGet oficiales.

Esta API se usa por el cliente de NuGet en Visual Studio, nuget.exe y la CLI de .NET para realizar operaciones de NuGet como [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), búsqueda en la IU de Visual Studio, y [ `nuget.exe push` ](../tools/cli-ref-push.md).

Tenga en cuenta que en algunos casos, nuget.org tiene requisitos adicionales que no se aplican por otros orígenes de paquetes. Estas diferencias se documentan por la [nuget.org protocolos](nuget-protocols.md).

## <a name="service-index"></a>Índice de servicio

El punto de entrada para la API es un documento JSON en una ubicación conocida. Este documento se conoce el **índice servicio**. La ubicación del índice de servicio de nuget.org es `https://api.nuget.org/v3/index.json`.

Este documento JSON contiene una lista de *recursos* que proporcionan una funcionalidad diferente y atender distintos casos de uso.

Los clientes compatibles con la API deben aceptar una o varias de estas direcciones URL de índice de servicio como medio para conectarse a los orígenes del paquete correspondiente.

Para obtener más información acerca del índice de servicio, consulte [su referencia de la API](service-index.md).

## <a name="versioning"></a>Control de versiones

La API es la versión 3 del protocolo HTTP de NuGet. Este protocolo se conoce a veces como "la API V3." Estos documentos de referencia se hará referencia a esta versión del protocolo simplemente como "la API".

La versión del esquema de índice de servicio se indica mediante el `version` propiedad en el índice de servicio. La API requiere que la cadena de versión tiene un número de versión principal de `3`. Cuando se realizan cambios no importantes en el esquema de índice de servicio, se aumentará la versión secundaria de la cadena de versión.

Los clientes más antiguos (como nuget.exe 2.x) no admiten la API V3 y solo admiten la API V2 anterior, que no se documenta aquí.

La API V3 de NuGet se denomina así porque es el sucesor de la API V2, que era el protocolo basado en OData implementado por la versión 2.x del cliente NuGet oficial. La API V3 primero era compatible con la versión 3.0 del cliente NuGet oficial y es todavía la versión de protocolo principal más reciente compatible con el cliente de NuGet, 4.0 y en. 

Se realizaron cambios en los protocolos poco problemático a la API desde su primera versión.

## <a name="resources-and-schema"></a>Recursos y esquema

El **índice servicio** describe una variedad de recursos. El conjunto actual de los recursos admitidos son los siguientes:

Nombre del recurso                                                          | Obligatorio | Descripción
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | sí      | Insertar y eliminar (u ocultar) paquetes.
[`SearchQueryService`](search-query-service-resource.md)               | sí      | Filtrar y buscar paquetes por palabra clave.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | sí      | Obtener metadatos de paquete.
[`PackageBaseAddress`](package-base-address-resource.md)               | sí      | Obtener el contenido del paquete (.nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | No       | Detectar el Id. de paquete y las versiones, subcadena.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | No       | Construir una dirección URL para tener acceso a una página web de "notificar un abuso".
[`Catalog`](catalog-resource.md)                                       | No       | Registro completo de todos los eventos de paquete.

En general, todos los datos no binarios devueltos por un recurso de la API se serializan mediante JSON. El esquema de respuesta devuelto por cada recurso en el índice de servicio se define individualmente para ese recurso. Para obtener más información acerca de cada recurso, vea los temas enumerados anteriormente.

> [!Note]
> Cuando un origen no implementa `SearchAutocompleteService` correctamente se debe deshabilitar cualquier comportamiento de Autocompletar. Cuando `ReportAbuseUriTemplate` no está implementada, dirección URL de abuso del informe de la recurren oficial de cliente de NuGet a de nuget.org (sometidos a seguimiento por [NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924)). Pueden optar por otros clientes para simplemente no mostrar una dirección URL de abuso de informes para el usuario.

## <a name="timestamps"></a>Marcas de tiempo

Todas las marcas de tiempo devueltos por la API son del tipo UTC o en caso contrario, se especifican utilizando [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) representación. 

## <a name="http-methods"></a>Métodos HTTP

Verbo   | Usar
------ | -----------
GET    | Realiza una operación de sólo lectura, normalmente recuperar datos.
HEAD   | Obtiene los encabezados de respuesta correspondiente `GET` solicitud.
PUT    | Crea un recurso que no existe o, si existe, se actualiza. Algunos recursos pueden no admitir la actualización.
SUPRIMIR | Elimina o unlists un recurso.

## <a name="http-status-codes"></a>Códigos de estado HTTP

Código | Descripción
---- | -----
200  | Se ejecuta correctamente, y no hay un cuerpo de respuesta.
201  | Se creó correctamente y el recurso.
202  | Se ejecuta correctamente, la solicitud se ha aceptado pero algún trabajo aún estén incompletos y completados asincrónicamente.
204  | Se ejecuta correctamente, pero no hay ningún cuerpo de respuesta.
301  | Una redirección permanente.
302  | Una redirección temporal.
400  | Los parámetros en la dirección URL o en el cuerpo de solicitud no son válidos.
401  | Las credenciales proporcionadas no son válidas.
403  | No se permite la acción dadas las credenciales proporcionadas.
404  | El recurso solicitado no existe.
409  | La solicitud está en conflicto con un recurso existente.
500  | El servicio ha encontrado un error inesperado.
503  | El servicio no está disponible temporalmente.

Cualquier `GET` solicitud realizada a un extremo de API puede devolver una redirección HTTP (301 o 302). Los clientes deben controlar correctamente estas redirecciones observando el `Location` encabezado y emitiendo una posterior `GET`. Documentación relativa a extremos específicos no se llamar explícitamente a los que pueden utilizarse redirecciones.

En el caso de un código de estado de nivel de 500, el cliente puede implementar un mecanismo de reintento razonable. El oficial NuGet cliente reintenta tres veces al encontrar cualquier código de estado del nivel 500 o error TCP/DNS.

## <a name="http-request-headers"></a>Encabezados de solicitud HTTP

nombre                     | Descripción
------------------------ | -----------
X-NuGet-ApiKey           | Necesario para la inserción y eliminación, consulte [ `PackagePublish` recursos](package-publish-resource.md)
X-NuGet-versión de cliente   | **En desuso** y reemplazado por `X-NuGet-Protocol-Version`
Protocolo versión X-NuGet | Requerido en determinados casos solo en nuget.org, vea [nuget.org protocolos](NuGet-Protocols.md)
X-NuGet-identificador de sesión       | *Opcional*. NuGet clientes v4.7 + identificar las solicitudes HTTP que forman parte de la misma sesión de cliente de NuGet. Para `PackageReference` hay operaciones de restauración es un identificador de sesión único, para otros escenarios como Autocompletar, y `packages.config` restauración puede haber varias diferentes Id. de sesión debido a cómo se divide el código.

## <a name="authentication"></a>Autenticación

La autenticación se deja a la implementación de origen del paquete para definir. Para nuget.org, solo el `PackagePublish` recurso requiere la autenticación a través de un encabezado especial de clave de API. Vea [ `PackagePublish` recursos](package-publish-resource.md) para obtener más información.
