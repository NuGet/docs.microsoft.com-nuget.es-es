---
title: "Notas de la versión de NuGet 3.1 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión para 3.1 de NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "3.1 de NuGet notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-31-release-notes"></a>Notas de la versión 3.1 de NuGet

[Notas de la versión de NuGet 3.0](../release-notes/nuget-3.0.0.md) | [notas de la versión de NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

3.1 de NuGet se publicó en el 27 de julio de 2015 como una extensión integrada para el SDK de plataforma Universal de Windows para Visual Studio 2015. Se entrega esta versión con el SDK de la plataforma Windows de modo que la experiencia de desarrollo de Windows puede aprovechar el trabajo de multiplataforma de NuGet que se inició previamente. Esta versión de extensión de NuGet solo está disponible para Visual Studio 2015.

Se recomienda que los desarrolladores que tienen acceso a la actualización de la Galería de Visual Studio a la versión más reciente que está disponible, como siempre estamos publicando actualizaciones con nuevas características y correcciones de errores.

## <a name="nuget-visual-studio-extension"></a>Extensión de NuGet Visual Studio

Problemas y características de esta versión se etiquetan en GitHub con el ["soporte transitiva de RTM UWP 3.1" hito](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) en total, se cierran 67 problemas de la versión 3.1.

### <a name="new-features"></a>Características nuevas

* `project.json`soporte técnico para la compatibilidad con Windows UWP y ASP.NET 5
* Instalación del paquete transitiva

Descripción y definición de estas características pueden encontrarse en otro lugar en la documentación.

### <a name="deprecated"></a>En desuso

Las siguientes características ya no están disponibles para Visual Studio 2015:

* Ya no se pueden instalar paquetes de solución de nivel

Las siguientes características ya no están disponibles para Visual Studio 2015 y proyectos que utilizan el `project.json` especificación

* `install.ps1`y `uninstall.ps1` -estos scripts se pasará por alto durante la instalación del paquete, restaurar, actualizar y desinstalar
* Transformaciones de configuración se pasará por alto
* Contenido se realizando, pero no se copian en un proyecto.
    * El equipo está trabajando para volver a implementar esta característica, siga el análisis y progreso a fecha de: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problemas conocidos

No hay un número de problemas conocidos que se entregan con esta versión.

* Instalación de la versión 3.1 con el SDK de Windows 10 degradará cualquier versión de extensión de NuGet que se instaló previamente

## <a name="nuget-command-line"></a>Línea de comandos de NuGet

El ejecutable de línea de comandos de NuGet se actualizó y se mueve a una nueva ubicación distribuible para que pueden continuar versiones históricas del nuget.exe para que estén disponibles.  Puede descargar la versión 3.1 beta de nuget.exe para Windows en: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

La nueva ubicación distribuible reside en el host dist.nuget.org, con una estructura de carpetas que sigue a esta plantilla:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Características nuevas

* NuGet.exe puede restaurar e instalar paquetes en los proyectos que usan un `project.json` archivo.
* puede conectarse y utilizar el protocolo de NuGet v3 en NuGet.exe: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problemas conocidos ##

1.    No se puede ejecutar el paquete con un `project.json` archivo - [928](https://github.com/NuGet/Home/issues/928)
2.    No se admite en Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    No se localiza - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    No está firmado, al igual que el existente http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)
