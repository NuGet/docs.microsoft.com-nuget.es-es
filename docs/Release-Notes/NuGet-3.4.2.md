---
title: "Notas de la versión de NuGet 3.4.2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b514da09-da1f-416b-9bfc-692f08fb6957
description: "Notas de la versión de NuGet 3.4.2 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.4.2 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6761c59b6dc85b9a8503041928c2707549006d9c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-342-release-notes"></a>Notas de la versión de NuGet 3.4.2

[Notas de la versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

Se liberó NuGet 3.4.2 del 8 de abril de 2016 soluciona algunos problemas que se identificaron en el 3.4 y 3.4.1 liberar.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe 3.4.2 RC ya está disponible

Puede descargar la versión release candidate de nuget.exe 3.4.2 [aquí](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Hemos mejorado significativamente el rendimiento de las actualizaciones en un escenario específico, donde las actualizaciones en los paquetes con gráficos de dependencia profunda tardaron mucho tiempo y había bloqueado Visual Studio.
* restauración de NuGet sin tráfico de red es 2,5 x – 3 veces más rápidos en Visual Studio.
* Además de este cambio, se ha corregido un problema donde se estábamos alcanzar la red dos veces cuando la actualización de filas cuentan en la interfaz de usuario de VS. Esto era parcialmente responsable para algunos clientes de problemas de tiempo de espera con experiencia en 3.4/3.4.1.
* Se agregó compatibilidad para la configuración de no_proxy

##<a name="fixes"></a>Correcciones

* Se ha corregido un problema donde nuget.org origen faltaba en valores de configuración de NuGet o configuración después de actualizar a 3.4.1.
* Se ha corregido un problema donde un cambio de mayúsculas y minúsculas en FindPackagesById en 3.4.1 interrumpe Artifactory.
* Se ha corregido un problema con FIPS que produjeron errores con la restauración de NuGet con nuget.exe.
* Se ha corregido un bloqueo al examinar los orígenes de dirección URL de icono no válido.
* Se han corregido los problemas con la combinación de versiones y las entradas de todos los orígenes' de'.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problemas conocidos en 3.4.2 línea de comandos de Windows x86 (RC)

Estos problemas se corregirán primeras semanas siguientes antes de que lleguen a RTM.

*  Ejecutando restauración de nuget en una solución se producirá un error si el archivo de solución se coloca en una jerarquía de carpetas inferior que los archivos de proyecto.
*  Ejecuta el comando de eliminación de nuget en un paquete mediante la fuente V2 se producirá un error. Usar fuentes de distribución de V3 en su lugar.


Para obtener la lista completa de correcciones y mejoras en esta versión, visite la lista de problemas [aquí](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).