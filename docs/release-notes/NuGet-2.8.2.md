---
title: Notas de la versión de NuGet 2.8.2
description: Notas de la versión para incluir NuGet 2.8.2 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551153"
---
# <a name="nuget-282-release-notes"></a>Notas de la versión de NuGet 2.8.2

[Notas de la versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 se publicó en el 22 de mayo de 2014.  Esta versión incluye solo los cambios realizados en la línea de comandos nuget.exe, el paquete NuGet.Server y otros paquetes de NuGet.  La versión no incluía una extensión actualizada de Visual Studio o WebMatrix.

## <a name="notable-updates"></a>Actualizaciones importantes

Las actualizaciones más importantes se encontraban en la línea de comandos de nuget.exe y el paquete NuGet.Server (para las fuentes de NuGet autohospedados).

### <a name="important-nugetexe-bug-fixes"></a>Correcciones de errores importantes nuget.exe

1. [NuGet.exe se produce un error de inserción y sigue reintentando](https://nuget.codeplex.com/workitem/4000)
1. [Inserción de NuGet.exe no envía correctamente las credenciales de autenticación básica](https://nuget.codeplex.com/workitem/4109)
1. [Inserción de NuGet.exe no siga Redirección temporal](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Corrección de errores importantes NuGet.Server

1. [Valor incorrecto de IsAbsoluteLatestVersion devuelto por NuGet.Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Paquetes actualizados

La línea de comandos de nuget.exe y NuGet.Server correcciones se incluyen como actualizaciones de paquetes de NuGet.  Se han producido otros paquetes actualizados con 2.8.2 también.

Esta es la lista de paquetes actualizadas:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (el paquete, no la extensión)

## <a name="all-changes"></a>Todos los cambios
Se produjeron los 10 problemas solucionados en la versión. Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8.2, por favor, ver el [Issue Tracker para esta versión de NuGet](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
