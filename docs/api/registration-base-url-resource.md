---
title: Metadatos de paquete, API de NuGet
description: La dirección URL base de registro de paquetes permite capturar metadatos sobre los paquetes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1a2e98ab36c8dc08e5f14b19b57f5ea0d790524c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488313"
---
# <a name="package-metadata"></a>Metadatos de paquete

Es posible capturar metadatos acerca de los paquetes disponibles en un origen de paquete mediante la API de NuGet V3. Estos metadatos se pueden capturar mediante el `RegistrationsBaseUrl` recurso que se encuentra en el [Índice de servicio](service-index.md).

La colección de los documentos que se `RegistrationsBaseUrl` encuentran en se denomina a menudo "registros" o "blobs de registro". El conjunto de documentos en un solo `RegistrationsBaseUrl` se conoce como "registro de subárbol". Un subárbol de registro contiene todos los metadatos de todos los paquetes disponibles en el origen de un paquete.

## <a name="versioning"></a>Control de versiones

Se usan `@type` los siguientes valores:

Valor de@type                     | Notas
------------------------------- | -----
RegistrationsBaseUrl            | La versión inicial
RegistrationsBaseUrl/3.0.0-beta | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Respuestas de gzip
RegistrationsBaseUrl/3.6.0      | Incluye paquetes SemVer 2.0.0

Esto representa tres subárboles de registro distintos disponibles para varias versiones de cliente.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Estos registros no se comprimen (lo que significa que `Content-Encoding: identity`usan un implícito). Los paquetes de SemVer 2.0.0 se excluyen de este subárbol.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Estos registros se comprimen `Content-Encoding: gzip`mediante. Los paquetes de SemVer 2.0.0 se excluyen de este subárbol.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Estos registros se comprimen `Content-Encoding: gzip`mediante. Los paquetes de SemVer 2.0.0 se **incluyen** en este subárbol.
Para obtener más información acerca de SemVer 2.0.0, consulte [SemVer 2.0.0 Support for Nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las siguientes API es el valor de `@id` la propiedad asociada a los valores `@type` de recursos mencionados anteriormente. En el siguiente documento, se usará la dirección `{@id}` URL base del marcador de posición.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL encontradas en el recurso de registro admiten `HEAD`los métodos `GET` http y.

## <a name="registration-index"></a>Índice de registro

El recurso de registro agrupa los metadatos del paquete por identificador de paquete. No es posible obtener datos sobre más de un identificador de paquete a la vez. Este recurso no proporciona ninguna manera de detectar los identificadores de paquete. En su lugar, se supone que el cliente ya conoce el identificador de paquete deseado. Los metadatos disponibles sobre cada versión del paquete varían según la implementación del servidor. Los blobs de registro del paquete tienen la siguiente estructura jerárquica:

- **Índice**: el punto de entrada de los metadatos del paquete, compartido por todos los paquetes en un origen con el mismo identificador de paquete.
- **Página**: una agrupación de versiones de paquete. El número de versiones de paquete en una página se define mediante la implementación de servidor.
- **Hoja**: documento específico de una versión de paquete única.

La dirección URL del índice de registro es predecible y la puede determinar el cliente dado un identificador de paquete y el valor del `@id` recurso de registro del índice de servicio. Las direcciones URL de las páginas de registro y las hojas se detectan examinando el índice de registro.

### <a name="registration-pages-and-leaves"></a>Páginas y hojas de registro

Aunque no es estrictamente necesario para que una implementación de servidor almacene hojas de registro en documentos de páginas de registro independientes, se recomienda conservar la memoria del lado cliente. En lugar de insertar todo el registro en el índice o almacenar de inmediato hojas en documentos de página, se recomienda que la implementación del servidor defina alguna heurística para elegir entre los dos enfoques en función del número de versiones del paquete o tamaño acumulado del paquete.

El almacenamiento de todas las versiones del paquete (hojas) en el índice de registro se guarda en el número de solicitudes HTTP necesarias para capturar los metadatos del paquete, pero significa que se debe descargar un documento más grande y se debe asignar más memoria del cliente. Por otro lado, si la implementación del servidor almacena inmediatamente las hojas de registro en documentos de página independientes, el cliente debe realizar más solicitudes HTTP para obtener la información que necesita.

La heurística que usa nuget.org es la siguiente: si hay 128 o más versiones de un paquete, divida las hojas en páginas de tamaño 64. Si hay menos de 128 versiones, inserta todas las hojas en el índice de registro.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parámetros de solicitud

NOMBRE     | En     | Type    | Obligatorio | Notas
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | sí      | El identificador del paquete, en minúsculas

El `LOWER_ID` valor es el identificador de paquete deseado en minúsculas mediante las reglas implementadas por. Método de [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) la red.

### <a name="response"></a>Respuesta

La respuesta es un documento JSON que tiene un objeto raíz con las siguientes propiedades:

NOMBRE  | Type             | Obligatorio | Notas
----- | ---------------- | -------- | -----
count | integer          | sí      | El número de páginas de registro del índice
items | matriz de objetos | sí      | La matriz de páginas de registro

Cada elemento de la matriz del `items` objeto index es un objeto JSON que representa una página de registro.

#### <a name="registration-page-object"></a>Objeto de página de registro

El objeto de página de registro que se encuentra en el índice de registro tiene las siguientes propiedades:

NOMBRE   | Type             | Obligatorio | Notas
------ | ---------------- | -------- | -----
@id    | string           | sí      | La dirección URL de la página de registro
count  | integer          | sí      | El número de hojas de registro en la página
items  | matriz de objetos | No       | La matriz de las hojas de registro y sus metadatos asociados
inferiores  | string           | sí      | La versión más baja de SemVer 2.0.0 en la página (inclusivo)
parent | string           | No       | Dirección URL del índice de registro.
esquina superior  | string           | sí      | La versión más alta de SemVer 2.0.0 en la página (inclusiva)

Los `lower` límites `upper` y del objeto Page son útiles cuando se necesitan los metadatos de una versión de página concreta.
Estos límites se pueden usar para capturar la única página de registro necesaria. Las cadenas de versión se adhieren a [las reglas de versión de NuGet](../concepts/package-versioning.md). Las cadenas de versión se normalizan y no incluyen los metadatos de la compilación. Como con todas las versiones del ecosistema de NuGet, la comparación de las cadenas de versión se implementa con [las reglas de prioridad de la versión de SemVer 2.0.0](http://semver.org/spec/v2.0.0.html#spec-item-11).

La `parent` propiedad solo aparecerá si el objeto de la página de registro `items` tiene la propiedad.

Si la `items` propiedad no está presente en el objeto de la página de registro, la dirección `@id` URL especificada en debe usarse para capturar metadatos sobre versiones de paquetes individuales. A `items` veces, la matriz se excluye del objeto de página como una optimización. Si el número de versiones de un único identificador de paquete es muy grande, el documento de índice de registro será masivo y impedirá el procesamiento de un cliente que solo se ocupa de una versión específica o de una pequeña gama de versiones.

Tenga en cuenta que `items` si la propiedad está presente `@id` , no es necesario usar la propiedad, ya que todos los datos de la página ya están insertados en la `items` propiedad.

Cada elemento de la matriz del `items` objeto de página es un objeto JSON que representa una hoja de registro y sus metadatos asociados.

#### <a name="registration-leaf-object-in-a-page"></a>Objeto hoja de registro en una página

El objeto hoja de registro que se encuentra en una página de registro tiene las siguientes propiedades:

NOMBRE           | Type   | Obligatorio | Notas
-------------- | ------ | -------- | -----
@id            | string | sí      | La dirección URL de la hoja de registro
catalogEntry   | objeto | sí      | Entrada del catálogo que contiene los metadatos del paquete
packageContent | string | sí      | La dirección URL del contenido del paquete (. nupkg)

Cada objeto hoja de registro representa los datos asociados a una única versión de paquete.

#### <a name="catalog-entry"></a>Entrada del catálogo

La `catalogEntry` propiedad del objeto hoja de registro tiene las siguientes propiedades:

NOMBRE                     | Type                       | Obligatorio | Notas
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | sí      | Dirección URL del documento que se usa para generar este objeto.
authors                  | cadena o matriz de cadenas | No       | 
dependencyGroups         | matriz de objetos           | No       | Las dependencias del paquete, agrupadas por la plataforma de destino
desuso              | objeto                     | No       | El desuso asociado al paquete
description              | string                     | No       | 
iconUrl                  | string                     | No       | 
id                       | string                     | sí      | Identificador del paquete.
licenseUrl               | string                     | No       |
licenseExpression        | string                     | No       | 
lista                   | boolean                    | No       | Se debe considerar como si no estuviera presente
minClientVersion         | string                     | No       | 
projectUrl               | string                     | No       | 
sin                | string                     | No       | Una cadena que contiene una marca de tiempo ISO 8601 de Cuándo se publicó el paquete
requireLicenseAcceptance | boolean                    | No       | 
resumen                  | string                     | No       | 
tags                     | cadena o matriz de cadena  | No       | 
title                    | string                     | No       | 
version                  | string                     | sí      | La cadena de versión completa después de la normalización

La propiedad `version` del paquete es la cadena de versión completa después de la normalización. Esto significa que los datos de compilación de SemVer 2.0.0 pueden incluirse aquí.

La `dependencyGroups` propiedad es una matriz de objetos que representan las dependencias del paquete, agrupadas por la plataforma de destino. Si el paquete no tiene dependencias, falta `dependencyGroups` la propiedad, una matriz vacía o la `dependencies` propiedad de todos los grupos está vacía o falta.

El valor de la `licenseExpression` propiedad cumple con la [Sintaxis](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)de las expresiones de licencia de NuGet.

#### <a name="package-dependency-group"></a>Grupo de dependencias de paquete

Cada objeto de grupo de dependencias tiene las siguientes propiedades:

NOMBRE            | Type             | Obligatorio | Notas
--------------- | ---------------- | -------- | -----
targetFramework | string           | No       | Plataforma de destino a la que se aplican estas dependencias.
dependencias    | matriz de objetos | No       |

La `targetFramework` cadena usa el formato implementado por la biblioteca .net de Nuget de Nuget [. frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Si no `targetFramework` se especifica, el grupo de dependencias se aplica a todas las plataformas de destino.

La `dependencies` propiedad es una matriz de objetos, cada uno de los cuales representa una dependencia del paquete del paquete actual.

#### <a name="package-dependency"></a>Dependencia de paquete

Cada dependencia del paquete tiene las siguientes propiedades:

NOMBRE         | Type   | Obligatorio | Notas
------------ | ------ | -------- | -----
id           | string | sí      | Identificador de la dependencia del paquete.
range        | objeto | No       | El [intervalo de versiones](../concepts/package-versioning.md#version-ranges-and-wildcards) permitido de la dependencia
registro | string | No       | Dirección URL del índice de registro para esta dependencia.

Si la `range` propiedad está excluida o es una cadena vacía, el cliente debe tener como valor `(, )`predeterminado el intervalo de versiones. Es decir, se permite cualquier versión de la dependencia.

#### <a name="package-deprecation"></a>Desuso de paquetes

Cada desuso de paquetes tiene las siguientes propiedades:

NOMBRE             | Type             | Obligatorio | Notas
---------------- | ---------------- | -------- | -----
principales          | matriz de cadenas | sí      | Los motivos por los que el paquete quedó en desuso
message          | string           | No       | Detalles adicionales sobre este desuso
alternatePackage | objeto           | No       | La dependencia del paquete que se debe usar en su lugar.

La `reasons` propiedad debe contener al menos una cadena y solo debe contener cadenas de la tabla siguiente:

Reason       | DESCRIPCIÓN             
------------ | -----------
Heredado       | El paquete ya no se mantiene
CriticalBugs | El paquete tiene errores que hacen que no sea adecuado para el uso
Otros        | El paquete está en desuso debido a un motivo que no está en esta lista

Si la `reasons` propiedad contiene cadenas que no son del conjunto conocido, se deben omitir. Las cadenas no distinguen mayúsculas de minúsculas, por lo que `legacy` deben tratarse igual que. `Legacy` No hay ninguna restricción de ordenación en la matriz, por lo que las cadenas pueden organizarse en cualquier orden arbitrario. Además, si la propiedad solo contiene cadenas que no son del conjunto conocido, debe tratarse como si solo contuviera la cadena "Other".

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

En este caso concreto, el índice de registro tiene la página de registro insertada, por lo que no se necesitan solicitudes adicionales para capturar metadatos sobre versiones de paquetes individuales.

## <a name="registration-page"></a>Página de registro

La página de registro contiene las hojas de registro. La dirección URL para obtener una página de registro viene determinada `@id` por la propiedad del objeto de la [Página de registro](#registration-page-object) mencionado anteriormente.

Cuando no `items` se proporciona la matriz en el índice de registro, una solicitud HTTP GET `@id` del valor devolverá un documento JSON que tiene un objeto como raíz. El objeto tiene las siguientes propiedades:

NOMBRE   | Type             | Obligatorio | Notas
------ | ---------------- | -------- | -----
@id    | string           | sí      | La dirección URL de la página de registro
count  | integer          | sí      | El número de hojas de registro en la página
items  | matriz de objetos | sí      | La matriz de las hojas de registro y sus metadatos asociados
inferiores  | string           | sí      | La versión más baja de SemVer 2.0.0 en la página (inclusivo)
parent | string           | sí      | Dirección URL del índice de registro.
esquina superior  | string           | sí      | La versión más alta de SemVer 2.0.0 en la página (inclusiva)

La forma de los objetos hoja de registro es la misma que en el índice de registro [anterior](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Hoja de registro

La hoja de registro contiene información sobre un identificador de paquete y una versión específicos. Es posible que los metadatos acerca de la versión específica no estén disponibles en este documento. Los metadatos del paquete se deben capturar desde el [Índice de registro](#registration-index) o desde la [Página de registro](#registration-page) (que se detecta mediante el índice de registro).

La dirección URL para capturar una hoja de registro se obtiene `@id` de la propiedad de un objeto hoja de registro en un índice de registro o en una página de registro.

La hoja de registro es un documento JSON con un objeto raíz con las siguientes propiedades:

NOMBRE           | Type    | Obligatorio | Notas
-------------- | ------- | -------- | -----
@id            | string  | sí      | La dirección URL de la hoja de registro
catalogEntry   | string  | No       | La dirección URL de la entrada del catálogo que generó estas hojas
lista         | boolean | No       | Se debe considerar como si no estuviera presente
packageContent | string  | No       | La dirección URL del contenido del paquete (. nupkg)
sin      | string  | No       | Una cadena que contiene una marca de tiempo ISO 8601 de Cuándo se publicó el paquete
registro   | string  | No       | Dirección URL del índice de registro.

> [!Note]
> En Nuget.org, el `published` valor se establece en Year 1900 cuando el paquete no está en la lista.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
