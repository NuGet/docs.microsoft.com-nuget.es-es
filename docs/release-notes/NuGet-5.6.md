---
title: Notas de la versión de NuGet 5,6
description: Notas de la versión de NuGet 5,6, incluidas nuevas características, correcciones de errores y DCR.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727810"
---
# <a name="nuget-56-release-notes"></a>Notas de la versión de NuGet 5,6

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio| Disponible en los SDK de .NET|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 versión 16.6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core

## <a name="summary-whats-new-in-56"></a>Resumen: novedades en 5,6

* Compatibilidad con paquetes de versión preliminar con versiones flotantes. `Version="*-*"`, `Version="1.*-*"` y son similares a las versiones más recientes, incluidas las versiones preliminares, dentro del intervalo especificado: [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Detectar**

* `nuget push *.nupkg`se produce un error cuando snupkg no existe: [#8148](https://github.com/NuGet/Home/issues/8148)

* Pack, y otras rutas de acceso de código, que no dependen de la configuración regional. Usar RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* Rendimiento: la especificación de DG para escenarios de proyecto descargados no se debe escribir en las restauraciones de vista previa: [#8793](https://github.com/NuGet/Home/issues/8793)

* Restauración: mejorar el rendimiento mediante el almacenamiento en caché del gráfico de dependencias de la solución- [#9201](https://github.com/NuGet/Home/issues/9201)

* La interfaz de usuario de PM no funciona para los proyectos de estilo SDK después de instalar un paquete con la consola PM- [#9203](https://github.com/NuGet/Home/issues/9203)

* No se puede mostrar el icono incrustado en la interfaz de usuario de PM con la fuente de paquetes local, dependiendo de/vs \ [#9225](https://github.com/NuGet/Home/issues/9225)

* NuGetVersion. TryParseStrict () debe devolver false si no se puede analizar- [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`ayuda para `-source` , debe sugerir el uso del nombre de origen, no de la dirección URL de origen- [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`crea un nombre de origen de paquete predeterminado incorrecto: [#9277](https://github.com/NuGet/Home/issues/9277)

* El lector de pantalla no anuncia "buscando..." mensaje al cambiar de pestañas: [#9307](https://github.com/NuGet/Home/issues/9307)

* Accesibilidad: el color del rectángulo de foco no es accesible CP pestañas de la interfaz de usuario en el tema oscuro: [#9336](https://github.com/NuGet/Home/issues/9336)

* Nuget. exe 5,5 no se puede restaurar con MSBuild 14 o inferior [#9458](https://github.com/NuGet/Home/issues/9458)

* No registrar las horas de milisegundos en los mensajes de restauración: [#8977](https://github.com/NuGet/Home/issues/8977)

* Crear IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)

* La selección de versiones de MSBuild funciona mal en algunas culturas que no están en inglés, [#9322](https://github.com/NuGet/Home/issues/9322)

* Falta el formato predeterminado en `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Rendimiento: RestoreOperationLogger tiene afinidad de subprocesos innecesarias- [#9288](https://github.com/NuGet/Home/issues/9288)

* Creación automatizada de documentos para `dotnet nuget` comandos- [#9146](https://github.com/NuGet/Home/issues/9146)

* El nivel de detalle predeterminado no debe notificar la restauración de NOOP del proyecto [#8792](https://github.com/NuGet/Home/issues/8792)

* `-DependencyVersion`Parámetro de compatibilidad para `NuGet.exe update` , similar a [#7694](https://github.com/NuGet/Home/issues/7694) de comandos de instalación


**DCR**

* Agregar compatibilidad inicial para el marco de destino de .net 5.0: [#9584](https://github.com/NuGet/Home/issues/9584)

* Ordenar paquetes por identificador en la pestaña actualizaciones de la interfaz de usuario de PM- [#9278](https://github.com/NuGet/Home/issues/9278)


**[Lista de todos los problemas corregidos en esta versión: 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
