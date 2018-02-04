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
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="d2936-104">Notas de la versión de NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="d2936-104">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="d2936-105">[Notas de la versión de NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [notas de la versión de NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="d2936-105">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="d2936-106">NuGet 2.8.6 se publicó el 20 de julio de 2015 como una actualización secundaria de nuestro 2.8.5 VSIX con algunos destino correcciones y mejoras para admitir los paquetes que se pueden suministrar con soporte para el modelo de desarrollo de UWP de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d2936-106">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="d2936-107">Esta versión de la extensión de administrador de paquetes de NuGet proporciona compatibilidad con Visual Studio 2013 solo.</span><span class="sxs-lookup"><span data-stu-id="d2936-107">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="d2936-108">En esta versión, el cuadro de diálogo Administrador de paquetes de NuGet tenía compatibilidad agregada para:</span><span class="sxs-lookup"><span data-stu-id="d2936-108">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="d2936-109">Introdujo el Moniker UAP de la plataforma de destino para admitir el desarrollo de aplicaciones de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d2936-109">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="d2936-110">Extremos de la versión 3 del protocolo de NuGet</span><span class="sxs-lookup"><span data-stu-id="d2936-110">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="d2936-111">Compatibilidad con [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion en orígenes del repositorio.</span><span class="sxs-lookup"><span data-stu-id="d2936-111">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="d2936-112">Valor predeterminado es "2"</span><span class="sxs-lookup"><span data-stu-id="d2936-112">Default value is "2"</span></span>
* <span data-ttu-id="d2936-113">Revirtiendo a repositorio remoto si una versión de paquete necesaria no está disponible en la memoria caché local</span><span class="sxs-lookup"><span data-stu-id="d2936-113">Falling back to remote repository if a required package version is not available in the local cache</span></span>