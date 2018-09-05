---
title: Recurso de catálogo, API de NuGet V3
description: El catálogo es un índice de todos los paquetes creados y eliminados en nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d4c13200494ed3c6fa897ce0083a52c13688b44b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547398"
---
# <a name="catalog"></a>Catálogo

El **catálogo** es un recurso que registra todas las operaciones de paquete en un origen de paquete, como la creación y eliminación. El recurso de catálogo tiene el `Catalog` escriba en el [índice de servicio](service-index.md).

> [!Note]
> Dado que el catálogo no se usa el cliente NuGet oficial, no todos los orígenes de paquetes implementan el catálogo.

> [!Note]
> Actualmente, el catálogo de nuget.org no está disponible en China. Para obtener más información, consulte [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Control de versiones

La siguiente `@type` se usa el valor:

Valor de @type   | Notas
------------- | -----
Catalog/3.0.0 | La versión inicial

## <a name="base-url"></a>Dirección URL base

La dirección URL de punto de entrada para las siguientes API es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valores. Este tema usa la dirección URL del marcador de posición `{@id}`.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL se encuentra en el soporte del catálogo de recursos solo los métodos HTTP `GET` y `HEAD`.

## <a name="catalog-index"></a>Índice del catálogo

El índice del catálogo es un documento en una ubicación conocida que tiene una lista de elementos de catálogo, ordenados cronológicamente. Es el punto de entrada del recurso de catálogo.

El índice se compone de páginas del catálogo. Cada página del catálogo contiene los elementos del catálogo. Cada elemento de catálogo representa un evento relativa a un único paquete en un momento dado. Un elemento de catálogo puede representar un paquete que se creó, dados de baja, de vuelto o eliminadas desde el origen del paquete. Mediante el procesamiento de los elementos del catálogo en orden cronológico, el cliente puede crear una vista actualizada de cada paquete que existe en el origen del paquete V3.

En resumen, los blobs de catálogo tienen la siguiente estructura jerárquica:

- **Índice**: el punto de entrada para el catálogo.
- **Página**: una agrupación de elementos del catálogo.
- **Hoja**: un documento que representa un elemento de catálogo, que es una instantánea del estado de un paquete único.

Cada objeto de catálogo tiene una propiedad denominada el `commitTimeStamp` que representa cuando se agregó el elemento en el catálogo. Los elementos del catálogo se agregan a una página de catálogo por lotes que se denominan confirmaciones. Todos los elementos del catálogo en la misma confirmación tienen la misma marca de tiempo de confirmación (`commitTimeStamp`) y el Id. de confirmación (`commitId`). Elementos de catálogo que se colocan en la misma confirmación representan eventos que se produjeron alrededor del mismo punto en el tiempo en el origen del paquete. No hay ningún orden dentro de una confirmación de catálogo.

Dado que cada identificador de paquete y la versión son único, nunca habrá más de un elemento de catálogo en una confirmación. Esto garantiza que los elementos del catálogo para un único paquete siempre se pueden ordenar sin ambigüedad con respecto a la marca de tiempo de confirmación.

Hay que no ser nunca más de una confirmación en el catálogo por `commitTimeStamp`. En otras palabras, el `commitId` es redundante con el `commitTimeStamp`.

Por el contrario el [recurso de metadatos de paquete](registration-base-url-resource.md), indizada por Id. de paquete, el catálogo está indizada (y puede consultar) solo por tiempo.

Siempre se agregan los elementos del catálogo en el catálogo en un orden cronológico progresión. Esto significa que si se agrega una confirmación de catálogo en el momento X, a continuación, no hay ninguna confirmación catálogo nunca se agregará con un tiempo inferior o igual a X.

La siguiente solicitud recupera el índice del catálogo.

    GET {@id}

El índice del catálogo es un documento JSON que contiene un objeto con las siguientes propiedades:

nombre            | Tipo             | Obligatorio | Notas
--------------- | ---------------- | -------- | -----
commitid & gt        | cadena           | sí      | Un identificador único asociado con la confirmación más reciente
commitTimeStamp | cadena           | sí      | Una marca de tiempo de la confirmación más reciente
count           | enteros          | sí      | El número de páginas del índice
items           | matriz de objetos | sí      | Una matriz de objetos, cada objeto que representa una página

Cada elemento en el `items` matriz es un objeto con algunos detalles mínimos sobre cada página. Estos objetos de página no contienen las hojas del catálogo (elementos). No se define el orden de los elementos de esta matriz. Las páginas se pueden ordenar por el cliente en memoria mediante sus `commitTimeStamp` propiedad.

Medida se introducen nuevas páginas, el `count` se incrementa y nuevos objetos aparecerán en el `items` matriz.

Cuando se agregan elementos a, el índice del catálogo `commitId` cambiará y `commitTimeStamp` aumentará. Estas dos propiedades son básicamente un resumen sobre todas las página `commitId` y `commitTimeStamp` valores en el `items` matriz.

### <a name="catalog-page-object-in-the-index"></a>Objeto de página en el índice del catálogo

Los objetos de la página de catálogo se encuentran en el índice de catálogo `items` propiedad tiene las siguientes propiedades:

nombre            | Tipo    | Obligatorio | Notas
--------------- | ------- | -------- | -----
@id             | cadena  | sí      | La dirección URL para obtener la página de catálogo
commitid & gt        | cadena  | sí      | Un identificador único asociado con la confirmación más reciente en esta página
commitTimeStamp | cadena  | sí      | Una marca de tiempo de la confirmación más reciente en esta página
count           | enteros | sí      | El número de elementos en la página del catálogo

Por el contrario el [recurso de metadatos de paquete](registration-base-url-resource.md) que en algunos casos inlines deja en el índice, nunca se alinean en el índice de hojas del catálogo y siempre se deben buscar mediante el uso de la página `@id` dirección URL.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Página del catálogo

La página del catálogo es una colección de elementos del catálogo. Es un documento que se capturan mediante uno de los `@id` valores que se encuentran en el índice del catálogo. La dirección URL a una página de catálogo no pretende ser predecible y se debe detectar mediante solo el índice del catálogo.

Nuevos elementos de catálogo se agregan a la página en el índice del catálogo solo con la marca de tiempo máximo de confirmación o a una página nueva. Una vez que se agrega una página con una marca de tiempo mayor de confirmación en el catálogo, las páginas anteriores nunca se agregan o cambian.

El documento de página del catálogo es un objeto JSON con las siguientes propiedades:

nombre            | Tipo             | Obligatorio | Notas
--------------- | ---------------- | -------- | -----
commitid & gt        | cadena           | sí      | Un identificador único asociado con la confirmación más reciente en esta página
commitTimeStamp | cadena           | sí      | Una marca de tiempo de la confirmación más reciente en esta página
count           | enteros          | sí      | El número de elementos en la página
items           | matriz de objetos | sí      | Los elementos del catálogo en esta página
parent          | cadena           | sí      | Una dirección URL para el índice del catálogo

Cada elemento en el `items` matriz es un objeto con algunos detalles mínimos sobre el elemento de catálogo. Estos objetos de elemento no contienen todos los datos del elemento de catálogo. El orden de los elementos de la página `items` matriz no está definida. Los elementos se pueden ordenar por el cliente en memoria mediante sus `commitTimeStamp` propiedad.

El número de elementos de catálogo en una página se define mediante la implementación del servidor. Para nuget.org, a lo sumo hay 550 elementos en cada página, aunque el número real puede ser menor para algunas páginas según el tamaño del lote de confirmación siguiente en el punto en el tiempo.

Medida se introducen nuevos elementos, el `count` es objetos de elemento de catálogo incrementado y nuevos aparecen en la `items` matriz.

Cuando se agregan elementos a la página, el `commitId` cambios y la `commitTimeStamp` aumenta. Estas dos propiedades son básicamente un resumen sobre las `commitId` y `commitTimeStamp` valores en el `items` matriz.

### <a name="catalog-item-object-in-a-page"></a>Objeto de elemento de una página del catálogo

Los objetos de elemento de catálogo se encontraron en la página catálogo `items` propiedad tiene las siguientes propiedades:

nombre            | Tipo    | Obligatorio | Notas
--------------- | ------- | -------- | -----
@id             | cadena  | sí      | La dirección URL para recuperar el elemento de catálogo
@type           | cadena  | sí      | El tipo del elemento del catálogo
commitid & gt        | cadena  | sí      | El identificador de confirmación asociado con este elemento de catálogo
commitTimeStamp | cadena  | sí      | La marca de tiempo de confirmación de este elemento de catálogo
NuGet:Id        | cadena  | sí      | El identificador del paquete que está relacionado con esta hoja
NuGet:Version   | cadena  | sí      | La versión del paquete que está relacionado con esta hoja

El `@type` tendrá uno de los dos valores siguientes:

1. `nuget:PackageDetails`: corresponde al `PackageDetails` tipo en el documento de hoja de catálogo.
1. `nuget:PackageDelete`: Esto se corresponde con el `PackageDelete` tipo en el documento de hoja de catálogo.

Para obtener más detalles sobre cada tipo de qué significa, consulte el [correspondientes elementos de tipo](#item-types) a continuación.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Hoja de catálogo

La hoja de catálogo contiene metadatos sobre un identificador de paquete específico y la versión en algún momento en el tiempo. Es un documento que se obtienen mediante la `@id` valor se encuentra en una página del catálogo. La dirección URL a una hoja de catálogo no pretende ser predecible y se debe detectar mediante solo una página del catálogo.

El documento de hoja de catálogo es un objeto JSON con las siguientes propiedades:

nombre                    | Tipo                       | Obligatorio | Notas
----------------------- | -------------------------- | -------- | -----
@type                   | cadena o matriz de cadenas | sí      | Los tipos del elemento del catálogo
commitId: catálogo        | cadena                     | sí      | Un identificador de confirmación asociado con este elemento de catálogo
catálogo: commitTimeStamp | cadena                     | sí      | La marca de tiempo de confirmación de este elemento de catálogo
id                      | cadena                     | sí      | El identificador del paquete del elemento del catálogo
Publicado               | cadena                     | sí      | La fecha de publicación del elemento del catálogo de paquetes
version                 | cadena                     | sí      | La versión del paquete del elemento del catálogo

### <a name="item-types"></a>Tipos de elemento

El `@type` propiedad es una cadena o matriz de cadenas. Para mayor comodidad, si la `@type` valor es una cadena, debe tratarse como una matriz de tamaño. No todos los valores posibles para `@type` están documentados. Sin embargo, cada elemento de catálogo tiene exactamente uno de los dos valores de tipo de cadena siguientes:

1. `PackageDetails`: representa una instantánea de los metadatos del paquete
1. `PackageDelete`: representa un paquete que se ha eliminado

### <a name="package-details-catalog-items"></a>Elementos del catálogo los detalles del paquete

Elementos con el tipo de catálogo `PackageDetails` contienen una instantánea de los metadatos del paquete para un paquete específico (combinación de identificador y la versión). Un elemento de catálogo los detalles de paquete se genera cuando un origen del paquete encuentra cualquiera de los siguientes escenarios:

1. Un paquete es **insertado**.
1. Un paquete es **enumerados**.
1. Un paquete es **dados de baja**.
1. Un paquete es **adaptarse**.

Un reflujo de paquete es un gesto administrativo que básicamente genera una falsa inserción de un paquete existente sin cambios al propio paquete. En nuget.org, se usa un reflujo después de corregir un error en uno de los trabajos en segundo plano que consumen el catálogo.

Los clientes de consumo de los elementos de catálogo no deben intentar determinar cuál de estos escenarios provocan el elemento de catálogo. En su lugar, el cliente simplemente debe actualizar cualquier vista mantenida o índice con los metadatos contenidos en el elemento de catálogo. Además, deben controlarse los elementos del catálogo duplicados o redundantes (manera idempotente).

Elementos del catálogo de los detalles de paquete tienen las siguientes propiedades además de los [incluida en todas las hojas del catálogo](#catalog-leaf).

nombre                    | Tipo                       | Obligatorio | Notas
----------------------- | -------------------------- | -------- | -----
authors                 | cadena                     | No       |
created                 | cadena                     | No       | Una marca de tiempo de cuando se creó el paquete por primera vez. Propiedad de reserva: `published`.
dependencyGroups        | matriz de objetos           | No       | Mismo formato que el [recurso de metadatos de paquete](registration-base-url-resource.md#package-dependency-group)
Descripción             | cadena                     | No       |
iconUrl                 | cadena                     | No       |
isPrerelease            | booleano                    | No       | Si la versión del paquete es una versión preliminar. Se pueden detectar desde `version`.
lenguaje                | cadena                     | No       |
licenseUrl              | cadena                     | No       |
lista                  | booleano                    | No       | Si aparece el paquete
MinClientVersion        | cadena                     | No       |
packageHash             | cadena                     | sí      | El hash del paquete, la codificación mediante [estándar en base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | cadena                     | sí      |
packageSize             | enteros                    | sí      | El tamaño de los archivos .nupkg de paquete en bytes
projectUrl              | cadena                     | No       |
releaseNotes            | cadena                     | No       |
requireLicenseAgreement | booleano                    | No       | Suponga `false` Si excluye
resumen                 | cadena                     | No       |
etiquetas                    | matriz de cadenas           | No       |
título                   | cadena                     | No       |
verbatimVersion         | cadena                     | No       | La cadena de versión que originalmente se encuentra en el archivo .nuspec

El paquete `version` propiedad es la cadena de versión completa, normalizado. Esto significa que los datos de generación de SemVer 2.0.0 se pueden incluidos aquí.

El `created` marca de tiempo es cuando se recibe por primera vez el paquete por el origen del paquete, que suele ser poco tiempo antes de la marca de tiempo de confirmación del elemento de catálogo.

El `packageHashAlgorithm` es una cadena definida por la implementación del servidor que representa el algoritmo hash utilizado para generar el `packageHash`. NuGet.org siempre utilizado la `packageHashAlgorithm` valor `SHA512`.

El `published` marca de tiempo es la hora cuando el paquete por última vez enumerado.

> [!Note]
> En nuget.org, el `published` valor se establece en el año 1900 cuando se da de baja el paquete.

#### <a name="sample-request"></a>Solicitud de ejemplo

OBTENER https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Elementos del catálogo de eliminación de paquete

Elementos con el tipo de catálogo `PackageDelete` contienen un conjunto mínimo de información que indique a los clientes del catálogo que un paquete se ha eliminado del origen del paquete y ya no está disponible para cualquier operación de paquete (por ejemplo, restauración).

> [!Note]
> Es posible que un paquete va a eliminar y posteriormente se han vuelto a publicar utilizando el mismo Id. de paquete y la versión. En nuget.org, este es un caso muy poco frecuente, porque interrumpe suposición oficial del cliente que un identificador de paquete y versión implican un contenido de paquete específico. Para obtener más información acerca de la eliminación del paquete en nuget.org, vea [nuestra directiva](../policies/deleting-packages.md).

Los elementos del catálogo de eliminación de paquete no tienen ninguna propiedad adicional además de los [incluida en todas las hojas del catálogo](#catalog-leaf).

El `version` propiedad es la cadena de versión original se encuentra en el archivo .nuspec del paquete.

El `published` propiedad es el tiempo cuando se eliminó el paquete, que normalmente es como poco tiempo antes de la marca de tiempo de confirmación del elemento de catálogo.

#### <a name="sample-request"></a>Solicitud de ejemplo

OBTENER https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>Información general

Esta sección describe un concepto de cliente que, aunque no está necesariamente asignada por el protocolo, debe ser parte de cualquier implementación de cliente de catálogo práctico.

Dado que el catálogo es una estructura de datos de solo anexión indizada por tiempo, el cliente debe almacenar un **cursor** localmente, que representa hasta qué punto en el tiempo que el cliente ha procesado los elementos del catálogo. Tenga en cuenta que este valor de cursor nunca se debe generar utilizando el reloj del equipo del cliente. En su lugar, el valor debe provenir de un objeto de catálogo `commitTimestamp` valor.

Cada vez que el cliente desea procesar nuevos eventos en el origen del paquete, necesita sólo consulta el catálogo para todos los elementos de catálogo con una marca de tiempo de confirmación mayor que su cursor almacenado. Una vez que el cliente procesa correctamente todos los nuevos elementos de catálogo, registra la marca de tiempo de confirmación más reciente de los elementos del catálogo que solo se procesan como su nuevo valor de cursor.

Con este enfoque, el cliente puede estar seguro de que nunca se pierdan los eventos de paquete que se ha producido en el origen del paquete.
Además, el cliente nunca debe volver a procesar los eventos antiguos antes de la marca de tiempo de confirmación registrado del cursor.

Este concepto eficaz de los cursores se utiliza para muchos de los trabajos en segundo plano de nuget.org y se usa para mantener actualizada la propia API V3. 

### <a name="initial-value"></a>Valor inicial

Cuando el cliente de catálogo se inicia por primera vez (y, por tanto, no tiene ningún valor del cursor), debe usar valor predeterminado es cursor. La red `System.DateTimeOffset.MinValue` o alguna noción tal análoga de marca de tiempo mínimo que se puede representar.

### <a name="iterating-over-catalog-items"></a>Recorrer en iteración los elementos del catálogo

Para consultar el siguiente conjunto de elementos de catálogo que se va a procesar, el cliente debe:

1. Capturar el valor del cursor grabados desde un almacén local.
1. Descargar y deserializar el índice del catálogo.
1. Buscar todas las páginas con una marca de tiempo de confirmación de catálogo *mayor* el cursor.
1. Declare una lista vacía de elementos de catálogo que se va a procesar.
1. Para cada página del catálogo hacen coincidir en el paso 3:
   1. Descargar y deserializar la página del catálogo.
   1. Buscar todos los elementos con una marca de tiempo de confirmación del catálogo *mayor* el cursor.
   1. Agregar todos los elementos de catálogo correspondiente a la lista que se declara en el paso 4.
1. Ordenar la lista de elementos de catálogo por marca de tiempo de confirmación.
1. Procesar cada elemento de catálogo de secuencia:
   1. Descargar y deserializar el elemento de catálogo.
   1. Reaccionar de manera apropiada para el tipo de elemento de catálogo.
   1. Procesar el documento de elemento de catálogo de forma específica del cliente.
1. Registre la marca de tiempo de confirmación del último elemento catálogo como el nuevo valor del cursor.

Con este algoritmo básico, la implementación del cliente puede crear una vista completa de todos los paquetes disponibles en el origen del paquete. El cliente sólo tendrá que ejecutar este algoritmo periódicamente para que siempre sea consciente de los cambios más recientes para el origen del paquete.

> [!Note]
> Este es el algoritmo que nuget.org se usa para mantener la [los metadatos del paquete](registration-base-url-resource.md), [contenido del paquete](package-base-address-resource.md), [búsqueda](search-query-service-resource.md) y [Autocompletar](search-autocomplete-service-resource.md) recursos actualizados.

### <a name="dependent-cursors"></a>Cursores dependientes

Supongamos que hay dos clientes de catálogo que tienen una dependencia inherente que salida de un cliente depende de salida de otro cliente. 

#### <a name="example"></a>Ejemplo

Por ejemplo, en nuget.org un paquete publicado recientemente no debe aparecer en el recurso de búsqueda antes de que aparezca en el recurso de metadatos de paquete. Esto es porque la operación de "restauración" realizada por el cliente NuGet oficial usa el recurso de metadatos del paquete. Si un cliente detecta un paquete con el servicio de búsqueda, debería poder restaurar correctamente ese paquete con el recurso de metadatos del paquete. En otras palabras, el recurso de búsqueda depende el recurso de metadatos del paquete. Cada recurso tiene un trabajo en segundo plano del cliente de catálogo actualizar ese recurso. Cada cliente tiene su propio cursor.

Dado que ambos recursos se crean en el catálogo, el cursor del cliente de catálogo que actualiza el recurso de búsqueda *no debe superar* el cursor del cliente de catálogo de metadatos de paquete.

#### <a name="algorithm"></a>algoritmo

Para implementar esta restricción, basta con modificar el algoritmo anterior para ser:

1. Capturar el valor del cursor grabados desde un almacén local.
1. Descargar y deserializar el índice del catálogo.
1. Buscar todas las páginas con una marca de tiempo de confirmación de catálogo *mayor* el cursor **menor o igual que el cursor de la dependencia.**
1. Declare una lista vacía de elementos de catálogo que se va a procesar.
1. Para cada página del catálogo hacen coincidir en el paso 3:
   1. Descargar y deserializar la página del catálogo.
   1. Buscar todos los elementos con una marca de tiempo de confirmación del catálogo *mayor* el cursor **menor o igual que el cursor de la dependencia.**
   1. Agregar todos los elementos de catálogo correspondiente a la lista que se declara en el paso 4.
1. Ordenar la lista de elementos de catálogo por marca de tiempo de confirmación.
1. Procesar cada elemento de catálogo de secuencia:
   1. Descargar y deserializar el elemento de catálogo.
   1. Reaccionar de manera apropiada para el tipo de elemento de catálogo.
   1. Procesar el documento de elemento de catálogo de forma específica del cliente.
1. Registre la marca de tiempo de confirmación del último elemento catálogo como el nuevo valor del cursor.

Con este algoritmo modificado, puede crear un sistema de clientes dependientes catálogo producir todas sus propios índices específicos, artefactos, etcetera.
