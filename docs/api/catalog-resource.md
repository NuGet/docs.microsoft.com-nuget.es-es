---
title: Recurso de catálogo, API de NuGet V3
description: El catálogo es un índice de todos los paquetes creados y eliminados en nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6c04453fec9beb7b0998953384ec60694e1213c1
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990147"
---
# <a name="catalog"></a>Catálogo

El **Catálogo** es un recurso que registra todas las operaciones de paquetes en un origen de paquete, como creaciones y eliminaciones. El recurso de catálogo tiene el `Catalog` tipo en el [Índice de servicio](service-index.md). Puede usar este recurso para [consultar todos los paquetes publicados](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Dado que el cliente de NuGet oficial no usa el catálogo, no todos los orígenes de paquete implementan el catálogo.

> [!Note]
> Actualmente, el catálogo de nuget.org no está disponible en China. Para obtener más información, consulte [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Control de versiones

`@type`Se usa el siguiente valor:

Valor de @type   | Notas
------------- | -----
Catálogo/3.0.0 | La versión inicial

## <a name="base-url"></a>URL base

La dirección URL del punto de entrada para las siguientes API es el valor de la `@id` propiedad asociada a los valores de recursos mencionados anteriormente `@type` . En este tema se utiliza la dirección URL del marcador de posición `{@id}` .

## <a name="http-methods"></a>Métodos HTTP

Todas las direcciones URL encontradas en el recurso de catálogo solo admiten los métodos HTTP `GET` y `HEAD` .

## <a name="catalog-index"></a>Índice del catálogo

El índice del catálogo es un documento en una ubicación conocida que tiene una lista de elementos de catálogo, ordenada cronológicamente. Es el punto de entrada del recurso de catálogo.

El índice está formado por páginas de catálogo. Cada página de catálogo contiene elementos de catálogo. Cada elemento del catálogo representa un evento relacionado con un solo paquete en un momento dado. Un elemento de catálogo puede representar un paquete que se ha creado, quitado de la lista, se ha eliminado de la lista o eliminado del origen del paquete. Al procesar los elementos del catálogo en orden cronológico, el cliente puede crear una vista actualizada de cada paquete que existe en el origen del paquete V3.

En Resumen, los blobs de catálogo tienen la siguiente estructura jerárquica:

- **Index**: el punto de entrada del catálogo.
- **Página**: una agrupación de elementos de catálogo.
- **Hoja**: documento que representa un elemento de catálogo, que es una instantánea del estado de un paquete único.

Cada objeto de catálogo tiene una propiedad denominada `commitTimeStamp` que representa el momento en que se agregó el elemento al catálogo. Los elementos de catálogo se agregan a una página de catálogo en los lotes denominados confirmaciones. Todos los elementos de catálogo de la misma confirmación tienen la misma marca de tiempo de confirmación ( `commitTimeStamp` ) y el identificador de confirmación ( `commitId` ). Los elementos de catálogo colocados en la misma confirmación representan eventos que se produjeron aproximadamente en el mismo momento en el origen del paquete. No hay ninguna ordenación dentro de una confirmación del catálogo.

Dado que cada identificador y versión de paquete es único, nunca habrá más de un elemento de catálogo en una confirmación. Esto garantiza que los elementos de catálogo para un único paquete siempre se pueden ordenar de forma no ambigua con respecto a la marca de tiempo de confirmación.

Nunca hay más de una confirmación en el catálogo por `commitTimeStamp` . En otras palabras, el `commitId` es redundante con `commitTimeStamp` .

A diferencia del [recurso de metadatos del paquete](registration-base-url-resource.md), que está indizado por el identificador del paquete, el catálogo se indexa (y se consulta) solo por tiempo.

Los elementos del catálogo siempre se agregan al catálogo en un orden cronológico de progresión continua. Esto significa que, si se agrega una confirmación de catálogo en el tiempo X, no se agregará ninguna confirmación de catálogo con una hora menor o igual que X.

La solicitud siguiente captura el índice del catálogo.

```
GET {@id}
```

El índice del catálogo es un documento JSON que contiene un objeto con las siguientes propiedades:

Nombre            | Tipo             | Obligatorio | Notas
--------------- | ---------------- | -------- | -----
commitId        | string           | sí      | Un identificador único asociado a la confirmación más reciente
commitTimeStamp | string           | sí      | Marca de tiempo de la confirmación más reciente
count           | integer          | sí      | Número de páginas del índice
items           | matriz de objetos | sí      | Matriz de objetos, cada objeto que representa una página.

Cada elemento de la `items` matriz es un objeto con algunos detalles mínimos sobre cada página. Estos objetos de página no contienen el catálogo (items). No se ha definido el orden de los elementos de esta matriz. Las páginas se pueden ordenar por el cliente en memoria mediante su `commitTimeStamp` propiedad.

A medida que se introducen nuevas páginas, se `count` incrementarán y los nuevos objetos aparecerán en la `items` matriz.

A medida que se agregan elementos al catálogo, cambiará el del índice `commitId` y `commitTimeStamp` aumentará. Estas dos propiedades son básicamente un resumen de todas las páginas `commitId` y `commitTimeStamp` los valores de la `items` matriz.

### <a name="catalog-page-object-in-the-index"></a>Objeto de página de catálogo en el índice

Los objetos de la página de catálogo que se encuentran en la propiedad del índice del catálogo `items` tienen las siguientes propiedades:

Nombre            | Tipo    | Obligatorio | Notas
--------------- | ------- | -------- | -----
@id             | string  | sí      | La página dirección URL para recuperar el catálogo
commitId        | string  | sí      | Un identificador único asociado a la confirmación más reciente en esta página
commitTimeStamp | string  | sí      | Marca de tiempo de la confirmación más reciente en esta página
count           | integer | sí      | El número de elementos en la página del catálogo

A diferencia del [recurso de metadatos del paquete](registration-base-url-resource.md) que en algunos casos los inserta en el índice, los catálogos no se insertan nunca en el índice y siempre se deben capturar mediante la dirección URL de la página `@id` .

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Página del catálogo

La página del catálogo es una colección de elementos de catálogo. Se trata de un documento capturado con uno de los `@id` valores que se encuentran en el índice del catálogo. La dirección URL de una página de catálogo no está diseñada para ser predecible y debe detectarse solo con el índice de catálogo.

Los elementos de catálogo nuevos se agregan a la página en el índice del catálogo solo con la marca de tiempo de confirmación más alta o en una nueva página. Una vez que se agrega al catálogo una página con una marca de tiempo de confirmación superior, las páginas anteriores nunca se agregan o se cambian.

El documento de la página del catálogo es un objeto JSON con las siguientes propiedades:

Nombre            | Tipo             | Obligatorio | Notas
--------------- | ---------------- | -------- | -----
commitId        | string           | sí      | Un identificador único asociado a la confirmación más reciente en esta página
commitTimeStamp | string           | sí      | Marca de tiempo de la confirmación más reciente en esta página
count           | integer          | sí      | El número de elementos de la página
items           | matriz de objetos | sí      | Elementos del catálogo en esta página
primario          | string           | sí      | Una dirección URL al índice del catálogo

Cada elemento de la `items` matriz es un objeto con algunos detalles mínimos sobre el elemento de catálogo. Estos objetos de elemento no contienen todos los datos del elemento de catálogo. No se ha definido el orden de los elementos de la matriz de la página `items` . Los elementos se pueden ordenar por el cliente en memoria mediante su `commitTimeStamp` propiedad.

El número de elementos de catálogo de una página se define mediante la implementación de servidor. En el caso de nuget.org, hay como máximo 550 elementos en cada página, aunque el número real puede ser menor para algunas páginas, según el tamaño del siguiente lote de confirmación en el momento dado.

A medida que se introducen nuevos elementos, `count` se incrementa y los nuevos objetos de elemento de catálogo aparecen en la `items` matriz.

A medida que se agregan elementos a la página, los `commitId` cambios y `commitTimeStamp` aumentan. Estas dos propiedades son básicamente un resumen de todos `commitId` los `commitTimeStamp` valores y de la `items` matriz.

### <a name="catalog-item-object-in-a-page"></a>Objeto de elemento de catálogo en una página

Los objetos de elemento de catálogo que se encuentran en la propiedad de la página de catálogo `items` tienen las siguientes propiedades:

Nombre            | Tipo    | Obligatorio | Notas
--------------- | ------- | -------- | -----
@id             | string  | sí      | Dirección URL para capturar el elemento de catálogo.
@type           | string  | sí      | El tipo del elemento de catálogo
commitId        | string  | sí      | El ID. de confirmación asociado a este elemento de catálogo
commitTimeStamp | string  | sí      | Marca de tiempo de confirmación de este elemento de catálogo
Nuget: ID.        | string  | sí      | Identificador del paquete al que está relacionada esta hoja.
Nuget: versión   | string  | sí      | La versión del paquete con la que está relacionada esta hoja

El `@type` valor será uno de los dos valores siguientes:

1. `nuget:PackageDetails`: se corresponde con `PackageDetails` el tipo del documento de hoja del catálogo.
1. `nuget:PackageDelete`: corresponde al tipo del `PackageDelete` documento hoja del catálogo.

Para obtener más información sobre lo que significa cada tipo, vea el [tipo de elementos correspondiente](#item-types) a continuación.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Hoja del catálogo

La hoja de catálogo contiene metadatos sobre un identificador de paquete y una versión específicos en algún momento. Se trata de un documento capturado mediante el `@id` valor que se encuentra en una página de catálogo. La dirección URL a una hoja de catálogo no está diseñada para ser predecible y debe detectarse solo con una página de catálogo.

El documento hoja del catálogo es un objeto JSON con las siguientes propiedades:

Nombre                    | Tipo                       | Obligatorio | Notas
----------------------- | -------------------------- | -------- | -----
@type                   | cadena o matriz de cadenas | sí      | Los tipos del elemento de catálogo
Catálogo: commitId        | string                     | sí      | Un ID. de confirmación asociado a este elemento de catálogo
Catálogo: commitTimeStamp | string                     | sí      | Marca de tiempo de confirmación de este elemento de catálogo
id                      | string                     | sí      | Identificador del paquete del elemento de catálogo.
published               | string                     | sí      | Fecha de publicación del elemento del catálogo de paquetes
version                 | string                     | sí      | Versión del paquete del elemento de catálogo

### <a name="item-types"></a>Tipos de elemento

La `@type` propiedad es una cadena o una matriz de cadenas. Para mayor comodidad, si el `@type` valor es una cadena, debe tratarse como cualquier matriz de tamaño uno. No se documentan todos los valores posibles para `@type` . Sin embargo, cada elemento de catálogo tiene exactamente uno de los dos valores de tipo de cadena siguientes:

1. `PackageDetails`: representa una instantánea de metadatos del paquete.
1. `PackageDelete`: representa un paquete que se ha eliminado.

### <a name="package-details-catalog-items"></a>Elementos del catálogo de detalles de paquetes

Los elementos del catálogo con el tipo `PackageDetails` contienen una instantánea de los metadatos del paquete para un paquete específico (combinación de identificador y versión). Un elemento de catálogo de detalles de paquete se genera cuando un origen de paquete encuentra alguno de los escenarios siguientes:

1. Se **inserta** un paquete.
1. **Aparece** un paquete.
1. Un paquete no está en la **lista**.
1. Se **refluye** un paquete.

Un reflujo de paquetes es un gesto administrativo que genera esencialmente una extracción falsa de un paquete existente sin cambios en el propio paquete. En nuget.org, se usa un reflujo después de corregir un error en uno de los trabajos en segundo plano que consumen el catálogo.

Los clientes que consumen los elementos del catálogo no deben intentar determinar cuál de estos escenarios generó el elemento de catálogo. En su lugar, el cliente simplemente debe actualizar cualquier vista o índice mantenido con los metadatos contenidos en el elemento de catálogo. Además, los elementos de catálogo duplicados o redundantes se deben controlar correctamente (manera idempotente).

Los elementos del catálogo de detalles del paquete tienen las siguientes propiedades además de las [incluidas en todas las hojas del catálogo](#catalog-leaf).

Nombre                    | Tipo                       | Obligatorio | Notas
----------------------- | -------------------------- | -------- | -----
authors                 | string                     | no       |
created                 | string                     | no       | Marca de tiempo de la primera vez que se creó el paquete. Propiedad fallback: `published` .
dependencyGroups        | matriz de objetos           | no       | Las dependencias del paquete, agrupadas por la plataforma de destino ([el mismo formato que el recurso de metadatos del paquete](registration-base-url-resource.md#package-dependency-group))
desuso             | object                     | no       | El desuso asociado al paquete (el[mismo formato que el recurso de metadatos del paquete](registration-base-url-resource.md#package-deprecation))
description             | string                     | no       |
iconUrl                 | string                     | no       |
isPrerelease            | boolean                    | no       | Indica si la versión del paquete está en versión preliminar. Se puede detectar desde `version` .
language                | string                     | no       |
licenseUrl              | string                     | no       |
lista                  | boolean                    | no       | Indica si el paquete aparece o no
minClientVersion        | string                     | no       |
packageHash             | string                     | sí      | El hash del paquete, codificar con [base estándar 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | string                     | sí      |
Empaquetar             | integer                    | sí      | Tamaño del paquete. nupkg en bytes
packageTypes            | matriz de objetos           | no       | Los tipos de paquetes especificados por el autor.
projectUrl              | string                     | no       |
releaseNotes            | string                     | no       |
requireLicenseAgreement | boolean                    | no       | Asuma `false` si está excluido
Resumen                 | string                     | no       |
etiquetas                    | Matriz de cadenas           | no       |
title                   | string                     | no       |
verbatimVersion         | string                     | no       | La cadena de versión tal y como se encontró originalmente en el archivo. nuspec
vulnerabilidades         | matriz de objetos           | no       | Las vulnerabilidades de seguridad del paquete

La propiedad del paquete `version` es la cadena de versión completa después de la normalización. Esto significa que los datos de compilación de SemVer 2.0.0 pueden incluirse aquí.

La `created` marca de tiempo es cuando el origen del paquete recibió el paquete por primera vez, que suele ser un breve período antes de la marca de tiempo de confirmación del elemento de catálogo.

`packageHashAlgorithm`Es una cadena definida por la implementación del servidor que representa el algoritmo hash utilizado para generar `packageHash` . nuget.org siempre usó el `packageHashAlgorithm` valor de `SHA512` .

La `packageTypes` propiedad solo estará presente si el autor especificó un tipo de paquete. Si está presente, siempre tendrá al menos una (1) entrada. Cada elemento de la `packageTypes` matriz es un objeto JSON con las siguientes propiedades:

Nombre      | Tipo    | Obligatorio | Notas
--------- | ------- | -------- | -----
name      | string  | sí      | Nombre del tipo de paquete.
version    | string  | no       | Versión del tipo de paquete. Solo está presente si el autor especificó explícitamente una versión en el archivo nuspec.

La `published` marca de tiempo es la hora a la que se muestra el paquete por última vez.

> [!Note]
> En nuget.org, el `published` valor se establece en el año 1900 cuando el paquete no está en la lista.

#### <a name="vulnerabilities"></a>Puntos vulnerables

Matriz de objetos `vulnerability`. Cada vulnerabilidad tiene las siguientes propiedades:

Nombre         | Tipo   | Obligatorio | Notas
------------ | ------ | -------- | -----
advisoryUrl  | string | sí      | Ubicación del aviso de seguridad para el paquete
severity     | string | sí      | Gravedad del aviso: "0" = bajo, "1" = moderado, "2" = alto, "3" = crítico

Si la `severity` propiedad contiene valores distintos de los enumerados aquí, la gravedad del aviso se tratará como baja.

#### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Elementos del catálogo de eliminación de paquetes

Los elementos de catálogo con el tipo `PackageDelete` contienen un conjunto mínimo de información que indica a los clientes de catálogo que se ha eliminado un paquete del origen del paquete y que ya no está disponible para ninguna operación de paquete (por ejemplo, restore).

> [!NOTE]
> Es posible que un paquete se elimine y se vuelva a publicar posteriormente con el mismo identificador de paquete y versión. En nuget.org, este es un caso muy poco frecuente, ya que interrumpe la suposición del cliente oficial de que un identificador de paquete y una versión implican un contenido de paquete específico. Para obtener más información sobre la eliminación de paquetes en nuget.org, consulte [nuestra directiva](../nuget-org/policies/deleting-packages.md).

Los elementos del catálogo de eliminación de paquetes no tienen propiedades adicionales además de las que se [incluyen en todas las hojas del catálogo](#catalog-leaf).

La `version` propiedad es la cadena de versión original que se encuentra en package. nuspec.

La `published` propiedad es la hora a la que se eliminó el paquete, que suele ser una hora corta antes de la marca de tiempo de confirmación del elemento de catálogo.

#### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>Información general

En esta sección se describe un concepto de cliente que, aunque no es necesariamente obligatorio por el protocolo, debe formar parte de cualquier implementación de cliente de catálogo práctico.

Dado que el catálogo es una estructura de datos de solo anexar indizada por tiempo, el cliente debe almacenar un **cursor** localmente, que representa hasta qué punto en el tiempo el cliente ha procesado elementos de catálogo. Tenga en cuenta que este valor de cursor nunca debe generarse mediante el reloj del equipo del cliente. En su lugar, el valor debe proviene del valor de un objeto de catálogo `commitTimestamp` .

Cada vez que el cliente desea procesar nuevos eventos en el origen del paquete, solo necesita consultar el catálogo de todos los elementos del catálogo con una marca de tiempo de confirmación mayor que su cursor almacenado. Una vez que el cliente procesa correctamente todos los elementos de catálogo nuevos, registra la marca de tiempo de confirmación más reciente de los elementos de catálogo que se han procesado como el nuevo valor de cursor.

Con este enfoque, el cliente puede estar seguro de que nunca se han perdido los eventos de paquete que se produjeron en el origen del paquete.
Además, el cliente nunca tiene que volver a procesar los eventos anteriores antes de la marca de tiempo de confirmación registrada del cursor.

Este importante concepto de cursores se usa para muchos de los trabajos en segundo plano de nuget.org y se usa para mantener la API de V3 actualizada. 

### <a name="initial-value"></a>Valor inicial

Cuando el cliente del catálogo se inicia por primera vez (y, por tanto, no tiene ningún valor de cursor), debe utilizar un valor de cursor predeterminado de. La red `System.DateTimeOffset.MinValue` o alguna de estas nociones análogas de la marca de tiempo mínima que se va a representar.

### <a name="iterating-over-catalog-items"></a>Recorrer en iteración los elementos del catálogo

Para consultar el siguiente conjunto de elementos de catálogo que se va a procesar, el cliente debe:

1. Captura el valor de cursor registrado desde un almacén local.
1. Descargar y deserializar el índice del catálogo.
1. Busque todas las páginas del catálogo con una marca de tiempo de confirmación *mayor que* el cursor.
1. Declare una lista vacía de elementos de catálogo para procesar.
1. Para cada página de catálogo que coincida con el paso 3:
   1. Descargar y deserializar la página de catálogos.
   1. Buscar todos los elementos del catálogo con una marca de tiempo de confirmación *mayor que* el cursor.
   1. Agregue todos los elementos de catálogo coincidentes a la lista declarada en el paso 4.
1. Ordene la lista de elementos de catálogo por marca de tiempo de confirmación.
1. Procese cada elemento del catálogo en secuencia:
   1. Descargar y deserializar el elemento de catálogo.
   1. Reaccione correctamente en el tipo de elemento de catálogo.
   1. Procesar el documento de elemento de catálogo en un modo específico del cliente.
1. Registra la marca de tiempo de confirmación del último elemento del catálogo como el nuevo valor del cursor.

Con este algoritmo básico, la implementación del cliente puede crear una vista completa de todos los paquetes disponibles en el origen del paquete. El cliente solo necesita ejecutar este algoritmo periódicamente para tener siempre en cuenta los últimos cambios en el origen del paquete.

> [!Note]
> Este es el algoritmo que nuget.org usa para mantener actualizados los [metadatos del paquete](registration-base-url-resource.md), el [contenido del paquete](package-base-address-resource.md), la [búsqueda](search-query-service-resource.md) y los recursos de [Autocompletar](search-autocomplete-service-resource.md) .

### <a name="dependent-cursors"></a>Cursores dependientes

Suponga que hay dos clientes de catálogo que tienen una dependencia inherente en la que la salida de un cliente depende de la salida de otro cliente. 

#### <a name="example"></a>Ejemplo

Por ejemplo, en nuget.org un paquete recién publicado no debe aparecer en el recurso de búsqueda antes de que aparezca en el recurso de metadatos del paquete. Esto se debe a que la operación de restauración realizada por el cliente de NuGet oficial usa el recurso de metadatos del paquete. Si un cliente detecta un paquete mediante el servicio de búsqueda, debería poder restaurarlo correctamente mediante el recurso de metadatos del paquete. En otras palabras, el recurso de búsqueda depende del recurso de metadatos del paquete. Cada recurso tiene un trabajo en segundo plano del cliente del catálogo que actualiza ese recurso. Cada cliente tiene su propio cursor.

Puesto que ambos recursos se compilan en el catálogo, el cursor del cliente del catálogo que actualiza el recurso de búsqueda *no debe ir más allá* del cursor del cliente del catálogo de metadatos del paquete.

#### <a name="algorithm"></a>Algoritmo

Para implementar esta restricción, simplemente modifique el algoritmo anterior para que sea:

1. Captura el valor de cursor registrado desde un almacén local.
1. Descargar y deserializar el índice del catálogo.
1. Buscar todas las páginas del catálogo con una marca de tiempo de confirmación *mayor que* el cursor **menor o igual que el cursor de la dependencia.**
1. Declare una lista vacía de elementos de catálogo para procesar.
1. Para cada página de catálogo que coincida con el paso 3:
   1. Descargar y deserializar la página de catálogos.
   1. Buscar todos los elementos del catálogo con una marca de tiempo de confirmación *mayor que* el cursor **menor o igual que el cursor de la dependencia.**
   1. Agregue todos los elementos de catálogo coincidentes a la lista declarada en el paso 4.
1. Ordene la lista de elementos de catálogo por marca de tiempo de confirmación.
1. Procese cada elemento del catálogo en secuencia:
   1. Descargar y deserializar el elemento de catálogo.
   1. Reaccione correctamente en el tipo de elemento de catálogo.
   1. Procesar el documento de elemento de catálogo en un modo específico del cliente.
1. Registra la marca de tiempo de confirmación del último elemento del catálogo como el nuevo valor del cursor.

Con este algoritmo modificado, puede compilar un sistema de clientes de catálogo dependiente que producen sus propios índices, artefactos, etc.
