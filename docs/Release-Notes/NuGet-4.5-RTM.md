---
title: "Notas de la versión de NuGet 4.5 RTM | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 12/4/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 4.5 RTM, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR."
keywords: "Notas de la versión de NuGet 4.5 RTM, correcciones de errores, problemas conocidos, características agregadas y DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: e4727d46812cbfeb2e7094ddf28bf4e738e8aeea
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-45-rtm-release-notes"></a>Notas de la versión de NuGet 4.5 RTM

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="known-issues"></a>Problemas conocidos

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemas con .NET 2.0 Standard con .NET Framework y NuGet 

.NET Standard y sus herramientas se han diseñado de forma que los proyectos destinados a .NET Framework 4.6.1 puedan usar los paquetes y proyectos de NuGet que tienen como destino .NET Standard 2.0 o versiones anteriores. [En este documento](https://github.com/dotnet/standard/issues/481) se resumen los problemas relacionados con ese escenario, el plan para abordarlos, así como soluciones alternativas que se pueden implementar con el estado actual de las herramientas.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Un paquete en un proyecto de .NET Core que contiene un ensamblado con una firma no válida puede desencadenar un bucle infinito de restauración

#### <a name="issue"></a>Problema

En algunas ocasiones, al usar un paquete que contiene un ensamblado con una firma no válida o cuando la versión del paquete está establecida con el valor "DateTime", la restauración automática del paquete se ejecutará en un bucle infinito [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Solución

No hay ninguna solución alternativa para este problema.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Problemas corregidos en el período de NuGet 4.5 RTM

Para los problemas corregidos en NuGet 4.4 RTM, consulte las [notas de la versión de NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Características

- Deshabilitar la inserción automática de un paquete de símbolos: [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Errores

- [Regresión] en 15.5p1: se omite Portable0.0: [#6105](https://github.com/NuGet/Home/issues/6105)
- Faltan recursos de los paquetes después de la restauración: [#5995](https://github.com/NuGet/Home/issues/5995)
- Los proveedores de credenciales de complementos no funcionan con los URI que contienen espacios: [#5982](https://github.com/NuGet/Home/issues/5982)
- Si se produce un error al restaurar el paquete, se debe imprimir el error en la salida, aunque la opción de detalle mínimo esté activada: [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet restore a nivel de solución no sigue ProjectReference con ReferenceOutputAssembly al comportar incorrectamente errores de compilación aleatorios: [#5490](https://github.com/NuGet/Home/issues/5490)
- Autocompletar en PMC funciona incorrectamente con métodos de objeto: [#4800](https://github.com/NuGet/Home/issues/4800)
- Se produce un error en la restauración de nuget.exe con el conjunto de herramientas de Visual Studio 2015: [#4713](https://github.com/NuGet/Home/issues/4713)
- Crear instancias de perf - pmc en vs2017 es costoso: [#4205](https://github.com/NuGet/Home/issues/4205)
- Lentitud para obtener información de dependencias en una conexión lenta: [#4089](https://github.com/NuGet/Home/issues/4089)
- Se produce un error de uninstall-package w/ -RemoveDependencies si varios paquetes comparten una dependencia común: [#4026](https://github.com/NuGet/Home/issues/4026)
- Finalizar NuGet.Core.nupkg para la publicación: [#3581](https://github.com/NuGet/Home/issues/3581)
- El paquete de NuGet resuelve el Id. de dependencia del nombre de directorio cuando se usa -IncludeProjectReferences para csproj + project.json: [#3566](https://github.com/NuGet/Home/issues/3566)
- El inicializador de tipo para "NuGet.ProxyCache" generó una excepción: [#3144](https://github.com/NuGet/Home/issues/3144)
- problema de rendimiento en la restauración de nuget con kudu: [#3087](https://github.com/NuGet/Home/issues/3087)
- Se produce un error en el cliente de la interfaz de usuario al mostrar errores o advertencias cuando la búsqueda está por delante de los blobs de registro: [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages-Updates genera una consulta incorrecta: [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Vínculos a problemas de GitHub corregidos en 4.5 RTM

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
