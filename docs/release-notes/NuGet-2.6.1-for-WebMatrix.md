---
title: NuGet 2.6.1 para las notas de lanzamiento de WebMatrix
description: Notas de la versión de NuGet 2.6.1 para WebMatrix incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550322"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 para las notas de lanzamiento de WebMatrix

[Notas de la versión de NuGet 2.6](../release-notes/nuget-2.6.md) | [notas de la versión de NuGet 2.7](../release-notes/nuget-2.7.md)

El equipo de NuGet publicó una extensión actualizada del Administrador de paquetes de NuGet para WebMatrix de 26 de marzo de 2014.  Esta actualización puede instalarse desde el [Galería de extensión de WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) mediante los siguientes pasos:

1. Abra WebMatrix 3
1. Haga clic en el icono de extensiones en la cinta de opciones de inicio
1. Seleccione la pestaña actualizaciones
1. Haga clic para actualizar el Administrador de paquetes de NuGet para 2.6.1
1. Cierre y reinicie el 3 de WebMatrix

## <a name="notable-changes"></a>Cambios importantes

Esta extensión actualización corrige dos de los usuarios problemas mayores tienen que afrontar consumo de paquetes de NuGet dentro de WebMatrix.  El primero era un error de versión de esquema de NuGet y la segunda era un error que dan lugar a archivos DLL de cero bytes en el `bin` carpeta.

### <a name="nuget-schema-version-error"></a>Error de la versión de esquema de NuGet

Desde el lanzamiento de WebMatrix 3, se han incorporado nuevas características a NuGet que requieren una nueva versión de esquema para los paquetes de NuGet.  Al intentar administrar los paquetes de NuGet en su sitio web, estos nuevos paquetes pueden conducir a errores que se ven en WebMatrix.

![Error. La versión de esquema no es compatible. Actualice NuGet a la versión más reciente.](./media/NuGet-2.8/webmatrix-schema-version.png)

Esta última versión ofrece compatibilidad con los paquetes de NuGet más recientes, impide que se produzca este error. Ahora se pueden instalar las nuevas versiones de los paquetes incluidos Microsoft.AspNet.WebPages en WebMatrix.  Algunos de estos paquetes estaban usando las características de NuGet como [transformaciones XDT config](../release-notes/nuget-2.6.md#xdt), que no se admite en WebMatrix hasta ahora.

### <a name="zero-byte-dlls-in-bin-folder"></a>Archivos DLL de cero bytes en la carpeta bin

Algunos usuarios han notificado que después de instalar NuGet empaqueta en WebMatrix que incluyen los archivos DLL que se copian en la ubicación que los archivos DLL se muestran en el `bin` carpeta como archivos de 0 bytes.  Esto interrumpe la aplicación en tiempo de ejecución.

[Este problema](https://nuget.codeplex.com/workitem/4060) ahora se ha corregido.

## <a name="other-recent-improvements"></a>Otras mejoras recientes

Cuando se lanzó el Administrador de paquetes de NuGet 2.8 para Visual Studio, también hemos publicado Administrador de paquetes de NuGet 2.5.0 para WebMatrix.  Aunque esto se ha mencionado en el [notas de la versión de NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), no lo hemos dicho específicos de las características nuevas que introdujo la actualización.

### <a name="update-all"></a>Actualizar todo

Ahora puede actualizar todos los paquetes de su sitio web en un solo paso.  Al abrir la extensión de NuGet en WebMatrix, consulte la lista de todos los paquetes en la galería, están instalados y los que tienen actualizaciones disponibles.  Anteriormente, cada paquete tendría que actualizar de forma individual, pero ahora hay un botón "Actualizar todo" útil que se muestra en la pestaña actualizaciones.

![Haga clic en Actualizar todo para actualizar todos los paquetes con las actualizaciones disponibles](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Sobrescribir archivos existentes

Al instalar los paquetes que contienen archivos que ya existen en su sitio web, NuGet ha ignorado siempre en modo silencioso esos archivos (dejando los archivos existentes por sí solo).  Esto podría provocar la impresión de que un paquete se ha instalado o actualizado correctamente cuando en realidad no era.  Ahora NuGet le pedirá que se sobrescriban archivos.

![Resolución de conflictos de archivos](./media/NuGet-2.8/webmatrix-overwrite-file.png)
