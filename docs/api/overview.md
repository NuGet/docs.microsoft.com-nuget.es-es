---
title: Información general de la API del servidor NuGet
description: La API del servidor de NuGet es un conjunto de puntos de conexión HTTP que se pueden usar para descargar paquetes, capturar metadatos, publicar paquetes nuevos, etc.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428292"
---
# <a name="nuget-server-api"></a>API del servidor de NuGet

La API de servidor de NuGet es un conjunto de puntos de conexión HTTP que se pueden usar para descargar paquetes, capturar metadatos, publicar paquetes nuevos y realizar la mayoría de las demás operaciones disponibles en los clientes de NuGet oficiales.

Esta API la usa el cliente de NuGet en Visual Studio, NuGet. exe y la CLI de .NET para realizar operaciones de NuGet como [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), buscar en la interfaz de usuario de Visual Studio y [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md).

Tenga en cuenta que, en algunos casos, nuget.org tiene requisitos adicionales que no exigen otros orígenes de paquetes. Estas diferencias se documentan mediante los [protocolos Nuget.org](nuget-protocols.md).

Para obtener una enumeración sencilla y descargar las versiones disponibles de Nuget. exe, consulte el punto de conexión [Tools. JSON](tools-json.md) .

## <a name="service-index"></a>Índice de servicio

El punto de entrada de la API es un documento JSON en una ubicación bien conocida. Este documento se denomina **Índice de servicio**. La ubicación del índice de servicio para nuget.org es `https://api.nuget.org/v3/index.json`.

Este documento JSON contiene una lista de *recursos* que proporcionan una funcionalidad diferente y cumplen diferentes casos de uso.

Los clientes que admiten la API deben aceptar una o varias de estas direcciones URL de índice de servicio como medio para conectarse a los orígenes de paquetes respectivos.

Para obtener más información sobre el índice de servicio, consulte [su referencia de API](service-index.md).

## <a name="versioning"></a>Control de versiones

La API es la versión 3 del protocolo HTTP de NuGet. Este protocolo se denomina a veces "API V3". Estos documentos de referencia hará referencia a esta versión del protocolo simplemente como "la API".

La versión del esquema de índice de servicio se indica mediante la propiedad `version` en el índice de servicio. La API asigna que la cadena de versión tiene un número de versión principal de `3`. A medida que se realizan cambios no importantes en el esquema de índice de servicio, se aumentará la versión secundaria de la cadena de versión.

Los clientes más antiguos (como Nuget. exe 2. x) no admiten la API V3 y solo admiten la API V2 anterior, que no se documenta aquí.

La API de NuGet V3 se denomina como tal porque es el sucesor de la API V2, que era el protocolo basado en OData implementado por la versión 2. x del cliente de NuGet oficial. La API V3 se admitía por primera vez en la versión 3,0 del cliente de NuGet oficial y sigue siendo la versión más reciente del protocolo compatible con el cliente de NuGet, 4,0 y on. 

Se han realizado cambios de Protocolo no problemáticos en la API desde que se lanzó por primera vez.

## <a name="resources-and-schema"></a>Recursos y esquema

El **Índice de servicio** describe una variedad de recursos. El conjunto actual de recursos admitidos es el siguiente:

Nombre del recurso                                                        | Obligatorio | Descripción
-------------------------------------------------------------------- | -------- | -----------
[Catálogo](catalog-resource.md)                                       | no       | Registro completo de todos los eventos de paquete.
[PackageBaseAddress](package-base-address-resource.md)               | sí      | Obtiene el contenido del paquete (. nupkg).
[PackageDetailsUriTemplate](package-details-template-resource.md)    | no       | Construya una dirección URL para tener acceso a una página web de detalles del paquete.
[PackagePublish](package-publish-resource.md)                        | sí      | Inserte y elimine (o desenumere) paquetes.
[RegistrationsBaseUrl](registration-base-url-resource.md)            | sí      | Obtiene los metadatos del paquete.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | no       | Construya una dirección URL para tener acceso a una página web notificar abuso.
[RepositorySignatures](repository-signatures-resource.md)            | no       | Obtiene los certificados que se usan para la firma del repositorio.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | no       | Detectar ID. de paquete y versiones por subcadena.
[SearchQueryService](search-query-service-resource.md)               | sí      | Filtre y busque paquetes por palabra clave.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | no       | Paquetes de símbolos de envío.

En general, todos los datos no binarios devueltos por un recurso de API se serializan mediante JSON. El esquema de respuesta que devuelve cada recurso en el índice de servicio se define individualmente para ese recurso. Para obtener más información acerca de cada recurso, consulte los temas enumerados anteriormente.

En el futuro, a medida que evolucione el protocolo, se pueden agregar nuevas propiedades a las respuestas JSON. Para que el cliente sea una prueba futura, la implementación no debe suponer que el esquema de respuesta es final y no puede incluir datos adicionales. Todas las propiedades que la implementación no entiende deben omitirse.

> [!Note]
> Cuando un origen no implementa `SearchAutocompleteService` se debe deshabilitar correctamente el comportamiento de autocompletar. Cuando `ReportAbuseUriTemplate` no está implementado, el cliente de NuGet oficial recurre a la dirección URL de la notificación de abuso de [NuGet/Home#4924](https://github.com/NuGet/Home/issues/4924)la organización. Otros clientes pueden optar por no mostrar simplemente la dirección URL de un informe de abuso para el usuario.

### <a name="undocumented-resources-on-nugetorg"></a>Recursos no documentados en nuget.org

El índice de servicio V3 de nuget.org tiene algunos recursos que no se han documentado anteriormente. Hay varias razones para no documentar un recurso.

En primer lugar, no documentamos los recursos usados como un detalle de implementación de nuget.org. El `SearchGalleryQueryService` entra en esta categoría. [NuGetGallery](https://github.com/NuGet/NuGetGallery) usa este recurso para delegar algunas consultas V2 (OData) en el índice de búsqueda en lugar de usar la base de datos. Este recurso se presentó por motivos de escalabilidad y no está pensado para uso externo.

En segundo lugar, no documentamos recursos que nunca se enviaron en una versión RTM del cliente oficial.
`PackageDisplayMetadataUriTemplate` y `PackageVersionDisplayMetadataUriTemplate` entran dentro de esta categoría.

En tercer lugar, no se documentan los recursos estrechamente acoplados con el protocolo v2, que a su vez no se documenta. El recurso `LegacyGallery` pertenece a esta categoría. Este recurso permite que un índice de servicio V3 señale a una dirección URL de origen de V2 correspondiente. Este recurso es compatible con el `nuget.exe list`.

Si un recurso no se documenta aquí, se recomienda *encarecidamente* que no tome una dependencia en ellos. Es posible que se quite o cambie el comportamiento de estos recursos no documentados, lo que podría interrumpir la implementación de maneras inesperadas.

## <a name="timestamps"></a>Marcas de tiempo

Todas las marcas de tiempo devueltas por la API son UTC o, de lo contrario, se especifican mediante la representación [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) . 

## <a name="http-methods"></a>Métodos HTTP

Verbo   | Uso
------ | -----------
GET    | Realiza una operación de solo lectura, que normalmente recupera datos.
HEAD   | Obtiene los encabezados de respuesta para la solicitud de `GET` correspondiente.
PUT    | Crea un recurso que no existe o, si existe, lo actualiza. Es posible que algunos recursos no admitan Update.
Delete | Elimina o elimina la lista de un recurso.

## <a name="http-status-codes"></a>Códigos de estado HTTP

Código | Descripción
---- | -----
200  | Success y hay un cuerpo de respuesta.
201  | Correcto y se creó el recurso.
202  | Correcto, se aceptó la solicitud, pero es posible que algún trabajo siga estando incompleto y completado de forma asincrónica.
204  | Correcto, pero no hay ningún cuerpo de respuesta.
301  | Una redirección permanente.
302  | Una redirección temporal.
400  | Los parámetros de la dirección URL o en el cuerpo de la solicitud no son válidos.
401  | Las credenciales proporcionadas no son válidas.
403  | La acción no se permite debido a las credenciales proporcionadas.
404  | El recurso solicitado no existe.
409  | La solicitud entra en conflicto con un recurso existente.
500  | El servicio ha encontrado un error inesperado.
503  | El servicio no está disponible temporalmente.

Cualquier solicitud de `GET` realizada a un punto de conexión de API puede devolver una redirección HTTP (301 o 302). Los clientes deben controlar correctamente estas redirecciones observando el encabezado de `Location` y emitiendo una `GET`posterior. La documentación relacionada con puntos de conexión específicos no llamará explícitamente a donde se pueden usar redirecciones.

En el caso de un código de estado de nivel 500, el cliente puede implementar un mecanismo de reintento razonable. El cliente de NuGet oficial vuelve a intentarlo tres veces cuando se encuentra un código de estado de nivel 500 o un error de TCP/DNS.

## <a name="http-request-headers"></a>Encabezados de solicitud HTTP

Nombre                     | Descripción
------------------------ | -----------
X-NuGet-ApiKey           | Necesario para la extracción y eliminación, vea [`PackagePublish` recurso](package-publish-resource.md)
X-NuGet-Client-Version   | En **desuso** y reemplazado por `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Requerido en ciertos casos solo en nuget.org, consulte [protocolos Nuget.org](NuGet-Protocols.md)
X-NuGet-Session-ID       | *Opcional*. Los clientes de NuGet v 4.7 + identifican las solicitudes HTTP que forman parte de la misma sesión de cliente de NuGet.

El `X-NuGet-Session-Id` tiene un único valor para todas las operaciones relacionadas con una única restauración en `PackageReference`. En otros escenarios, como Autocompletar y `packages.config` restore, puede haber varios IDENTIFICADOres de sesión diferentes debido a la forma en que se factoriza el código.

## <a name="authentication"></a>Authentication

La autenticación se deja hasta la implementación del origen del paquete que se va a definir. En el caso de nuget.org, solo el recurso `PackagePublish` requiere autenticación a través de un encabezado de clave de API especial. Consulte [`PackagePublish` recurso](package-publish-resource.md) para obtener más información.
