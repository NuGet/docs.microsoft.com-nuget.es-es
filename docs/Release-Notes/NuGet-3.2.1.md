---
title: "Notas de la versión de NuGet 3.2.1 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.2.1 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.2.1 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c9c2457c33eb3630f632c98bf0cf96703c3a548
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-321-release-notes"></a>Notas de la versión de NuGet 3.2.1

[Notas de la versión 3.2 de NuGet](../release-notes/nuget-3.2.md) | [notas de la versión 3.3 de NuGet](../release-notes/nuget-3.3.md)

NuGet 3.2.1 para la línea de comandos se publicó el 12 de octubre de 2015 con una serie de optimizaciones y soluciones para la versión 3.2 y está disponible en [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Mejoras

* NuGet ahora usa el archivo de configuración con las mayúsculas y minúsculas original de `NuGet.Config`.  Esto es importante en sistemas operativos entre mayúsculas y minúsculas [1427](https://github.com/NuGet/Home/issues/1427)
* Restauración de NuGet ahora hará caso omiso de proyectos dnx (`*.xproj`) que debe procesarse con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Optimiza el uso de la red cuando se trabaja con `index.json` y datos de registro del paquete [1426](https://github.com/NuGet/Home/issues/1426)
* Descarga de recursos mejorado controlan para ser más eficaces con los servicios de v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correcciones

* Actualización de NuGet se actualiza correctamente `.csproj` / `.vcxproj` referencias [1483](https://github.com/NuGet/Home/issues/1483)
* Ahora que impide que una carpeta .nuget local se crea cuando no se encuentra un SpecialFolders.UserProfile [1531](https://github.com/NuGet/Home/issues/1531)
* El control mejorado de paquetes en la memoria caché local que se hayan dañado durante la descarga [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Una lista completa de temas que se tratan de la extensión de línea de comandos y Visual Studio se encuentran en NuGet GitHub [3.2.1 hito](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)