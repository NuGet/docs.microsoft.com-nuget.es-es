---
title: Notas de la versión 2.9 RC de NuGet
description: Notas de la versión de NuGet 2.9 RC incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548329"
---
# <a name="nuget-29-rc-release-notes"></a>Notas de la versión 2.9 RC de NuGet

[Notas de la versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [notas de la versión de NuGet 3.0 versión preliminar](../release-notes/nuget-3.0-preview.md)

2.9 de NuGet se lanzó el 10 de septiembre de 2015 como una actualización de la 2.8.7 VSIX para Visual Studio 2012 y 2013.

### <a name="updates-in-this-release"></a>Actualizaciones de esta versión

* Ahora omitiendo el procesamiento de paquetes si sus contenidos `.nuspec` documento tiene un formato incorrecto: [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Se ha corregido el control multipartwebrequest de \r\n para escenarios de Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Se ha corregido la integración con los eventos de compilación en las ediciones de Visual Studio Community 2013 - [1180](https://github.com/NuGet/Home/issues/1180)


La lista completa de las correcciones de esta versión se puede encontrar en GitHub en el [2.8.8 hito](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
