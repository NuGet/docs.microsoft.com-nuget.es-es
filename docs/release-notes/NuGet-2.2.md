---
title: Notas de la versión 2.2 de NuGet
description: Notas de la versión 2.2 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545997"
---
# <a name="nuget-22-release-notes"></a>Notas de la versión 2.2 de NuGet

[Notas de la versión 2.1 de NuGet](../release-notes/nuget-2.1.md) | [notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

2.2 de NuGet se publicó en el 12 de diciembre de 2012.

## <a name="visual-studio-quick-launch"></a>Inicio rápido de Visual Studio
Una de las nuevas características que se agregó en Visual Studio 2012 fue el [cuadro de diálogo de inicio rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 amplía este cuadro de diálogo para que puedan inicializar el cuadro de diálogo del Administrador de paquetes con los términos de búsqueda especificados en el inicio rápido. Por ejemplo, la introducción de "jquery" en Inicio rápido ahora incluye una opción en los resultados para buscar la coincidencia de "jquery" de paquetes de NuGet.

![NuGet en Inicio rápido de Visual Studio](./media/quick-launch.png)

Si selecciona esta opción, se iniciará la experiencia de búsqueda estándar de manager paquete de NuGet para el término "jquery".

![Cuadro de diálogo de administrador de paquetes de NuGet rellenada previamente](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Especifique la carpeta completa para el contenido del paquete
2.2 de NuGet ahora le permite especificar una carpeta completa en el `<file>` elemento de la `.nuspec` archivo para incluir todo el contenido de esa carpeta. Por ejemplo, el siguiente hará que todos los scripts en la carpeta de scripts del paquete que se agregará a la carpeta contents\scripts cuando el paquete se instala en un proyecto.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Actualizar 24/6/16: se omiten las carpetas vacías en la carpeta "content" al instalar el paquete.**

## <a name="known-issues"></a>Problemas conocidos

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Instalación del paquete se produce un error para los proyectos de F # cuando se usa la consola de administrador de paquetes
Al intentar instalar un paquete de NuGet en un proyecto de F # mediante la consola del Administrador de paquetes, se produce una excepción InvalidOperationException. Estamos trabajando activamente con el equipo de F # para resolver el problema, pero mientras tanto, la solución es instalar los paquetes de NuGet en proyectos de F # a través de diálogo de administrador de paquetes de NuGet en lugar de la consola. [Obtener más información está disponible en CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2.2 incluye numerosas correcciones de errores. Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.2, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
