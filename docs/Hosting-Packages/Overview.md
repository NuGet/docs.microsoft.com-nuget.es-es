---
title: "Información general sobre el hospedaje de sus propias fuentes de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Información general sobre códigos abiertos para hospedar sus propias fuentes o galerías de paquetes de NuGet, ya sea de forma local o remota."
keywords: "Fuente de NuGet, galería de NuGet, fuente de paquetes personalizada, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 738190e20603046d075faa3f50402601890583c1
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="bda58-104">Hospedar sus propias fuentes de NuGet</span><span class="sxs-lookup"><span data-stu-id="bda58-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="bda58-105">En lugar de hacer que los paquetes estén disponibles de forma pública, es posible que quiera liberar los paquetes únicamente a un público restringido (por ejemplo, su organización o grupo de trabajo).</span><span class="sxs-lookup"><span data-stu-id="bda58-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="bda58-106">Además, puede que algunas compañías quieran restringir las bibliotecas de terceros que pueden usar sus desarrolladores y, de este modo, hacer que estos desarrolladores las saquen de un origen de paquete limitado, en lugar de sacarlas de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="bda58-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="bda58-107">Para todos estos propósitos, NuGet admite la configuración de orígenes de paquetes privados de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="bda58-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="bda58-108">Fuente local: los paquetes se colocan en un recurso compartido de red adecuado, idealmente con `nuget init` y `nuget add` para crear una estructura jerárquica de carpetas (NuGet 3.3+).</span><span class="sxs-lookup"><span data-stu-id="bda58-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="bda58-109">Para más información, vea [Fuentes locales](../hosting-packages/local-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="bda58-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="bda58-110">NuGet.Server: los paquetes están disponibles a través de un servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="bda58-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="bda58-111">Para más información, vea [NuGet.Server](../hosting-packages/nuget-server.md).</span><span class="sxs-lookup"><span data-stu-id="bda58-111">For details, see [NuGet.Server](../hosting-packages/nuget-server.md).</span></span>
- <span data-ttu-id="bda58-112">Galería de NuGet: los paquetes se hospedan en un servidor de Internet mediante el [proyecto de la galería de NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span><span class="sxs-lookup"><span data-stu-id="bda58-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="bda58-113">La galería de NuGet proporciona características y administración de usuarios, como una interfaz de usuario web amplia que permite efectuar búsquedas y explorar paquetes desde dentro del explorador, de forma similar a nuget.org.</span><span class="sxs-lookup"><span data-stu-id="bda58-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="bda58-114">Hay muchos más productos de hospedaje de NuGet que admiten las fuentes privadas remotas, como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="bda58-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="bda58-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), que también está disponible en Team Foundation Server 2017 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="bda58-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="bda58-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="bda58-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="bda58-117">[ProGet](http://inedo.com/proget) de Inedo</span><span class="sxs-lookup"><span data-stu-id="bda58-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="bda58-118">[NuGet Server](http://nugetserver.net/), un proyecto de la comunidad de Inedo</span><span class="sxs-lookup"><span data-stu-id="bda58-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="bda58-119">[NuGet Server (código abierto)](http://nuget-server.net), una implementación de código abierto parecida a NuGet Server de Inedo</span><span class="sxs-lookup"><span data-stu-id="bda58-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="bda58-120">[Artifactory](https://www.jfrog.com/artifactory/) de JFrog.</span><span class="sxs-lookup"><span data-stu-id="bda58-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="bda58-121">[Nexus](http://www.sonatype.org/nexus/) de Sonatype.</span><span class="sxs-lookup"><span data-stu-id="bda58-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="bda58-122">[TeamCity](https://www.jetbrains.com/teamcity/) de JetBrains.</span><span class="sxs-lookup"><span data-stu-id="bda58-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="bda58-123">Independientemente de cómo se hospeden los paquetes, se obtiene acceso a ellos agregándolos a la lista de orígenes disponibles en `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="bda58-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="bda58-124">Esto puede hacerse en Visual Studio como se describe en [Orígenes de paquetes](../tools/package-manager-ui.md#package-sources) o desde la línea de comandos mediante [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="bda58-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="bda58-125">La ruta de acceso a un origen puede ser un nombre de ruta de acceso de carpeta local, un nombre de red o una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="bda58-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
