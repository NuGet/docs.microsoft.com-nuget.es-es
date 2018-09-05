---
title: Notas de la versión de NuGet 2.2.1
description: Notas de la versión para incluir NuGet 2.2.1 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550703"
---
# <a name="nuget-221-release-notes"></a>Notas de la versión de NuGet 2.2.1

[Notas de la versión de NuGet 2.2](../release-notes/nuget-2.2.md) | [notas de la versión de NuGet 2.5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 se publicó en el 15 de febrero de 2013.  El número de versión de extensión de VS es 2.2.40116.9051.

## <a name="localization-refresh"></a>Actualización de localización
Cuando NuGet se incluye como parte de Visual Studio 2012, se ha traducido en inglés + 13 otros idiomas.  Desde entonces, se han enviado NuGet 2.1 y 2.2 pero no había se ha actualizado la localización.  La versión de NuGet 2.2.1 actualiza la localización.

Interfaz de usuario y la consola de PowerShell de NuGet están localizados en los idiomas siguientes:

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Las plantillas de Visual Studio admiten varios repositorios de paquetes preinstalados
Si se generan las plantillas de Visual Studio, puede usar NuGet para [preinstalar paquetes](../visual-studio-extensibility/visual-studio-templates.md) como parte de la plantilla.  Hasta ahora, esta característica tenía una limitación que todos los paquetes necesitan para proceden del mismo origen.  Sin embargo, con NuGet 2.2.1 puede tener los paquetes instalados en varios repositorios (dentro de la plantilla, un archivo VSIX o una carpeta en el disco definido en el registro).

El escenario principal para esta característica son plantillas de proyecto ASP.NET personalizadas.  Las plantillas ASP.NET integradas usan paquetes preinstalados, extraen paquetes desde el disco local.  Ahora puede crear una plantilla de proyecto ASP.NET personalizada que usa los paquetes existentes instalados por ASP.NET pero agregar paquetes de NuGet adicionales en la plantilla.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2.2.1 incluye algunas correcciones de errores de destino. Para obtener una lista de trabajo elementos corregidos en NuGet 2.2.1, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problemas conocidos

Si está ampliando las plantillas de proyecto ASP.NET, todos los repositorios de paquetes preinstalados deben usar el mismo valor para el `isPreunzipped` atributo.
