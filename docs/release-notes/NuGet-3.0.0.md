---
title: Notas de la versión de NuGet 3,0
description: Notas de la versión de NuGet 3.0.0, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776552"
---
# <a name="nuget-30-release-notes"></a>Notas de la versión de NuGet 3,0

Notas de la [versión de NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Notas de la versión de NuGet 3,1](../release-notes/nuget-3.1.md)

NuGet 3,0 se lanzó el 20 de julio de 2015 como extensión de agrupación a Visual Studio 2015. Hemos insertado en el lanzamiento de esta versión con Visual Studio para que la experiencia completa de NuGet 3,0 actualizada esté disponible para los nuevos usuarios de Visual Studio. Esta versión de la extensión de NuGet solo está disponible para Visual Studio 2015.

Se recomienda que los desarrolladores que tienen acceso a la galería de Visual Studio se actualicen a la versión más reciente disponible, ya que estamos publicando una actualización poco después del lanzamiento de Visual Studio 2015 que contiene compatibilidad con el desarrollo de Windows 10.

En total, hemos cerrado 240 problemas en la versión 3,0 y puede revisar la [lista completa de problemas en github](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problemas conocidos

Se han entregado varios problemas conocidos con esta versión, y todos estos elementos se han corregido en la versión 3,1 programada para que coincida con la versión de Windows 10 el 29 de julio.  Puede actualizar la extensión de Visual Studio desde la galería de o después de esa fecha para corregir estos problemas conocidos.

*  No se proporciona traducción para la etiqueta "no volver a mostrar" en la ventana de vista previa y la etiqueta "authors" en la ventana de Descripción del paquete.
*  Cuando se trabaja en un proyecto mediante el control de código fuente de TFS, NuGet no puede presentar la interfaz de usuario del administrador de paquetes si el archivo Nuget.Config está marcado como de solo lectura.
   * **Solución alternativa** Desproteja el archivo de TFS.
*  El texto de la "barra de reinicio" amarilla de la ventana de PowerShell de NuGet no es visible cuando se usa el tema oscuro de Visual Studio.
   * **Solución alternativa** Use el tema claro de Visual Studio.


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
* [Se ha corregido el vínculo "más información sobre las opciones" para evitar el bloqueo en Windows 10](https://github.com/NuGet/Home/issues/822)
* [Opción de casilla recordar versión preliminar](https://github.com/NuGet/Home/issues/732)
* [Rendimiento de recopilación mejorado al almacenar en caché los resultados entre los proyectos de una solución](https://github.com/NuGet/Home/issues/721)
* [Se pueden recopilar varios paquetes en paralelo](https://github.com/NuGet/Home/issues/713)
* [Se quitó el comando Install-Package-Force](https://github.com/NuGet/Home/issues/697)

Eche un vistazo a [nuestro blog](http://blog.nuget.org) para obtener más información sobre el progreso y los anuncios a medida que nos preparamos para ofrecer soporte técnico para el desarrollo de Windows 10.