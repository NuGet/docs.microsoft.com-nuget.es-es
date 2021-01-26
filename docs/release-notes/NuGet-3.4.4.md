---
title: Notas de la versión de NuGet 3.4.4
description: Notas de la versión de 3.4.4 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780226"
---
# <a name="nuget-344-release-notes"></a>Notas de la versión de NuGet 3.4.4

Notas de la [versión de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [Notas de la versión de NuGet 3,5-beta](../release-notes/nuget-3.5-Beta.md)

El objetivo principal de esta versión es mejorar la calidad de la versión de 3.4.3 de nuget.exe con algunas correcciones de la extensión de Visual Studio.

Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).

## <a name="344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Registro de cambios completo](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Cambios

- Mejoras en los paquetes: mejoras en el empaquetado de símbolos, empaquetado con `project.json` y más [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)
- Mostrar excepción cuando se produce un error al buscar proyectos en el comando de actualización [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- Leer el tipo de paquete de la entrada `.nuspec` y `project.json` al empaquetar [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)
- Haga que NuGet. Shared no sea un proyecto. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Usar el tiempo de espera de la inserciones como el tiempo de espera de respuesta HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)
- Los archivos de paquete con tiempos futuros no tendrán su tiempo en usarse [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- Actualización `NuGet.Core.dll` de la versión a 2.12.0 para corregir el problema de XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- Compatibilidad con./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- Mostrar error al restaurar sin `project.json` o `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)
- Corregir versiones de dependencia cuando las versiones requeridas difieren de [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)