---
title: "Notas de la versión de NuGet 1.6 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ed433790-99bf-4b71-92a8-17314bd49867
description: "Notas de la versión de 1.6 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 1.6 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7824d62cb73c54205175ec742cfc26d1ca3aa741
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
 # <a name="nuget-16-release-notes"></a>Notas de la versión 1.6 de NuGet

[Notas de la versión 1.5 de NuGet](../release-notes/nuget-1.5.md) | [notas de la versión 1.7 de NuGet](../release-notes/nuget-1.7.md)

1.6 de NuGet se publicó en el 13 de diciembre de 2011.

## <a name="known-installation-issue"></a>Problema de instalación conocido
Si está ejecutando VS 2010 SP1, puede ejecutar en un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar simplemente NuGet y, a continuación, instalar desde la Galería de extensión de VS.  Vea [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obtener más información.

Nota: Si Visual Studio no permiten la desinstalación (el botón de desinstalación está deshabilitado), a continuación, es posible que deben reiniciar Visual Studio usando "Ejecutar como administrador".

## <a name="features"></a>Características

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Compatibilidad con control de versiones semántico y paquetes de versión preliminar
NuGet 1.6 introduce compatibilidad con control de versiones semántico (SemVer). Para obtener más información sobre cómo usa SemVer, lea la [documentación del control de versiones](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Uso de NuGet sin comprobar en los paquetes (restauración del paquete)
NuGet 1.6 tiene ahora compatibilidad de primera clase para el flujo de trabajo en qué NuGet paquetes no se agregan al control de código fuente, pero en su lugar se restauran en tiempo de compilación si no se especifica. Para obtener más información, lea la [usar NuGet sin confirmar paquetes en el control de código fuente](../consume-packages/packages-and-source-control.md) tema.

### <a name="item-templates-that-install-nuget-packages"></a>Plantillas de elementos que instalación paquetes de NuGet
El trabajo para admitir el paquete de NuGet preinstalado en las plantillas de proyecto de Visual Studio, NuGet 1.6 también agrega compatibilidad con plantillas de elementos de Visual Studio. Plantillas de elementos pueden tener asociados paquetes de NuGet que se instalan cuando se invoca la plantilla en.

Para obtener más información sobre cómo cambiar una plantilla de proyecto o este artículo para instalar paquetes de NuGet, lea la [paquetes en plantillas de Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tema.

### <a name="support-for-disabling-package-sources"></a>Compatibilidad para deshabilitar orígenes de paquetes
Cuando se configuran varios orígenes de paquetes, NuGet buscará en cada uno de los paquetes durante la instalación de un paquete y sus dependencias. Un origen de paquete que está inactivo por algún motivo puede graves ralentizan NuGet.

Antes de NuGet 1.6, puede quitar el origen del paquete, pero, a continuación, se tienen que recordar los detalles para cuando desee agregarla de nuevo.

NuGet 1.6 permite desactivar un origen del paquete para deshabilitarlo, pero conservarla.

![Deshabilitar un paquete](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.6 tenía un total de 106 fijo de elementos de trabajo. 95 de ellas se clasifican como errores y 10 de esas sin características.

Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.6, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
