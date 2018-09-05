---
title: Límites, API de NuGet de frecuencia
description: Las APIs NuGet habrá aplica límites de velocidad para evitar abusos.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548682"
---
# <a name="rate-limits"></a>Límites de velocidad

La API de NuGet.org aplica la limitación de velocidad para evitar abusos. Las solicitudes que superen el límite de velocidad devuelven el error siguiente: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Además de los límites de frecuencia de uso de la limitación de solicitudes, algunas API de aplicar la cuota. Las solicitudes que superan la cuota, devuelven el error siguiente:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Las siguientes tablas enumeran los límites de frecuencia para la API de NuGet.org.

## <a name="package-search"></a>Búsqueda de paquetes

> [!Note]
> Se recomienda el uso de NuGet.org [API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) actualmente para la búsqueda de alto rendimiento y no tienen ningún límite. API de búsquedas de V1 y V2, se aplican los límites de followins:


| API | Tipo de límite | Valor de límite | API usecase |
|:---|:---|:---|:---|
**OBTENER** `/api/v1/Packages` | IP | 1000 / minuto | Consultar los metadatos del paquete de NuGet a través de OData v1 `Packages` colección |
**OBTENER** `/api/v1/Search()` | IP | 3000 / minuto | Buscar paquetes de NuGet a través del punto de conexión v1 búsqueda | 
**OBTENER** `/api/v2/Packages` | IP | 20000 / minuto | Consultar los metadatos de paquete de NuGet a través de OData v2 `Packages` colección | 
**OBTENER** `/api/v2/Packages/$count` | IP | 100 / minuto | Consultar el número de paquetes de NuGet a través de OData v2 `Packages` colección | 

## <a name="package-push-and-unlist"></a>Paquete de insertar y quitar de la lista

| API | Tipo de límite | Valor de límite | API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Clave de API | 250 / hora | Cargar un nuevo paquete de NuGet (versión) a través del punto de conexión de inserción de v2 
**ELIMINAR** `/api/v2/package/{id}/{version}` | Clave de API | 250 / hora | Quitar de la lista un paquete de NuGet (versión) a través del punto de conexión v2 
