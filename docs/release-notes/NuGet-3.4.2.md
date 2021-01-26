---
title: Notas de la versión de NuGet 3.4.2
description: Notas de la versión de 3.4.2 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780247"
---
# <a name="nuget-342-release-notes"></a>Notas de la versión de NuGet 3.4.2

Notas de la [versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 se lanzó el 8 de abril de 2016 para solucionar varios problemas que se identificaron en la versión 3,4 y 3.4.1.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC ya está disponible

Puede descargar el candidato de versión comercial de nuget.exe 3.4.2 [aquí](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Hemos mejorado considerablemente el rendimiento de las actualizaciones en un escenario específico, en el que las actualizaciones de los paquetes con gráficos de dependencias profundos tardan mucho tiempo y no responden a Visual Studio.
* la restauración de Nuget sin tráfico de red es 2,5 x – tres veces más rápida en Visual Studio.
* Además de este cambio, se ha corregido un problema por el que hemos alcanzado la red dos veces al capturar el número de actualizaciones en la interfaz de usuario de VS. Esto era responsable parcialmente de algunos problemas de tiempo de espera que los clientes experimentaron en 3.4/3.4.1.
* Compatibilidad agregada para la configuración de no_proxy

## <a name="fixes"></a>Correcciones

* Se corrigió un problema en el que faltaba el origen de nuget.org en la configuración de NuGet o la configuración después de actualizar a 3.4.1.
* Se corrigió un problema por el que un cambio de mayúsculas y minúsculas en FindPackagesById en 3.4.1 rompe Artifactory.
* Se corrigió un problema con FIPS que causó errores con la restauración de NuGet con nuget.exe.
* Se corrigió un bloqueo al examinar orígenes con una dirección URL de icono no válida.
* Se han corregido problemas con la combinación de versiones y entradas de "todos los orígenes".

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problemas conocidos de 3.4.2 Windows x86 CommandLine (RC)

Estos problemas se corregirán antes de la próxima semana antes de que llegue el RTM.

*  La ejecución de la restauración de Nuget en una solución producirá un error si el archivo de solución se coloca en una jerarquía de carpetas inferior a la de los archivos de proyecto.
*  Se producirá un error al ejecutar el comando DELETE de Nuget en un paquete con la fuente V2. En su lugar, utilice la fuente V3.


Para obtener una lista completa de correcciones y mejoras en esta versión, consulte la lista de problemas [aquí](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).