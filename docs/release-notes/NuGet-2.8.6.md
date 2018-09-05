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
# <a name="nuget-286-release-notes"></a><span data-ttu-id="cefcb-103">Notas de la versión de NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="cefcb-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="cefcb-104">[Notas de la versión de NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [notas de la versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="cefcb-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="cefcb-105">NuGet 2.8.6 se lanzó el 20 de julio de 2015 como una actualización secundaria de nuestro 2.8.5 como destino VSIX con algunas correcciones y mejoras para admitir los paquetes que se puedan entregar con compatibilidad para el modelo de desarrollo de Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="cefcb-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="cefcb-106">Esta versión de la extensión del Administrador de paquetes de NuGet proporciona soporte técnico para Visual Studio 2013 solo.</span><span class="sxs-lookup"><span data-stu-id="cefcb-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="cefcb-107">En esta versión, el cuadro de diálogo Administrador de paquetes de NuGet tenía ha agregado compatibilidad para:</span><span class="sxs-lookup"><span data-stu-id="cefcb-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="cefcb-108">Introdujo el Moniker del marco de destino UAP para admitir el desarrollo de aplicaciones de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="cefcb-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="cefcb-109">Extremos de la versión 3 del protocolo de NuGet</span><span class="sxs-lookup"><span data-stu-id="cefcb-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="cefcb-110">Compatibilidad con [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion en orígenes del repositorio.</span><span class="sxs-lookup"><span data-stu-id="cefcb-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="cefcb-111">Valor predeterminado es "2"</span><span class="sxs-lookup"><span data-stu-id="cefcb-111">Default value is "2"</span></span>
* <span data-ttu-id="cefcb-112">Recurriendo al repositorio remoto si una versión de paquete necesaria no está disponible en la memoria caché local</span><span class="sxs-lookup"><span data-stu-id="cefcb-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>