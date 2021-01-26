---
title: Notas de la versión de NuGet 3,0 beta
description: Notas de la versión de NuGet 3,0 beta, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776630"
---
# <a name="nuget-30-beta-release-notes"></a>Notas de la versión de NuGet 3,0 beta

Notas de la [versión de NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)  |  [Notas de la versión de NuGet 3,0 RC](../release-notes/nuget-3.0-rc.md)

NuGet 3,0 beta se publicó el 23 de febrero de 2015 para la versión de Visual Studio 2015 CTP 6. Esta versión es una gran parte de nuestro equipo, ya que tenemos una serie de mejoras de arquitectura y rendimiento para compartir y nos complace comenzar a ajustar la configuración de rendimiento en nuestro servicio nuget.org.

Se recomienda encarecidamente desinstalar cualquier versión anterior de la extensión NuGet de Visual Studio 2015 antes de instalar esta nueva versión.  Si tiene algún problema con esta versión de la extensión, se recomienda volver a la [versión anterior](http://nuget.codeplex.com/downloads/get/909582) para usarla con Visual Studio 2015 Preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Esta versión beta de NuGet 3,0 está disponible para su instalación en la galería de extensiones de Visual Studio 2015 CTP 6. Estamos trabajando para obtener la vista previa de Visual Studio 2012 y Visual Studio 2013 muy pronto. Anteriormente compartimos nuestro intento de [dejar de actualizar las actualizaciones de Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)y nos decidimos tomar esa decisión difícil.

## <a name="new-clientserver-api"></a>Nueva API de cliente/servidor

Hemos estado trabajando en algunos detalles de implementación del protocolo cliente/servidor de NuGet. El trabajo que hemos hecho es crear "API V3" para NuGet, que está diseñado en torno a la alta disponibilidad en escenarios críticos, como la restauración de paquetes y la instalación de paquetes. La nueva API se basa en REST y Hypermedia y hemos seleccionado [JSON-LD](http://json-ld.org) como nuestro formato de recursos.

En los bits de la versión beta 3,0 de NuGet, verá un nuevo origen de paquete llamado "api.nuget.org" en la lista desplegable origen del paquete.   Si selecciona el origen del paquete, usaremos la nueva API en lugar de conectarse a nuget.org. En NuGet 3,0 RC, este nuevo origen de paquete basado en API V3 reemplazará el origen del paquete "nuget.org" basado en v2.  Se recomienda deshabilitar todos los demás orígenes de paquetes públicos y dejar solo api.nuget.org como el único repositorio de paquetes público.

Hemos puesto mucho tiempo en crear nuestra API de V3 y seguirán manteniendo la API de la versión V2 estándar para los clientes antiguos que buscan acceder al repositorio público.

## <a name="updated-ui"></a>Interfaz de usuario actualizada

Hemos mejorado la interfaz de usuario en esta versión para incluir un cuadro combinado que le permitirá elegir la acción que se llevará a cabo con el paquete y pasar el botón de vista previa a una casilla en el área Opciones de la pantalla.  El área de opciones ya no es contraíble y ahora proporciona un vínculo de ayuda que describe las opciones disponibles.

![La nueva interfaz de usuario de NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Registro de operaciones

Hemos quitado la ventana modal con información de registro que se mostraría y ocultaría rápidamente al instalar o desinstalar.  Esta ventana no ha agregado ningún valor si realmente desea ver la información o puede copiar y pegar desde ella.  En su lugar, ahora redirigimos todo el registro de salida al panel del administrador de paquetes de la ventana de salida.  Creemos que esto es más cómodo y similar a un informe de compilación típico que desea inspeccionar.


### <a name="focus-on-performance"></a>Centrarse en el rendimiento

Hemos realizado muchos cambios en el nombre de la mejora del rendimiento de las búsquedas de NuGet y las capturas.  Este es el número que nos preocupa de nuestros clientes y queríamos asegurarnos de que nos hemos solucionado en esta versión.  Se han optimizado los servidores, se ha creado una nueva red CDN y se ha mejorado la lógica de búsqueda de coincidencias para que se entreguen resultados más importantes y más rápidos.

A medida que avancemos en esta fase del desarrollo de NuGet 3,0, se optimizará y supervisará el servicio nuget.org para garantizar que proporcionamos una experiencia mejorada.  No tenemos previsto entrar en ningún tiempo de inactividad, sino que va a agregar y cambiar recursos en el servicio.  Siga observando nuestra fuente de [Twitter](http://twitter.com/nuget) para obtener más información sobre cuándo se cambia la configuración del servicio.

## <a name="building-nuget-with-nuget"></a>Compilación de NuGet con NuGet

Ahora hemos rediseñado nuestros clientes de NuGet en varios componentes que se integran en paquetes NuGet. Esta reutilización de nuestras propias bibliotecas nos obliga a compilar componentes que se pueden volver a usar y que se pueden empaquetar correctamente.  Hemos podido eliminar el código duplicado y hemos aprendido a configurar mejor nuestro proceso de desarrollo para que sea compatible con la necesidad de crear paquetes a lo largo de nuestras soluciones.  Busque una entrada de blog en breve donde hablaremos sobre cómo se estructuran los proyectos de código y cómo funciona el proceso de compilación.

## <a name="stay-tuned"></a>Manténgase atento

Eche un vistazo a [nuestro blog](http://blog.nuget.org) para obtener más información sobre el progreso y los anuncios de NuGet 3,0.
