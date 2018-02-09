---
title: "Resolución de conflictos de nombres de paquetes de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Proceso de resolución de conflictos entre los publicadores de paquetes de NuGet en cuanto a la personalización de marca, las marcas comerciales y otras situaciones conflictivas."
keywords: "Conflictos de paquetes de NuGet, resolución de conflictos de NuGet, proceso de resolución de conflictos"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="ffea7-104">Resolver conflictos sobre los nombres de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="ffea7-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="ffea7-105">Este artículo ofrece un proceso de resolución recomendado para que los miembros de la comunidad resuelvan conflictos con otros publicadores de NuGet.</span><span class="sxs-lookup"><span data-stu-id="ffea7-105">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="ffea7-106">Por ejemplo, imagínese que Northwind Traders crea un sistema CRM para el que proporcionan controladores de cliente en forma de archivo MSI descargable desde su sitio web.</span><span class="sxs-lookup"><span data-stu-id="ffea7-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="ffea7-107">Nancy, una desarrolladora independiente, quiere que resulte más fácil usar la biblioteca de clientes de Northwind y la convierte en un paquete de NuGet llamado `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="ffea7-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="ffea7-108">Más adelante, Northwind quiere generar su propio paquete de NuGet oficial para su biblioteca de clientes y, por tanto, le gustaría disputar la propiedad de Nancy del nombre del paquete.</span><span class="sxs-lookup"><span data-stu-id="ffea7-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="ffea7-109">En este escenario, no parece que Nancy actúe con mala intención, pero da apoyo a las herramientas y los clientes de Northwind aportando su propio tiempo y su propio código.</span><span class="sxs-lookup"><span data-stu-id="ffea7-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="ffea7-110">Al mismo tiempo, Northwind es el propietario legítimo del nombre de Northwind.</span><span class="sxs-lookup"><span data-stu-id="ffea7-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="ffea7-111">Si siguen el siguiente procedimiento, Northwind y Nancy pueden colaborar para llegar a una solución adecuada, ya que ambos están interesados en servir a la comunidad de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="ffea7-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="ffea7-112">No suele ser necesario que el equipo de NuGet se implique. La colaboración normalmente da mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="ffea7-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="ffea7-113">De hecho, todos los conflictos puestos en conocimiento del equipo de NuGet hasta la fecha se han tratado sin que el equipo haya tenido que pronunciarse.</span><span class="sxs-lookup"><span data-stu-id="ffea7-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="ffea7-114">Proceso</span><span class="sxs-lookup"><span data-stu-id="ffea7-114">Process</span></span>

1. <span data-ttu-id="ffea7-115">Póngase en contacto con los propietarios del paquete con los que tiene el conflicto mediante el vínculo de **contacto con los propietarios** de la página de detalles del paquete.</span><span class="sxs-lookup"><span data-stu-id="ffea7-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="ffea7-116">Explique el problema de una manera amable y directa.</span><span class="sxs-lookup"><span data-stu-id="ffea7-116">Explain your issue in a kind and direct manner.</span></span>
1. <span data-ttu-id="ffea7-117">Envíe una copia del mensaje a [support@nuget.org](mailto:support@nuget.org) para que NuGet y .NET Foundation sean conscientes del conflicto.</span><span class="sxs-lookup"><span data-stu-id="ffea7-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
1. <span data-ttu-id="ffea7-118">En un plazo máximo de 30 días se emitirá una resolución. Después, vuelva a notificar a [support@nuget.org](mailto:support@nuget.org).</span><span class="sxs-lookup"><span data-stu-id="ffea7-118">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="ffea7-119">El equipo de soporte técnico de nuget.org se implicará e intentará tratar el conflicto con ambas partes.</span><span class="sxs-lookup"><span data-stu-id="ffea7-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
