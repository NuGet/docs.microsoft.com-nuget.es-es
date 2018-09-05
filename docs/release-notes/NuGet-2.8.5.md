---
title: Notas de la versión de NuGet 2.8.5
description: Notas de la versión para incluir NuGet 2.8.5 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548630"
---
# <a name="nuget-285-release-notes"></a>Notas de la versión de NuGet 2.8.5

[Notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [notas de la versión de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 se lanzó el 30 de marzo de 2015. Es una actualización secundaria a nuestro 2.8.3 VSIX con algunos dirigida correcciones.

En esta versión, se ha agregado compatibilidad con el cuadro de diálogo Administrador de paquetes de NuGet para [DNX Monikers de la plataforma de destino](https://github.com/aspnet/dnx).  Estos nuevos monikers de la plataforma que se admiten son:

* **core50** - un moniker de la plataforma (TFM) que es compatible con Core CLR de destino 'base'.
* **dnx452** : mediante la 4.5.2 completa de aplicaciones específicas basados en DNX TFM de una versión de framework
* **dnx46** : con la versión 4.6 completa del marco de aplicaciones específicas basados en DNX un TFM
* **dnxcore50** : aplicaciones específicas basados en DNX un TFM utilizando la versión 5.0 de núcleo de framework

Uno se arregló que impedía paquetes instalen en proyectos FSharp correctamente:

https://nuget.codeplex.com/workitem/4400