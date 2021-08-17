---
title: NuGet de la versión 5.8
description: Notas de la versión NuGet 5.8, incluidas nuevas características, correcciones de errores y DCR.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: fca9d2d068aadec207bfbf12f3ea82af872825a5
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209935"
---
# <a name="nuget-58-release-notes"></a>NuGet de la versión 5.8

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio | Disponible en los SDK de .NET |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.8](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1 Instalado</sup> con Visual Studio 2019 con la carga de trabajo de .NET Core
  
> [!NOTE]
> Visual Studio 16.8, MSBuild 16.8 y .NET 5.0 requieren NuGet.exe 5.8 o posterior.


## <a name="summary-whats-new-in-58"></a>Resumen: Novedades de la versión 5.8
🎉 esta es la primera versión que ofrece compatibilidad completa con la creación y restauración de paquetes NuGet que tienen como destino **.NET 5.0** 🎉

* Acelerar la extracción de nupkg mediante mmap/CreateFileMapping [- #9807](https://github.com/NuGet/Home/issues/9807)

* Mostrar los detalles de vulnerabilidad del paquete en el panel Administrador de paquetes detalles del paquete de interfaz de usuario: [#9850](https://github.com/NuGet/Home/issues/9850)

* Compruebe los paquetes NuGet firmados con el [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) nuevo comando [: #8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) admite `--prerelease` la opción para agregar la versión más reciente de un paquete, incluidas las versiones preliminares: [#4699](https://github.com/NuGet/Home/issues/4699)

* Búsqueda de paquetes en la CLI [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) con el comando : [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) command admite `--verbosity` la opción : [#9600](https://github.com/NuGet/Home/issues/9600)

* Habilitar la optimización No-Op de restauración rápida para proyectos basados en PackageReference de estilo csproj en Visual Studio - [#9565](https://github.com/NuGet/Home/issues/9565)

* Las operaciones de Administrador de paquetes de interfaz de usuario, como las actualizaciones y las instalaciones de paquetes, son hasta 10 veces más [rápidas: #6010](https://github.com/NuGet/Home/issues/6010)

* Otras NuGet mejoras de rendimiento en Visual Studio - [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**DCR:**

* TFM de .NET 5.0: reglas de precedencia de marco [- #9436](https://github.com/NuGet/Home/issues/9436)

* NuGet inferir la versión de la plataforma de puntos al analizar TargetFramework: [#9842](https://github.com/NuGet/Home/issues/9842)

* Use TargetFrameworkMoniker & TargetPlatformMoniker para deducir los marcos en lugar de usar propiedades TFI, TFV, TPI y TPV [individuales: #9895](https://github.com/NuGet/Home/issues/9895)

* Actualización `GetReferenceNearestTargetFrameworkTask()` para admitir marcos de destino con plataformas (como net5.0-windows): [#9894](https://github.com/NuGet/Home/issues/9894)

* API de Visual Studio .NET 5.0: [#9650](https://github.com/NuGet/Home/issues/9650)

* Administrador de paquetes Interfaz de usuario: las operaciones de consolidación o actualización de paquetes no deben bloquearse debido a errores (degradación de paquetes, etc.): [#9224](https://github.com/NuGet/Home/issues/9224)

* NuGet características deben encenderse para los proyectos que tienen la funcionalidad; "PackageReferences": [#9957](https://github.com/NuGet/Home/issues/9957)

* Suprimir No-Op restaurar mensajes en Visual Studio : [#6384](https://github.com/NuGet/Home/issues/6384)

**bugs:**

* No se debe llamar al constructor OutputWindowTextWriter en el subproceso en segundo [plano: #9764](https://github.com/NuGet/Home/issues/9764)

* Restauración de paquetes firmados en CPU de Big [Endian: #9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger no debe llamar a métodos afinitized en constructores [MEF: #9591](https://github.com/NuGet/Home/issues/9591)

* Error en NuGet. Método CommandLine.Console: `PrintJustified()` [#9737](https://github.com/NuGet/Home/issues/9737)

* Administrador de paquetes Pérdida de memoria de la interfaz de usuario cuando los metadatos del paquete se recopilan como elementos no utilizados debido a un enlace [no #9757](https://github.com/NuGet/Home/issues/9757)

* [Firma] No se muestra ninguna advertencia en la lista de errores al instalar un paquete firmado con packages.config en Administrador de paquetes ui - [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine.XPlat no debe tener API públicas: [#9821](https://github.com/NuGet/Home/issues/9821)

* Reducir la contención de recursos en tiempo de carga de la solución debido al bloqueo de un subproceso de grupo de subprocesos `BlockingCollection.Take()`  -  [con #9822](https://github.com/NuGet/Home/issues/9822)

* En la restauración de la línea de comandos, con proyectos de varios destinos, NuGet debe leer la información relacionada con el marco de destino de la compilación [interna: #9869](https://github.com/NuGet/Home/issues/9869)

* Leer el gráfico de identificador de tiempo de ejecución a través del elemento TargetFrameworkInformation [: #9874](https://github.com/NuGet/Home/issues/9874)

* La restauración de grafos estáticos es incoherente con respecto a la propiedad CrossTargeting en comparación con la restauración de Visual Studio y la MSBuild de evaluación periódica [: #9881](https://github.com/NuGet/Home/issues/9881)

* En la restauración de grafos estáticos, con proyectos de varios destinos, NuGet debe leer la información relacionada con el marco de destino de la compilación interna. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Permitir `net5.0-platform` la carga y restauración de proyectos en Visual Studio : [#9863](https://github.com/NuGet/Home/issues/9863)

* Mostrar la versión resuelta en la interfaz de usuario Administrador de paquetes : [#9826](https://github.com/NuGet/Home/issues/9826)

* Administrador de paquetes Interfaz de usuario: Explorador de soluciones no muestra todas las dependencias NuGet paquetes : [#9898](https://github.com/NuGet/Home/issues/9898)

* Actualización de la lista de licencias de [SPDX: #9946](https://github.com/NuGet/Home/issues/9946)

* VS 2019 se bloquea después de abrir Administrar paquetes NuGet: el icono provoca una excepción no controlada en image conversio - [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Packaging.Extraction necesita ilmerge para excluir Newtonsoft.Jsen : [#9966](https://github.com/NuGet/Home/issues/9966)

* El empaquetado con ContinuePackingAfterGeneratingNuspec=false no debe producir un error cuando no hay errores: [#9786](https://github.com/NuGet/Home/issues/9786)

* Administrador de paquetes Interfaz de usuario: los iconos no invierten colores correctamente: [#10017](https://github.com/NuGet/Home/issues/10017)

* Recuentos de proyectos incorrectos para proyectos actualizados y No-Op en Restauración [- #10026](https://github.com/NuGet/Home/issues/10026)

* El `/p:RestoreUseStaticGraphEvaluation=true` uso de resultados en el valor no puede ser [null: #9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` usa por error alias para proyectos de biblioteca de [WPF: #10020](https://github.com/NuGet/Home/issues/10020)

* Administrador de paquetes Interfaz de usuario: NullReferenceException cuando se produce un error en la validación de [firmas: #10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: no use el tipo `object` para los valores de metadatos del [proyecto: #10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: guardar los orígenes de paquetes en las opciones de herramientas sobrescribirá las [credenciales #9711](https://github.com/NuGet/Home/issues/9711)


**[Lista de todos los problemas corregidos en esta versión: 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Lista de problemas de esta versión: 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Contribuciones de la comunidad

Gracias a todos los colaboradores que ayudaron a que este NuGet lanzamiento sea impresionante.

|Quién|Prs|Issues|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Error tipográfico en el mensaje de error. "administator" en lugar de ["administrador": #9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | NuGet Empaquetado con informes de AssemblyInformationalVersion no válidos "se requiere [descripción": #5548](https://github.com/NuGet/Home/issues/5548)
[yau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` no tiene en cuenta las propiedades Branch y Commit [: #9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Al hacer clic en código NU Visual Studio ventana Lista de errores debe ir [https://docs.microsoft.com/nuget/reference/errors-and-warnings/](/nuget/reference/errors-and-warnings/)  -  [a #9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Use "https://" al agregar un nuevo origen de paquete mediante Visual Studio opciones [de](https://github.com/NuGet/Home/issues/9974) #9974
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problema de rendimiento en [Mono: #9989](https://github.com/NuGet/Home/issues/9989)
[thomasovesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Agregar un TypeConverter para la clase SemanticVersion [: #9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Resumen: Novedades de la versión 5.8.1

* packages.config package.lock.jsen usa una plataforma de destino incorrecta en 5.8 [- #10257](https://github.com/NuGet/Home/issues/10257)

* 5.8 + 16.8 No se pueden resolver las dependencias transitivas del proyecto al combinar PackageReference y packages.config - [#10326](https://github.com/NuGet/Home/issues/10326)

**[Lista de todos los problemas corregidos en esta versión: 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Lista de confirmaciones de esta versión: 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Bienvenida a los comentarios

Sus comentarios son importantes.  Si hay algún problema con esta versión, consulte los problemas de GitHub [y](https://github.com/NuGet/Home/issues) Visual Studio [developer Community](https://developercommunity.visualstudio.com/) problemas existentes.  Si hay nuevos problemas en NuGet, informe de un [GitHub problema](https://github.com/NuGet/Home/issues/new).
Para obtener NuGet problemas de experiencia general, [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) háganoslo saber a través de la opción Notificar un problema que se encuentra en su IDE favorito en Ayuda **> notificar un problema**.