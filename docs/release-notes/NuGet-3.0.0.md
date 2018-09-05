---
title: Notas de la versión 3.0 de NuGet
description: Notas de la versión 3.0.0 NuGet incluidos conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551868"
---
# <a name="nuget-30-release-notes"></a>Notas de la versión 3.0 de NuGet

[Notas de la versión de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [notas de la versión de NuGet 3.1](../release-notes/nuget-3.1.md)

NuGet 3.0 se lanzó en 20 de julio de 2015 como una extensión de agrupación para Visual Studio 2015. Se insertan en ofrecer esta versión con Visual Studio para que la experiencia completa de NuGet 3.0 actualizada estaría disponible para los nuevos usuarios de Visual Studio. Esta versión de la extensión NuGet solo está disponible para Visual Studio 2015.

Se recomienda que los desarrolladores que tengan acceso a la actualización de la Galería de Visual Studio a la versión más reciente que está disponible, ya que publicaremos una actualización poco después del lanzamiento de Visual Studio 2015 que contiene compatibilidad para el desarrollo de Windows 10.

En total, se cierran 240 problemas de la versión 3.0, y puede revisar el [lista completa de los problemas en GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problemas conocidos

Hubo un número de problemas conocidos que se entregan con esta versión, y todos estos elementos se han corregido en nuestra versión 3.1 programada para que coincida con la versión de Windows 10 en 29 de julio.  Es posible actualizar la extensión de Visual Studio desde la galería en o después de esa fecha para corregir estos problemas conocidos.

*  No se proporciona la traducción de la etiqueta "no volver a mostrar" en la ventana Vista previa y la etiqueta de "Authors" en la ventana de descripción del paquete.
*  Cuando se trabaja en un proyecto mediante el uso de TFS control de código fuente, NuGet no puede presentar al administrador de paquetes de interfaz de usuario si el archivo Nuget.Config está marcado como de solo lectura.
   * **Solución alternativa** desproteger el archivo de TFS.
*  Texto en el amarillo "barra de reinicio" en la ventana de Powershell de NuGet no está visible cuando se usa el tema oscuro de Visual Studio.
   * **Solución alternativa** utilizar el tema claro de Visual Studio.


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
* [Se ha corregido el vínculo 'Más información acerca de las opciones' para evitar que se bloquee en Windows 10](https://github.com/NuGet/Home/issues/822)
* [Recuerde la configuración de la casilla de verificación de versión preliminar](https://github.com/NuGet/Home/issues/732)
* [Rendimiento mejorado de recopilación al almacenar en caché los resultados en proyectos de una solución](https://github.com/NuGet/Home/issues/721)
* [Se pueden recopilar varios paquetes en paralelo](https://github.com/NuGet/Home/issues/713)
* [Quitar install-package-forzar comando](https://github.com/NuGet/Home/issues/697)

Por favor, vigile [nuestro blog](http://blog.nuget.org) más progreso y los anuncios que nos encontremos listos para proporcionar compatibilidad para el desarrollo de Windows 10.