---
title: "Notas de la versión de NuGet 3.0 RC2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20f9b360-2d78-4676-a803-e86996eb2f10
description: "Notas de la versión de NuGet 3.0 RC2 incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.0 RC2 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2a708babf200a650a0faffc704235d3c142f510f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-rc2-release-notes"></a>Notas de la versión de NuGet RC2 3.0

[Notas de la versión RC de NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [notas de la versión 3.0 de NuGet](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 se publicó en el 3 de junio de 2015 como una versión provisional de la Galería de extensión de Visual Studio 2015 y [Codeplex](https://nuget.codeplex.com/releases/view/615507). Esta versión tiene un número importantes de correcciones de errores y mejoras de rendimiento que creímos eran importantes para la versión antes de la versión de Visual Studio 2015 completada. Esta versión de extensión de NuGet solo está disponible para Visual Studio 2015.

En total, se cierran 158 problemas en esta versión, y puede revisar la [lista completa de los problemas en GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Resumen de los principales problemas resueltos

* [Actualizar la red frecuentes llama cuando se actualiza la ventana del Administrador de paquetes](https://github.com/NuGet/Home/issues/515)
* [Retrasa el desplazamiento al cambiar a instala la vista en el Administrador de paquetes](https://github.com/NuGet/Home/issues/519)
* [Llamadas de red deben ejecutarse en un subproceso en segundo plano](https://github.com/NuGet/Home/issues/516)
* [Agrega la casilla 'No mostrar la ventana de vista previa'](https://github.com/NuGet/Home/issues/566)
* [Limitación para reducir el uso de procesador del proceso de agregado](https://github.com/NuGet/Home/issues/356)
* Referencia de biblioteca de clases portable control mejorado
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [El servicio de función Autocompletar está entre mayúsculas y minúsculas](https://github.com/NuGet/Home/issues/198)
* [Actualizar para volver a introducir las credenciales de autenticación básica](https://github.com/NuGet/Home/issues/456)
* [Registro de errores mejorada](https://github.com/NuGet/Home/issues/407)
* [Mensajes de error de powershell mejorada al llamar al paquete de actualización](https://github.com/NuGet/Home/issues/5)

Descargue este [actualizar a la extensión de NuGet](https://nuget.codeplex.com/releases/view/615507) desde Codeplex y por favor, esté atento [nuestro blog](http://blog.nuget.org) para obtener más progreso y anuncios de NuGet 3.0.