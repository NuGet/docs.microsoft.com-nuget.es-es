---
title: Consultar todos los paquetes publicados en nuget.org | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/02/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Con la API de NuGet puede consultar todos los paquetes publicados en nuget.org y mantenerse siempre al día.
keywords: La API de NuGet enumera todos los paquetes, la API de NuGet replica paquetes, últimos paquetes publicados en nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5ea11e1b4edd87b6d30d3838986ca60aaa77870f
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="19bb2-104">Consultar todos los paquetes publicados en nuget.org</span><span class="sxs-lookup"><span data-stu-id="19bb2-104">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="19bb2-105">Un modelo de consulta común en la API heredada OData V2 consistía en enumerar todos los paquetes publicados en nuget.org, ordenados por la fecha de publicación del paquete.</span><span class="sxs-lookup"><span data-stu-id="19bb2-105">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="19bb2-106">Los escenarios que requieren este tipo de consulta en nuget.org varían considerablemente:</span><span class="sxs-lookup"><span data-stu-id="19bb2-106">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="19bb2-107">Replicar nuget.org completamente</span><span class="sxs-lookup"><span data-stu-id="19bb2-107">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="19bb2-108">Detectar cuándo se publican nuevas versiones de los paquetes</span><span class="sxs-lookup"><span data-stu-id="19bb2-108">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="19bb2-109">Buscar paquetes que dependen de su paquete</span><span class="sxs-lookup"><span data-stu-id="19bb2-109">Finding packages that depend on your package</span></span>

<span data-ttu-id="19bb2-110">El método heredado para hacer esto solía depender de ordenar la entidad del paquete de OData por una marca de tiempo y efectuar una paginación por el enorme conjunto de resultados mediante los parámetros `skip` y `top` (tamaño de página).</span><span class="sxs-lookup"><span data-stu-id="19bb2-110">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="19bb2-111">Desafortunadamente, este enfoque presenta algunos inconvenientes:</span><span class="sxs-lookup"><span data-stu-id="19bb2-111">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="19bb2-112">Posibilidad de extraviar paquetes, ya que las consultas se efectúan en datos que a menudo cambian de orden</span><span class="sxs-lookup"><span data-stu-id="19bb2-112">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="19bb2-113">Tiempo de respuesta lento de las consultas, ya que las consultas no están optimizadas (las consultas más optimizadas son aquellas que admiten un escenario principal para el cliente de NuGet oficial)</span><span class="sxs-lookup"><span data-stu-id="19bb2-113">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="19bb2-114">Uso de una API en desuso y no documentada, lo que significa que la compatibilidad de estas consultas en el futuro no está garantizada</span><span class="sxs-lookup"><span data-stu-id="19bb2-114">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="19bb2-115">Incapacidad de reproducir el historial en el orden exacto en el que tuvo lugar</span><span class="sxs-lookup"><span data-stu-id="19bb2-115">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="19bb2-116">Por este motivo, se puede aplicar la guía siguiente para tratar los escenarios mencionados de una forma más confiable y con garantía de futuro.</span><span class="sxs-lookup"><span data-stu-id="19bb2-116">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="19bb2-117">Información general</span><span class="sxs-lookup"><span data-stu-id="19bb2-117">Overview</span></span>

<span data-ttu-id="19bb2-118">En el centro de esta guía hay un recurso en la [API de NuGet](../../api/overview.md) denominado **catálogo**.</span><span class="sxs-lookup"><span data-stu-id="19bb2-118">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="19bb2-119">El catálogo es una API de solo anexión que permite que el autor de la llamada vea un historial completo de los paquetes agregados, modificados y eliminados de nuget.org. Si le interesan todos o incluso un subconjunto de los paquetes publicados en nuget.org, el catálogo es una manera excelente de ir manteniéndose al día con el conjunto de paquetes disponibles.</span><span class="sxs-lookup"><span data-stu-id="19bb2-119">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="19bb2-120">Esta guía está pensada como un tutorial de alto nivel, pero si le interesan los detalles concretos del catálogo, vea el correspondiente [documento de referencia de la API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="19bb2-120">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="19bb2-121">Los siguientes pasos se pueden implementar en cualquier lenguaje de programación que quiera.</span><span class="sxs-lookup"><span data-stu-id="19bb2-121">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="19bb2-122">Si quiere ver un ejemplo completo en funcionamiento, eche un vistazo al [ejemplo de C#](#c-sample-code) que se menciona más abajo.</span><span class="sxs-lookup"><span data-stu-id="19bb2-122">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="19bb2-123">Si no, siga esta guía para crear un lector de catálogos confiable.</span><span class="sxs-lookup"><span data-stu-id="19bb2-123">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="19bb2-124">Inicializar un cursor</span><span class="sxs-lookup"><span data-stu-id="19bb2-124">Initialize a cursor</span></span>

<span data-ttu-id="19bb2-125">El primer paso a la hora de crear un lector de catálogos confiable consiste en implementar un cursor.</span><span class="sxs-lookup"><span data-stu-id="19bb2-125">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="19bb2-126">Para información detallada sobre el diseño de un cursor de catálogo, vea el [documento de referencia de catálogos](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="19bb2-126">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="19bb2-127">En pocas palabras, un cursor es un punto en el tiempo hasta el cual ha procesado eventos del catálogo.</span><span class="sxs-lookup"><span data-stu-id="19bb2-127">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="19bb2-128">Los eventos del catálogo representan publicaciones de paquetes y otras modificaciones de paquetes.</span><span class="sxs-lookup"><span data-stu-id="19bb2-128">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="19bb2-129">Si le interesan todos los paquetes que se han publicado en NuGet (desde el principio de los tiempos), inicializaría el cursor en una marca de tiempo de "valor mínimo" (por ejemplo, `DateTime.MinValue` en .NET).</span><span class="sxs-lookup"><span data-stu-id="19bb2-129">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="19bb2-130">Si solo le interesan los paquetes publicados a partir de ahora, usaría la marca de tiempo actual como valor inicial del cursor.</span><span class="sxs-lookup"><span data-stu-id="19bb2-130">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="19bb2-131">En esta guía inicializaremos nuestro cursor en una marca de tiempo de hace una hora.</span><span class="sxs-lookup"><span data-stu-id="19bb2-131">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="19bb2-132">De momento, lo único que tiene que hacer es guardar la marca de hora en la memoria.</span><span class="sxs-lookup"><span data-stu-id="19bb2-132">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="19bb2-133">Determinar la dirección URL del índice del catálogo</span><span class="sxs-lookup"><span data-stu-id="19bb2-133">Determine catalog index URL</span></span>

<span data-ttu-id="19bb2-134">La ubicación de cada recurso (punto de conexión) de la API de NuGet se debe detectar mediante el [índice de servicio](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="19bb2-134">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="19bb2-135">Dado que esta guía se centra en nuget.org, usaremos el índice de servicio de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="19bb2-135">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="19bb2-136">El documento de servicio es un documento JSON que contiene todos los recursos en nuget.org. Busque el recurso que tenga el valor de propiedad `@type` de `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="19bb2-136">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="19bb2-137">El valor de propiedad `@id` asociado es la dirección URL al índice del catálogo en cuestión.</span><span class="sxs-lookup"><span data-stu-id="19bb2-137">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="19bb2-138">Buscar nuevas hojas de catálogo</span><span class="sxs-lookup"><span data-stu-id="19bb2-138">Find new catalog leaves</span></span>

<span data-ttu-id="19bb2-139">Descargue el índice de catálogo con el valor de propiedad `@id` del paso anterior:</span><span class="sxs-lookup"><span data-stu-id="19bb2-139">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="19bb2-140">Deserialice el [índice del catálogo](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="19bb2-140">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="19bb2-141">Filtre todos los [objetos de páginas del catálogo](../../api/catalog-resource.md#catalog-page-object-in-the-index) con `commitTimeStamp` menor o igual que el valor actual del cursor.</span><span class="sxs-lookup"><span data-stu-id="19bb2-141">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="19bb2-142">Para el resto de las páginas del catálogo, descargue el documento completo con la propiedad `@id`.</span><span class="sxs-lookup"><span data-stu-id="19bb2-142">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="19bb2-143">Deserialice la [página del catálogo](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="19bb2-143">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="19bb2-144">Filtre todos los [objetos de hojas del catálogo](../../api/catalog-resource.md#catalog-item-object-in-a-page) con `commitTimeStamp` menor o igual que el valor actual del cursor.</span><span class="sxs-lookup"><span data-stu-id="19bb2-144">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="19bb2-145">Cuando haya descargado todas las páginas del catálogo que no se hayan filtrado, tendrá un conjunto de objetos hoja de catálogo que representan los paquetes publicados, enumerados, no enumerados o eliminados entre la fecha de la marca de tiempo del cursor y ahora.</span><span class="sxs-lookup"><span data-stu-id="19bb2-145">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="19bb2-146">Procesar las hojas del catálogo</span><span class="sxs-lookup"><span data-stu-id="19bb2-146">Process catalog leaves</span></span>

<span data-ttu-id="19bb2-147">Ahora puede llevar a cabo cualquier procesamiento personalizado que quiera en los elementos del catálogo.</span><span class="sxs-lookup"><span data-stu-id="19bb2-147">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="19bb2-148">Si lo que necesita es el identificador y la versión del paquete, puede inspeccionar las propiedades `nuget:id` y `nuget:version` de los objetos de elementos del catálogo, que se encuentran en las páginas.</span><span class="sxs-lookup"><span data-stu-id="19bb2-148">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="19bb2-149">No olvide examinar la propiedad `@type` para saber si el elemento del catálogo hace referencia a un paquete existente o a un paquete eliminado.</span><span class="sxs-lookup"><span data-stu-id="19bb2-149">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="19bb2-150">Si le interesan los metadatos del paquete (por ejemplo, la descripción, las dependencias, el tamaño del archivo .nupkg, etc.), puede capturar el [documento de hojas del catálogo](../../api/catalog-resource.md#catalog-leaf) con la propiedad `@id`.</span><span class="sxs-lookup"><span data-stu-id="19bb2-150">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="19bb2-151">Este documento contiene todos los metadatos que se incluyen en el [recurso de metadatos de paquete](../../api/registration-base-url-resource.md), ¡y mucho más!</span><span class="sxs-lookup"><span data-stu-id="19bb2-151">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="19bb2-152">Es en este paso en el que debe implementar la lógica personalizada.</span><span class="sxs-lookup"><span data-stu-id="19bb2-152">This step is where you implement your custom logic.</span></span> <span data-ttu-id="19bb2-153">Los demás pasos de esta guía se implementan prácticamente del mismo modo, independientemente de lo que haga con las hojas del catálogo.</span><span class="sxs-lookup"><span data-stu-id="19bb2-153">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="19bb2-154">Descargar los archivos .nupkg</span><span class="sxs-lookup"><span data-stu-id="19bb2-154">Downloading the .nupkg</span></span>

<span data-ttu-id="19bb2-155">Si le interesa descargar los archivos .nupkg de los paquetes del catálogo, puede usar el [recurso de contenido del paquete](../../api/package-base-address-resource.md),</span><span class="sxs-lookup"><span data-stu-id="19bb2-155">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="19bb2-156">aunque debe tener en cuenta que hay un breve retraso entre el momento en el que se encuentra un paquete en el catálogo y cuando está disponible en el recurso de contenido del paquete.</span><span class="sxs-lookup"><span data-stu-id="19bb2-156">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="19bb2-157">Por lo tanto, si detecta `404 Not Found` al intentar descargar un archivo .nupkg para un paquete que encontró en el catálogo, vuelva a intentarlo un poco más tarde.</span><span class="sxs-lookup"><span data-stu-id="19bb2-157">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="19bb2-158">En el problema de GitHub [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) se hace un seguimiento para corregir este retraso.</span><span class="sxs-lookup"><span data-stu-id="19bb2-158">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="19bb2-159">Mover el cursor hacia delante</span><span class="sxs-lookup"><span data-stu-id="19bb2-159">Move the cursor forward</span></span>

<span data-ttu-id="19bb2-160">Cuando haya procesado correctamente los elementos del catálogo, deberá determinar el nuevo valor del cursor que se va a guardar.</span><span class="sxs-lookup"><span data-stu-id="19bb2-160">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="19bb2-161">Para ello, busque el `commitTimeStamp` máximo (el más reciente cronológicamente) de todos los elementos del catálogo que haya procesado.</span><span class="sxs-lookup"><span data-stu-id="19bb2-161">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="19bb2-162">Este es el nuevo valor del cursor.</span><span class="sxs-lookup"><span data-stu-id="19bb2-162">This is your new cursor value.</span></span> <span data-ttu-id="19bb2-163">Guárdelo en algún almacén persistente (por ejemplo, una base de datos, un sistema de archivos o Blob Storage).</span><span class="sxs-lookup"><span data-stu-id="19bb2-163">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="19bb2-164">Cuando quiera obtener más elementos del catálogo, basta con empezar por el [primer paso](#initialize-a-cursor) inicializando el valor del cursor desde dicho almacén persistente.</span><span class="sxs-lookup"><span data-stu-id="19bb2-164">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="19bb2-165">Si la aplicación genera errores o una excepción, no mueva el cursor hacia delante.</span><span class="sxs-lookup"><span data-stu-id="19bb2-165">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="19bb2-166">La acción de mover el cursor hacia delante tiene el significado de que no volverá a necesitar procesar los elementos del catálogo que se encuentren delante del cursor.</span><span class="sxs-lookup"><span data-stu-id="19bb2-166">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="19bb2-167">Si por algún motivo recibe un error en la forma de procesar hojas del catálogo, puede mover el cursor hacia atrás en el tiempo y permitir que el código vuelva a procesar los elementos del catálogo antiguos.</span><span class="sxs-lookup"><span data-stu-id="19bb2-167">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="19bb2-168">Código de ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="19bb2-168">C# sample code</span></span>

<span data-ttu-id="19bb2-169">Como el catálogo es un conjunto de documentos JSON disponibles a través de HTTP, se puede interactuar con él con cualquier lenguaje de programación que tenga un cliente HTTP y un deserializador JSON.</span><span class="sxs-lookup"><span data-stu-id="19bb2-169">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="19bb2-170">En el [repositorio NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample) hay ejemplos de C#.</span><span class="sxs-lookup"><span data-stu-id="19bb2-170">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="19bb2-171">SDK del catálogo</span><span class="sxs-lookup"><span data-stu-id="19bb2-171">Catalog SDK</span></span>

<span data-ttu-id="19bb2-172">La forma más fácil de consumir el catálogo consiste en usar el paquete de versión preliminar del SDK del catálogo de .NET: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="19bb2-172">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="19bb2-173">Este paquete está disponible en la fuente de MyGet `nuget-build`, para la que se debe usar la dirección URL de origen del paquete de NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="19bb2-173">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="19bb2-174">Puede instalar este paquete en un proyecto compatible con `netstandard1.3` o una versión posterior (por ejemplo, .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="19bb2-174">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="19bb2-175">En el [proyecto NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample) de GitHub hay un ejemplo en el que se usa este paquete.</span><span class="sxs-lookup"><span data-stu-id="19bb2-175">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="19bb2-176">Resultados de ejemplo</span><span class="sxs-lookup"><span data-stu-id="19bb2-176">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="19bb2-177">Ejemplo mínimo</span><span class="sxs-lookup"><span data-stu-id="19bb2-177">Minimal sample</span></span>

<span data-ttu-id="19bb2-178">Para ver un ejemplo con menos dependencias en el que se muestre con más detalle la interacción con el catálogo, vea el [proyecto de ejemplo CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="19bb2-178">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="19bb2-179">El proyecto tiene como destino `netcoreapp2.0` y depende de [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (para resolver el índice de servicio) y de [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (para la deserialización JSON).</span><span class="sxs-lookup"><span data-stu-id="19bb2-179">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="19bb2-180">La lógica principal del código está visible en el [archivo Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="19bb2-180">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="19bb2-181">Resultados de ejemplo</span><span class="sxs-lookup"><span data-stu-id="19bb2-181">Sample output</span></span>

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
