---
title: "Catálogo, NuGet V3 API | Documentos de Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cfd338b5-6253-48c0-88ba-17c6b98fc935
description: "El catálogo es un índice de todos los paquetes creados y eliminados en nuget.org."
keywords: "Catálogo de API de NuGet V3, registro de transacciones de nuget.org, replique NuGet.org, clonar NuGet.org, registro solo de adición de NuGet.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 4c98b7cbd92575f6905e98a5bca5602a4d8ac0dd
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="catalog"></a>Catálogo

El **catálogo** es un recurso que registra todas las operaciones de paquete en un origen del paquete, como operaciones de creación y eliminación. El recurso de catálogo tiene el `Catalog` escriba en el [índice servicio](service-index.md).

> [!Note]
> Dado que el catálogo no se usa el cliente de NuGet oficial, no todos los orígenes de paquetes implementan el catálogo.

> [!Note]
> Actualmente, el catálogo de nuget.org no está disponible en China. Para obtener más información, consulte [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Control de versiones

El siguiente `@type` valor se utiliza:

Valor de @type   | Notas
------------- | -----
Catalog/3.0.0 | La versión inicial

## <a name="base-url"></a>Dirección URL base

La dirección URL de punto de entrada para las API siguientes es el valor de la `@id` propiedad asociada con el recurso mencionado anteriormente `@type` valores. Este tema utiliza la dirección URL del marcador de posición `{@id}`.

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL se encuentra en el soporte del catálogo de recursos únicamente los métodos HTTP `GET` y `HEAD`.

## <a name="catalog-index"></a>Índice del catálogo

El índice del catálogo es un documento en una ubicación conocida que tiene una lista de elementos de catálogo, ordenados cronologically. Es el punto de entrada del recurso de catálogo.

El índice se compone de páginas del catálogo. Cada página de catálogo contiene elementos de catálogo. Cada elemento de catálogo representa un evento relativas a un único paquete en un momento dado. Un elemento de catálogo puede representar un paquete que se creó, dados de baja, poner o eliminado del origen del paquete. Mediante el procesamiento de los elementos de catálogo en orden cronológico, el cliente puede crear una vista actualizada de cada paquete que existe en el origen del paquete V3.

En resumen, blobs de catálogo tienen la siguiente estructura jerárquica:

- **Índice**: el punto de entrada para el catálogo.
- **Página**: una agrupación de elementos de catálogo.
- **Hoja**: un documento que representa un elemento de catálogo, que es una instantánea del estado de un paquete único.

Cada objeto de catálogo tiene una propiedad denominada el `commitTimeStamp` que representa cuándo se agregó el elemento en el catálogo. Elementos del catálogo se agregan a una página de catálogo por lotes denominado confirmaciones. Todos los elementos del catálogo en el mismo confirmación tienen la misma marca de tiempo de confirmación (`commitTimeStamp`) e Id. de confirmación (`commitId`). Elementos de catálogo que se coloca en el mismo confirmación representan eventos ocurridos aproximadamente el mismo punto en el tiempo en el origen del paquete. No hay ningún orden dentro de una confirmación de catálogo.

Dado que cada identificador de paquete y la versión son único, nunca habrá más de un elemento de catálogo en una instrucción commit. Esto garantiza que los elementos de catálogo para un único paquete siempre se pueden ordenar sin ambigüedades con respecto a la marca de tiempo de confirmación.

Hay que no ser nunca más de una confirmación en el catálogo por `commitTimeStamp`. En otras palabras, el `commitId` es redundante con el `commitTimeStamp`.

Contrasta con la [recurso de metadatos de paquete](registration-base-url-resource.md), que se indiza por Id. de paquete, el catálogo está indizada (y consultable) sólo por tiempo.

Elementos de catálogo siempre se agregan al catálogo en un orden cronológico aumento de forma continua. Esto significa que si se agrega una confirmación de catálogo en tiempo de X, a continuación, ninguna confirmación de catálogo nunca se agregarán con un tiempo inferior o igual a X.

La siguiente solicitud de captura el índice del catálogo.

```
GET {@id}
```

El índice del catálogo es un documento JSON que contiene un objeto con las siguientes propiedades:

nombre            | Tipo             | Obligatorio | Notas
--------------- | ---------------- | -------- | -----
commitId        | cadena           | sí      | Un identificador único asociado a la confirmación más reciente
commitTimeStamp | cadena           | sí      | Una marca de tiempo de la última confirmación
count           | enteros          | sí      | El número de páginas del índice
items           | Matriz de objetos | sí      | Una matriz de objetos, cada objeto que representa una página

Cada elemento de la `items` matriz es un objeto con algunos detalles mínimos sobre cada página. Estos objetos de página no contienen las hojas de catálogo (elementos). No se define el orden de los elementos de esta matriz. Se pueden ordenar las páginas por el cliente en la memoria con sus `commitTimeStamp` propiedad.

Tal y como se introducen nuevas páginas, el `count` se incrementará y nuevos objetos aparecerán en el `items` matriz.

Cuando se agregan elementos al catálogo, el índice `commitId` cambiará y `commitTimeStamp` aumentará. Estas dos propiedades son básicamente un resumen sobre todas las página `commitId` y `commitTimeStamp` valores en el `items` matriz.

### <a name="catalog-page-object-in-the-index"></a>Objeto de página en el índice del catálogo

Los objetos de la página de catálogo que se encuentran en el índice de catálogo `items` propiedad tienen las siguientes propiedades:

nombre            | Tipo    | Obligatorio | Notas
--------------- | ------- | -------- | -----
@id             | cadena  | sí      | La dirección URL a la página de catálogo de fetch
commitId        | cadena  | sí      | Un identificador único asociado a la confirmación más reciente en esta página
commitTimeStamp | cadena  | sí      | Una marca de tiempo de la confirmación más reciente en esta página
count           | enteros | sí      | El número de elementos en la página de catálogo

Contrasta con la [recurso de metadatos de paquete](registration-base-url-resource.md) que en algunos casos, elementos incorporados deja en el índice, catálogo deja nunca se alinean en el índice y siempre se debe recopilar mediante la página `@id` dirección URL.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Página de catálogo

La página de catálogo es una colección de elementos de catálogo. Es un documento que se capturan mediante uno de los `@id` valores que se encuentran en el índice del catálogo. La dirección URL a una página de catálogo no está diseñada para ser predecibles y debe ser detectada con solo el índice del catálogo.

Nuevos elementos de catálogo se agregan a la página en el índice del catálogo únicamente con la marca de tiempo mayor de confirmación o a una página nueva. Una vez que se agrega una página con una marca de tiempo mayor de confirmación en el catálogo, las páginas antiguas nunca se agregan o cambian.

El documento de página de catálogo es un objeto JSON con las siguientes propiedades:

nombre            | Tipo             | Obligatorio | Notas
--------------- | ---------------- | -------- | -----
commitId        | cadena           | sí      | Un identificador único asociado a la confirmación más reciente en esta página
commitTimeStamp | cadena           | sí      | Una marca de tiempo de la confirmación más reciente en esta página
count           | enteros          | sí      | El número de elementos en la página
items           | Matriz de objetos | sí      | Los elementos del catálogo en esta página
parent          | cadena           | sí      | Una dirección URL para el índice del catálogo

Cada elemento de la `items` matriz es un objeto con algunos detalles mínimos sobre el elemento de catálogo. Estos objetos de elemento no contienen todos los datos del elemento de catálogo. El orden de los elementos de la página `items` matriz no está definida. Los elementos se pueden ordenar por el cliente en la memoria con sus `commitTimeStamp` propiedad.

El número de elementos de catálogo en una página se define mediante la implementación del servidor. Para nuget.org, a lo sumo hay 550 elementos en cada página, aunque el número real puede ser menor algunos dependong de páginas en el tamaño del lote de confirmación siguiente en el punto en el tiempo.

Cuando se Introducción nuevos elementos, el `count` es objetos de elemento de catálogo incrementado y nuevos aparecen en la `items` matriz.

Cuando se agregan elementos a la página, el `commitId` cambios y `commitTimeStamp` aumenta. Estas dos propiedades son básicamente un resumen sobre todas `commitId` y `commitTimeStamp` valores en el `items` matriz.

### <a name="catalog-item-object-in-a-page"></a>Objeto de elemento de una página de catálogo

Los objetos de elemento de catálogo que se encuentren en la página de catálogo `items` propiedad tienen las siguientes propiedades:

nombre            | Tipo    | Obligatorio | Notas
--------------- | ------- | -------- | -----
@id             | cadena  | sí      | La dirección URL para buscar el elemento de catálogo
@type           | cadena  | sí      | El tipo de elemento de catálogo
commitId        | cadena  | sí      | El identificador de confirmación asociado a este elemento de catálogo
commitTimeStamp | cadena  | sí      | La marca de tiempo de confirmación de este elemento de catálogo
NuGet:Id        | cadena  | sí      | El identificador del paquete que está relacionado con esta hoja
NuGet:Version   | cadena  | sí      | La versión del paquete que está relacionado con esta hoja

El `@type` valor será uno de los dos valores siguientes:

1. `nuget:PackageDetails`: corresponde al `PackageDetails` tipo en el documento de hoja de catálogo.
1. `nuget:PackageDelete`: Esto se corresponde con el `PackageDelete` tipo en el documento de hoja de catálogo.

Para obtener más detalles sobre cada tipo de qué significa, consulte el [correspondientes elementos de tipo](#item-types) a continuación.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Hoja de catálogo

La hoja de catálogo contiene metadatos sobre un identificador de paquete específico y la versión en algún momento en el tiempo. Es un documento que se obtienen mediante la `@id` valor se encuentra en una página de catálogo. La dirección URL a una hoja de catálogo no está diseñada para ser predictedable y debe detectarse mediante una página de catálogo.

El documento de hoja de catálogo es un objeto JSON con las siguientes propiedades:

nombre                    | Tipo                       | Obligatorio | Notas
----------------------- | -------------------------- | -------- | -----
@type                   | cadena o matriz de cadenas | sí      | Los tipos de elemento de catálogo
catálogo: commitId        | cadena                     | sí      | Un identificador de confirmación asociado a este elemento de catálogo
catálogo: commitTimeStamp | cadena                     | sí      | La marca de tiempo de confirmación de este elemento de catálogo
id                      | cadena                     | sí      | El identificador del paquete del elemento de catálogo
Publicado               | cadena                     | sí      | Elemento de catálogo de la fecha de publicación del paquete
version                 | cadena                     | sí      | La versión del paquete del elemento de catálogo

### <a name="item-types"></a>Tipos de elemento

El `@type` propiedad es una cadena o una matriz de cadenas. Para mayor comodidad, si la `@type` valor es una cadena, deben tratarse como una matriz de tamaño. No todos los valores posibles para `@type` están documentados. Sin embargo, cada elemento de catálogo tiene exactamente a uno de los dos valores de tipo string siguientes:

1. `PackageDetails`: representa una instantánea de los metadatos de paquete
1. `PackageDelete`: representa un paquete que se eliminó

### <a name="package-details-catalog-items"></a>Detalles del paquete de elementos de catálogo

Elementos con el tipo de catálogo `PackageDetails` contienen una instantánea de los metadatos de paquete para un paquete específico (combinación de identificador y la versión). Un elemento de catálogo de detalles de paquete se genera cuando un origen del paquete encuentra cualquiera de los siguientes escenarios:

1. Un paquete es **inserta**.
1. Un paquete es **aparece**.
1. Un paquete es **dados de baja**.
1. Un paquete es **adaptarse**.

Una redistribución del paquete es un movimiento administrativo que básicamente genera una inserción falsa de un paquete existente sin cambios en el propio paquete. En nuget.org, se utiliza una redistribución después de corregir un error en uno de los trabajos en segundo plano que es compatible con el catálogo.

Clientes que consumen los elementos de catálogo no deberían intentar determinar cuál de estos escenarios genera el elemento de catálogo. En su lugar, el cliente simplemente debe actualizar las vistas de mantener o índice con los metadatos contenidos en el elemento de catálogo. Además, deben controlarse elementos de catálogo duplicado o redundantes (idempotente).

Elementos del catálogo de detalles de paquete tienen las siguientes propiedades además de los [incluido en todas las ramas de catálogo](#catalog-leaf).

nombre                    | Tipo                       | Obligatorio | Notas
----------------------- | -------------------------- | -------- | -----
authors                 | cadena                     | No       |
created                 | cadena                     | sí      | Una marca de tiempo de cuando se creó el paquete por primera vez
dependencyGroups        | Matriz de objetos           | No       | Mismo formato que el [recurso de metadatos de paquete](registration-base-url-resource.md#package-dependency-group)
Descripción             | cadena                     | No       |
iconUrl                 | cadena                     | No       |
isPrerelease            | booleano                    | sí      | Si la versión del paquete es una versión preliminar
lenguaje                | cadena                     | No       |
licenseUrl              | cadena                     | No       |
lista                  | booleano                    | No       | Si no aparece el paquete
MinClientVersion        | cadena                     | No       |
packageHash             | cadena                     | sí      | El código hash del paquete, codificación utilizando [estándar en base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | cadena                     | sí      |
packageSize             | enteros                    | sí      | El tamaño de la .nupkg de paquete en bytes
projectUrl              | cadena                     | No       |
releaseNotes            | cadena                     | No       |
requireLicenseAgreement | booleano                    | No       | Suponga `false` Si excluye
resumen                 | cadena                     | No       |
etiquetas                    | Matriz de cadenas           | No       |
título                   | cadena                     | No       |
verbatimVersion         | cadena                     | No       | La cadena de versión que originalmente se encuentra en el NuSpec

El paquete `version` propiedad es la cadena de versión completa, normalizado. Esto significa que los datos de generación de SemVer 2.0.0 pueden incluirse aquí.

El `created` marca de tiempo es cuando el paquete se recibió en primer lugar por el origen del paquete, que suele ser poco tiempo antes de la marca de tiempo de confirmación del elemento de catálogo.

El `packageHashAlgorithm` es una cadena definida por el represeting de implementación de servidor el algoritmo hash utilizado para generar el `packageHash`. NuGet.org siempre utilizado la `packageHashAlgorithm` valo `SHA512`.

El `published` marca de tiempo es la hora en que se incluyó por última cuando el paquete.

> [!Note]
> En nuget.org, el `published` valor se establece en año 1900 cuando es que no figuran en el paquete.

#### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Elementos del catálogo de eliminación de paquetes

Elementos con el tipo de catálogo `PackageDelete` contienen un conjunto mínimo de información que indica a los clientes de catálogo que un paquete se ha eliminado del origen del paquete y ya no está disponible para cualquier operación de paquete (por ejemplo, restauración).

> [!Note]
> Es posible que un paquete va a eliminar y posteriormente se ha vuelto a publicar utilizando el mismo Id. de paquete y la versión. En nuget.org, este es un caso muy poco habitual, ya que interrumpe suposición oficial del cliente que un identificador de paquete y versión implican un contenido de paquete específico. Para obtener más información acerca de la eliminación de paquetes en nuget.org, consulte [nuestra directiva](../policies/deleting-packages.md).

Elementos del catálogo de eliminación de paquetes no tienen ninguna propiedad adicional además de los [incluido en todas las ramas de catálogo](#catalog-leaf).

El `version` propiedad es la cadena de versión original se encuentra en el paquete NuSpec.

El `published` propiedad es el tiempo cuando se eliminó el paquete, que normalmente es como hora corta antes de la marca de tiempo de confirmación del elemento de catálogo.

#### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>Información general

Esta sección describe un concepto de cliente que, aunque no es necesariamente asignadas por el protocolo debe ser parte de cualquier implementación de cliente de catálogo resulta muy práctico.

Dado que el catálogo es una estructura de datos de solo anexar indizada por hora, el cliente debe almacenar una **cursor** localmente, que representa hasta qué punto en el tiempo que el cliente ha procesado elementos del catálogo. Tenga en cuenta que este valor de cursor nunca se debe generar con el reloj del equipo del cliente. En su lugar, el valor debe provenir de un objeto de catálogo `commitTimestamp` valor.

Cada vez que el cliente desea procesar los nuevos eventos en el origen del paquete, necesita sólo consulta el catálogo para todos los elementos del catálogo con una marca de tiempo de confirmación mayor que el cursor almacenado. Una vez que el cliente procese correctamente todos los nuevos elementos de catálogo, registra la marca de tiempo más reciente de confirmación de elementos de catálogo que solo se procesan como su nuevo valor de cursor.

Con este enfoque, el cliente puede estar seguro de que nunca se pierda cualquier evento de paquete que se ha producido en el origen del paquete.
Además, el cliente nunca tiene que volver a procesar los eventos anteriores antes de la marca de tiempo de confirmación registrados del cursor.

Este concepto eficaz de los cursores se utiliza para muchos de los trabajos en segundo plano nuget.org y se usa para mantener actualizada la propia API V3. 

### <a name="initial-value"></a>Valor inicial

Cuando el cliente de catálogo se inicia por primera vez (y, por tanto, no tiene ningún valor de cursor), debe usar un valor de cursor predeterminado de. De NET `System.DateTimeOffset.MinValue` o alguna noción tal análoga de marca de tiempo mínima puede representar.

### <a name="iterating-over-catalog-items"></a>Recorrer en iteración los elementos de catálogo

Para consultar el siguiente conjunto de elementos de catálogo que se va a procesar, el cliente debe ser:

1. Capturar el valor de cursor registrados de un almacén local.
1. Descargue y deserializar el índice del catálogo.
1. Buscar todas las páginas con una marca de tiempo de confirmación de catálogo *mayor* el cursor.
1. Declare una lista vacía de elementos de catálogo que se va a procesar.
1. Para cada página de catálogo hacen coincidir en el paso 3:
   1. Descargar y deserializa la página de catálogo.
   1. Buscar todos los elementos con una marca de tiempo de confirmación del catálogo *mayor* el cursor.
   1. Agregue todos los elementos de catálogo correspondiente a la lista que se declara en el paso 4.
1. Ordenar la lista de elementos de catálogo por marca de tiempo de confirmación.
1. Procesar cada elemento de catálogo en secuencia:
   1. Descargue y deserializar el elemento de catálogo.
   1. Reaccionar de manera apropiada para el tipo de elemento de catálogo.
   1. Procesar el documento de elemento de catálogo de manera específica del cliente.
1. Registre la marca de tiempo de confirmación del último elemento catálogo como el nuevo valor de cursor.

Con este algoritmo básico, la implementación del cliente puede crear una vista completa de todos los paquetes disponibles en el origen del paquete. El cliente sólo tendrá que ejecutar este algoritmo periódicamente para que siempre sea consciente de los cambios más recientes en el origen del paquete.

> [!Note]
> Este es el algoritmo que nuget.org usa para mantener la [metadatos de paquete](registration-base-url-resource.md), [contenido del paquete](package-base-address-resource.md), [búsqueda](search-query-service-resource.md) y [Autocompletar](search-autocomplete-service-resource.md) recursos actualizados.

### <a name="dependent-cursors"></a>Cursores dependientes

Supongamos que hay dos clientes de catálogo que tienen una dependencia inherant donde depende de salida de un cliente en la salida de otro cliente. 

#### <a name="example"></a>Ejemplo

Por ejemplo, en nuget.org un paquete publicado recientemente no aparecerán en el recurso de búsqueda antes de que aparezca en el recurso de metadatos de paquete. Esto es porque la operación de "restore" realizada por el cliente de NuGet oficial usa los recursos de metadatos de paquete. Si un cliente detecta un paquete mediante el servicio de búsqueda, debe poder restaurar correctamente ese paquete mediante los recursos de metadatos de paquete. En otras palabras, el recurso de búsqueda depende de los recursos de metadatos de paquete. Cada recurso tiene un trabajo en segundo plano catálogo cliente actualizar ese recurso. Cada cliente tiene su propio cursor.

Dado que ambos recursos están integrados en el catálogo, el cursor del cliente de catálogo que actualiza el recurso de búsqueda *no debe ir más allá de* el cursor del cliente de catálogo de metadatos de paquete.

#### <a name="algorithm"></a>Algoritmo

Para implementar esta restricción, sencillo modificar el algoritmo anterior para ser:

1. Capturar el valor de cursor registrados de un almacén local.
1. Descargue y deserializar el índice del catálogo.
1. Buscar todas las páginas con una marca de tiempo de confirmación de catálogo *mayor* el cursor **menor o igual que el cursor de la dependencia.**
1. Declare una lista vacía de elementos de catálogo que se va a procesar.
1. Para cada página de catálogo hacen coincidir en el paso 3:
   1. Descargar y deserializa la página de catálogo.
   1. Buscar todos los elementos con una marca de tiempo de confirmación del catálogo *mayor* el cursor **menor o igual que el cursor de la dependencia.**
   1. Agregue todos los elementos de catálogo correspondiente a la lista que se declara en el paso 4.
1. Ordenar la lista de elementos de catálogo por marca de tiempo de confirmación.
1. Procesar cada elemento de catálogo en secuencia:
   1. Descargue y deserializar el elemento de catálogo.
   1. Reaccionar de manera apropiada para el tipo de elemento de catálogo.
   1. Procesar el documento de elemento de catálogo de manera específica del cliente.
1. Registre la marca de tiempo de confirmación del último elemento catálogo como el nuevo valor de cursor.

Mediante este algoritmo modificado, puede crear un sistema de clientes dependientes de catálogo que produce todas sus propios índices específicos, artefactos, etcetera.
