---
title: NuGet de la versión 5.11
description: Notas de la versión NuGet 5.11, incluidas nuevas características, correcciones de errores y DCR.
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728426"
---
# <a name="nuget-511-release-notes"></a>NuGet de la versión 5.11

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio | Disponible en los SDK de .NET |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.11](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Instalado</sup> con Visual Studio 2019 con carga de trabajo de .NET Core
  
> [!NOTE]
> Visual Studio 16.11, MSBuild 16.11 y .NET 5.0.400+ requiere NuGet.exe 5.11 o posterior.

## <a name="summary-whats-new-in-511"></a>Resumen: Novedades de la versión 5.11

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Bugs:**

* Tools -> Options -> NuGet Administrador de paquetes string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)

* Se produce un hang cuando se desencadena el evento PackagesMissingStatusChanged [( #10854](https://github.com/NuGet/Home/issues/10854)

* El NuGet no tiene en cuenta la configuración de NO_PROXY : [#10902](https://github.com/NuGet/Home/issues/10902)

**[Lista de todos los problemas corregidos en esta versión: 5.11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[Lista de confirmaciones de esta versión: 5.11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>Bienvenida a los comentarios

Sus comentarios son importantes.  Si hay algún problema con esta versión, consulte los problemas de GitHub [y](https://github.com/NuGet/Home/issues) Visual Studio [desarrolladores Community](https://developercommunity.visualstudio.com/) problemas existentes.  Para los nuevos problemas de NuGet, informe de un [GitHub problema](https://github.com/NuGet/Home/issues/new).
Para obtener NuGet problemas de experiencia general, [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) háganoslo saber a través de la opción Notificar un problema que se encuentra en su IDE favorito en Ayuda **> notificar un problema**.
