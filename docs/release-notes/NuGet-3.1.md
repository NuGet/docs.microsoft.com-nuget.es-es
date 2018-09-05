---
title: Notas de la versión 3.1 de NuGet
description: Notas de la versión de NuGet 3.1, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545352"
---
# <a name="nuget-31-release-notes"></a>Notas de la versión 3.1 de NuGet

[Notas de la versión de NuGet 3.0](../release-notes/nuget-3.0.0.md) | [notas de la versión de NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3.1 se lanzó en el 27 de julio de 2015 como una extensión integrada de Universal Windows Platform SDK para Visual Studio 2015. Esta versión con el SDK de plataforma de Windows se entrega para que la experiencia de desarrollo de Windows puede aprovechar el trabajo de desarrollo multiplataforma de NuGet que se inició previamente. Esta versión de la extensión NuGet solo está disponible para Visual Studio 2015.

Se recomienda que los desarrolladores que tengan acceso a la actualización de la Galería de Visual Studio a la versión más reciente que está disponible, como siempre estamos publicando actualizaciones con nuevas características y correcciones de errores.

## <a name="nuget-visual-studio-extension"></a>Extensión de NuGet Visual Studio

Problemas y las características de esta versión están etiquetadas en GitHub con el [hito "soporte transitiva de UWP RTM 3.1"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) en total, se cierran 67 problemas de la versión 3.1.

### <a name="new-features"></a>Características nuevas

* `project.json` soporte técnico para obtener soporte técnico de UWP de Windows y ASP.NET 5
* Instalación de paquetes transitiva

Descripción y la definición de estas características pueden encontrarse en otro lugar en la documentación.

### <a name="deprecated"></a>En desuso

Las siguientes características ya no están disponibles para Visual Studio 2015:

* Ya no se pueden instalar los paquetes de nivel de solución

Las siguientes características ya no están disponibles para Visual Studio 2015 y los proyectos que usan el `project.json` especificación

* `install.ps1` y `uninstall.ps1` -estos scripts se omitirá durante la instalación del paquete, restaurar, actualizar y desinstalar
* Transformaciones de configuración se omitirá.
* Contenido se lleva a, pero no se copian en un proyecto.
    * El equipo está trabajando para volver a implementar esta característica, siga las discusiones y avanzar: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problemas conocidos

Hubo un número de problemas conocidos que se entregan con esta versión.

* Instalación de la versión 3.1 con el SDK de Windows 10 degradará cualquier versión de extensión de NuGet que se instaló previamente

## <a name="nuget-command-line"></a>Línea de comandos de NuGet

Se actualizó el archivo ejecutable de línea de comandos de NuGet y se mueve a una nueva ubicación distribuible para que pueden continuar versiones históricas de nuget.exe esté disponible.  Puede descargar la versión 3.1 beta de nuget.exe para Windows en: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

La nueva ubicación distribuible reside en el host dist.nuget.org, con una estructura de carpetas que sigue a esta plantilla:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Características nuevas

* NuGet.exe puede restaurar e instalar paquetes en proyectos que usan un `project.json` archivo.
* NuGet.exe puede conectarse a y utilizar el protocolo de NuGet v3 en: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problemas conocidos ##

1.    No se puede ejecutar el paquete con un `project.json` archivo - [928](https://github.com/NuGet/Home/issues/928)
2.    No se admite en Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    No se localiza - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    No está firmado, al igual que existente http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
