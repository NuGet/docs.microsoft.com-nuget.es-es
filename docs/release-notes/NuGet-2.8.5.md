---
title: Notas de la versión de NuGet 2.8.5
description: Notas de la versión de 2.8.5 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780362"
---
# <a name="nuget-285-release-notes"></a>Notas de la versión de NuGet 2.8.5

Notas de la [versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Notas de la versión de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

2.8.5 de NuGet se lanzó el 30 de marzo de 2015. Es una actualización secundaria de la VSIX 2.8.3 con algunas correcciones de destino.

En esta versión, se ha agregado el cuadro de diálogo del administrador de paquetes de NuGet para los [monikers de la plataforma de destino DNX](https://github.com/aspnet/dnx).  Estos nuevos monikers de Framework que se admiten son:

* **core50** : un moniker de la plataforma de destino (TFM) que es compatible con el CLR básico.
* **dnx452** : un TFM específico para aplicaciones basadas en dnx con la versión completa de 4.5.2 del marco de trabajo
* **dnx46** : un TFM específico para aplicaciones basadas en dnx con la versión completa de 4,6 del marco de trabajo
* **dnxcore50** : un TFM específico para aplicaciones basadas en dnx con la versión Core 5,0 del marco de trabajo

Se corrigió un error que impedía que los paquetes se instalaran correctamente en los proyectos de FSharp:

https://nuget.codeplex.com/workitem/4400