---
title: Notas de la versión de NuGet 4.3 RTM | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de la versión de NuGet 4.3 RTM incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
keywords: Notas de la versión de NuGet 4.3 RTM, correcciones de errores, problemas, conocidos, características agregadas, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 3c798bde11548b866cad62697315e907dea91aa5
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-43-rtm-release-notes"></a>Notas de la versión de NuGet 4.3 RTM

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye NuGet 4.3 RTM que agrega compatibilidad para escenarios nuevos, como .NET Standard 2.0 y .NET Core 2.0, contiene numerosas correcciones de calidad y mejora el rendimiento. En esta versión también se ofrecen varias mejoras como compatibilidad para Versionamiento Semántico 2.0.0, integración de MSBuild de advertencias y errores de NuGet, y mucho más.

## <a name="known-issues"></a>Problemas conocidos

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>La restauración de NuGet puede tratar los orígenes de paquetes deshabilitados como habilitados en algunos casos

#### <a name="issue"></a>Problema

En las siguientes técnicas de línea de comandos de restauración se tratan los orígenes de paquetes deshabilitados como habilitados. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (ya sea con dotnet.exe, que se incluye con VS, o con el que se incluye con NetCore SDK 2.0.0)

#### <a name="workaround"></a>Solución

1. Use Visual Studio (2017 15.3 o posterior) o NuGet.exe (v4.3.0 o posterior).
1. Elimine el origen deshabilitado y siga usando msbuild o dotnet.exe.
1. Para la solución, puede usar "Clear" en NuGet.config y, después, definir los orígenes necesarios para esa solución.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Mientras usa la Consola del Administrador de paquetes, puede que la tecla "Entrar" no funcione

#### <a name="issue"></a>Problema

En algunas ocasiones, la tecla Entrar no funciona en la Consola del Administrador de paquetes. Si ve esto, revise el progreso de la corrección y proporcione información útil adicional sobre los pasos de reproducción. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Solución

Reinicie Visual Studio y abra la consola de Administración de paquetes antes de abrir la solución. Como alternativa, intente eliminar el archivo `project.lock.json` y restaurarlo de nuevo.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>No se puede ver, agregar ni actualizar DotNetCLITools con el Administrador de paquetes NuGet

#### <a name="issue"></a>Problema

El Administrador de paquetes de NuGet no muestra ni permite agregar o actualizar DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Solución

DotNetCLIToolReferences se debe editar manualmente en el archivo del proyecto.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta

#### <a name="issue"></a>Problema

Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta, en Visual Studio. Esto sucede cuando usa PackageReferences como el formato del administrador de paquete. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Solución

Haga una restauración manual.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problemas corregidos en el período de NuGet 4.3 RTM

[Notas de la versión de NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md): enumera todos los problemas corregidos en NuGet 4.0 RTM

### <a name="features"></a>Características

- Mejorar el rendimiento de restauración de NuGet: implementar NoOp más inteligente para las restauraciones de línea de comandos y VS: [#5080](https://github.com/NuGet/Home/issues/5080)

- .NET Core 2.0: la CLI de VS o Dotnet deben empezar a usar la funcionalidad existente de NuGet: carpetas FallBack: [#4939](https://github.com/NuGet/Home/issues/4939)

- .NET Core 2.0: permitir a los usuarios ignorar advertencias de restauración específicas (o elevarlas a error): [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0: ensamblados localizados de la CLI: [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0: registrar todas las advertencias o errores en el archivo de recursos (incluido PackageTargetFallback): [#4895](https://github.com/NuGet/Home/issues/4895)

- Habilitar la compatibilidad con TFM: NetStandard2.0, Tizen: [#4892](https://github.com/NuGet/Home/issues/4892)

- Reducir el número de proyectos de NuGet.Core NuGet.Client (y, por tanto, de archivos DLL): [#2446](https://github.com/NuGet/Home/issues/2446)

- Agregar la capacidad de marcar advertencias de NuGet como errores: [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Errores

- Se produce un error de msbuild /t:pack con el parámetro "DevelopmentDependency" que no es compatible con la tarea "PackTask": [#5584](https://github.com/NuGet/Home/issues/5584)

- La estructura de directorios para los archivos de contenido es plana si no se agrega el separador de directorios de Windows al final de PackagePath: [#4795](https://github.com/NuGet/Home/issues/4795)

- Los proyectos de netcore no admiten la configuración como developmentDependency: [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage se carga de forma sincrónica lo que bloquea el subproceso de la interfaz de usuario e interbloquea VS: [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet restore (y, por tanto, msbuild /t:restore) omite los proyectos con una dependencia de proyecto de solución explícita: [#4578](https://github.com/NuGet/Home/issues/4578)

- Si la solución tiene referencias de proyecto que hacen referencia al mismo proyecto, con distinto uso de mayúsculas y minúsculas, es posible que la restauración no funcione. Esto afecta también a diferentes rutas de acceso relativas, sin una diferencia de uso de mayúsculas y minúsculas: [#4574](https://github.com/NuGet/Home/issues/4574)

- Los archivos ejecutables restaurados desde paquetes NuGet ya no son ejecutables con .NET Core 2.0: [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe acepta los detalles de excepción al analizar el archivo de solución: [#4411](https://github.com/NuGet/Home/issues/4411)

- Pack coloca los archivos de contenido en una ubicación incorrecta si ContentTargetFolders contiene una ruta de acceso que termina con "/" en Windows: [#4407](https://github.com/NuGet/Home/issues/4407)

- No se puede restaurar una referencia DotNetCliToolReference para un paquete de herramientas destinado a netcoreapp1.1: [#4396](https://github.com/NuGet/Home/issues/4396)

- La actualización de la CLI de NuGet deja la condición anterior de versión de paquete en el archivo de proyecto (C++): [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCR

- Leer DotnetCliToolTargetFramework desde la nominación de CPS: [#5397](https://github.com/NuGet/Home/issues/5397)

- La comprobación de TPMinV debería funcionar para UWP de estilo de pj: [#4763](https://github.com/NuGet/Home/issues/4763)

- Mejorar la descripción de la interfaz de usuario para los paquetes con referencia automática: [#4471](https://github.com/NuGet/Home/issues/4471)

- La restauración de NuGet selecciona activos de compilación de la sección de tiempo de ejecución: - [#4207](https://github.com/NuGet/Home/issues/4207)

- Colocar el diagnóstico de dependencias en el archivo de bloqueo: [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Vínculos a problemas de GitHub corregidos en 4.3 RTM

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
