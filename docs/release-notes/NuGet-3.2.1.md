---
title: Notas de la versión de NuGet 3.2.1
description: Notas de la versión de NuGet 3.2.1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776518"
---
# <a name="nuget-321-release-notes"></a>Notas de la versión de NuGet 3.2.1

Notas de la [versión de NuGet 3,2](../release-notes/nuget-3.2.md)  |  [Notas de la versión de NuGet 3,3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 para la línea de comandos se lanzó el 12 de octubre de 2015 con una serie de optimizaciones y correcciones para la versión 3,2 y está disponible en [Dist.Nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Mejoras

* NuGet ahora usa el archivo de configuración con el uso de mayúsculas y minúsculas original de `NuGet.Config` .  Esto es importante en sistemas operativos con distinción de mayúsculas y minúsculas [1427](https://github.com/NuGet/Home/issues/1427)
* La restauración de NuGet ahora pasará por alto los proyectos de DNX ( `*.xproj` ) que deben procesarse con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Uso de red optimizado al trabajar con `index.json` datos de registro de paquetes [1426](https://github.com/NuGet/Home/issues/1426)
* Mejor control de la descarga de recursos para ser más sólido con los servicios V2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correcciones

* La actualización de NuGet actualiza correctamente `.csproj` / `.vcxproj` las referencias [1483](https://github.com/NuGet/Home/issues/1483)
* Ahora se impide que se cree una carpeta local. Nuget cuando no se encuentra SpecialFolders. UserProfile [1531](https://github.com/NuGet/Home/issues/1531)
* Control mejorado de los paquetes en la memoria caché local que están dañados durante la descarga [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Encontrará una lista completa de los problemas que se han solucionado para la extensión de la línea de comandos y de Visual Studio en el hito de GitHub de NuGet [3.2.1](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) .

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que se puede encontrar en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)