---
title: Notas de la versión de NuGet 3.4.3
description: Notas de la versión para incluir NuGet 3.4.3 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549170"
---
# <a name="nuget-343-release-notes"></a>Notas de la versión de NuGet 3.4.3

[Notas de la versión de NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [notas de la versión de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 se lanzó el 22 de abril de 2016 para resolver varios problemas que se identificaron en las versiones 3.4 y posteriores.

Puede descargar el VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Confiabilidad mejorada de Visual Studio. Hemos corregido algunos problemas de NuGet que provocar bloqueos en Visual Studio.

## <a name="fixes"></a>Correcciones

* Se ha corregido algunos problemas de autorización con nuget privado protegido con contraseña las fuentes de distribución.
* Se corrigió un problema en torno a la que no se pueda restaurar PCL desde `project.json` con tiempos de ejecución especificado.
* Algunos clientes se estaban ejecutando en errores intermitentes al instalar paquetes. Esto ahora se ha solucionado en esta versión.
* Se corrigió un problema que causaba errores de restauración en C / c++ / CLI proyectos con `project.json`.
* Algunos paquetes (p. ej. ModernHttpClient) donde no descomprimido correctamente al usar nuget en mono. Esto ahora se ha solucionado en esta versión.

Para obtener la lista completa de correcciones y mejoras en esta versión, consulte la lista de problemas [aquí](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).