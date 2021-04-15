---
title: Notas de la versión de NuGet 5.7
description: Notas de la versión de NuGet 5.7 que incluyen nuevas características, correcciones de errores y DCR.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508792"
---
# <a name="nuget-57-release-notes"></a>Notas de la versión de NuGet 5.7

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio | Disponible en los SDK de .NET |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |
| [**5.7.1**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1 Instalado</sup> con Visual Studio 2019 con carga de trabajo de .NET Core

## <a name="summary-whats-new-in-57"></a>Resumen: Novedades de la versión 5.7

### <a name="features-added-in-this-release"></a>Características agregadas en esta versión

* Se ha agregado compatibilidad con alias externos para las referencias de paquetes [NuGet: #4989](https://github.com/NuGet/Home/issues/4989)

* Se ha realizado un cambio más rápido entre las pestañas Instalado y Actualizaciones al permitirles compartir un origen de datos y reducir la frecuencia de [#8294](https://github.com/NuGet/Home/issues/8294)

* Hacer que la restauración sea más rápida: aceleres las evaluaciones mediante una llamada a las API de MSBuild Static Graph (dotnet.exe): [#9644](https://github.com/NuGet/Home/issues/9644)

* Se ha Visual Studio restauración parcial para proyectos PackageReference (no-op++): [#9513](https://github.com/NuGet/Home/issues/9513)

* Visual Studio Administrador de paquetes interfaz de usuario se bloqueará con menos frecuencia al buscar orígenes de paquetes que no se comportan y que devuelven más que el número solicitado de resultados por solicitud HTTP. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Se ha agregado integración de la información de PackageVersion para proyectos de estilo que no son de SDK en la restauración de [VS: #9236](https://github.com/NuGet/Home/issues/9236)

* Se ha agregado compatibilidad con nuget.exe actualización `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Se ha agregado compatibilidad con varios archivos de configuración en el directorio %APPDATA%\NuGet- [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths ahora tiene en cuenta los paquetes de origen de [NuGet: #9431](https://github.com/NuGet/Home/issues/9431)

* Se ha agregado la API de extensibilidad INuGetProjectService.GetInstalledPackagesAsync [: #9702](https://github.com/NuGet/Home/issues/9702)

* Se ha agregado la API de interoperabilidad para enumerar las carpetas de reserva sin necesidad de una solución o [proyecto: #9395](https://github.com/NuGet/Home/issues/9395)

* Se ha `latest` agregado la opción para `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**bugs:**

* En una restauración de la CLI de dotnet, al iniciar complementos de credenciales, pruebe la CLI de dotnet en la ruta de acceso del sistema si la variable de entorno `DOTNET_HOST_PATH`  no está definida. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe especificación genera una etiqueta de copyright con texto codificado de forma codificada de copyright YYYY en lugar de `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe excepción "authors required" durante el paquete de csproj omitiendo marcadores de posición y atributos assemblyinfo si se cambia el nombre del [ensamblado: #4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage se reutiliza varias veces, lo que no se admite con SocketHttpHandler [- #8661](https://github.com/NuGet/Home/issues/8661)

* NuGet.Indexing 5.6.0 preview 3 y versiones posteriores usan un token de clave pública [diferente: #9481](https://github.com/NuGet/Home/issues/9481)

* Respetar TreatWarningsAsErrors durante la creación del paquete [NuGet: #7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Degradaciones de paquetes falsos para varios proyectos p2p: [#9549](https://github.com/NuGet/Home/issues/9549)

* La pestaña "Examinar" no está alineada a la izquierda con el cuadro de [búsqueda: #9559](https://github.com/NuGet/Home/issues/9559)

* La versión instalada es incoherente con el icono incrustado en la interfaz de usuario de PM del nivel de solución para un identificador de paquete con varias versiones [instaladas: #9321](https://github.com/NuGet/Home/issues/9321)

* Pérdida: PartCreationPolicy(CreationPolicy.NonShared) NuGet.SolutionRestoreManager.RestoreOperationLogger [- #9595](https://github.com/NuGet/Home/issues/9595)

* Evite leer el archivo de recursos en restauraciones sin [operación: #9693](https://github.com/NuGet/Home/issues/9693)

* NuGet.Protocol no admite la obtención del recuento de descargas de una versión de la [búsqueda: #9086](https://github.com/NuGet/Home/issues/9086)

* Mejora del rendimiento de memoria de PackageMetadataResourceV3 mediante la reducción de las dependencias de JObject [#9719](https://github.com/NuGet/Home/issues/9719)

**Diseño de solicitudes de cambio:**

* Se suprime `<owners>` el elemento cuando es [redundante: #5134](https://github.com/NuGet/Home/issues/5134)

* Registrar IntervalTrackers como eventos [ETW: #9593](https://github.com/NuGet/Home/issues/9593)

* Se ha agregado un mensaje informativo sobre la restauración para informar a los usuarios de CPVM de que la característica está en versión [preliminar( #9340](https://github.com/NuGet/Home/issues/9340)

* Rellenar Explorador de soluciones paquete o proyecto de dependencias transitivas desde el archivo de [recursos : #9580](https://github.com/NuGet/Home/issues/9580)

* La pestaña Paquetes instalados no debe paginar la lista de [paquetes: #6995](https://github.com/NuGet/Home/issues/6995)

**[Lista de todos los problemas corregidos en esta versión: 5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Contribuciones de la comunidad

Gracias a todos los colaboradores que ayudaron a que esta versión de NuGet sea impresionante.

|Quién|Prs|Issues|
|----|----|----|
|[yau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet.Protocol no admite la obtención del recuento de descargas de una versión de la [búsqueda: #9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage se reutiliza varias veces, lo que no se admite con SocketHttpHandler [- #8661](https://github.com/NuGet/Home/issues/8661)|
|[IfifEstor (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Se suprime `<owners>` el elemento cuando es [redundante: #5134](https://github.com/NuGet/Home/issues/5134)|
|[Doradymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet no se puede restaurar desde orígenes HTTPS que requieren certificados de [cliente: #5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (Thetralok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|Corrección futura de HttpSourceAuthenticationHandler SemaphoreSlim: [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sudj (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe especificación genera una etiqueta de copyright con texto codificado de forma codificada de copyright YYYY en lugar de `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Spin spin (spin spin spin)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|En una restauración de la CLI de dotnet, al iniciar complementos de credenciales, pruebe la CLI de dotnet en la ruta de acceso del sistema si la variable de entorno `DOTNET_HOST_PATH`  no está definida. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Se ha `latest` agregado la opción para `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|

## <a name="summary-whats-new-in-571"></a>Resumen: Novedades de la versión 5.7.1

* Extienda el archivo .nupkg.metadata para incluir el origen de [instalación: #10354](https://github.com/NuGet/Home/issues/10354)

* Registro del contenido del paquetehash durante el registro de restauración (durante la extracción): [#10384](https://github.com/NuGet/Home/issues/10384)

* Al restaurar con un nivel de detalle normal, registre el origen desde el que se restaura un [paquete #10461](https://github.com/NuGet/Home/issues/10461)

**[Lista de todos los problemas corregidos en esta versión: 5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**

**[Lista de confirmaciones de esta versión: 5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**
