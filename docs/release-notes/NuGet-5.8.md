---
title: Notas de la versión de NuGet 5,8
description: Notas de la versión de NuGet 5,8, incluidas nuevas características, correcciones de errores y DCR.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 7f641c669cdb0cc979d698f6b219cbb4f2692a2e
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235755"
---
# <a name="nuget-58-release-notes"></a>Notas de la versión de NuGet 5,8

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio | Disponible en los SDK de .NET |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 versión 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1</sup> instalado con Visual Studio 2019 con la carga de trabajo de .net Core
  
> [!NOTE]
> Visual Studio 16,8, MSBuild 16,8 y .NET 5,0 requieren NuGet.exe 5,8 o posterior.


## <a name="summary-whats-new-in-58"></a>Resumen: novedades en 5,8
🎉 **esta es la primera versión para ofrecer compatibilidad completa con la creación y restauración de paquetes NuGet que tienen como destino .net 5,0** 🎉

* Acelerar la extracción de nupkg con mmap/CreateFileMapping- [#9807](https://github.com/NuGet/Home/issues/9807)

* Mostrar detalles de vulnerabilidad del paquete en el panel de detalles del paquete de interfaz de usuario del administrador de paquetes- [#9850](https://github.com/NuGet/Home/issues/9850)

* Comprobar los paquetes de NuGet firmados con el nuevo [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) comando: [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) admite `--prerelease` la opción para agregar la versión más reciente de un paquete, incluidas versiones preliminares: [#4699](https://github.com/NuGet/Home/issues/4699)

* Buscar paquetes en la CLI con el [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) comando [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) el comando admite `--verbosity` la opción [#9600](https://github.com/NuGet/Home/issues/9600)

* Habilitación de la optimización de restauración rápida No-Op para proyectos basados en PackageReference con estilo csproj en Visual Studio- [#9565](https://github.com/NuGet/Home/issues/9565)

* Las operaciones de la interfaz de usuario del administrador de paquetes de nivel de solución, como las instalaciones y actualizaciones de paquetes, son hasta 10 veces más rápidas: [#6010](https://github.com/NuGet/Home/issues/6010)

* Otras mejoras de rendimiento de NuGet en Visual Studio: [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**DCR**

* .NET 5,0 TFM: reglas de prioridad de marco de trabajo- [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet no debe deducir la versión de la plataforma de puntos al analizar TargetFramework- [#9842](https://github.com/NuGet/Home/issues/9842)

* Use TargetFrameworkMoniker & TargetPlatformMoniker para inferir los marcos de trabajo en lugar de usar las propiedades individuales TFI, TFV, TPI, TPV- [#9895](https://github.com/NuGet/Home/issues/9895)

* Actualización `GetReferenceNearestTargetFrameworkTask()` para admitir las versiones de .NET Framework de destino con plataformas (como net 5.0-Windows)- [#9894](https://github.com/NuGet/Home/issues/9894)

* API de .NET 5,0 de Visual Studio: [#9650](https://github.com/NuGet/Home/issues/9650)

* Interfaz de usuario del administrador de paquetes: las operaciones de consolidación o actualización de paquetes no deben bloquearse debido a errores (degradación de paquetes, etc.)- [#9224](https://github.com/NuGet/Home/issues/9224)

* Las características de NuGet deberían aclararse en los proyectos que tienen la capacidad; "PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)

* Suprimir No-Op restaurar mensajes en Visual Studio- [#6384](https://github.com/NuGet/Home/issues/6384)

**Detectar**

* No se debe llamar al constructor OutputWindowTextWriter en el subproceso en segundo plano: [#9764](https://github.com/NuGet/Home/issues/9764)

* Restauración de paquetes firmados en CPU Big Endian: [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger no debe llamar a métodos afinidad con en constructores MEF: [#9591](https://github.com/NuGet/Home/issues/9591)

* Error en el método NuGet. CommandLine. Console `PrintJustified()` : [#9737](https://github.com/NuGet/Home/issues/9737)

* Pérdida de memoria de la interfaz de usuario del administrador de paquetes cuando los metadatos del paquete se recolectan como elementos no utilizados debido a un enlace incorrecto [#9757](https://github.com/NuGet/Home/issues/9757)

* Firme No se muestra ninguna advertencia en Lista de errores al instalar un paquete firmado con packages.config formato en la interfaz de usuario del administrador de paquetes [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine. XPlat no debe tener API públicas: [#9821](https://github.com/NuGet/Home/issues/9821)

* Reduzca la contención de recursos en el tiempo de carga de la solución debido al bloqueo de un subproceso de grupo de subprocesos con `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* En la restauración de la línea de comandos, con proyectos de varios destinos, NuGet debe leer la información relacionada con la versión de .NET Framework de destino desde la compilación interna- [#9869](https://github.com/NuGet/Home/issues/9869)

* Leer el gráfico de identificador en tiempo de ejecución mediante el elemento TargetFrameworkInformation- [#9874](https://github.com/NuGet/Home/issues/9874)

* La restauración de gráficos estáticos es incoherente con respecto a la propiedad multidestino en comparación con Visual Studio y con la restauración de evaluación de MSBuild normal: [#9881](https://github.com/NuGet/Home/issues/9881)

* En la restauración de gráficos estáticos, con proyectos de destino múltiples, NuGet debe leer la información relacionada con la versión de .NET Framework de destino de la compilación interna. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Permitir `net5.0-platform` la carga y restauración de proyectos en Visual Studio: [#9863](https://github.com/NuGet/Home/issues/9863)

* Mostrar la versión resuelta en la interfaz de usuario del administrador de paquetes- [#9826](https://github.com/NuGet/Home/issues/9826)

* Interfaz de usuario del administrador de paquetes: Explorador de soluciones no muestra todas las dependencias del paquete NuGet- [#9898](https://github.com/NuGet/Home/issues/9898)

* Actualización de la lista de licencias de SPDX: [#9946](https://github.com/NuGet/Home/issues/9946)

* VS 2019 se bloquea después de abrir administrar paquetes NuGet: el icono produce una excepción no controlada en la imagen conversio- [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Packaging. distract necesita ILMerge para excluir Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)

* No se producirá un error al empaquetar con ContinuePackingAfterGeneratingNuspec = false cuando no haya errores: [#9786](https://github.com/NuGet/Home/issues/9786)

* Interfaz de usuario del administrador de paquetes: los iconos no invierten los colores correctamente [#10017](https://github.com/NuGet/Home/issues/10017)

* Recuentos de proyectos incorrectos para los proyectos actualizados y No-Op en restore- [#10026](https://github.com/NuGet/Home/issues/10026)

* `/p:RestoreUseStaticGraphEvaluation=true`El uso de los resultados en un valor no puede ser NULL: [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` usa erróneamente el alias para proyectos de biblioteca de WPF: [#10020](https://github.com/NuGet/Home/issues/10020)

* Interfaz de usuario del administrador de paquetes: NullReferenceException cuando se produce un error de validación de firma- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: no usar `object` el tipo para los valores de metadatos del proyecto- [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: el almacenamiento de orígenes de paquetes en las opciones de herramientas sobrescribirá las credenciales: [#9711](https://github.com/NuGet/Home/issues/9711)


**[Lista de todos los problemas corregidos en esta versión: 5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Lista de problemas en esta versión: 5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Contribuciones de la comunidad

Gracias por todos los colaboradores que le han ayudado a hacer que esta versión de NuGet sea impresionante.

|Quién|Incorporación|Incidencias|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Error tipográfico en el mensaje de error. "hizo" en lugar de "administrador"- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | Paquete de NuGet con informes AssemblyInformationalVersion no válidos "se requiere la descripción"- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` no tiene en cuenta las propiedades de rama y confirmación: [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Al hacer clic en el código nu en Visual Studio lista de errores ventana debe ir a https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Use ' https://' cuando agregue un nuevo origen de paquete a través de opciones de Visual Studio: [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problema de rendimiento en mono- [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Agregue un TypeConverter para la clase SemanticVersion: [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Resumen: novedades de 5.8.1

* packages.config package.lock.jsen utiliza una versión de .NET Framework de destino incorrecta en 5,8- [#10257](https://github.com/NuGet/Home/issues/10257)

* 5,8 + 16,8 no puede resolver dependencias de proyecto transitivas al mezclar PackageReference y packages.config- [#10326](https://github.com/NuGet/Home/issues/10326)

**[Lista de todos los problemas corregidos en esta versión: 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Lista de confirmaciones en esta versión: 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Página principal de comentarios

Sus comentarios son importantes.  Si hay algún problema con esta versión, consulte los problemas de [GitHub](https://github.com/NuGet/Home/issues) y la [comunidad de desarrolladores de Visual Studio](https://developercommunity.visualstudio.com/) para ver los problemas existentes.  Para nuevos problemas en NuGet, informe de un [problema de github](https://github.com/NuGet/Home/issues/new).
En el caso de problemas generales de la experiencia de NuGet, háganoslo saber a través de la opción [notificar un problema](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) que se encuentra en su IDE favorito en **ayuda > notificar un problema**.
