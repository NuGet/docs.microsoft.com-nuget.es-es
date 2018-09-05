---
title: Notas de la versión de NuGet 3.0 RC2
description: Notas de la versión RC2 de NuGet 3.0 incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545826"
---
# <a name="nuget-30-rc2-release-notes"></a>Notas de la versión de NuGet 3.0 RC2

[Notas de la versión de NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [notas de la versión de NuGet 3.0](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 se lanzó en 3 de junio de 2015 como una versión provisional desde la Galería de extensiones de Visual Studio 2015 y [Codeplex](https://nuget.codeplex.com/releases/view/615507). Esta versión tiene un número importante de correcciones de errores y mejoras de rendimiento que pensamos que era importantes liberar antes de la versión completa de Visual Studio 2015. Esta versión de la extensión NuGet solo está disponible para Visual Studio 2015.

En total, se cierran 158 problemas en esta versión, y puede revisar el [lista completa de los problemas en GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Resumen de los principales problemas resueltos

* [Actualización de la red frecuentes llama cuando se actualiza la ventana del Administrador de paquetes](https://github.com/NuGet/Home/issues/515)
* [Retrasa el desplazamiento al cambiar a instala vista en el Administrador de paquetes](https://github.com/NuGet/Home/issues/519)
* [Las llamadas de red se deben ejecutar en un subproceso en segundo plano](https://github.com/NuGet/Home/issues/516)
* [Casilla 'No mostrar ventana de vista previa' agregada](https://github.com/NuGet/Home/issues/566)
* [Proceso agregado limitación para reducir el uso del procesador](https://github.com/NuGet/Home/issues/356)
* Referencia de biblioteca de clases portable control mejorado
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Servicio de Autocompletar distinguía mayúsculas y minúsculas](https://github.com/NuGet/Home/issues/198)
* [Actualizar para volver a introducir las credenciales de autenticación básica](https://github.com/NuGet/Home/issues/456)
* [Registro de errores mejorado](https://github.com/NuGet/Home/issues/407)
* [Powershell mejorado los mensajes de error al llamar a Update-Package](https://github.com/NuGet/Home/issues/5)

Descargue este [actualizar a la extensión NuGet](https://nuget.codeplex.com/releases/view/615507) desde Codeplex y no pierda de vista, [nuestro blog](http://blog.nuget.org) más progreso y los anuncios para NuGet 3.0!