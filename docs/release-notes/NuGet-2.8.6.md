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
# <a name="nuget-286-release-notes"></a><span data-ttu-id="bb34f-103">Notas de la versión de NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="bb34f-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="bb34f-104">Notas de la [versión de NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Notas de la versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="bb34f-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="bb34f-105">NuGet 2.8.6 se lanzó el 20 de julio de 2015 como una pequeña actualización de nuestra 2.8.5 VSIX con algunas correcciones y mejoras dirigidas a los paquetes de soporte que se pueden ofrecer con compatibilidad con el modelo de desarrollo de Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="bb34f-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="bb34f-106">Esta versión de la extensión del administrador de paquetes NuGet solo proporciona compatibilidad con Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="bb34f-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="bb34f-107">En esta versión, el cuadro de diálogo Administrador de paquetes NuGet tenía compatibilidad agregada para:</span><span class="sxs-lookup"><span data-stu-id="bb34f-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="bb34f-108">Incorporó el moniker de la plataforma de destino UAP para admitir el desarrollo de aplicaciones de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="bb34f-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="bb34f-109">Extremos de la versión 3 del protocolo NuGet</span><span class="sxs-lookup"><span data-stu-id="bb34f-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="bb34f-110">Compatibilidad con [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion en orígenes de repositorio.</span><span class="sxs-lookup"><span data-stu-id="bb34f-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="bb34f-111">El valor predeterminado es "2"</span><span class="sxs-lookup"><span data-stu-id="bb34f-111">Default value is "2"</span></span>
* <span data-ttu-id="bb34f-112">Vuelta al repositorio remoto si una versión del paquete necesaria no está disponible en la memoria caché local</span><span class="sxs-lookup"><span data-stu-id="bb34f-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>