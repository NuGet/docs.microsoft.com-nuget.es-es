---
title: "Notas de la versión de NuGet 2.8.2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 2.8.2 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.8.2 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f50bd1f0c981ef293a4d2ff425e0dffbdf58036c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-282-release-notes"></a>Notas de la versión de NuGet 2.8.2

[Notas de la versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 se publicó en el 22 de mayo de 2014.  Esta versión solo incluye cambios en la línea de comandos nuget.exe, el paquete de NuGet.Server y otros paquetes de NuGet.  La versión no incluía una extensión de Visual Studio actualizado o WebMatrix.

## <a name="notable-updates"></a>Actualizaciones importantes

Las actualizaciones más importantes se encontraban en la línea de comandos nuget.exe y el paquete de NuGet.Server (para las fuentes de NuGet hospedados por sí mismo).

### <a name="important-nugetexe-bug-fixes"></a>Correcciones de errores importantes nuget.exe

1. [NuGet.exe inserción produce un error y sigue reintentando](https://nuget.codeplex.com/workitem/4000)
1. [NuGet.exe inserción no envía correctamente las credenciales de autenticación básica](https://nuget.codeplex.com/workitem/4109)
1. [NuGet.exe inserción no siga Redirección temporal](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Corrección de errores importantes NuGet.Server

1. [Valor incorrecto de IsAbsoluteLatestVersion devuelto por NuGet.Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Paquetes actualizado

La línea de comandos nuget.exe y correcciones de NuGet.Server se incluyen como actualizaciones de paquetes de NuGet.  No hay otros paquetes actualizado con 2.8.2 así.

Esta es la lista de paquetes actualizados:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (el paquete, no la extensión)

## <a name="all-changes"></a>Todos los cambios
No hay 10 problemas solucionados en la versión. Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8.2, por favor, vista la [NuGet Issue Tracker para esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
