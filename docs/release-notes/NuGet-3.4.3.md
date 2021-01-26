---
title: Notas de la versión de NuGet 3.4.3
description: Notas de la versión de 3.4.3 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776472"
---
# <a name="nuget-343-release-notes"></a>Notas de la versión de NuGet 3.4.3

Notas de la [versión de NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Notas de la versión de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 se lanzó el 22 de abril de 2016 para solucionar varios problemas que se identificaron en las versiones 3,4 y posteriores.

Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Confiabilidad mejorada de Visual Studio. Hemos corregido algunos problemas en NuGet que causaron bloqueos en Visual Studio.

## <a name="fixes"></a>Correcciones

* Se corrigieron algunos problemas de autorización con las fuentes de Nuget privadas protegidas por contraseña.
* Se ha corregido un problema por el que no se podía restaurar PCL desde `project.json` con los tiempos de ejecución especificados.
* Algunos clientes estaban ejecutando errores intermitentes al instalar paquetes. Esto se ha corregido en esta versión.
* Se corrigió un problema que provocaba errores de restauración en proyectos de C++/CLI con `project.json` .
* Algunos paquetes (por ejemplo, ModernHttpClient) donde no se descomprimen correctamente cuando se usa Nuget en mono. Esto se ha corregido en esta versión.

Para obtener una lista completa de correcciones y mejoras en esta versión, consulte la lista de problemas [aquí](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).