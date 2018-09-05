---
title: Notas de la versión de NuGet 2.8.1
description: Notas de la versión para incluir NuGet 2.8.1 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545244"
---
# <a name="nuget-281-release-notes"></a>Notas de la versión de NuGet 2.8.1

[Notas de la versión de NuGet 2.8](../release-notes/nuget-2.8.md) | [notas de la versión de NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 se publicó en el 2 de abril de 2014.

## <a name="notable-features-in-the-release"></a>Características importantes de la versión

### <a name="support-for-windows-phone-81-projects"></a>Compatibilidad con proyectos de Windows Phone 8.1
Esta versión admite ahora los monikers de framework de destino nueva siguientes que se pueden usar para los proyectos tienen como destino Windows Phone 8.1:

* WindowsPhone81 / WP81 (para los proyectos de Windows Phone basadas en Silverlight)
* WindowsPhoneApp81 / WPA81 (para los proyectos de aplicación de Windows Phone basada en WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Actualización de la extensión de WebMatrix de NuGet
Esta versión actualiza el cliente de NuGet se encuentra en WebMatrix para [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 y lleva con las características como las transformaciones XDT. Más importante aún, la 2.6.1 actualización core permite que el cliente de WebMatrix instalar paquetes de NuGet que contienen las versiones más recientes de la `.nuspec` esquema, que incluye los paquetes de NuGet de ASP.NET.

Para obtener más información acerca de la actualización de la extensión de WebMatrix, consulte esas específicas [notas de la versión](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Correcciones de errores
Además de estas características, esta versión de NuGet incluye otras correcciones de errores. Se produjeron 16 total de problemas solucionado en la versión. Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8.1, por favor, ver el [Issue Tracker para esta versión de NuGet](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping con Visual Studio "14" CTP
En Visual Studio "14" CTP publicada de 3 de junio de 2014, NuGet 2.8.1 se incluye en el cuadro. Las características admiten permanecen en el par con otros 2.8.1 VSIXes como el de Visual Studio 2013.
