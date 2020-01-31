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
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813200"
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

| API | Tipo de límite | Valor límite | API usecase |
|:---|:---|:---|:---|
**Obtener** `/api/v1/Packages` | IP | 1000/minuto | Consulta de metadatos de paquetes NuGet mediante la colección de `Packages` de OData de v1 |
**Obtener** `/api/v1/Search()` | IP | 3000/minuto | Buscar paquetes NuGet a través del punto de conexión de búsqueda v1 | 
**Obtener** `/api/v2/Packages` | IP | 20000/minuto | Consulta de metadatos de paquetes NuGet a través de V2 OData `Packages` colección | 
**Obtener** `/api/v2/Packages/$count` | IP | 100/minuto | Consultar el recuento de paquetes NuGet mediante la colección de `Packages` OData V2 | 

## <a name="package-push-and-unlist"></a>Instalación y deslista de paquetes

| API | Tipo de límite | Valor límite | API usecase | 
|:---|:---|:---|:--- |
**Colocar** `/api/v2/package` | Clave de API | 350 por hora | Carga de un nuevo paquete NuGet (versión) a través del punto de conexión de inserciones V2 
**Eliminar** `/api/v2/package/{id}/{version}` | Clave de API | 250 por hora | Mostrar un paquete NuGet (versión) a través del punto de conexión V2 
