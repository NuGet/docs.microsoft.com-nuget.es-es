---
title: Notas de la versión de NuGet 3,1
description: Notas de la versión de NuGet 3,1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776532"
---
# <a name="nuget-31-release-notes"></a>Notas de la versión de NuGet 3,1

Notas de la [versión de NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Notas de la versión de NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3,1 se lanzó el 27 de julio de 2015 como una extensión incluida en el SDK de Plataforma universal de Windows para Visual Studio 2015. Esta versión se ha entregado con el SDK de la plataforma Windows para que la experiencia de desarrollo de Windows pueda aprovechar el trabajo entre plataformas de NuGet que se había iniciado anteriormente. Esta versión de la extensión de NuGet solo está disponible para Visual Studio 2015.

Se recomienda que los desarrolladores que tengan acceso a la galería de Visual Studio se actualicen a la versión más reciente que esté disponible, ya que siempre publicamos actualizaciones con correcciones de errores y nuevas características.

## <a name="nuget-visual-studio-extension"></a>Extensión de Visual Studio de NuGet

Los problemas y las características de esta versión se etiquetan en GitHub con el [hito "soporte transitivo de UWP 3,1 RTM"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  en total. hemos cerrado 67 problemas en la versión 3,1.

### <a name="new-features"></a>Nuevas características

* `project.json` compatibilidad con la compatibilidad con Windows UWP y ASP.NET 5
* Instalación de paquetes transitivos

La descripción y la definición de estas características se pueden encontrar en cualquier otra parte de la documentación.

### <a name="deprecated"></a>Obsoleto

Las siguientes características ya no están disponibles para Visual Studio 2015:

* Los paquetes de nivel de solución ya no se pueden instalar

Las siguientes características ya no están disponibles para Visual Studio 2015 y los proyectos que usan la `project.json` especificación

* `install.ps1` y `uninstall.ps1` : estos scripts se omitirán durante la instalación, restauración, actualización y desinstalación del paquete.
* Las transformaciones de configuración se omitirán
* El contenido se llevará a cabo, pero no se copiará en un proyecto.
    * El equipo está trabajando para volver a implementar esta característica, siga la explicación y el progreso en: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problemas conocidos

Se han entregado varios problemas conocidos con esta versión.

* La instalación de la versión 3,1 con el SDK de Windows 10 degradará cualquier versión de la extensión de NuGet instalada previamente.

## <a name="nuget-command-line"></a>Línea de comandos de NuGet

El ejecutable de la línea de comandos de NuGet se actualizó y se ha migrado a una nueva ubicación distribuible para que las versiones históricas de nuget.exe puedan seguir estando disponibles.  Puede descargar la versión beta 3,1 de nuget.exe para Windows en: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

La nueva ubicación distribuible reside en el host de dist.nuget.org, con una estructura de carpetas que sigue a esta plantilla:

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>Nuevas características

* nuget.exe puede restaurar e instalar paquetes en proyectos que usan un `project.json` archivo.
* nuget.exe puede conectarse al protocolo NuGet V3 y consumirlo en: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problemas conocidos ##

1.    No se puede ejecutar el paquete en un `project.json` archivo: [928](https://github.com/NuGet/Home/issues/928)
2.    No se admite en mono- [1059](https://github.com/NuGet/Home/issues/1059)
3.    No está localizado- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    No está firmado, al igual que el existente http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
