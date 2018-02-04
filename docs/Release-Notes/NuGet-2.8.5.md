---
title: "Notas de la versión de NuGet 2.8.5 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 2.8.5 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.8.5 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
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