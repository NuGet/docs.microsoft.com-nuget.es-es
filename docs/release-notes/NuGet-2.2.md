---
title: Notas de la versión de NuGet 2,2
description: Notas de la versión de NuGet 2,2, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780438"
---
# <a name="nuget-22-release-notes"></a>Notas de la versión de NuGet 2,2

Notas de la [versión de NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

NuGet 2,2 se lanzó el 12 de diciembre de 2012.

## <a name="visual-studio-quick-launch"></a>Inicio rápido de Visual Studio
Una de las nuevas características que se agregó en Visual Studio 2012 era el [cuadro de diálogo Inicio rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2,2 extiende este cuadro de diálogo, permitiéndole inicializar el cuadro de diálogo del administrador de paquetes con los términos de búsqueda especificados en el inicio rápido. Por ejemplo, al escribir ' jQuery ' en el inicio rápido, ahora se incluye una opción en los resultados para buscar paquetes NuGet que coincidan con ' jQuery '.

![Inicio rápido de NuGet en Visual Studio](./media/quick-launch.png)

Al seleccionar esta opción se iniciará la experiencia de búsqueda del administrador de paquetes NuGet estándar para el término ' jQuery '.

![Cuadro de diálogo Administrador de paquetes NuGet rellenado previamente](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Especificar toda la carpeta para el contenido del paquete
NuGet 2,2 ahora permite especificar una carpeta completa en el `<file>` elemento del `.nuspec` archivo para incluir todo el contenido de esa carpeta. Por ejemplo, lo siguiente hará que todos los scripts de la carpeta scripts del paquete se agreguen a la carpeta contents\scripts cuando el paquete se instala en un proyecto.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Actualización 6/24/16: se omiten las carpetas vacías en la carpeta "Content" al instalar el paquete.**

## <a name="known-issues"></a>Problemas conocidos

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Se produce un error en la instalación del paquete para los proyectos de F # cuando se usa la consola del administrador de paquetes
Al intentar instalar un paquete de NuGet en un proyecto de F # mediante la consola del administrador de paquetes, se produce una excepción InvalidOperationException. Trabajamos activamente con el equipo de F # para resolver el problema, pero, mientras tanto, la solución consiste en instalar paquetes NuGet en proyectos de F # mediante el cuadro de diálogo Administrador de paquetes de NuGet en lugar de la consola. [Hay más información disponible en Codeplex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2,2 incluye muchas correcciones de errores. Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2,2, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
