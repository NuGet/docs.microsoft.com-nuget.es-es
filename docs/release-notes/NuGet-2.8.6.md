---
title: Notas de la versión de NuGet 2.8.6
description: Notas de la versión para incluir NuGet 2.8.6 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546496"
---
# <a name="nuget-286-release-notes"></a>Notas de la versión de NuGet 2.8.6

[Notas de la versión de NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [notas de la versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 se lanzó el 20 de julio de 2015 como una actualización secundaria de nuestro 2.8.5 como destino VSIX con algunas correcciones y mejoras para admitir los paquetes que se puedan entregar con compatibilidad para el modelo de desarrollo de Windows 10 UWP.

Esta versión de la extensión del Administrador de paquetes de NuGet proporciona soporte técnico para Visual Studio 2013 solo.

En esta versión, el cuadro de diálogo Administrador de paquetes de NuGet tenía ha agregado compatibilidad para:

* Introdujo el Moniker del marco de destino UAP para admitir el desarrollo de aplicaciones de Windows 10.
* Extremos de la versión 3 del protocolo de NuGet
* Compatibilidad con [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion en orígenes del repositorio. Valor predeterminado es "2"
* Recurriendo al repositorio remoto si una versión de paquete necesaria no está disponible en la memoria caché local