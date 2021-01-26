---
title: Notas de la versión de NuGet 1,7
description: Notas de la versión de NuGet 1,7, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777063"
---
# <a name="nuget-17-release-notes"></a>Notas de la versión de NuGet 1,7

Notas de la [versión de NuGet 1,6](../release-notes/nuget-1.6.md)  |  [Notas de la versión de NuGet 1,8](../release-notes/nuget-1.8.md)

NuGet 1,7 se lanzó el 4 de abril de 2012.

## <a name="known-installation-issue"></a>Problema de instalación conocido
Si está ejecutando VS 2010 SP1, es posible que se encuentre con un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar NuGet y luego instalarlo desde la galería de extensiones de VS.  Vea <https://support.microsoft.com/kb/2581019> para obtener más información.

Nota: Si Visual Studio no le permite desinstalar la extensión (el botón Desinstalar está deshabilitado), es probable que tenga que reiniciar Visual Studio con "ejecutar como administrador".

## <a name="features"></a>Características

### <a name="support-opening-readmetxt-file-after-installation"></a>Compatibilidad con la apertura de readme.txt archivo después de la instalación
Novedad en 1,7, si el paquete incluye un `readme.txt` archivo en la raíz del paquete, NuGet abrirá automáticamente este archivo una vez que haya terminado de instalar el paquete.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostrar paquetes de versión preliminar en el cuadro de diálogo administrar paquetes NuGet
El cuadro de diálogo administrar paquetes NuGet ahora incluye una lista desplegable que ofrece la opción de mostrar paquetes de versión preliminar.

![Mostrar paquetes de versión preliminar](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Botón Mostrar restaurar paquete cuando faltan archivos de paquete
Al abrir la consola del administrador de paquetes o el cuadro de diálogo paquetes NuGet de administrador, NuGet comprobará si la solución actual ha habilitado el modo de restauración de paquetes y si falta algún archivo de paquete en la `packages` carpeta. Si se cumplen estas dos condiciones, NuGet le notificará y mostrará un práctico botón de restauración. Al hacer clic en este botón, se desencadena NuGet para restaurar todos los paquetes que faltan.

![Botón restaurar paquete en el cuadro de diálogo](./media/packagerestore-dialog.png)

![Botón restaurar paquete en la consola](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Agregar archivo de packages.config de nivel de solución
En versiones anteriores de NuGet, cada proyecto tiene un `packages.config` archivo que realiza un seguimiento de los paquetes de Nuget que se instalan en ese proyecto. Sin embargo, no había ningún archivo similar en el nivel de la solución para realizar un seguimiento de los paquetes de nivel de solución. Como resultado, no había forma de restaurar paquetes de nivel de solución.
Esta característica ahora está implementada en NuGet 1,7. El archivo de nivel de solución `packages.config` se coloca en la carpeta de la raíz de la `.nuget` solución y solo almacena los paquetes de nivel de solución.

### <a name="remove-new-package-command"></a>Quitar New-Package comando
Debido a un uso reducido, se ha quitado el comando New-Package. Se recomienda a los desarrolladores usar nuget.exe o el práctico explorador de paquetes NuGet para crear paquetes.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1,7 ha corregido muchos errores en torno al flujo de trabajo de restauración de paquetes y escenarios de control de código fuente y red.

Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 1,7, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
