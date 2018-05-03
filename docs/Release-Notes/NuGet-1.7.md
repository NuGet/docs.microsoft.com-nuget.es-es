---
title: Notas de la versión 1.7 de NuGet
description: Notas de la versión para 1.7 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-17-release-notes"></a>Notas de la versión 1.7 de NuGet

[Notas de la versión de NuGet 1.6](../release-notes/nuget-1.6.md) | [notas de la versión de NuGet 1.8](../release-notes/nuget-1.8.md)

1.7 de NuGet se publicó en 4 de abril de 2012.

## <a name="known-installation-issue"></a>Problema de instalación conocido
Si está ejecutando VS 2010 SP1, puede ejecutar en un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar simplemente NuGet y, a continuación, instalar desde la Galería de extensión de VS.  Para más información, vea [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Nota: Si Visual Studio no permiten la desinstalación (el botón de desinstalación está deshabilitado), a continuación, es posible que deben reiniciar Visual Studio usando "Ejecutar como administrador".

## <a name="features"></a>Características

### <a name="support-opening-readmetxt-file-after-installation"></a>Se admite abrir archivo readme.txt después de la instalación
Nuevo en 1.7, si el paquete incluye un `readme.txt` archivo en la raíz del paquete, NuGet abrirá automáticamente este archivo una vez que ha terminado de instalar el paquete.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostrar paquetes de versión preliminar en el cuadro de diálogo de paquetes de administración de NuGet
El cuadro de diálogo Administrar paquetes de NuGet ahora incluye una lista desplegable que proporciona la opción para mostrar los paquetes de versión preliminar.

![Mostrar paquetes de versión preliminar](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Mostrar botón Restaurar el paquete cuando faltan los archivos de paquete
Cuando se abra la consola de administrador de paquetes o paquetes de NuGet Administrador de cuadro de diálogo, NuGet comprobará si la solución actual ha habilitado el modo de restauración del paquete y si faltan los archivos de paquete en el `packages` carpeta. Si se cumplen ambas condiciones, NuGet le notificará y mostrará un botón Restaurar adecuado. Al hacer clic en este botón se desencadenará NuGet para restaurar todos los paquetes que faltan.

![Botón de restauración del paquete del cuadro de diálogo](./media/packagerestore-dialog.png)

![Botón de restauración del paquete en la consola de](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Agregar archivo packages.config de nivel de solución
En versiones anteriores de NuGet, cada proyecto tiene un `packages.config` archivo que realiza un seguimiento de los paquetes de NuGet se instalan en ese proyecto. Sin embargo, no había ningún archivo similar en el nivel de solución para realizar un seguimiento de los paquetes de nivel de solución. Como resultado, no había forma de restaurar los paquetes de nivel de solución.
Ahora, esta característica se implementa en NuGet 1.7. El nivel de solución `packages.config` archivo se coloca en el `.nuget` carpeta bajo solución raíz y se almacenarán los paquetes de nivel de solución solo.

### <a name="remove-new-package-command"></a>Quitar el comando New-Package
Se quitó debido a un uso bajo, el comando New-Package. Se recomiendan a los desarrolladores usar nuget.exe o el Explorador de paquetes de NuGet práctica para crear paquetes.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.7 resuelto muchos errores alrededor de los escenarios de Control de origen de red/y la restauración del paquete de flujo de trabajo.

Para obtener una lista completa de trabajo elementos corregidos en 1.7 de NuGet, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
