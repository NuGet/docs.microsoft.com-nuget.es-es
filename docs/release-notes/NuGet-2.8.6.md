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
ms.locfileid: "31819723"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="3e185-103">Notas de la versión de NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="3e185-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="3e185-104">[Notas de la versión de NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [notas de la versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="3e185-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="3e185-105">NuGet 2.8.6 se publicó el 20 de julio de 2015 como una actualización secundaria de nuestro 2.8.5 VSIX con algunos destino correcciones y mejoras para admitir los paquetes que se pueden suministrar con soporte para el modelo de desarrollo de UWP de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3e185-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="3e185-106">Esta versión de la extensión de administrador de paquetes de NuGet proporciona compatibilidad con Visual Studio 2013 solo.</span><span class="sxs-lookup"><span data-stu-id="3e185-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="3e185-107">En esta versión, el cuadro de diálogo Administrador de paquetes de NuGet tenía compatibilidad agregada para:</span><span class="sxs-lookup"><span data-stu-id="3e185-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="3e185-108">Introdujo el Moniker UAP de la plataforma de destino para admitir el desarrollo de aplicaciones de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3e185-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="3e185-109">Extremos de la versión 3 del protocolo de NuGet</span><span class="sxs-lookup"><span data-stu-id="3e185-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="3e185-110">Compatibilidad con [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion en orígenes del repositorio.</span><span class="sxs-lookup"><span data-stu-id="3e185-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="3e185-111">Valor predeterminado es "2"</span><span class="sxs-lookup"><span data-stu-id="3e185-111">Default value is "2"</span></span>
* <span data-ttu-id="3e185-112">Revirtiendo a repositorio remoto si una versión de paquete necesaria no está disponible en la memoria caché local</span><span class="sxs-lookup"><span data-stu-id="3e185-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>