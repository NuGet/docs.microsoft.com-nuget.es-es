---
title: Notas de la versión de NuGet 2.6.1 para WebMatrix
description: Notas de la versión de NuGet 2.6.1 para WebMatrix, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780423"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>Notas de la versión de NuGet 2.6.1 para WebMatrix

Notas de la [versión de NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Notas de la versión de NuGet 2,7](../release-notes/nuget-2.7.md)

El equipo de NuGet publicó una extensión actualizada del administrador de paquetes NuGet para WebMatrix el 26 de marzo de 2014.  Esta actualización se puede instalar desde la [Galería de extensiones de WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) mediante los pasos siguientes:

1. Abrir WebMatrix 3
1. Haga clic en el icono extensiones de la cinta de opciones Inicio
1. Seleccione la pestaña actualizaciones.
1. Haga clic para actualizar el administrador de paquetes NuGet a 2.6.1
1. Cierre y reinicie WebMatrix 3

## <a name="notable-changes"></a>Cambios importantes

Esta actualización de extensión soluciona dos de los problemas más importantes que los usuarios han utilizado para usar paquetes de NuGet en WebMatrix.  El primero fue un error de versión de esquema de NuGet y el segundo era un error que conduce a archivos dll de cero bytes en la `bin` carpeta.

### <a name="nuget-schema-version-error"></a>Error de versión de esquema NuGet

Desde que se lanzó WebMatrix 3, se han incorporado nuevas características en NuGet que requieren una nueva versión de esquema para los paquetes NuGet.  Al intentar administrar los paquetes de NuGet en el sitio web, estos nuevos paquetes pueden provocar errores que se ven en WebMatrix.

![Se produjo un error. La versión del esquema no es compatible. Actualice NuGet a la versión más reciente.](./media/NuGet-2.8/webmatrix-schema-version.png)

Esta última versión proporciona compatibilidad con los paquetes de NuGet más recientes, lo que impide que se produzca este error. Ahora se pueden instalar en WebMatrix nuevas versiones de paquetes, incluidas las páginas Microsoft. AspNet. Webpages.  Algunos de estos paquetes usaban características de NuGet, como [transformaciones de configuración de XDT](../release-notes/nuget-2.6.md#xdt), que no se admitían en WebMatrix hasta ahora.

### <a name="zero-byte-dlls-in-bin-folder"></a>Zero-Byte archivos dll en la carpeta bin

Algunos usuarios han comunicado que, después de instalar paquetes NuGet en WebMatrix que incluyen archivos DLL que se copian en la ubicación, los archivos DLL se muestran en la `bin` carpeta como archivos de 0 bytes.  Esto interrumpe la aplicación en tiempo de ejecución.

[Este problema](https://nuget.codeplex.com/workitem/4060) se ha corregido.

## <a name="other-recent-improvements"></a>Otras mejoras recientes

Cuando se lanzó el administrador de paquetes NuGet 2,8 para Visual Studio, también se lanzó el administrador de paquetes de NuGet 2.5.0 para WebMatrix.  Aunque esto se mencionó en las [notas de la versión de NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), no se mencionaron las nuevas características específicas que se introdujeron en la actualización.

### <a name="update-all"></a>Actualizar todo

Ahora puede actualizar todos los paquetes de su sitio web en un solo paso.  Al abrir la extensión NuGet en WebMatrix, verá la lista de todos los paquetes en la galería, los instalados y los que tienen actualizaciones disponibles.  Anteriormente, cada paquete tendría que actualizarse individualmente, pero ahora hay un útil botón "Actualizar todo" que se muestra en la pestaña actualizaciones.

![Haga clic en Actualizar todo para actualizar todos los paquetes con las actualizaciones disponibles](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Sobrescribir archivos existentes

Cuando se instalan paquetes que contienen archivos que ya existen en el sitio web, NuGet siempre ha omitido los archivos de forma silenciosa (sin tener en cuenta los archivos existentes).  Esto podría dar lugar a la impresión de que un paquete se instaló o actualizó correctamente cuando no era así.  NuGet pedirá ahora que se sobrescriban los archivos.

![Resolución de conflictos de archivo](./media/NuGet-2.8/webmatrix-overwrite-file.png)
