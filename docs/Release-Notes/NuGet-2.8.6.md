---
title: "Notas de la versión de NuGet 2.8.6 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Notas de la versión de NuGet 2.8.6 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.8.6 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f33c1edd3ef703a8cd97b7bdd97c37e12426aafa
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
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