---
title: Notas de la versión de NuGet 3.2.1
description: Notas de la versión de NuGet 3.2.1 incluidos conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548195"
---
# <a name="nuget-321-release-notes"></a>Notas de la versión de NuGet 3.2.1

[Notas de la versión de NuGet 3.2](../release-notes/nuget-3.2.md) | [notas de la versión de NuGet 3.3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 para la línea de comandos se lanzó el 12 de octubre de 2015 con un puñado de las optimizaciones y las soluciones para la versión 3.2 y está disponible en [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Mejoras

* Ahora, NuGet usa el archivo de configuración con las mayúsculas y minúsculas originales de `NuGet.Config`.  Esto es importante en sistemas operativos distingue mayúsculas de minúsculas [1427](https://github.com/NuGet/Home/issues/1427)
* Restauración de NuGet ahora pasará por alto los proyectos de dnx (`*.xproj`) que deben procesarse con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Optimizado para la utilización de la red cuando se trabaja con `index.json` y datos de registro del paquete [1426](https://github.com/NuGet/Home/issues/1426)
* Descarga de recursos mejorado de control para que sea más sólida con los servicios de v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correcciones

* Actualización de NuGet se actualiza correctamente `.csproj` / `.vcxproj` referencias [1483](https://github.com/NuGet/Home/issues/1483)
* Ahora que impide que una carpeta local .nuget se crea al no encontrar un SpecialFolders.UserProfile [1531](https://github.com/NuGet/Home/issues/1531)
* El control mejorado de los paquetes en la memoria caché local que estén dañados durante la descarga [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Una lista completa de los problemas solucionados para la extensión de línea de comandos y Visual Studio puede encontrarse en NuGet GitHub [3.2.1 hito](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)