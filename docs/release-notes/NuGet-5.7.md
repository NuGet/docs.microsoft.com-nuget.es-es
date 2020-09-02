---
title: Notas de la versión de NuGet 5,7
description: Notas de la versión de NuGet 5,7, incluidas nuevas características, correcciones de errores y DCR.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364157"
---
# <a name="nuget-57-release-notes"></a>Notas de la versión de NuGet 5,7

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio | Disponible en los SDK de .NET |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> instalado con Visual Studio 2019 con la carga de trabajo de .net Core

## <a name="summary-whats-new-in-57"></a>Resumen: novedades en 5,7

### <a name="features-added-in-this-release"></a>Características agregadas en esta versión

* Compatibilidad con alias extern agregada para las referencias de paquetes NuGet: [#4989](https://github.com/NuGet/Home/issues/4989)

* Cambio entre pestañas instaladas y actualizaciones más rápido permitiéndoles compartir un origen de datos y reducir resfreshing- [#8294](https://github.com/NuGet/Home/issues/8294)

* Realizar la restauración más rápido: acelerar las evaluaciones llamando a las API de grafos estáticos de MSBuild (dotnet.exe)- [#9644](https://github.com/NuGet/Home/issues/9644)

* Se ha agregado la restauración parcial de Visual Studio para proyectos de PackageReference (no-OP + +)- [#9513](https://github.com/NuGet/Home/issues/9513)

* La interfaz de usuario del administrador de paquetes de Visual Studio se bloqueará con menos frecuencia al buscar orígenes de paquetes que devuelvan un rendimiento superior al número solicitado de resultados por solicitud HTTP. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Integración agregada de información de PackageVersion para proyectos de estilo que no son de SDK en VS restore- [#9236](https://github.com/NuGet/Home/issues/9236)

* Compatibilidad agregada para la actualización de nuget.exe `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Se ha agregado compatibilidad con varios archivos de configuración en el directorio%APPDATA%\NuGet- [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths Now toma los paquetes de origen de NuGet en la cuenta [#9431](https://github.com/NuGet/Home/issues/9431)

* API de extensibilidad de INuGetProjectService. GetInstalledPackagesAsync agregada: [#9702](https://github.com/NuGet/Home/issues/9702)

* Se ha agregado la API de interoperabilidad para enumerar carpetas de reserva sin necesidad de una solución/proyecto [#9395](https://github.com/NuGet/Home/issues/9395)

* Opción agregada `latest` para `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Detectar**

* En una restauración de la CLI de dotnet, al iniciar los complementos de credenciales, pruebe la CLI de DotNET en la ruta de acceso del sistema si `DOTNET_HOST_PATH`  no se define la variable de entorno. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe Spec genera una etiqueta de copyright con texto codificado de forma rígida de copyright yyyy en lugar de `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe produce una excepción ' authors Required ' durante el paquete de un csproj que omite los marcadores de posición y atributos AssemblyInfo si se cambia el nombre del ensamblado- [#4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage se reutiliza varias veces, lo que no es compatible con SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)

* NuGet. Indexing 5.6.0 del Preview 3 y versiones posteriores usan un token de clave pública diferente: [#9481](https://github.com/NuGet/Home/issues/9481)

* Respetar TreatWarningsAsErrors durante la creación del paquete de NuGet: [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Degradación de paquetes falsos para varios proyectos P2P: [#9549](https://github.com/NuGet/Home/issues/9549)

* La pestaña "examinar" no está alineada a la izquierda con el cuadro de búsqueda: [#9559](https://github.com/NuGet/Home/issues/9559)

* La versión instalada es incoherente con el icono incrustado en la interfaz de usuario del nivel de solución PM para un identificador de paquete con varias versiones instaladas: [#9321](https://github.com/NuGet/Home/issues/9321)

* Fuga: PartCreationPolicy (CreationPolicy. Nonshared) NuGet. SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* Evite leer el archivo de recursos en restauraciones no operativas: [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet. Protocol no admite la obtención del número de descargas de la versión de Search- [#9086](https://github.com/NuGet/Home/issues/9086)

* Mejorar el rendimiento de la memoria de PackageMetadataResourceV3 al reducir las dependencias de JObject- [#9719](https://github.com/NuGet/Home/issues/9719)

**Diseñar solicitudes de cambio:**

* Se suprime el `<owners>` elemento cuando es redundante- [#5134](https://github.com/NuGet/Home/issues/5134)

* Registrar IntervalTrackers como eventos ETW: [#9593](https://github.com/NuGet/Home/issues/9593)

* Se ha agregado un mensaje informativo en la restauración para informar a los usuarios de CPVM de que la característica está en versión preliminar [#9340](https://github.com/NuGet/Home/issues/9340)

* Rellene Explorador de soluciones dependencias transitivas de paquete/proyecto desde el archivo de recursos [#9580](https://github.com/NuGet/Home/issues/9580)

* La pestaña paquetes instalados no debe paginar la lista de paquetes- [#6995](https://github.com/NuGet/Home/issues/6995)

**[Lista de todos los problemas corregidos en esta versión: 5,7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Contribuciones de la comunidad

Gracias por todos los colaboradores que le han ayudado a hacer que esta versión de NuGet sea impresionante.

|Quién|Incorporación|Incidencias|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet. Protocol no admite la obtención del número de descargas de la versión de Search- [#9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage se reutiliza varias veces, lo que no es compatible con SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Se suprime el `<owners>` elemento cuando es redundante- [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet no se puede restaurar desde orígenes HTTPS que requieran certificados de cliente: [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|Prueba futura de HttpSourceAuthenticationHandler SemaphoreSlim: [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe Spec genera una etiqueta de copyright con texto codificado de forma rígida de copyright yyyy en lugar de `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Spinelli de Spinelli](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|En una restauración de la CLI de dotnet, al iniciar los complementos de credenciales, pruebe la CLI de DotNET en la ruta de acceso del sistema si `DOTNET_HOST_PATH`  no se define la variable de entorno. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Opción agregada `latest` para `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|
