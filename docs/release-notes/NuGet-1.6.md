---
title: Notas de la versión de NuGet 1,6
description: Notas de la versión de NuGet 1,6, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384142"
---
 # <a name="nuget-16-release-notes"></a>Notas de la versión de NuGet 1,6

[Notas de la versión de nuget 1,5](../release-notes/nuget-1.5.md) | notas de la [versión de Nuget 1,7](../release-notes/nuget-1.7.md)

NuGet 1,6 se lanzó el 13 de diciembre de 2011.

## <a name="known-installation-issue"></a>Problema de instalación conocido
Si está ejecutando VS 2010 SP1, es posible que se encuentre con un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar NuGet y luego instalarlo desde la galería de extensiones de VS.  Vea <https://support.microsoft.com/kb/2581019> para obtener más información.

Nota: Si Visual Studio no le permite desinstalar la extensión (el botón Desinstalar está deshabilitado), es probable que tenga que reiniciar Visual Studio con "ejecutar como administrador".

## <a name="features"></a>Características

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Compatibilidad con versiones semánticas y paquetes de versión preliminar
NuGet 1,6 presenta compatibilidad con el control de versiones semántico (SemVer). Para obtener más información sobre cómo usa SemVer, lea la [documentación de control de versiones](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Usar NuGet sin proteger los paquetes (restauración de paquetes)
NuGet 1,6 ahora tiene compatibilidad de primera clase con el flujo de trabajo en el que los paquetes NuGet no se agregan al control de código fuente, sino que se restauran en tiempo de compilación si faltan. Para obtener más información, consulte el tema [uso de NuGet sin confirmar paquetes en el control de código fuente](../consume-packages/packages-and-source-control.md) .

### <a name="item-templates-that-install-nuget-packages"></a>Plantillas de elementos que instalan paquetes NuGet
A partir del trabajo para admitir el paquete NuGet preinstalado en las plantillas de proyecto de Visual Studio, NuGet 1,6 también agrega compatibilidad con las plantillas de elementos de Visual Studio. Las plantillas de elementos pueden tener asociados paquetes NuGet que se instalan al invocar la plantilla.

Para más información sobre cómo cambiar una plantilla de proyecto o elemento para instalar paquetes NuGet, lea el tema [paquetes en plantillas de Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .

### <a name="support-for-disabling-package-sources"></a>Compatibilidad para deshabilitar orígenes de paquetes
Cuando se configuran varios orígenes de paquetes, NuGet buscará en cada uno de los paquetes durante la instalación de un paquete y sus dependencias. Un origen de paquete que está inactivo por algún motivo puede ralentizar seriamente NuGet.

Antes de NuGet 1,6, podría quitar el origen del paquete, pero debe recordar los detalles sobre cuándo desea agregarlo de nuevo.

NuGet 1,6 permite desactivar un origen de paquete para deshabilitarlo, pero mantenerlo.

![Deshabilitar un paquete](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1,6 tenía un total de 106 elementos de trabajo fijos. 95 se clasificaron como errores y 10 de ellos eran características.

Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 1,6, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
