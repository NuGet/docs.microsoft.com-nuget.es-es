---
title: SDK de cliente de NuGet
description: La API está evolucionando y aún no se ha documentado, pero los ejemplos están disponibles en el blog de David Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231245"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="c472f-103">SDK de cliente de NuGet</span><span class="sxs-lookup"><span data-stu-id="c472f-103">NuGet Client SDK</span></span>

<span data-ttu-id="c472f-104">El *SDK de cliente de Nuget* hace referencia a un grupo de paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="c472f-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="c472f-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) : se usa para interactuar con http y fuentes de NuGet basadas en archivos</span><span class="sxs-lookup"><span data-stu-id="c472f-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="c472f-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : se usa para interactuar con paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="c472f-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="c472f-107">`NuGet.Protocol` depende de este paquete</span><span class="sxs-lookup"><span data-stu-id="c472f-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="c472f-108">Puede encontrar el código fuente de estos paquetes en el repositorio de github [Nuget/Nuget. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="c472f-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="c472f-109">Para obtener documentación sobre el protocolo de servidor NuGet, consulte la [API del servidor de Nuget](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="c472f-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="c472f-110">Introducción</span><span class="sxs-lookup"><span data-stu-id="c472f-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="c472f-111">Instalar el paquete</span><span class="sxs-lookup"><span data-stu-id="c472f-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="c472f-112">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c472f-112">Examples</span></span>

<span data-ttu-id="c472f-113">Puede encontrar estos ejemplos en el proyecto [NuGet. Protocol. samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) en github.</span><span class="sxs-lookup"><span data-stu-id="c472f-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="c472f-114">Enumerar versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="c472f-114">List package versions</span></span>

<span data-ttu-id="c472f-115">Busque todas las versiones de Newtonsoft. JSON mediante la [API de contenido del paquete NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="c472f-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="c472f-116">Descargar un paquete</span><span class="sxs-lookup"><span data-stu-id="c472f-116">Download a package</span></span>

<span data-ttu-id="c472f-117">Descargue Newtonsoft. JSON v 12.0.1 mediante la [API de contenido del paquete NuGet V3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="c472f-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="c472f-118">Obtener los metadatos del paquete</span><span class="sxs-lookup"><span data-stu-id="c472f-118">Get package metadata</span></span>

<span data-ttu-id="c472f-119">Obtener los metadatos del paquete "Newtonsoft. JSON" mediante la [API de metadatos del paquete NuGet V3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="c472f-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="c472f-120">Buscar paquetes</span><span class="sxs-lookup"><span data-stu-id="c472f-120">Search packages</span></span>

<span data-ttu-id="c472f-121">Busque paquetes "JSON" mediante la [API de búsqueda de NuGet V3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="c472f-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="c472f-122">Documentación de terceros</span><span class="sxs-lookup"><span data-stu-id="c472f-122">Third-party documentation</span></span>

<span data-ttu-id="c472f-123">Puede encontrar ejemplos y documentación para algunas de las API en la siguiente serie de blog de Dave Glick, publicado 2016:</span><span class="sxs-lookup"><span data-stu-id="c472f-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="c472f-124">Exploración de las bibliotecas de NuGet V3, parte 1: introducción y conceptos</span><span class="sxs-lookup"><span data-stu-id="c472f-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="c472f-125">Exploración de las bibliotecas de NuGet V3, parte 2: búsqueda de paquetes</span><span class="sxs-lookup"><span data-stu-id="c472f-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="c472f-126">Exploración de las bibliotecas de NuGet V3, parte 3: instalación de paquetes</span><span class="sxs-lookup"><span data-stu-id="c472f-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="c472f-127">Estas entradas de blog se escribieron poco después de que se publicara la versión **3.4.3** de los paquetes del SDK del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="c472f-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="c472f-128">Las versiones más recientes de los paquetes pueden ser incompatibles con la información de las entradas de blog.</span><span class="sxs-lookup"><span data-stu-id="c472f-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="c472f-129">Martin Björkström realizó una entrada de blog de seguimiento a la serie de blogs de Dave Glick, donde presenta un enfoque diferente sobre el uso del SDK de cliente de NuGet para instalar paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="c472f-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="c472f-130">Revisar las bibliotecas de NuGet V3</span><span class="sxs-lookup"><span data-stu-id="c472f-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
