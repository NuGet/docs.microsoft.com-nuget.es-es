---
title: Notas de la versión de NuGet 5.10
description: Notas de la versión de NuGet 5.10, incluidas nuevas características, correcciones de errores y DCR.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356504"
---
# <a name="nuget-510-release-notes"></a>Notas de la versión de NuGet 5.10

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio | Disponible en los SDK de .NET |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Instalado</sup> con Visual Studio 2019 con carga de trabajo de .NET Core
  
> [!NOTE]
> Visual Studio 16.10, MSBuild 16.10 y .NET 5.0.300+ NuGet.exe 5.10 o posterior.

## <a name="summary-whats-new-in-510"></a>Resumen: Novedades de la versión 5.10

* Firma: implemente el comando dotnet trusted-signers [- #8053](https://github.com/NuGet/Home/issues/8053)

* Hacer que la validación predeterminada esté deshabilitada en Linux, pero habilitada de forma predeterminada en [Windows: #10713](https://github.com/NuGet/Home/issues/10713)

* Agregar una variable ENV para la comprobación de firma de paquetes en .NET 5+ Linux/MAC: [#10742](https://github.com/NuGet/Home/issues/10742)

* Mejora del rendimiento de la instalación de nuevos paquetes para soluciones de [gran tamaño: #10166](https://github.com/NuGet/Home/issues/10166)

* Agregue el tipo de `nfproj` proyecto a la lista de supportedProjectExtensions para la CLI de Nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

* Suprimir el <requireLicenseAcceptance> elemento al empaquetar un [proyecto: #5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] La advertencia de versión preliminar debe mostrarse en la cli de [dotnet: #10226](https://github.com/NuGet/Home/issues/10226)

* Actualice los tokens de color de fondo y primer plano de PMUI a CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bug Bash] El error "operación cancelada por el usuario" se muestra en la ventana Lista de errores al cambiar rápidamente entre pestañas en la interfaz de usuario de [PM: #10671](https://github.com/NuGet/Home/issues/10671)

* Interfaz de usuario de PM: mejorar el rendimiento de la instalación de paquetes en el nivel de [solución: #10210](https://github.com/NuGet/Home/issues/10210)

* Reemplace GetService por GetServiceAsync en cualquier lugar de NuGet.Clients: [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe de rendimiento del paquete con `..` la ruta de acceso [relativa: #5016](https://github.com/NuGet/Home/issues/5016)

* El rendimiento del "paquete nuget" disminuye con niveles crecientes en las rutas de acceso de [origen: #5706](https://github.com/NuGet/Home/issues/5706)

* NuGet no genera errores al empaquetar nuspec con archivos duplicados. - [#6941](https://github.com/NuGet/Home/issues/6941)

* Paquete NuGet "El dateTimeOffset especificado no se puede convertir en una marca de tiempo de archivo [ZIP": #7001](https://github.com/NuGet/Home/issues/7001)

* Las marcas de tiempo del archivo del paquete empaquetado se desplazan por la zona [horaria: #7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 debe contener información más útil: [#7696](https://github.com/NuGet/Home/issues/7696)

* [Bug Bash] [Error de prueba] El archivo de bloqueo vacío o con formato no debe actualizarse al ejecutar "dotnet restore --use-lock-file --locked-mode": [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange permite analizar intervalos lógicamente incorrectos: [#9145](https://github.com/NuGet/Home/issues/9145)

* La interfaz de usuario de PM no puede mostrar un color de fondo distintivo entre los orígenes de paquetes seleccionados y los que mantienen el [puntero: #9538](https://github.com/NuGet/Home/issues/9538)

* El lector de pantalla no lee la casilla para seleccionar los proyectos en los que se va a [instalar : #9578](https://github.com/NuGet/Home/issues/9578)

* La selección predeterminada del menú desplegable Versiones del panel de detalles debe ser Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)

* Quite la cuenta de solución alternativa para algunos SDK de .NET 5 informe TargetPlatformMoniker de ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget verify es demasiado silencioso: [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange no puede analizar intervalos de un solo [dígito: #10342](https://github.com/NuGet/Home/issues/10342)

* El administrador de soluciones de VS produce una excepción null para durante la [depuración: #10352](https://github.com/NuGet/Home/issues/10352)

* Traslado de mensajes de excepción de la CLI a archivos de recursos de [cadena: #10392](https://github.com/NuGet/Home/issues/10392)

* Quitar código no encontrado (TabItemButtonAutomationPeer): [#10435](https://github.com/NuGet/Home/issues/10435)

* El menú contextual de actualización debe desplazarse hasta el primer elemento [seleccionado: #10498](https://github.com/NuGet/Home/issues/10498)

* Los detalles de PMUI de la solución tienen barras horizontales [superpuestas: #10533](https://github.com/NuGet/Home/issues/10533)

* Firma: los detalles de la firma principal no se muestran cuando el certificado ha expirado y la marca de tiempo no es de [confianza: #10535](https://github.com/NuGet/Home/issues/10535)

* No tener ningún orígenes habilitado impide que se muestre la interfaz de usuario de PM [#10541](https://github.com/NuGet/Home/issues/10541)

* Los metadatos del paquete (detalles, desuso) a veces no se extraen nuget.org en CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)

* Se produce un error en la inicialización de PMUI con una excepción durante la sesión [de depuración: #10559](https://github.com/NuGet/Home/issues/10559)

* La restauración de nuget produce un error de comprobación de integridad del paquete big endian sistema: [#10567](https://github.com/NuGet/Home/issues/10567)

* FormatException se produce en lugar de [PackagingException: #10595](https://github.com/NuGet/Home/issues/10595)

* CPVM: problemas de simultaneidad en el algoritmo de recorrido del [grafo: #10598](https://github.com/NuGet/Home/issues/10598)

* Adición de telemetría de la versión de PowerShell de [PMC: #10609](https://github.com/NuGet/Home/issues/10609)

* Mejora del rendimiento de ordenación de NuGetVersion: [#10611](https://github.com/NuGet/Home/issues/10611)

* Agregar firmantes de confianza tiene argumentos incoherentes: [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v16.9.0: al cambiar las pestañas de NuGet Administrador de paquetes de "Actualizaciones" a "Instalado" no se actualiza el marco. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Quite la "v" del número de versión en PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync inicia antes de recibir la nominación del sistema de proyectos de [CPS: #10681](https://github.com/NuGet/Home/issues/10681)

* Los iconos incrustados provocan el acceso denegado desde el origen "Microsoft Visual Studio sin conexión" en la pestaña [Examinar : #10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService.GetInstalledPackagesAsync inicia cuando MSBuildProjectExtensionsPath no está [establecido: #10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org" no funciona la primera vez: [#10745](https://github.com/NuGet/Home/issues/10745)

* Nuget bloquea un subproceso de grupo de subprocesos en un método asincrónico que realiza una llamada sincrónica al subproceso de interfaz de [usuario: #10775](https://github.com/NuGet/Home/issues/10775)

* Tools -> Options -> NuGet Administrador de paquetes string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` es código no encontrado y daña el [rendimiento: #10790](https://github.com/NuGet/Home/issues/10790)

* Uso del icono incrustado en paquetes del SDK de [NuGet: #10795](https://github.com/NuGet/Home/issues/10795)

* Actualización de la lista de licencias de [SPDX: #10806](https://github.com/NuGet/Home/issues/10806)

**[Lista de todos los problemas corregidos en esta versión: 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Lista de confirmaciones de esta versión: 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Contribuciones de la comunidad

Gracias a todos los colaboradores que ayudaron a que esta versión de NuGet sea impresionante.

|Quién|Prs|Issues|
|----|----|----|
[z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange no puede analizar intervalos de un solo [dígito: #10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet.Client build.sh está roto: [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet.Client build.sh está roto: [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | El rendimiento del "paquete nuget" disminuye con niveles crecientes en las rutas de acceso de [origen: #5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe problema de rendimiento del paquete con . ruta de acceso [relativa: #5016](https://github.com/NuGet/Home/issues/5016)
[marcin-yunsjunto](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM: problemas de simultaneidad en el algoritmo de recorrido del [grafo: #10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Agregue el tipo de proyecto nfproj a la lista de supportedProjectExtensions para la CLI de Nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Bienvenida a los comentarios

Sus comentarios son importantes.  Si hay algún problema con esta versión, consulte los problemas de [GitHub](https://github.com/NuGet/Home/issues) [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) problemas existentes.  Si hay nuevos problemas en NuGet, informe de un [problema de GitHub.](https://github.com/NuGet/Home/issues/new)
Para problemas generales de la experiencia [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) de NuGet, háganoslo saber a través de la opción Notificar un problema que se encuentra en su IDE favorito en Ayuda **> notificar un problema.**
