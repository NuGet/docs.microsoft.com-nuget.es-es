---
title: Notas de la versión de NuGet 2.8.1
description: Notas de la versión de 2.8.1 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776765"
---
# <a name="nuget-281-release-notes"></a>Notas de la versión de NuGet 2.8.1

Notas de la [versión de NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Notas de la versión de NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

2.8.1 de NuGet se publicó el 2 de abril de 2014.

## <a name="notable-features-in-the-release"></a>Características destacadas de la versión

### <a name="support-for-windows-phone-81-projects"></a>Compatibilidad con proyectos de Windows Phone 8,1
Esta versión admite ahora los siguientes monikers de la plataforma de destino que se pueden usar para tener como destino Windows Phone proyectos de 8,1:

* WindowsPhone81/WP81 (para proyectos de Windows Phone basados en Silverlight)
* WindowsPhoneApp81/WPA81 (para proyectos de aplicaciones Windows Phone basados en WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Actualización de la extensión de WebMatrix de NuGet
Esta versión actualiza el cliente de NuGet que se encuentra en WebMatrix a [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 y aporta características de ti como transformaciones XDT. Lo que es más importante, la actualización principal de 2.6.1 permite al cliente de WebMatrix instalar paquetes NuGet que contienen versiones más recientes del `.nuspec` esquema, que incluye los paquetes Nuget de ASP.net.

Para obtener más información sobre la actualización de la extensión WebMatrix, consulte las notas de la [versión](../release-notes/nuget-2.6.1-for-WebMatrix.md)específicas.

### <a name="bug-fixes"></a>Correcciones de errores
Además de estas características, esta versión de NuGet incluye otras correcciones de errores. Se han solucionado 16 problemas totales en la versión. Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2.8.1, consulte el [seguimiento de problemas de Nuget en esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reenvío con Visual Studio "14" CTP
En Visual Studio "14" CTP publicado el 3 de junio de 2014, 2.8.1 de NuGet se incluye en el cuadro. Las características que admite permanecen en su par con otras VSIXes de 2.8.1, como la de Visual Studio 2013.
