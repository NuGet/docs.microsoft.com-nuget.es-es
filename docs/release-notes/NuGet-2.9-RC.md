---
title: Notas de la versión de NuGet 2,9-RC
description: Notas de la versión de NuGet 2,9 RC, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780316"
---
# <a name="nuget-29-rc-release-notes"></a>Notas de la versión de NuGet 2,9-RC

Notas de la [versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)  |  [Notas de la versión de NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)

NuGet 2,9 se lanzó el 10 de septiembre de 2015 como una actualización de 2.8.7 VSIX para Visual Studio 2012 y 2013.

### <a name="updates-in-this-release"></a>Actualizaciones en esta versión

* Omitiendo ahora los paquetes de procesamiento si su `.nuspec` documento contenido tiene un formato incorrecto- [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Se corrigió el control de multipartwebrequest de \r\n para escenarios de UNIX/Linux: [776](https://github.com/NuGet/Home/issues/776)
* Se corrigió la integración con eventos de compilación en Visual Studio 2013 Community Edition- [1180](https://github.com/NuGet/Home/issues/1180)


La lista completa de correcciones de esta versión se puede encontrar en GitHub en el [hito 2.8.8](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
