---
title: Notas de la versión de NuGet 2.8.1
description: Notas de la versión de NuGet 2.8.1 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-281-release-notes"></a>Notas de la versión de NuGet 2.8.1

[Notas de la versión de NuGet 2.8](../release-notes/nuget-2.8.md) | [notas de la versión de NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 se publicó en el 2 de abril de 2014.

## <a name="notable-features-in-the-release"></a>Características importantes de la versión

### <a name="support-for-windows-phone-81-projects"></a>Soporte técnico para los proyectos de Windows Phone 8.1
Esta versión ahora es compatible con los monikers de framework de destino nuevo siguientes que pueden usarse para proyectos de destino Windows Phone 8.1:

* WindowsPhone81 / WP81 (para los proyectos de Windows Phone basadas en Silverlight)
* WindowsPhoneApp81 / WPA81 (para los proyectos de aplicación de Windows Phone WinRT-based)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Actualización de la extensión de WebMatrix de NuGet
Esta versión actualiza el cliente de NuGet que se encuentra en WebMatrix para [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 y pone con ofrece como transformaciones XDT. Lo que es más importante, el 2.6.1 actualización principal permite al cliente de WebMatrix instalar paquetes de NuGet que contienen versiones más recientes de la `.nuspec` esquema, que incluye los paquetes de NuGet de ASP.NET.

Para obtener más información acerca de la actualización de la extensión de WebMatrix, vea los específico [notas de la versión](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Correcciones de errores
Además de estas características, esta versión de NuGet incluye otras correcciones de errores. No hay 16 problemas total cubiertos en la versión. Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8.1, por favor, vista la [NuGet Issue Tracker para esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping con Visual Studio «14» CTP
En CTP de Visual Studio "14" publicada el 3 de junio de 2014, NuGet 2.8.1 se incluye en el cuadro. Las características que admite permanecen en el par con otros 2.8.1 VSIXes como el de Visual Studio 2013.
