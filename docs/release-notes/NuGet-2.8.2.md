---
title: Notas de la versión de NuGet 2.8.2
description: Notas de la versión de 2.8.2 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780365"
---
# <a name="nuget-282-release-notes"></a>Notas de la versión de NuGet 2.8.2

Notas de la [versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

2.8.2 de NuGet se lanzó el 22 de mayo de 2014.  Esta versión solo incluye los cambios en el nuget.exe línea de comandos, el paquete NuGet. Server y otros paquetes NuGet.  La versión no incluía una extensión de Visual Studio o una extensión WebMatrix actualizada.

## <a name="notable-updates"></a>Actualizaciones importantes

Las actualizaciones más destacadas estaban en la línea de comandos nuget.exe y el paquete NuGet. Server (para las fuentes NuGet autohospedadas).

### <a name="important-nugetexe-bug-fixes"></a>Correcciones de errores nuget.exe importantes

1. [ Se produce un error en lanuget.exe de la extracción y sigue intentándolo](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe la instalación de inserciones no envía las credenciales de autenticación básicas correctamente](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe inserciones no sigue la redirección temporal](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Corrección de errores importantes de NuGet. Server

1. [Valor incorrecto de IsAbsoluteLatestVersion devuelto por NuGet. Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Paquetes actualizados

Las correcciones de nuget.exe línea de comandos y NuGet. Server se incluyen como actualizaciones de paquetes NuGet.  También había otros paquetes actualizados con 2.8.2.

Esta es la lista de paquetes actualizados:

1. [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet. Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (el paquete, no la extensión)

## <a name="all-changes"></a>Todos los cambios
Se han solucionado 10 problemas en la versión. Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2.8.2, consulte el [seguimiento de problemas de Nuget en esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
