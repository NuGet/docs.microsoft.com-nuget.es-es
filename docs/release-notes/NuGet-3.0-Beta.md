---
title: Notas de la versión Beta de NuGet 3.0
description: Notas de la versión Beta de NuGet 3.0 incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550918"
---
# <a name="nuget-30-beta-release-notes"></a>Notas de la versión Beta de NuGet 3.0

[Notas de la versión preliminar de NuGet 3.0](../release-notes/nuget-3.0-preview.md) | [notas de la versión de NuGet 3.0 RC](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta se ha publicado el 23 de febrero de 2015 para el lanzamiento de Visual Studio 2015 CTP 6. Esta versión es muy importante a nuestro equipo, como tenemos una serie de mejoras de arquitectura y rendimiento para compartir, y estamos encantados de iniciar la optimización de la configuración de rendimiento de nuestro servicio de nuget.org.

Se recomienda que desinstale cualquier versión anterior de la extensión NuGet Visual Studio 2015 antes de instalar esta nueva versión.  Si tiene problemas con esta versión de la extensión, se recomienda volver a la [versión anterior](http://nuget.codeplex.com/downloads/get/909582) para su uso con Visual Studio 2015 preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Esta versión Beta de NuGet 3.0 está disponible para su instalación en la Galería de Visual Studio 2015 CTP 6 extensiones. Estamos trabajando para difundir gotas de versión preliminar de Visual Studio 2012 y Visual Studio 2013 muy pronto. Anteriormente publicamos nuestra intención a [interrumpir las actualizaciones para Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), y se tomar esa decisión difícil.

## <a name="new-clientserver-api"></a>Nuevo cliente/servidor de API

Hemos trabajado en algunos detalles de implementación para el protocolo de cliente/servidor de NuGet. El trabajo que hemos hecho es crear "API v3" de NuGet, que se ha diseñado en torno a la alta disponibilidad para escenarios críticos como la restauración de paquetes e instalar paquetes. La nueva API se basa en REST e hipermedia y nos hemos seleccionado [JSON-LD](http://json-ld.org) como nuestro formato de recursos.

En las versiones Beta de NuGet 3.0, verá un nuevo origen de paquete denominado "api.nuget.org" en la lista desplegable origen de paquete.   Si selecciona ese origen del paquete, vamos a usar la nueva API en su lugar para conectarse a nuget.org. En NuGet 3.0 RC, este nuevo origen de paquetes basado en v3 API reemplazará el origen del paquete en función de v2 "nuget.org".  Se recomienda deshabilitar todos los demás orígenes de paquetes públicos y deje sólo api.nuget.org como el repositorio de paquete solo pública.

Nos has realizado una gran cantidad de tiempo en compilar nuestra API v3 y seguirá manteniendo la API v2 estándar para los clientes antiguos que se desean obtener acceso al repositorio público.

## <a name="updated-ui"></a>Interfaz de usuario actualizada

Hemos mejorado la interfaz de usuario en esta versión para incluir un cuadro combinado que le permitirá realizar elija la acción que se realizará con el paquete y el botón Vista previa ha pasado una casilla en el área de opciones de la pantalla.  El área opciones ya no es que puede contraerse y ahora proporciona un vínculo de ayuda que describen las opciones disponibles.

![La nueva UI NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Registro de operaciones

Se ha eliminado la ventana modal con información de registro que aparecería rápidamente y ocultar durante la instalación o desinstalación.  Esta ventana aportaba ningún valor cuando realmente desearía ver la información o ser capaz de copiar y pegar desde él.  En su lugar, se están ahora redireccionando a toda la salida de registro en el panel del Administrador de paquetes de la ventana de salida.  Creemos que es más cómodo y similar a un informe de compilación normal que desee inspeccionar.


### <a name="focus-on-performance"></a>Centrarse en el rendimiento

Se han realizado muchos cambios en el nombre de mejorar el rendimiento de las búsquedas de NuGet y recuperaciones.  Esto fue nuestra preocupación número uno de nuestros clientes, y queríamos para asegurarse de que se solucionaron en esta versión.  Hemos optimizado nuestros servidores, creados una nueva red CDN y ha mejorado la lógica para espero que ofrecerle más relevantes de coincidencia de consulta y los resultados de la búsqueda de paquetes más rápida.

Conforme avancemos a través de esta fase del desarrollo de NuGet 3.0, agregaremos optimización y supervisión del servicio de nuget.org para asegurarse de que se puedan ofrecer una experiencia mejorada.  Hemos no va a participar en tiempo de inactividad, pero se agregar y cambiar los recursos en el servicio.  Eche un vistazo a nuestro [fuente de twitter](http://twitter.com/nuget) para obtener más información sobre cuando se cambia la configuración del servicio.

## <a name="building-nuget-with-nuget"></a>Creación NuGet con NuGet

Ahora hemos arquitectura de nuestros clientes de NuGet en varios componentes que son por sí mismos está integrado en paquetes de NuGet. Este uso de nuestras propias bibliotecas nos vemos obligados a crear componentes que son reutilizables y que se pueden empaquetar correctamente.  Hemos podidos eliminar código duplicado y ha aprendido cómo configurar mejor nuestro proceso de desarrollo para admitir la necesidad de compilar paquetes a lo largo de nuestras soluciones.  Busque pronto una entrada de blog donde se habla sobre cómo se estructuran los proyectos de código y cómo funciona nuestro proceso de compilación.

## <a name="stay-tuned"></a>Permanezca atento

Por favor, vigile [nuestro blog](http://blog.nuget.org) más progreso y los anuncios para NuGet 3.0!
