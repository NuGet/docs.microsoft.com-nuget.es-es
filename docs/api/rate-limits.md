---
title: Límites de frecuencia, API de NuGet
description: Las API de NuGet tendrán límites de frecuencia aplicados para evitar el abuso.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367939"
---
# <a name="rate-limits"></a>Límites de velocidad

La API de NuGet.org aplica la limitación de velocidad para impedir el abuso. Las solicitudes que superan el límite de velocidad devuelven el siguiente error: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Además de la limitación de solicitudes con límites de frecuencia, algunas API también aplican la cuota. Las solicitudes que superan la cuota devuelven el siguiente error:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

En las tablas siguientes se enumeran los límites de frecuencia de la API de NuGet.org.

## <a name="package-search"></a>Búsqueda de paquetes

> [!Note]
> Se recomienda el uso de las [API de búsqueda de V3](search-query-service-resource.md) en la organización, ya que no tiene una tasa limitada actualmente. En el caso de las API de búsqueda V1 y V2, se aplican los límites siguientes:

| API | Tipo de límite | Valor límite | Caso de uso de la API |
|:---|:---|:---|:---|
**Obtener**`/api/v1/Packages` | IP | 1000/minuto | Consulta de metadatos de paquetes NuGet mediante la colección de OData v1 `Packages` |
**Obtener**`/api/v1/Search()` | IP | 3000/minuto | Buscar paquetes NuGet a través del punto de conexión de búsqueda v1 | 
**Obtener**`/api/v2/Packages` | IP | 20000/minuto | Consultar metadatos de paquetes NuGet a través de la colección OData V2 `Packages` | 
**Obtener**`/api/v2/Packages/$count` | IP | 100/minuto | Consultar el recuento de paquetes NuGet mediante la colección OData V2 `Packages` | 

## <a name="package-push-and-unlist"></a>Instalación y deslista de paquetes

| API | Tipo de límite | Valor límite | Caso de uso de la API | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Clave de API | 350 por hora | Carga de un nuevo paquete NuGet (versión) a través del punto de conexión de inserciones V2 
**Eliminar**`/api/v2/package/{id}/{version}` | Clave de API | 250 por hora | Mostrar un paquete NuGet (versión) a través del punto de conexión V2 

## <a name="nugetorg-website-page-views"></a>vistas de página del sitio web de nuget.org

Si tiene acceso a las páginas web de nuget.org mediante programación, considere la posibilidad de investigar nuestras [API de V3](overview.md)documentadas. Estos puntos de conexión permiten un acceso más sencillo a los metadatos y al contenido del paquete. La API V3 tiene una mejor disponibilidad y tiene un mayor rendimiento que el acceso a las páginas web de la galería de NuGet, que están diseñadas para la interacción del explorador Web.

| API | Tipo de límite | Valor límite | Caso de uso de la API | 
|:---|:---|:---|:--- |
**Obtener**`/package/{id}/{version}` | IP | 50/minuto | Mostrar la página de detalles del paquete (versión). 
