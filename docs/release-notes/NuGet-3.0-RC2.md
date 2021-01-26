---
title: Notas de la versión de NuGet 3,0 RC2
description: Notas de la versión de NuGet 3,0 RC2, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780279"
---
# <a name="nuget-30-rc2-release-notes"></a>Notas de la versión de NuGet 3,0 RC2

Notas de la [versión de NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Notas de la versión de NuGet 3,0](../release-notes/nuget-3.0.0.md)

NuGet 3,0 RC2 se lanzó el 3 de junio de 2015 como una versión provisional disponible en la galería de extensiones de Visual Studio 2015 y [CodePlex](https://nuget.codeplex.com/releases/view/615507). Esta versión tiene una serie de correcciones de errores importantes y mejoras de rendimiento que consideramos importantes para su lanzamiento antes de la versión completa de Visual Studio 2015. Esta versión de la extensión de NuGet solo está disponible para Visual Studio 2015.

En total, hemos cerrado 158 problemas en esta versión y puede revisar la [lista completa de problemas en github](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Resumen de los principales problemas resueltos

* [Llamadas frecuentes de actualización de red cuando se actualiza la ventana del administrador de paquetes](https://github.com/NuGet/Home/issues/515)
* [Desplazamiento retrasado al cambiar a la vista instalada en el administrador de paquetes](https://github.com/NuGet/Home/issues/519)
* [Las llamadas de red se deben ejecutar en un subproceso en segundo plano](https://github.com/NuGet/Home/issues/516)
* [Casilla ' no Mostrar ventana de vista previa ' agregada](https://github.com/NuGet/Home/issues/566)
* [Limitación del proceso agregada para reducir el uso del procesador](https://github.com/NuGet/Home/issues/356)
* Control mejorado de la referencia de la biblioteca de clases portátiles
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [El servicio Autocompletar distingue mayúsculas de minúsculas](https://github.com/NuGet/Home/issues/198)
* [Actualización para volver a introducir las credenciales de autenticación básica](https://github.com/NuGet/Home/issues/456)
* [Se mejoró el registro de errores](https://github.com/NuGet/Home/issues/407)
* [Se han mejorado los mensajes de error de PowerShell al llamar a Update-package](https://github.com/NuGet/Home/issues/5)

Descargue esta [actualización a la extensión NuGet](https://nuget.codeplex.com/releases/view/615507) desde CodePlex y eche un vistazo a [nuestro blog](http://blog.nuget.org) para obtener más información sobre el progreso y los anuncios de NuGet 3,0.