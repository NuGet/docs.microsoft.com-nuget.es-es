---
title: Notas de la versión 1.7 de NuGet
description: Notas de la versión 1.7 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551472"
---
# <a name="nuget-17-release-notes"></a>Notas de la versión 1.7 de NuGet

[Notas de la versión 1.6 de NuGet](../release-notes/nuget-1.6.md) | [notas de la versión de NuGet 1.8](../release-notes/nuget-1.8.md)

NuGet 1.7 se publicó en 4 de abril de 2012.

## <a name="known-installation-issue"></a>Problema de instalación conocidos
Si está ejecutando VS 2010 SP1, es posible que experimenta un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar NuGet y, a continuación, vuelva a instalarlo desde la Galería de extensiones de VS.  Para más información, vea [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Nota: Si Visual Studio no podrá desinstalar la extensión (está deshabilitado el botón desinstalar), a continuación, es posible que deben reiniciar Visual Studio con la opción "Ejecutar como administrador".

## <a name="features"></a>Características

### <a name="support-opening-readmetxt-file-after-installation"></a>Abra el archivo readme.txt después de la instalación de soporte técnico
Nuevo en 1.7, si el paquete incluye un `readme.txt` archivo en la raíz del paquete, NuGet abrirá automáticamente este archivo cuando termine de instalar el paquete.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostrar paquetes de versión preliminar en el cuadro de diálogo Administrar paquetes NuGet paquetes
El cuadro de diálogo Administrar paquetes de NuGet ahora incluye una lista desplegable que proporciona la opción para mostrar los paquetes de versión preliminar.

![Que muestra los paquetes de versión preliminar](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Mostrar botón de la restauración del paquete cuando faltan los archivos de paquete
Cuando se abra la consola de administrador de paquetes o paquetes de Manager NuGet cuadro de diálogo, NuGet comprobará si la solución actual ha habilitado el modo de restauración de paquetes y si faltan los archivos de paquete de la `packages` carpeta. Si se cumplen ambas condiciones, NuGet le notificará y mostrará un botón Restaurar cómodo. Al hacer clic en este botón se desencadenará NuGet para restaurar todos los paquetes que faltan.

![Botón de restauración del paquete en el cuadro de diálogo](./media/packagerestore-dialog.png)

![Botón de restauración del paquete en la consola](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Agregar archivo packages.config de nivel de solución
En versiones anteriores de NuGet, cada proyecto tiene un `packages.config` archivo que realiza un seguimiento de qué paquetes de NuGet están instalados en ese proyecto. Sin embargo, no hubo ningún archivo similar en el nivel de solución para realizar un seguimiento de los paquetes de nivel de solución. Como resultado, no hubo ninguna manera de restaurar los paquetes de nivel de solución.
Ahora, esta característica se implementa en NuGet 1.7. El nivel de solución `packages.config` archivo se coloca en el `.nuget` carpeta solución raíz y se almacenarán los paquetes de solución solo nivel.

### <a name="remove-new-package-command"></a>Quitar el comando New-Package
Se quitó debido a un uso bajo, el comando New-Package. Se recomiendan que los desarrolladores usar nuget.exe o el Explorador de paquetes NuGet útiles para crear paquetes.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.7 se corregido muchos errores en torno a la restauración del paquete de flujo de trabajo y escenarios de Control de origen o de red.

Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.7, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
