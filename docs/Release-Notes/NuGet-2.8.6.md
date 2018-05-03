---
title: Notas de la versión de NuGet 2.8.6
description: Notas de la versión de NuGet 2.8.6 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-286-release-notes"></a>Notas de la versión de NuGet 2.8.6

[Notas de la versión de NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [notas de la versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 se publicó el 20 de julio de 2015 como una actualización secundaria de nuestro 2.8.5 VSIX con algunos destino correcciones y mejoras para admitir los paquetes que se pueden suministrar con soporte para el modelo de desarrollo de UWP de Windows 10.

Esta versión de la extensión de administrador de paquetes de NuGet proporciona compatibilidad con Visual Studio 2013 solo.

En esta versión, el cuadro de diálogo Administrador de paquetes de NuGet tenía compatibilidad agregada para:

* Introdujo el Moniker UAP de la plataforma de destino para admitir el desarrollo de aplicaciones de Windows 10.
* Extremos de la versión 3 del protocolo de NuGet
* Compatibilidad con [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion en orígenes del repositorio. Valor predeterminado es "2"
* Revirtiendo a repositorio remoto si una versión de paquete necesaria no está disponible en la memoria caché local