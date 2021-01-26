---
title: Notas de la versión de NuGet 2.2.1
description: Notas de la versión de NuGet 2.2.1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776803"
---
# <a name="nuget-221-release-notes"></a>Notas de la versión de NuGet 2.2.1

Notas de la [versión de NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Notas de la versión de NuGet 2,5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 se lanzó el 15 de febrero de 2013.  El número de versión de la extensión de VS es 2.2.40116.9051.

## <a name="localization-refresh"></a>Actualización de la localización
Cuando NuGet se incluye como parte de Visual Studio 2012, estaba totalmente localizado en inglés + 13 otros idiomas.  Desde entonces, se han enviado NuGet 2,1 y 2,2, pero la localización no se ha actualizado.  La versión 2.2.1 de NuGet actualiza nuestra localización.

La interfaz de usuario de NuGet y la consola de PowerShell se localizan en los siguientes idiomas:

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
Si genera plantillas de Visual Studio, puede usar NuGet para [Preinstalar paquetes](../visual-studio-extensibility/visual-studio-templates.md) como parte de la plantilla.  Hasta ahora, esta característica tenía una limitación de que todos los paquetes debían provienen del mismo origen.  Sin embargo, con NuGet 2.2.1, puede tener paquetes instalados desde varios repositorios (dentro de la plantilla, un VSIX o una carpeta en el disco definidos en el registro).

El escenario principal de esta característica son las plantillas de proyecto de ASP.NET personalizadas.  Las plantillas ASP.NET integradas usan paquetes preinstalados, extrayendo paquetes del disco local.  Ahora puede crear una plantilla de proyecto ASP.NET personalizada que use los paquetes existentes instalados por ASP.NET, pero agregue paquetes NuGet adicionales a la plantilla.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2.2.1 incluye algunas correcciones de errores de destino. Para obtener una lista de los elementos de trabajo corregidos en NuGet 2.2.1, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problemas conocidos

Si va a extender plantillas de proyecto de ASP.NET, todos los repositorios de paquetes preinstalados deben usar el mismo valor para el `isPreunzipped` atributo.
