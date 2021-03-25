---
title: Consultar todos los paquetes publicados en nuget.org
description: Con la API de NuGet puede consultar todos los paquetes publicados en nuget.org y mantenerse siempre al día.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 8f21aad93eb952035683314c10cd964f265ec4fd
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859348"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Consultar todos los paquetes publicados en nuget.org

Un modelo de consulta común en la API heredada OData V2 consistía en enumerar todos los paquetes publicados en nuget.org, ordenados por la fecha de publicación del paquete. Los escenarios que requieren este tipo de consulta en nuget.org varían considerablemente:

- Replicar nuget.org completamente
- Detectar cuándo se publican nuevas versiones de los paquetes
- Buscar paquetes que dependen de su paquete

El método heredado para hacer esto solía depender de ordenar la entidad del paquete de OData por una marca de tiempo y efectuar una paginación por el enorme conjunto de resultados mediante los parámetros `skip` y `top` (tamaño de página). Desafortunadamente, este enfoque presenta algunos inconvenientes:

- Posibilidad de extraviar paquetes, ya que las consultas se efectúan en datos que a menudo cambian de orden
- Tiempo de respuesta lento de las consultas, ya que las consultas no están optimizadas (las consultas más optimizadas son aquellas que admiten un escenario principal para el cliente de NuGet oficial)
- Uso de una API en desuso y no documentada, lo que significa que la compatibilidad de estas consultas en el futuro no está garantizada
- Incapacidad de reproducir el historial en el orden exacto en el que tuvo lugar

Por este motivo, se puede aplicar la guía siguiente para tratar los escenarios mencionados de una forma más confiable y con garantía de futuro.

## <a name="overview"></a>Información general

En el centro de esta guía hay un recurso en la [API de NuGet](../../api/overview.md) denominado **catálogo**. El catálogo es una API de solo anexión que permite que el autor de la llamada vea un historial completo de los paquetes agregados, modificados y eliminados de nuget.org. Si le interesan todos o incluso un subconjunto de los paquetes publicados en nuget.org, el catálogo es una manera excelente de ir manteniéndose al día con el conjunto de paquetes disponibles.

Esta guía está pensada como un tutorial de alto nivel, pero si le interesan los detalles concretos del catálogo, vea el correspondiente [documento de referencia de la API](../../api/catalog-resource.md).

Los siguientes pasos se pueden implementar en cualquier lenguaje de programación que quiera. Si quiere ver un ejemplo completo en funcionamiento, eche un vistazo al [ejemplo de C#](#c-sample-code) que se menciona más abajo.

Si no, siga esta guía para crear un lector de catálogos confiable.

## <a name="initialize-a-cursor"></a>Inicializar un cursor

El primer paso a la hora de crear un lector de catálogos confiable consiste en implementar un cursor. Para información detallada sobre el diseño de un cursor de catálogo, vea el [documento de referencia de catálogos](../../api/catalog-resource.md#cursor). En pocas palabras, un cursor es un punto en el tiempo hasta el cual ha procesado eventos del catálogo. Los eventos del catálogo representan publicaciones de paquetes y otras modificaciones de paquetes. Si le interesan todos los paquetes que se han publicado en NuGet (desde el principio de los tiempos), inicializaría el cursor en una marca de tiempo de "valor mínimo" (por ejemplo, `DateTime.MinValue` en .NET). Si solo le interesan los paquetes publicados a partir de ahora, usaría la marca de tiempo actual como valor inicial del cursor.

En esta guía inicializaremos nuestro cursor en una marca de tiempo de hace una hora. De momento, lo único que tiene que hacer es guardar la marca de hora en la memoria.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Determinar la dirección URL del índice del catálogo

La ubicación de cada recurso (punto de conexión) de la API de NuGet se debe detectar mediante el [índice de servicio](../../api/service-index.md). Dado que esta guía se centra en nuget.org, usaremos el índice de servicio de nuget.org.

```
GET https://api.nuget.org/v3/index.json
```

El documento de servicio es un documento JSON que contiene todos los recursos en nuget.org. Busque el recurso que tenga el valor de propiedad `@type` de `Catalog/3.0.0`. El valor de propiedad `@id` asociado es la dirección URL al índice del catálogo en cuestión. 

## <a name="find-new-catalog-leaves"></a>Buscar nuevas hojas de catálogo

Descargue el índice de catálogo con el valor de propiedad `@id` del paso anterior:

```
GET https://api.nuget.org/v3/catalog0/index.json
```

Deserialice el [índice del catálogo](../../api/catalog-resource.md#catalog-index). Filtre todos los [objetos de páginas del catálogo](../../api/catalog-resource.md#catalog-page-object-in-the-index) con `commitTimeStamp` menor o igual que el valor actual del cursor.

Para el resto de las páginas del catálogo, descargue el documento completo con la propiedad `@id`.

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

Deserialice la [página del catálogo](../../api/catalog-resource.md#catalog-page). Filtre todos los [objetos de hojas del catálogo](../../api/catalog-resource.md#catalog-item-object-in-a-page) con `commitTimeStamp` menor o igual que el valor actual del cursor.

Cuando haya descargado todas las páginas del catálogo que no se hayan filtrado, tendrá un conjunto de objetos hoja de catálogo que representan los paquetes publicados, enumerados, no enumerados o eliminados entre la fecha de la marca de tiempo del cursor y ahora.

## <a name="process-catalog-leaves"></a>Procesar las hojas del catálogo

Ahora puede llevar a cabo cualquier procesamiento personalizado que quiera en los elementos del catálogo. Si lo que necesita es el identificador y la versión del paquete, puede inspeccionar las propiedades `nuget:id` y `nuget:version` de los objetos de elementos del catálogo, que se encuentran en las páginas. No olvide examinar la propiedad `@type` para saber si el elemento del catálogo hace referencia a un paquete existente o a un paquete eliminado.

Si le interesan los metadatos del paquete (por ejemplo, la descripción, las dependencias, el tamaño del archivo .nupkg, etc.), puede capturar el [documento de hojas del catálogo](../../api/catalog-resource.md#catalog-leaf) con la propiedad `@id`.

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

Este documento contiene todos los metadatos que se incluyen en el [recurso de metadatos de paquete](../../api/registration-base-url-resource.md), ¡y mucho más!

Es en este paso en el que debe implementar la lógica personalizada. Los demás pasos de esta guía se implementan prácticamente del mismo modo, independientemente de lo que haga con las hojas del catálogo.

### <a name="downloading-the-nupkg"></a>Descargar los archivos .nupkg

Si le interesa descargar los archivos .nupkg de los paquetes del catálogo, puede usar el [recurso de contenido del paquete](../../api/package-base-address-resource.md), aunque debe tener en cuenta que hay un breve retraso entre el momento en el que se encuentra un paquete en el catálogo y cuando está disponible en el recurso de contenido del paquete. Por lo tanto, si detecta `404 Not Found` al intentar descargar un archivo .nupkg para un paquete que encontró en el catálogo, vuelva a intentarlo un poco más tarde. En el problema de GitHub [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) se hace un seguimiento para corregir este retraso.

## <a name="move-the-cursor-forward"></a>Mover el cursor hacia delante

Cuando haya procesado correctamente los elementos del catálogo, deberá determinar el nuevo valor del cursor que se va a guardar. Para ello, busque el `commitTimeStamp` máximo (el más reciente cronológicamente) de todos los elementos del catálogo que haya procesado. Este es el nuevo valor del cursor. Guárdelo en algún almacén persistente (por ejemplo, una base de datos, un sistema de archivos o Blob Storage). Cuando quiera obtener más elementos del catálogo, basta con empezar por el [primer paso](#initialize-a-cursor) inicializando el valor del cursor desde dicho almacén persistente.

Si la aplicación genera errores o una excepción, no mueva el cursor hacia delante. La acción de mover el cursor hacia delante tiene el significado de que no volverá a necesitar procesar los elementos del catálogo que se encuentren delante del cursor.

Si por algún motivo recibe un error en la forma de procesar hojas del catálogo, puede mover el cursor hacia atrás en el tiempo y permitir que el código vuelva a procesar los elementos del catálogo antiguos.

## <a name="c-sample-code"></a>Código de ejemplo de C#

Como el catálogo es un conjunto de documentos JSON disponibles a través de HTTP, se puede interactuar con él con cualquier lenguaje de programación que tenga un cliente HTTP y un deserializador JSON.

En el [repositorio NuGet/Samples](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample) hay ejemplos de C#.

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>SDK del catálogo

La forma más fácil de consumir el catálogo es usar el paquete del SDK de catálogo de .NET en versión preliminar, `NuGet.Protocol.Catalog`, que está disponible en Azure Artifacts mediante la siguiente dirección URL de origen del paquete de NuGet: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json`.

Puede instalar este paquete en un proyecto compatible con `netstandard1.3` o una versión posterior (por ejemplo, .NET Framework 4.6).

En el [proyecto NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample/NuGet.Protocol.Catalog.Sample) de GitHub hay un ejemplo en el que se usa este paquete.

#### <a name="sample-output"></a>Salida de ejemplo

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>Ejemplo mínimo

Para ver un ejemplo con menos dependencias en el que se muestre con más detalle la interacción con el catálogo, vea el [proyecto de ejemplo CatalogReaderExample](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample/CatalogReaderExample). El proyecto tiene como destino `netcoreapp2.0` y depende de [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (para resolver el índice de servicio) y de [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (para la deserialización JSON).

La lógica principal del código está visible en el [archivo Program.cs](https://github.com/NuGet/Samples/blob/main/CatalogReaderExample/CatalogReaderExample/Program.cs).

#### <a name="sample-output"></a>Salida de ejemplo

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
