---
title: Notas de la versión de NuGet 2.8.5
description: Notas de la versión de NuGet 2.8.5 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820084"
---
# <a name="nuget-285-release-notes"></a>Notas de la versión de NuGet 2.8.5

[Notas de la versión de NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [notas de la versión de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 se publicó el 30 de marzo de 2015. Es una actualización secundaria a nuestro 2.8.3 VSIX con algunos dirigida correcciones.

En esta versión, se agregó la compatibilidad de cuadro de diálogo Administrador de paquetes de NuGet para [Monikers de Framework de destino de DNX](https://github.com/aspnet/dnx).  Estos nuevos monikers de framework que se admiten se incluyen:

* **core50** : un moniker de la plataforma (TFM) que es compatible con el núcleo de CLR de destino 'base'.
* **dnx452** : TFM A aplicaciones específicas basadas en DNX mediante la 4.5.2 completa versión de framework
* **dnx46** : TFM A aplicaciones específicas basadas en DNX utilizando la versión 4.6 completa de framework
* **dnxcore50** : TFM A aplicaciones específicas basadas en DNX utilizando la versión 5.0 de núcleo de framework

Se corrigió producidos por paquetes evita que se instale correctamente en proyectos de FSharp a un error:

https://nuget.codeplex.com/workitem/4400