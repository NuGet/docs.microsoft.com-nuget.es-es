---
title: SDK cliente de NuGet
description: La API está evolucionando y aún no se ha documentado, pero los ejemplos están disponibles en el blog de David Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622933"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="048e9-103">SDK cliente de NuGet</span><span class="sxs-lookup"><span data-stu-id="048e9-103">NuGet Client SDK</span></span>

<span data-ttu-id="048e9-104">El *SDK de cliente de Nuget* hace referencia a un grupo de paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="048e9-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="048e9-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) : Se usa para interactuar con HTTP y fuentes de NuGet basadas en archivos.</span><span class="sxs-lookup"><span data-stu-id="048e9-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="048e9-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Se usa para interactuar con paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="048e9-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="048e9-107">`NuGet.Protocol` depende de este paquete</span><span class="sxs-lookup"><span data-stu-id="048e9-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="048e9-108">Puede encontrar el código fuente de estos paquetes en el repositorio de github [Nuget/Nuget. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="048e9-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="048e9-109">Para obtener documentación sobre el protocolo de servidor NuGet, consulte la [API del servidor de Nuget](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="048e9-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="048e9-110">Introducción</span><span class="sxs-lookup"><span data-stu-id="048e9-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="048e9-111">Instalación de los paquetes</span><span class="sxs-lookup"><span data-stu-id="048e9-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="048e9-112">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="048e9-112">Examples</span></span>

<span data-ttu-id="048e9-113">Puede encontrar estos ejemplos en el proyecto [NuGet. Protocol. samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) en github.</span><span class="sxs-lookup"><span data-stu-id="048e9-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="048e9-114">Enumerar versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="048e9-114">List package versions</span></span>

<span data-ttu-id="048e9-115">Busque todas las versiones de Newtonsoft.Jscon el uso de la [API de contenido del paquete NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="048e9-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="048e9-116">Descargar un paquete</span><span class="sxs-lookup"><span data-stu-id="048e9-116">Download a package</span></span>

<span data-ttu-id="048e9-117">Descargue Newtonsoft.Jsen v 12.0.1 con la [API de contenido de paquete de NuGet V3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="048e9-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="048e9-118">Obtener los metadatos del paquete</span><span class="sxs-lookup"><span data-stu-id="048e9-118">Get package metadata</span></span>

<span data-ttu-id="048e9-119">Obtener los metadatos del paquete "Newtonsoft.Jsen" mediante la [API de metadatos del paquete NuGet V3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="048e9-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="048e9-120">Buscar paquetes</span><span class="sxs-lookup"><span data-stu-id="048e9-120">Search packages</span></span>

<span data-ttu-id="048e9-121">Busque paquetes "JSON" mediante la [API de búsqueda de NuGet V3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="048e9-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="048e9-122">Creación de un paquete</span><span class="sxs-lookup"><span data-stu-id="048e9-122">Create a package</span></span>

<span data-ttu-id="048e9-123">Cree un paquete, establezca los metadatos y agregue dependencias mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="048e9-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="048e9-124">Se recomienda encarecidamente que los paquetes NuGet se creen con las herramientas de NuGet oficiales y **no** se use esta API de bajo nivel.</span><span class="sxs-lookup"><span data-stu-id="048e9-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="048e9-125">Hay una variedad de características importantes para un paquete con el formato correcto y la versión más reciente de las herramientas ayuda a incorporar estos procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="048e9-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="048e9-126">Para obtener más información sobre la creación de paquetes NuGet, consulte la información general del [flujo de trabajo de creación de paquetes](../create-packages/overview-and-workflow.md) y la documentación de las herramientas oficiales del paquete (por ejemplo, [mediante la CLI de dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="048e9-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="048e9-127">Leer un paquete</span><span class="sxs-lookup"><span data-stu-id="048e9-127">Read a package</span></span>

<span data-ttu-id="048e9-128">Lea un paquete de una secuencia de archivos mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="048e9-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="048e9-129">Documentación de terceros</span><span class="sxs-lookup"><span data-stu-id="048e9-129">Third-party documentation</span></span>

<span data-ttu-id="048e9-130">Puede encontrar ejemplos y documentación para algunas de las API en la siguiente serie de blog de Dave Glick, publicado 2016:</span><span class="sxs-lookup"><span data-stu-id="048e9-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="048e9-131">Exploración de las bibliotecas de NuGet V3, parte 1: introducción y conceptos</span><span class="sxs-lookup"><span data-stu-id="048e9-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="048e9-132">Exploración de las bibliotecas de NuGet V3, parte 2: búsqueda de paquetes</span><span class="sxs-lookup"><span data-stu-id="048e9-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="048e9-133">Exploración de las bibliotecas de NuGet V3, parte 3: instalación de paquetes</span><span class="sxs-lookup"><span data-stu-id="048e9-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="048e9-134">Estas entradas de blog se escribieron poco después de que se publicara la versión **3.4.3** de los paquetes del SDK del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="048e9-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="048e9-135">Las versiones más recientes de los paquetes pueden ser incompatibles con la información de las entradas de blog.</span><span class="sxs-lookup"><span data-stu-id="048e9-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="048e9-136">Martin Björkström realizó una entrada de blog de seguimiento a la serie de blogs de Dave Glick, donde presenta un enfoque diferente sobre el uso del SDK de cliente de NuGet para instalar paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="048e9-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="048e9-137">Revisar las bibliotecas de NuGet V3</span><span class="sxs-lookup"><span data-stu-id="048e9-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
