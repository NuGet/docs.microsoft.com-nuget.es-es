---
title: "NuGet 2.6.1 para notas de la versión de WebMatrix | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Notas de la versión de NuGet 2.6.1 para WebMatrix, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.6.1 de notas de la versión de WebMatrix, correcciones de errores, problemas conocidos, agregar características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6150fc34dd05c2e7ce132d2d6744b823daeb1a07
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 para notas de la versión de WebMatrix

[Notas de la versión de NuGet 2.6](../release-notes/nuget-2.6.md) | [notas de la versión 2.7 de NuGet](../release-notes/nuget-2.7.md)

El equipo de NuGet lanzó una extensión actualizada del Administrador de paquetes de NuGet para WebMatrix de 26 de marzo de 2014.  Esta actualización puede instalarse desde el [Galería de extensión de WebMatrix](http://extensions.webmatrix.com/packages/NuGetPackageManager/) mediante los siguientes pasos:

1. Abra WebMatrix 3
2. Haga clic en el icono de extensiones en la cinta de opciones de inicio
3. Seleccione la ficha actualizaciones
4. Haga clic para actualizar el Administrador de paquetes de NuGet para 2.6.1
6. Cierre y reinicie 3 de WebMatrix

## <a name="notable-changes"></a>Cambios importantes

Esta extensión actualización corrige dos de los usuarios de los problemas más importantes ha enfrentado consumo paquetes de NuGet dentro de WebMatrix.  La primera era un error de versión de esquema de NuGet y el segundo era un error que dan lugar a archivos DLL de cero bytes en el `bin` carpeta.

### <a name="nuget-schema-version-error"></a>Error de versión de esquema de NuGet

Desde el lanzamiento de WebMatrix 3, se han introducido nuevas características en NuGet que requieren una nueva versión de esquema para los paquetes de NuGet.  Al intentar administrar los paquetes de NuGet en el sitio web, estos nuevos paquetes pueden conducir a errores que se ven en WebMatrix.

![Error. La versión del esquema no es compatible. Actualice NuGet a la versión más reciente.](./media/NuGet-2.8/webmatrix-schema-version.png)

Esta última versión proporciona compatibilidad con los paquetes de NuGet más recientes, impide que se produzca este error. Ahora se pueden instalar nuevas versiones de los paquetes incluidos Microsoft.AspNet.WebPages en WebMatrix.  Algunos de estos paquetes mediante características de NuGet como [transforma XDT config](../release-notes/nuget-2.6.md#xdt), que no se admite en WebMatrix hasta ahora.

### <a name="zero-byte-dlls-in-bin-folder"></a>Archivos DLL de cero bytes en la carpeta bin

Algunos usuarios han informado de que después de instalar NuGet empaqueta en WebMatrix que incluyen los archivos DLL que se copien en la ubicación, que la presentación de archivos DLL en el `bin` carpeta como archivos de 0 bytes.  Esto interrumpe la aplicación en tiempo de ejecución.

[Este problema](https://nuget.codeplex.com/workitem/4060) ya se han corregido.

## <a name="other-recent-improvements"></a>Otras mejoras recientes

Cuando el Administrador de paquetes de NuGet 2.8 se ha publicado para Visual Studio, lanzamos también Administrador de paquetes de NuGet 2.5.0 para WebMatrix.  Aunque esto se mencionó en la [notas de la versión de NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), no lo hemos mencionado específicos de los características nuevas que introdujo la actualización.

### <a name="update-all"></a>Actualizar todo

Ahora puede actualizar todos los paquetes de su sitio web en un solo paso.  Al abrir la extensión de NuGet en WebMatrix, verá la lista de todos los paquetes en la galería, están instalados y aquellas con las actualizaciones disponibles.  Anteriormente, todos los paquetes que actualizarse de forma individual, pero ahora hay un botón "Actualizar todo" útil que se muestra en la ficha actualizaciones.

![Haga clic en Actualizar todo para actualizar todos los paquetes con las actualizaciones disponibles.](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Sobrescribir archivos existentes

Al instalar los paquetes que contienen archivos que ya existen en el sitio web, NuGet siempre en modo silencioso ha ignorado esos archivos (dejando los archivos existentes por sí solas).  Esto podría provocar la impresión de que un paquete se instaló o actualizó correctamente cuando en realidad no es.  NuGet ahora le pedirá que se sobrescriban archivos.

![Resolución de conflictos de archivos](./media/NuGet-2.8/webmatrix-overwrite-file.png)
