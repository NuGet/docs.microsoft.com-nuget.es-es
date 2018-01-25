---
title: Metadatos, NuGet API del paquete | Documentos de Microsoft
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
description: La URL base del registro de paquete permite capturar metadatos acerca de los paquetes.
keywords: Metadatos de paquete de NuGet API, registro de la API de NuGet, API de NuGet que no figuran en paquetes
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c098d70d58011bad7f9829f0c95c87c1339dd362
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="package-metadata"></a>Metadatos de paquete

Es posible capturar metadatos acerca de los paquetes disponibles en un origen de paquete mediante la API V3 de NuGet. Estos metadatos se pueden recuperar mediante el `RegistrationsBaseUrl` recurso se encuentra en la [índice servicio](service-index.md).

La colección de los documentos que se encuentran en `RegistrationsBaseUrl` a menudo se denominan "registros" o "blobs de registro". El conjunto de documentos en una sola `RegistrationsBaseUrl` se conoce como un "subárbol de registro". Un subárbol del registro contiene todos los metadatos acerca de cada paquete disponible en un origen del paquete.

## <a name="versioning"></a>Control de versiones

Los siguientes `@type` se usan valores:

Valor de @type                     | Notas
------------------------------- | -----
RegistrationsBaseUrl            | La versión inicial
RegistrationsBaseUrl/3.0.0-beta | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Respuestas de comprimido con gzip
RegistrationsBaseUrl/3.6.0      | Incluye paquetes de SemVer 2.0.0

Esto representa tres subárboles de registro distintos disponibles para las distintas versiones de cliente.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Estos registros no se comprimen (lo que significa que usan un implícita `Content-Encoding: identity`). Paquetes de SemVer 2.0.0 están **excluir** de esta sección.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Estos registros se comprimen mediante `Content-Encoding: gzip`. Paquetes de SemVer 2.0.0 están **excluir** de esta sección.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Estos registros se comprimen mediante `Content-Encoding: gzip`. Paquetes de SemVer 2.0.0 están **incluye** en esta sección.
Para obtener más información sobre SemVer 2.0.0, consulte [SemVer 2.0.0 compatibilidad con nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las API siguientes es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valores. En el siguiente documento, el marcador de posición de la dirección URL base `{@id}` se usará.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL se encuentra en el soporte de registro del recurso los métodos HTTP `GET` y `HEAD`.

## <a name="registration-index"></a>Índice de registro

Los grupos de recursos de registro del paquete metadatos por el identificador del paquete. No es posible obtener datos sobre más de un identificador de paquete a la vez. Este recurso no proporciona ninguna manera de detectar el Id. de paquete. En su lugar, se supone que el cliente ya conoce el identificador del paquete deseado. Metadatos disponibles acerca de cada versión del paquete varían según la implementación del servidor. Los blobs de registro del paquete tienen la siguiente estructura jerárquica:

- **Índice**: el punto de entrada para los metadatos de paquete, compartido por todos los paquetes en un origen con el mismo identificador de paquete.
- **Página**: una agrupación de versiones del paquete. El número de versiones del paquete en una página se define mediante la implementación del servidor.
- **Hoja**: un documento específico para una versión de paquete único.

La dirección URL del índice de registro sea predecible y se puede determinar mediante el cliente tiene un identificador de paquete y el recurso de registro `@id` valor desde el índice de servicio. Las direcciones URL de las páginas de registro y las hojas se detectan mediante la inspección del índice de registro.

### <a name="registration-pages-and-leaves"></a>Hojas y páginas de registro

Aunque no sea estrictamente necesario para que una implementación del servidor almacenar registro hojas en documentos de la página de registro independientes, es una práctica recomendada para ahorrar memoria del lado cliente. En lugar de alineando todos deja de registro en el índice o el almacenamiento inmediatamente deja en documentos de página, se recomienda que la implementación del servidor define algunos aspectos heurísticos para elegir entre los dos enfoques en función del número de versiones del paquete o deja el tamaño acumulado de paquete.

Almacenar todas las versiones de paquete (hojas) la guarda de índice de registro en el número de solicitudes HTTP que es necesario para los metadatos de paquete de captura, pero significa que se debe descargar un documento de mayor tamaño y se debe asignar más memoria de cliente. Por otro lado, si la implementación del servidor almacena inmediatamente deja de registro en documentos de página independiente, el cliente debe realizar más solicitudes HTTP para obtener la información que necesita.

La heurística que usa nuget.org es la siguiente: si hay 128 o más versiones de un paquete, dividir las hojas en páginas de tamaño de 64. Si hay menos de 128 versiones, en línea todos los deja en el índice de registro.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parámetros de solicitud

nombre     | En     | Tipo    | Obligatorio | Notas
-------- | ------ | ------- | -------- | -----
LOWER_ID | Dirección URL    | cadena  | sí      | El identificador del paquete, en minúsculas

El `LOWER_ID` valor es el identificador de paquete deseado en minúsculas utilizando las reglas implementadas por. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

### <a name="response"></a>Respuesta

La respuesta es un documento JSON que tiene un objeto raíz con las siguientes propiedades:

nombre  | Tipo             | Obligatorio | Notas
----- | ---------------- | -------- | -----
count | enteros          | sí      | El número de páginas de registro en el índice
items | Matriz de objetos | sí      | La matriz de páginas de registro

Cada elemento en el objeto index `items` matriz es un objeto JSON que representa una página de registro.

#### <a name="registration-page-object"></a>Objeto de página de registro

El objeto de página de registro se encuentra en el índice de registro tiene las siguientes propiedades:

nombre   | Tipo             | Obligatorio | Notas
------ | ---------------- | -------- | -----
@id    | cadena           | sí      | La dirección URL a la página de registro
count  | enteros          | sí      | El número de registro se deja en la página
items  | Matriz de objetos | No       | La matriz de hojas de registro y sus metadatos asociados
Inferior  | cadena           | sí      | La versión más antigua de SemVer 2.0.0 en la página (inclusive)
parent | cadena           | No       | La dirección URL para el índice de registro
superior  | cadena           | sí      | La versión de SemVer 2.0.0 más alta en la página (inclusive)

El `lower` y `upper` límites del objeto de página son útiles cuando es necesario los metadatos para una versión de la página específica.
Estos límites se pueden utilizar para capturar la página de registro solo sea necesitada. Las cadenas de versión adhieren a [reglas de la versión de NuGet](../reference/package-versioning.md). Las cadenas de versión se normalizan y no incluyen los metadatos de compilación. Como con todas las versiones en el ecosistema de NuGet, comparación de cadenas de versión se implementa mediante [las reglas de prioridad de versión SemVer 2.0.0's](http://semver.org/spec/v2.0.0.html#spec-item-11).

El `parent` propiedad solo aparecerá si el objeto de página de registro tiene el `items` propiedad.

Si el `items` propiedad no está presente en el objeto de página de registro, la dirección URL especificada en el `@id` debe usarse para capturar los metadatos acerca de las versiones de paquete individual. El `items` matriz a veces se excluye del objeto de página como una optimización. Si el número de versiones de un identificador de paquete único es muy grande, el documento de índice de registro será masivos e innecesarios al proceso para un cliente que solo se preocupa por una versión específica o un pequeño intervalo de versiones.

Tenga en cuenta que si el `items` propiedad está presente, el `@id` propiedad no es necesario usar, ya que todos los datos de la página ya está integrada en el `items` propiedad.

Cada elemento en el objeto de página `items` matriz es un objeto JSON que representa una hoja de registro y tiene metadatos asociados.

#### <a name="registration-leaf-object-in-a-page"></a>Objeto de hoja de registro en una página

El objeto de hoja de registro que se encuentren en una página de registro tiene las siguientes propiedades:

nombre           | Tipo   | Obligatorio | Notas
-------------- | ------ | -------- | -----
@id            | cadena | sí      | La dirección URL de la hoja de registro
catalogEntry   | objeto | sí      | La entrada del catálogo que contiene los metadatos de paquete
packageContent | cadena | sí      | La dirección URL para el contenido del paquete (.nupkg)

Cada objeto de hoja de registro representa los datos asociados a un único paquete.

#### <a name="catalog-entry"></a>Entrada de catálogo

El `catalogEntry` propiedad del objeto de hoja de registro tiene las siguientes propiedades:

nombre                     | Tipo                       | Obligatorio | Notas
------------------------ | -------------------------- | -------- | -----
@id                      | cadena                     | sí      | La dirección URL para el documento que se utiliza para generar este objeto
authors                  | cadena o matriz de cadenas | No       | 
dependencyGroups         | Matriz de objetos           | No       | La dirección URL para el contenido del paquete (.nupkg)
Descripción              | cadena                     | No       | 
iconUrl                  | cadena                     | No       | 
id                       | cadena                     | sí      | El identificador del paquete
licenseUrl               | cadena                     | No       | 
lista                   | booleano                    | No       | Se debe considerar que la lista si está ausente
minClientVersion         | cadena                     | No       | 
projectUrl               | cadena                     | No       | 
Publicado                | cadena                     | No       | Una cadena que contiene una marca de hora ISO 8601 de cuándo se publicó el paquete
requireLicenseAcceptance | booleano                    | No       | 
resumen                  | cadena                     | No       | 
etiquetas                     | cadena o matriz de cadena  | No       | 
título                    | cadena                     | No       | 
version                  | cadena                     | sí      | La versión del paquete

El `dependencyGroups` propiedad es una matriz de objetos que representan las dependencias del paquete, agrupados por .NET framework de destino. Si el paquete no tiene dependencias, el `dependencyGroups` falta propiedad, una matriz vacía, o la `dependencies` propiedad de todos los grupos falta o está vacío.

#### <a name="package-dependency-group"></a>Grupo de dependencia del paquete

Cada objeto de grupo de dependencia tiene las siguientes propiedades:

nombre            | Tipo             | Obligatorio | Notas
--------------- | ---------------- | -------- | -----
targetFramework | cadena           | No       | La plataforma de destino que se aplican a estas dependencias
dependencias    | Matriz de objetos | No       |

El `targetFramework` cadena usa el formato implementado por la biblioteca de .NET de NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Si no hay ningún `targetFramework` se especifica, el grupo de dependencia se aplica a todos los marcos de destino.

El `dependencies` propiedad es una matriz de objetos, que representa una dependencia del paquete del paquete actual.

#### <a name="package-dependency"></a>Dependencia del paquete

Cada dependencia del paquete tiene las siguientes propiedades:

nombre         | Tipo   | Obligatorio | Notas
------------ | ------ | -------- | -----
id           | cadena | sí      | El identificador de la dependencia del paquete
range        | objeto | No       | Permitido [intervalo de versiones](../reference/package-versioning.md#version-ranges-and-wildcards) de la dependencia
registro | cadena | No       | La dirección URL para el índice de registro de esta dependencia

Si el `range` propiedad se excluye o una cadena vacía, el cliente, de forma predeterminada el intervalo de versiones `(, )`. Es decir, se permite cualquier versión de la dependencia.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

En este caso concreto, el índice de registro tiene la página de registro insertada por lo que no se necesita ninguna solicitud adicional para capturar los metadatos acerca de las versiones de paquete individual.

## <a name="registration-page"></a>Página de registro

La página de registro contiene hojas de registro. La dirección URL para capturar una página de registro viene determinada por la `@id` propiedad en el [objeto de página de registro](#registration-page-object) mencionadas anteriormente.

Cuando el `items` matriz no se proporciona en el índice de registro, solicitar un HTTP GET de la `@id` valor devolverá un documento JSON que tiene un objeto raíz. El objeto tiene las siguientes propiedades:

nombre   | Tipo             | Obligatorio | Notas
------ | ---------------- | -------- | -----
@id    | cadena           | sí      | La dirección URL a la página de registro
count  | enteros          | sí      | El número de registro se deja en la página
items  | Matriz de objetos | sí      | La matriz de hojas de registro y sus metadatos asociados
Inferior  | cadena           | sí      | La versión más antigua de SemVer 2.0.0 en la página (inclusive)
parent | cadena           | sí      | La dirección URL para el índice de registro
superior  | cadena           | sí      | La versión de SemVer 2.0.0 más alta en la página (inclusive)

La forma de los objetos de la hoja de registro es el mismo que el índice de registro [anteriormente](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Hoja de registro

La hoja de registro contiene información sobre un identificador de paquete específico y la versión. Los metadatos acerca de la versión específica no estén disponibles en este documento. Se deben recuperar los metadatos de paquete de la [índice de registro](#registration-index) o [página de registro](#registration-page) (que se detecta mediante el índice de registro).

La dirección URL para capturar una hoja de registro se obtiene de la `@id` propiedad de un objeto de hoja de registro en un índice de registro o una página de registro.

La hoja de registro es un documento JSON con un objeto raíz con las siguientes propiedades:

nombre           | Tipo    | Obligatorio | Notas
-------------- | ------- | -------- | -----
@id            | cadena  | sí      | La dirección URL de la hoja de registro
catalogEntry   | cadena  | No       | La dirección URL a la entrada de catálogo que genera estos hoja
lista         | booleano | No       | Se debe considerar que la lista si está ausente
packageContent | cadena  | No       | La dirección URL para el contenido del paquete (.nupkg)
Publicado      | cadena  | No       | Una cadena que contiene una marca de hora ISO 8601 de cuándo se publicó el paquete
registro   | cadena  | No       | La dirección URL para el índice de registro

> [!Note]
> En nuget.org, el `published` valor se establece en año 1900 cuando es que no figuran en el paquete.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
