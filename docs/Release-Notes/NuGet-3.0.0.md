---
title: "Notas de la versión 3.0 de NuGet | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8ad13a67-9348-4f04-8f8b-b8f4a0b2c6df
description: "Notas de la versión de NuGet 3.0.0 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.0.0 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 95c4bf92f5eeb676fa6bcc3b7bcbf191efa9cb9e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-release-notes"></a>Notas de la versión 3.0 de NuGet

[Notas de la versión de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [notas de la versión 3.1 de NuGet](../release-notes/nuget-3.1.md)

NuGet 3.0 se publicó en 20 de julio de 2015 como una extensión de agrupación para Visual Studio 2015. Se insertan para ofrecer esta versión con Visual Studio para que la experiencia de NuGet 3.0 completa actualizada estaría disponible para los nuevos usuarios de Visual Studio. Esta versión de extensión de NuGet solo está disponible para Visual Studio 2015.

Se recomienda que los desarrolladores que tienen acceso a la actualización de la Galería de Visual Studio a la versión más reciente que está disponible, como estamos publicando una actualización poco tiempo después del lanzamiento de Visual Studio 2015 que contiene compatibilidad para el desarrollo de Windows 10.

En total, se cierran 240 problemas en la versión 3.0, y puede revisar la [lista completa de los problemas en GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problemas conocidos

Hubo un número de problemas conocidos que se entregan con esta versión, y todos estos elementos son fijos en nuestra versión 3.1 programada para que coincida con la versión de Windows 10 en 29 de julio.  Podrá actualizar la extensión de Visual Studio desde la galería en o después de esa fecha para solucionar estos problemas conocidos.

*  Traducción no se proporciona para la etiqueta "no volver a mostrar" en la ventana de vista previa y la etiqueta "Authors" en la ventana de descripción del paquete.
*  Cuando se trabaja en un proyecto mediante el uso de TFS control de código fuente, NuGet no puede crear al administrador de paquetes interfaz de usuario si el archivo Nuget.Config está marcado como de solo lectura.
   * **Solución alternativa** desproteger el archivo de TFS.
*  Texto en el amarillo "barra de reinicio" en la ventana de NuGet Powershell no está visible cuando se usa el tema oscuro de Visual Studio.
   * **Solución alternativa** utilizar el tema claro de Visual Studio.


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
* [Corregido el vínculo 'Más información acerca de las opciones' para evitar el bloqueo en Windows 10](https://github.com/NuGet/Home/issues/822)
* [Recordar la configuración de la casilla de verificación de versión preliminar](https://github.com/NuGet/Home/issues/732)
* [Rendimiento mejorado recopilación almacenando en memoria caché de resultados en proyectos de una solución](https://github.com/NuGet/Home/issues/721)
* [Se pueden recopilar varios paquetes en paralelo](https://github.com/NuGet/Home/issues/713)
* [Quita el paquete de instalación-forzar comando](https://github.com/NuGet/Home/issues/697)

Por favor, esté atento [nuestro blog](http://blog.nuget.org) para obtener más progreso y anuncios que obtenemos listos para proporcionar compatibilidad para el desarrollo de Windows 10.