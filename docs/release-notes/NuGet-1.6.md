---
title: Notas de la versión 1.6 de NuGet
description: Notas de la versión 1.6 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549017"
---
 # <a name="nuget-16-release-notes"></a>Notas de la versión 1.6 de NuGet

[Notas de la versión 1.5 de NuGet](../release-notes/nuget-1.5.md) | [notas de la versión 1.7 de NuGet](../release-notes/nuget-1.7.md)

1.6 de NuGet se publicó en el 13 de diciembre de 2011.

## <a name="known-installation-issue"></a>Problema de instalación conocidos
Si está ejecutando VS 2010 SP1, es posible que experimenta un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar NuGet y, a continuación, vuelva a instalarlo desde la Galería de extensiones de VS.  Para más información, vea [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Nota: Si Visual Studio no podrá desinstalar la extensión (está deshabilitado el botón desinstalar), a continuación, es posible que deben reiniciar Visual Studio con la opción "Ejecutar como administrador".

## <a name="features"></a>Características

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Compatibilidad con Versionamiento semántico y paquetes de versión preliminar
NuGet 1.6 introduce compatibilidad con Versionamiento semántico (SemVer). Para obtener más información sobre cómo usa SemVer, lea el [documentación de control de versiones](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Uso de NuGet sin comprobar en paquetes (restauración de paquetes)
NuGet 1.6 ahora tiene compatibilidad de primera clase para el flujo de trabajo en que NuGet paquetes no se agregan al control de código fuente, pero en su lugar se restauran en tiempo de compilación si faltan. Para obtener más información, lea el [usando NuGet sin confirmar paquetes en el control de código fuente](../consume-packages/packages-and-source-control.md) tema.

### <a name="item-templates-that-install-nuget-packages"></a>Plantillas de elemento que instalación los paquetes de NuGet
El trabajo para admitir plantillas de proyecto de Visual Studio del paquete NuGet preinstalado, NuGet 1.6 también agrega compatibilidad con plantillas de elementos de Visual Studio. Las plantillas de elemento pueden tener asociadas paquetes de NuGet que se instalan cuando se invoca la plantilla en.

Para obtener más información sobre cómo cambiar una plantilla de proyecto y elemento para instalar paquetes de NuGet, lea el [paquetes en plantillas de Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tema.

### <a name="support-for-disabling-package-sources"></a>Compatibilidad para deshabilitar los orígenes de paquetes
Cuando se configuran varios orígenes de paquetes, NuGet buscará en cada uno de los paquetes durante la instalación de un paquete y sus dependencias. Origen del paquete que está inactivo por algún motivo puede gravemente ralentizar NuGet.

Antes de NuGet 1.6, se pudo quitar el origen del paquete, pero, a continuación, tiene que recordar los detalles con la que desea agregarlo de nuevo.

NuGet 1.6 permite desactivar un origen del paquete para deshabilitarlo, pero manténgala a mano.

![Deshabilitación de un paquete](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.6 tenía un total de 106 fijo de elementos de trabajo. 95 de los que se han clasificado como errores y 10 de ellas eran las características.

Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.6, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
