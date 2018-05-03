---
title: Notas de la versión de NuGet 2.2.1
description: Notas de la versión de NuGet 2.2.1 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-221-release-notes"></a>Notas de la versión de NuGet 2.2.1

[Notas de la versión de NuGet 2.2](../release-notes/nuget-2.2.md) | [notas de la versión de NuGet 2.5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 se publicó en el 15 de febrero de 2013.  El número de versión de extensión de VS es 2.2.40116.9051.

## <a name="localization-refresh"></a>Actualización de localización
Cuando NuGet se envía como parte de Visual Studio 2012, se localizó totalmente en inglés + 13 otros lenguajes.  Desde entonces, incluidos NuGet 2.1 y 2.2 pero no tenía se ha actualizado la localización.  La versión de NuGet 2.2.1 actualiza la localización.

Interfaz de usuario y la consola de PowerShell de NuGet están localizados en los siguientes idiomas:

1. Chino (simplificado)
1. Chino (tradicional)
1. Checo
1. Inglés
1. Francés
1. Alemán
1. Italiano
1. Japonés
1. Coreano
1. Polaco
1. Portugués (Brasil)
1. Ruso
1. Español
1. Turco

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Plantillas de Visual Studio admiten varios repositorios de paquete preinstalado
Si generar plantillas de Visual Studio, puede usar NuGet para [preinstalar paquetes](../visual-studio-extensibility/visual-studio-templates.md) como parte de la plantilla.  Hasta ahora, esta característica era una limitación que todos los paquetes necesitan para proceden del mismo origen.  Sin embargo, con NuGet 2.2.1 puede tener paquetes instalados desde varios repositorios (dentro de la plantilla, una extensión VSIX o una carpeta en el disco definida en el registro).

El escenario principal para esta característica son plantillas de proyecto ASP.NET personalizadas.  Las plantillas ASP.NET integradas usan paquetes preinstalados, extraer paquetes desde el disco local.  Ahora puede crear una plantilla de proyecto ASP.NET personalizada que usa los paquetes existentes instalados con ASP.NET pero agregar paquetes de NuGet adicionales en la plantilla.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2.2.1 incluye algunas correcciones de errores de destino. Para obtener una lista de trabajo elementos corregidos en NuGet 2.2.1, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problemas conocidos

Si está ampliando plantillas de proyecto ASP.NET, todos los repositorios de paquete preinstalado deben usar el mismo valor para el `isPreunzipped` atributo.
