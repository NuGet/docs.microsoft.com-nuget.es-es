---
title: Notas de la versión de NuGet 2.8.6
description: Notas de la versión de 2.8.6 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776709"
---
# <a name="nuget-286-release-notes"></a>Notas de la versión de NuGet 2.8.6

Notas de la [versión de NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Notas de la versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 se lanzó el 20 de julio de 2015 como una pequeña actualización de nuestra 2.8.5 VSIX con algunas correcciones y mejoras dirigidas a los paquetes de soporte que se pueden ofrecer con compatibilidad con el modelo de desarrollo de Windows 10 UWP.

Esta versión de la extensión del administrador de paquetes NuGet solo proporciona compatibilidad con Visual Studio 2013.

En esta versión, el cuadro de diálogo Administrador de paquetes NuGet tenía compatibilidad agregada para:

* Incorporó el moniker de la plataforma de destino UAP para admitir el desarrollo de aplicaciones de Windows 10.
* Extremos de la versión 3 del protocolo NuGet
* Compatibilidad con [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion en orígenes de repositorio. El valor predeterminado es "2"
* Vuelta al repositorio remoto si una versión del paquete necesaria no está disponible en la memoria caché local