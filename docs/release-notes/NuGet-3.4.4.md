---
title: Notas de la versión de NuGet 3.4.4
description: Notas de la versión de NuGet 3.4.4 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820872"
---
# <a name="nuget-344-release-notes"></a>Notas de la versión de NuGet 3.4.4

[Notas de la versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [notas de la versión 3.5 Beta de NuGet](../release-notes/nuget-3.5-Beta.md)

El objetivo principal de esta versión fue las mejoras a la calidad del 3.4.3 versión de nuget.exe con algunas correcciones a la extensión de Visual Studio también.

Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Registro de cambios completo](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Cambios

- Mejoras de módulo: Mejoras empaquetado símbolos, empaquetado con `project.json` y más [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Mostrar excepciones cuando se produce un error de búsqueda de proyectos en el comando de actualización [\#605] ()https://github.com/NuGet/NuGet.Client/pull/605
- Lee el tipo de paquete de la entrada `.nuspec` y `project.json` cuando empaquetado [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Asegúrese de NuGet.Shared no es un proyecto. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Usar el tiempo de espera de inserción como el tiempo de espera de la respuesta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Archivos de paquete con tiempos de futuras no tendrán sus tiempos usa [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Actualizar `NuGet.Core.dll` versión 2.12.0 para solucionar el problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Admitir./NuGet.CommandLine.XPlat - v \<detalle\> \<modo\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Mostrar error restaurar sin `project.json` o `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Corregir las versiones de dependencia cuando difieren de las versiones necesarias [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)