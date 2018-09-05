---
title: Notas de la versión de NuGet 3.4.2
description: Notas de la versión para incluir NuGet 3.4.2 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549156"
---
# <a name="nuget-342-release-notes"></a>Notas de la versión de NuGet 3.4.2

[Notas de la versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 se lanzó el 8 de abril de 2016 para resolver varios problemas que se han identificado en la 3.4 y 3.4.1 de versión.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe 3.4.2 RC ya está disponible

Puede descargar la versión release candidate de nuget.exe 3.4.2 [aquí](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Hemos mejorado considerablemente el rendimiento de las actualizaciones en un escenario concreto, donde las actualizaciones en los paquetes con gráficos de dependencia profunda tardaron mucho tiempo y permanece en Visual Studio.
* restauración de NuGet sin que el tráfico de red es 2,5 x – 3 veces más rápido en Visual Studio.
* Además de este cambio, hemos corregido un problema donde nos estábamos alcanzar la red dos veces al recuento de obtención de la actualización en la interfaz de usuario de VS. Esto fue parcialmente responsable de algunos clientes de problemas de tiempo de espera con experiencia en 3.4 y 3.4.1.
* Se ha agregado compatibilidad con la configuración de no_proxy

## <a name="fixes"></a>Correcciones

* Se ha corregido un problema donde el origen de nuget.org faltaba en la configuración de NuGet o la configuración después de actualizar a 3.4.1.
* Se ha corregido un problema donde un cambio de mayúsculas y minúsculas en FindPackagesById en 3.4.1 interrumpe Artifactory.
* Se ha corregido un problema con el estándar FIPS que causaba errores con la restauración de NuGet con nuget.exe.
* Se ha corregido un bloqueo al examinar los orígenes con la dirección URL de icono no válido.
* Se han corregido los problemas con la combinación de versiones y las entradas de todos los orígenes' de'.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problemas conocidos en 3.4.2 Windows x86 Commandline (RC)

Estos problemas se corregirán temprana próxima semana antes de que lleguen a RTM.

*  Ejecución de restauración de nuget en una solución se producirá un error si el archivo de solución se coloca en una jerarquía de carpetas menor que los archivos de proyecto.
*  Ejecutar comando de eliminación de nuget en un paquete con la fuente de V2 se producirá un error. Usar fuente V3 en su lugar.


Para obtener la lista completa de correcciones y mejoras en esta versión, consulte la lista de problemas [aquí](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).