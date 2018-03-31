---
title: Límites de frecuencia | Documentos de Microsoft
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Las APIs NuGet habrá aplica límites de velocidad para evitar abusos.
keywords: Velocidad de NuGet API, limitar
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a>Límites de velocidad

La API de NuGet.org aplica la limitación de velocidad para evitar abusos. Solicitud que supere el límite de velocidad devolverá el error siguiente: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Las tablas siguientes muestran los límites de frecuencia para la API de NuGet.org.

## <a name="package-search"></a>Búsqueda de paquete

> [!Note]
> Recomendamos el uso de NuGet.org [API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) actualmente para la búsqueda de un rendimiento superior y no tiene ningún límite. Para V1 y V2 API de búsqueda, se aplican los límites de followins:


| API | Tipo de límite | Valor del límite | API usecase |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000 / minuto | Consultar los metadatos de paquete de NuGet a través de OData v1 `Packages` colección |
**GET** `/api/v1/Search()` | IP | 3000 / minuto | Buscar paquetes de NuGet a través del extremo de la búsqueda de v1 | 
**GET** `/api/v2/Packages` | IP | 20000 / minuto | Consultar los metadatos de paquete de NuGet a través de OData v2 `Packages` colección | 
**GET** `/api/v2/Packages/$count` | IP | 100 / minuto | Consultar el número de paquetes de NuGet a través de OData v2 `Packages` colección | 

## <a name="package-push-and-unlist"></a>Paquete de inserción y ocultar

| API | Tipo de límite | Valor del límite | APU usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Clave de API | 100 / minuto | Cargar un nuevo paquete de NuGet (versión) a través del extremo de inserción de v2 
**ELIMINAR** `/api/v2/package/{id}/{version}` | Clave de API | 100 / minuto | Ocultar un paquete de NuGet (versión) a través del extremo de v2 
