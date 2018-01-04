---
title: "\"Resolución de conflictos de nombres de paquetes de NuGet | Microsoft Docs\""
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6d664378-3f7b-426e-aef3-2254d745fe60
description: "Proceso de resolución de conflictos entre los publicadores de paquetes de NuGet en cuanto a la personalización de marca, las marcas comerciales y otras situaciones conflictivas."
keywords: "Conflictos de paquetes de NuGet, resolución de conflictos de NuGet, proceso de resolución de conflictos"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32f5f766a49a2e4254a81978757d973fc5353db1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="0c749-104">Resolver conflictos sobre los nombres de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="0c749-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="0c749-105">Este documento es un proceso de resolución recomendado para que los miembros de la comunidad resuelvan conflictos con otros publicadores de NuGet.</span><span class="sxs-lookup"><span data-stu-id="0c749-105">This document is a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>  

<span data-ttu-id="0c749-106">Por ejemplo, imagínese que Northwind Traders crea un sistema CRM para el que proporcionan controladores de cliente en forma de archivo MSI descargable desde su sitio web.</span><span class="sxs-lookup"><span data-stu-id="0c749-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="0c749-107">Nancy, una desarrolladora independiente, quiere que resulte más fácil usar la biblioteca de clientes de Northwind y la convierte en un paquete de NuGet llamado `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="0c749-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="0c749-108">Más adelante, Northwind quiere generar su propio paquete de NuGet oficial para su biblioteca de clientes y, por tanto, le gustaría disputar la propiedad de Nancy del nombre del paquete.</span><span class="sxs-lookup"><span data-stu-id="0c749-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="0c749-109">En este escenario, no parece que Nancy actúe con mala intención, pero da apoyo a las herramientas y los clientes de Northwind aportando su propio tiempo y su propio código.</span><span class="sxs-lookup"><span data-stu-id="0c749-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="0c749-110">Al mismo tiempo, Northwind es el propietario legítimo del nombre de Northwind.</span><span class="sxs-lookup"><span data-stu-id="0c749-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="0c749-111">Si siguen el siguiente procedimiento, Northwind y Nancy pueden colaborar para llegar a una solución adecuada, ya que ambos están interesados en servir a la comunidad de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="0c749-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="0c749-112">No suele ser necesario que el equipo de NuGet se implique. La colaboración normalmente da mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="0c749-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="0c749-113">De hecho, todos los conflictos puestos en conocimiento del equipo de NuGet hasta la fecha se han tratado sin que el equipo haya tenido que pronunciarse.</span><span class="sxs-lookup"><span data-stu-id="0c749-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>


## <a name="process"></a><span data-ttu-id="0c749-114">Proceso</span><span class="sxs-lookup"><span data-stu-id="0c749-114">Process</span></span>

1. <span data-ttu-id="0c749-115">Póngase en contacto con los propietarios del paquete con los que tiene el conflicto mediante el vínculo de **contacto con los propietarios** de la página de detalles del paquete.</span><span class="sxs-lookup"><span data-stu-id="0c749-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="0c749-116">Explique el problema de una manera amable y directa.</span><span class="sxs-lookup"><span data-stu-id="0c749-116">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="0c749-117">Envíe una copia del mensaje a [support@nuget.org](mailto:support@nuget.org) para que NuGet y .NET Foundation sean conscientes del conflicto.</span><span class="sxs-lookup"><span data-stu-id="0c749-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="0c749-118">En un plazo máximo de 30 días se emitirá una resolución. Después, vuelva a notificar a [support@nuget.org](mailto:support@nuget.org).</span><span class="sxs-lookup"><span data-stu-id="0c749-118">Wait a maximum of 30 days for a resolution, after which notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="0c749-119">El equipo de soporte técnico de nuget.org se implicará e intentará tratar el conflicto con ambas partes.</span><span class="sxs-lookup"><span data-stu-id="0c749-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
