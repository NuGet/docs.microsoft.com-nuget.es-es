---
title: Notas de la versión Beta 3.0 NuGet
description: Notas de la versión de NuGet 3.0 Beta, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4608b196d19f95410f9fe20f6a22e31c15955b89
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-beta-release-notes"></a>Notas de la versión Beta 3.0 NuGet

[Notas de la versión Preview NuGet 3.0](../release-notes/nuget-3.0-preview.md) | [notas de la versión RC de NuGet 3.0](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta se publicó en 23 de febrero de 2015 para la versión de Visual Studio 2015 CTP 6. Esta versión es muy importante a nuestro equipo, como tenemos una serie de mejoras de arquitectura y el rendimiento para compartir y nos complace optimizar la configuración de rendimiento en nuestro servicio nuget.org.

Se recomienda encarecidamente que desinstale cualquier versión anterior de la extensión de NuGet Visual Studio 2015 antes de instalar esta nueva versión.  Si tiene problemas con esta versión de la extensión, se recomienda volver a la [versión anterior](http://nuget.codeplex.com/downloads/get/909582) para su uso con la versión preliminar de Visual Studio 2015.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Esta versión Beta 3.0 de NuGet está disponible para su instalación en la Galería de Visual Studio 2015 CTP 6 extensión. Estamos trabajando para obtener eliminaciones de vista previa de Visual Studio 2012 y Visual Studio 2013 muy pronto. Ya se compartió nuestra intención de [interrumpir las actualizaciones para Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), y se hizo dicha decisión difícil.

## <a name="new-clientserver-api"></a>Nuevo cliente/servidor API

Hemos trabajado en algunos detalles de implementación para el protocolo de cliente/servidor de NuGet. El trabajo que hemos hecho es crear "API v3" de NuGet, que está diseñada para alta disponibilidad para escenarios críticos, como la restauración del paquete e instalación de paquetes. La nueva API se basa en REST e hipermedia y nos hemos seleccionado [JSON-LD](http://json-ld.org) como el formato del recurso.

En los bits de NuGet 3.0 Beta, verá un nuevo origen de paquete denominado "api.nuget.org" en la lista desplegable origen de paquete.   Si selecciona ese origen del paquete, vamos a usar la nueva API en su lugar para conectarse a nuget.org. En NuGet 3.0 RC, el nuevo origen de paquete basado en v3 API reemplazará el origen del paquete basado en v2 "nuget.org".  Se recomienda deshabilitar todos los demás orígenes de paquete pública y deja solo api.nuget.org como su repositorio de paquetes sólo pública.

Se ha colocado una gran cantidad de tiempo en generar nuestra API v3 y continuará mantener la API v2 estándar para los clientes antiguos intentando obtener acceso al repositorio público.

## <a name="updated-ui"></a>Interfaz de usuario actualizada

Hemos mejorado la interfaz de usuario en esta versión para incluir un control combobox que le permitirá elegir una acción que se realizará con el paquete y se ha pasado el botón Vista previa una casilla en el área de opciones de la pantalla.  El área opciones ya no es contraíble y ahora proporciona un vínculo de ayuda que describe las opciones disponibles.

![La nueva UI NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Registro de operaciones

Se ha eliminado la ventana modal con información de registro que aparecería rápidamente y ocultar durante la instalación o desinstalación.  Esta ventana no agrega ningún valor cuando realmente desearía ver la información o que pueda copiar y pegar de él.  En su lugar, se están ahora redireccionando a toda la salida de registro en el panel del Administrador de paquetes de la ventana de salida.  Creemos que esto es más cómodo y similar a un informe de compilación normal que desee inspeccionar.


### <a name="focus-on-performance"></a>Céntrese en el rendimiento

Hemos realizado muchos cambios en el nombre de mejorar el rendimiento de las búsquedas de NuGet y recuperaciones.  Esto ha sido nuestra preocupación número uno de nuestros clientes, y deseamos para asegurarse de que se trata en esta versión.  Hemos optimizado nuestros servidores, creados una CDN nuevo y mejorado la lógica para espero ofrecerle más relevantes de coincidencia de consulta y los resultados de búsqueda más rápida de paquete.

Conforme avancemos a través de esta fase del desarrollo de NuGet 3.0, se creará para la optimización y supervisar el servicio nuget.org para asegurarse de que se puedan ofrecer una experiencia mejorada.  No va a participar en los tiempos de inactividad, pero se pueden agregar y modificar los recursos en el servicio de.  Esté atento nuestro [fuente de twitter](http://twitter.com/nuget) para obtener más información sobre cuando se cambia la configuración del servicio.

## <a name="building-nuget-with-nuget"></a>Creación NuGet con NuGet.

Ahora se han reestructurado a nuestros clientes de NuGet en varios componentes que son por sí mismos está generando en paquetes de NuGet. Este uso de nuestras propia bibliotecas fuerza nos permite crear componentes que se puede volver a usar y que se puede empaquetar correctamente.  Hemos estado puede eliminar código duplicado y ha aprendido a configurar mejor el proceso de desarrollo para admitir la necesidad de generar paquetes a lo largo de nuestras soluciones.  Busque una entrada de blog pronto donde hablaremos sobre cómo se estructuran los proyectos de código y cómo funciona el proceso de compilación.

## <a name="stay-tuned"></a>Permanezca atento

Por favor, esté atento [nuestro blog](http://blog.nuget.org) para obtener más progreso y anuncios de NuGet 3.0.
