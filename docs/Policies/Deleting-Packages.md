---
title: Eliminar de nuget.org paquetes de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a348ca2e-0a5d-40ad-ba33-9bb37e1d980b
description: "Directivas para quitar paquetes de la lista en nuget.org; la eliminación permanente no se admite, excepto cuando los paquetes infringen otras directivas."
keywords: "Eliminación de paquetes de NuGet, quitar de la lista paquetes de NuGet, usos prohibidos de los paquetes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 331979bdc3703ddbeff18e2bd0e6b0a17551e68b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="deleting-packages"></a><span data-ttu-id="f7cb4-104">Eliminar paquetes</span><span class="sxs-lookup"><span data-stu-id="f7cb4-104">Deleting packages</span></span>

<span data-ttu-id="f7cb4-105">nuget.org no admite la eliminación permanente de paquetes.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-105">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="f7cb4-106">Si lo hace, se interrumpirían todos los proyectos según la disponibilidad del paquete, sobre todo con los flujos de trabajo de compilación que implican la restauración del paquete.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-106">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="f7cb4-107">nuget.org sí permite *quitar de una lista* un paquete, acción que se puede llevar a cabo en la página de administración de paquetes del sitio web.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-107">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="f7cb4-108">Los paquetes que se han quitado de la lista no constan en nuget.org ni en la interfaz de usuario de Visual Studio, ni tampoco aparecen en los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-108">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="f7cb4-109">Aun así, los paquetes que se han quitado de la lista se pueden descargar e instalar usando un número de versión exacto, que admite la restauración de paquetes.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-109">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="f7cb4-110">Además, los paquetes que se han quitado de la lista se pueden seguir detectando en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="f7cb4-110">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="f7cb4-111">Restauración de paquetes mediante versiones flotantes (por ejemplo, `1.0.0-*`) si el último paquete disponible que coincide con las restricciones de versión o de dependencia es un paquete que se ha quitado de la lista.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-111">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="f7cb4-112">Replicación de paquetes a través del catálogo (ya que el catálogo también contiene paquetes que se han quitado de la lista).</span><span class="sxs-lookup"><span data-stu-id="f7cb4-112">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="f7cb4-113">Excepciones</span><span class="sxs-lookup"><span data-stu-id="f7cb4-113">Exceptions</span></span>

<span data-ttu-id="f7cb4-114">En casos excepcionales (como la infracción de derechos de autor y el contenido potencialmente dañino), el equipo de NuGet puede eliminar los paquetes de forma manual.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-114">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="f7cb4-115">Envíe una solicitud de soporte técnico a través de la [galería de NuGet](http://www.nuget.org) para iniciar el proceso.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-115">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="f7cb4-116">Uso prohibido</span><span class="sxs-lookup"><span data-stu-id="f7cb4-116">Prohibited use</span></span>

<span data-ttu-id="f7cb4-117">Los paquetes que cumplan cualquiera de los siguientes criterios no se admiten en la galería de NuGet pública y se quitarán de inmediato sin discusión.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="f7cb4-118">Los propietarios de los paquetes recibirán una notificación sobre la eliminación.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="f7cb4-119">Contiene malware, adware o cualquier tipo de spyware.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="f7cb4-120">Está diseñado para dañar la estación de trabajo de un desarrollador o su organización.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="f7cb4-121">Vulnera los derechos de autor o infringe las licencias.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="f7cb4-122">Incluye contenido ilegal.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-122">Contains illegal content.</span></span>
- <span data-ttu-id="f7cb4-123">Se usa para apropiarse de identificadores de paquetes, incluidos los paquetes que no tienen contenido productivo.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="f7cb4-124">Los paquetes deben contener código o bien los propietarios deben ceder el identificador a alguien que tenga un producto para enviar.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="f7cb4-125">Intenta provocar que la galería haga algo para lo que no se ha diseñado expresamente.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-125">Attempt to make the gallery do something that it is not explicitly designed to do.</span></span>

<span data-ttu-id="f7cb4-126">Si encuentra un paquete que infringe cualquiera de estos puntos, haga clic en el vínculo **Notificar abuso** en la página de detalles del paquete y envíe un informe.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="f7cb4-127">Tenga en cuenta que el equipo de NuGet y .NET Foundation se reservan el derecho de modificar estos criterios en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="f7cb4-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
