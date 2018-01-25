---
title: "Notas de la versión de NuGet 2.2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión para 2.2 de NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "2.2 de NuGet notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 63a1ae2315ea0c26fb5d26507ac0bcba8567aa9a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-22-release-notes"></a>Notas de la versión 2.2 de NuGet

[Notas de la versión de NuGet 2.1](../release-notes/nuget-2.1.md) | [notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

2.2 de NuGet se publicó en el 12 de diciembre de 2012.

## <a name="visual-studio-quick-launch"></a>Inicio rápido de Visual Studio
Una de las nuevas características que se agregó en Visual Studio 2012 fue el [cuadro de diálogo de inicio rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). 2.2 de NuGet extiende este cuadro de diálogo, lo que le permite inicializar el cuadro de diálogo del Administrador de paquetes con los términos de búsqueda especificados en el inicio rápido. Por ejemplo, escriba 'jquery' en Inicio rápido ahora incluye una opción en los resultados para buscar paquetes de NuGet 'jquery' de la búsqueda de coincidencias.

![NuGet en Inicio rápido de Visual Studio](./media/quick-launch.png)

Al seleccionar esta opción se iniciará la experiencia de búsqueda estándar de administrador paquete de NuGet para el término 'jquery'.

![Cuadro de diálogo de administrador de paquetes de NuGet rellenada previamente](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Especificar toda la carpeta de contenido del paquete
2.2 de NuGet ahora le permite especificar una carpeta completa en el `<file>` elemento de la `.nuspec` archivo para incluir todo el contenido de esa carpeta. Por ejemplo, el código siguiente provocará todos los scripts en la carpeta de scripts del paquete para agregarse a la carpeta contents\scripts cuando se instala el paquete en un proyecto.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Actualizar 6/24/16: se omiten las carpetas vacías en la carpeta "content" al instalar el paquete.**

## <a name="known-issues"></a>Problemas conocidos

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Instalación del paquete se produce un error para los proyectos de F # cuando se usa la consola de administrador de paquetes
Al intentar instalar un paquete de NuGet en un proyecto de F # mediante la consola de administrador de paquetes, se produce una excepción InvalidOperationException. Estamos trabajando activamente con el equipo de F # para resolver el problema, pero mientras tanto, la solución es instalar los paquetes de NuGet en proyectos de F # mediante el cuadro de diálogo del Administrador de paquetes de NuGet en lugar de la consola. [Obtener más información está disponible en CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2.2 incluye numerosas correcciones de errores. Para obtener una lista completa de trabajo elementos corregidos en 2.2 de NuGet, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
