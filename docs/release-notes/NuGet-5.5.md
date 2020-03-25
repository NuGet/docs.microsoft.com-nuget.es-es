---
title: Notas de la versión de NuGet 5,5
description: Notas de la versión de NuGet 5,5, incluidas nuevas características, correcciones de errores y DCR.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148286"
---
# <a name="nuget-55-release-notes"></a>Notas de la versión de NuGet 5,5

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio| Disponible en los SDK de .NET|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 versión 16,5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core

## <a name="summary-whats-new-in-55"></a>Resumen: novedades en 5,5

* Experiencia mejorada de accesibilidad y lector de pantalla para la interfaz de usuario del administrador de paquetes NuGet en Visual Studio
    * Problemas de accesibilidad en experiencias del lector de pantalla, falta altText y el nombre accesible para el cuadro de texto instalado, etc.,- [#9059](https://github.com/NuGet/Home/issues/9059)
    * Problemas de accesibilidad en las experiencias del lector de pantalla en la lista de paquetes- [#9077](https://github.com/NuGet/Home/issues/9077)
    * Problemas de accesibilidad en las experiencias del lector de pantalla relacionadas con las pestañas "examinar", "instalar", "actualizar" [#9078](https://github.com/NuGet/Home/issues/9078)
    * El narrador no anuncia la etiqueta de vínculo "Blank", "no dependencies", "Nuget. org", "MIT" [#9157](https://github.com/NuGet/Home/issues/9157)

* Compatibilidad con la exposición de iconos independientes en la interfaz de usuario del administrador de paquetes de Visual Studio para paquetes hospedados en fuentes locales: [#8189](https://github.com/NuGet/Home/issues/8189)

* Rendimiento de restauración no operativa significativamente mejorado mediante `RestoreUseStaticGraphEvaluation` que acelera las evaluaciones mediante una llamada a las API de grafos estáticos de MSBuild- [8791](https://github.com/NuGet/Home/issues/8791)

* Confiabilidad mejorada de dotnet. exe con complementos de autenticación multiplataforma
    * error de dotnet restore con TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)
    * Complemento: "se canceló una tarea"-problema con la autenticación de ADO debido a esto. - [#8528](https://github.com/NuGet/Home/issues/8528)

* Agregar `dotnet nuget <add|remove|update|disable|enable|list> source` [#4126](https://github.com/NuGet/Home/issues/4126) de comandos

* Compatibilidad con para `--skip-duplicate` mediante el [#8778](https://github.com/NuGet/Home/issues/8778) de extracción de Nuget de dotnet

* Compatibilidad `packages.config` con MSBuild/restore- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Errores**

* Actualización automática del trabajo con las API de V3: [#4197](https://github.com/NuGet/Home/issues/4197)

* Versión de dependencia de paquete incorrecta si la versión de dependencia del paquete está establecida en ' * '- [#6697](https://github.com/NuGet/Home/issues/6697)

* El mensaje de error ErrorUnsafePackageEntry no está señalando el origen del problema [#7505](https://github.com/NuGet/Home/issues/7505)

* No se respeta el archivo de bloqueo en escenarios "*": [#8073](https://github.com/NuGet/Home/issues/8073)

* NuGet. exe no se resuelve como la versión más reciente de un paquete cuando se usa * en PackageReference (MSBuild/dotnet/VS restore do)- [#8432](https://github.com/NuGet/Home/issues/8432)

* paquete dotnet List con varios destinos de proyecto de WPF: [#8463](https://github.com/NuGet/Home/issues/8463)

* Mejorar ConcurrencyUtilities (reducir el uso de CPU)- [#8653](https://github.com/NuGet/Home/issues/8653)

* Las especificaciones de DG para escenarios de proyecto descargados no se deben escribir en las restauraciones de vista previa: [#8793](https://github.com/NuGet/Home/issues/8793)

* Los paquetes NuGet de Visual Studio (RestoreManagerPackage) deben cargarse automáticamente en eventos de compilación de la solución: [#8796](https://github.com/NuGet/Home/issues/8796)

* Interbloqueo en VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)

* El cuadro de herramientas de VisualStudio no se rellena desde un paquete NuGet si un proyecto se coloca en una carpeta de soluciones: [#8868](https://github.com/NuGet/Home/issues/8868)

* VS: la restauración de la solución no se realiza de forma perpetua debido a la condición de carrera: [#8881](https://github.com/NuGet/Home/issues/8881)

* Constante "cargando..." en la pestaña instalado y "buscando <term>.. "en la pestaña actualizaciones: [#8890](https://github.com/NuGet/Home/issues/8890)

* Faltan iconos incrustados en la interfaz de usuario de VS PM después de que expire la caché- [#9069](https://github.com/NuGet/Home/issues/9069)

* Inicio de la interfaz de usuario de FireAndForget PM- [#9112](https://github.com/NuGet/Home/issues/9112)

* La implementación de restore: IncludeExcludeFiles. Equals (...) es incorrecta- [#9167](https://github.com/NuGet/Home/issues/9167)

* Restore: PackageSpec. Clone () crea un clon distinto de [#9211](https://github.com/NuGet/Home/issues/9211)

* La lista de errores se muestra aunque "Mostrar siempre Lista de errores si la compilación termina con errores" no está activada- [#8190](https://github.com/NuGet/Home/issues/8190)

* La restauración de gráficos estáticos no debe pasar SolutionPath vacío- [#9061](https://github.com/NuGet/Home/issues/9061)

* Restore: cierre calculado para cada proyecto 4 veces: [#9042](https://github.com/NuGet/Home/issues/9042)

* Restore: DependencyGraphSpec. Load (...) no necesita JObject- [#9040](https://github.com/NuGet/Home/issues/9040)

* Restore: cadenas grandes creadas en el montón de objetos grandes (montón)- [#9031](https://github.com/NuGet/Home/issues/9031)

* El archivo Nuget. exe personalizado en mono más reciente podría interrumpirse debido a la resolución del SDK de MSBuild- [8848](https://github.com/NuGet/Home/issues/8848)

* se produce un error en la restauración cuando Nuget. dgspec. JSON es "usado por otro proceso"- [8692](https://github.com/NuGet/Home/issues/8692)

**DCR**

* La lógica de _GetRestoreProjectStyle debe estar en una tarea- [#8804](https://github.com/NuGet/Home/issues/8804)

* Agregar información de desuso de forma predeterminada en la pestaña instalado [#8541](https://github.com/NuGet/Home/issues/8541)

**[Lista de todos los problemas corregidos en esta versión: 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
