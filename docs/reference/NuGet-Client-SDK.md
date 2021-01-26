---
title: SDK cliente de NuGet
description: La API está evolucionando y aún no se ha documentado, pero los ejemplos están disponibles en el blog de David Glick.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: e89b50601deb204892536406b4ddabf7005e0642
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776127"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="50a95-103">SDK cliente de NuGet</span><span class="sxs-lookup"><span data-stu-id="50a95-103">NuGet Client SDK</span></span>

<span data-ttu-id="50a95-104">El *SDK de cliente de Nuget* hace referencia a un grupo de paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="50a95-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="50a95-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) : Se usa para interactuar con HTTP y fuentes de NuGet basadas en archivos.</span><span class="sxs-lookup"><span data-stu-id="50a95-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="50a95-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Se usa para interactuar con paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="50a95-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="50a95-107">`NuGet.Protocol` depende de este paquete</span><span class="sxs-lookup"><span data-stu-id="50a95-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="50a95-108">Puede encontrar el código fuente de estos paquetes en el repositorio de github [Nuget/Nuget. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="50a95-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="50a95-109">Puede encontrar el código fuente de estos ejemplos en el proyecto [NuGet. Protocol. samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) en github.</span><span class="sxs-lookup"><span data-stu-id="50a95-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="50a95-110">Para obtener documentación sobre el protocolo de servidor NuGet, consulte la [API del servidor de Nuget](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="50a95-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="50a95-111">NuGet. Protocolo</span><span class="sxs-lookup"><span data-stu-id="50a95-111">NuGet.Protocol</span></span>

<span data-ttu-id="50a95-112">Instale el `NuGet.Protocol` paquete para interactuar con http y fuentes de paquetes NuGet basadas en carpetas:</span><span class="sxs-lookup"><span data-stu-id="50a95-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a><span data-ttu-id="50a95-113">Enumerar versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="50a95-113">List package versions</span></span>

<span data-ttu-id="50a95-114">Busque todas las versiones de Newtonsoft.Jscon el uso de la [API de contenido del paquete NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="50a95-114">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="50a95-115">Descargar un paquete</span><span class="sxs-lookup"><span data-stu-id="50a95-115">Download a package</span></span>

<span data-ttu-id="50a95-116">Descargue Newtonsoft.Jsen v 12.0.1 con la [API de contenido de paquete de NuGet V3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="50a95-116">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="50a95-117">Obtener los metadatos del paquete</span><span class="sxs-lookup"><span data-stu-id="50a95-117">Get package metadata</span></span>

<span data-ttu-id="50a95-118">Obtener los metadatos del paquete "Newtonsoft.Jsen" mediante la [API de metadatos del paquete NuGet V3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="50a95-118">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="50a95-119">Buscar paquetes</span><span class="sxs-lookup"><span data-stu-id="50a95-119">Search packages</span></span>

<span data-ttu-id="50a95-120">Busque paquetes "JSON" mediante la [API de búsqueda de NuGet V3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="50a95-120">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="50a95-121">Inserte un paquete</span><span class="sxs-lookup"><span data-stu-id="50a95-121">Push a package</span></span>

<span data-ttu-id="50a95-122">Inserte un paquete mediante la [API de extracción y eliminación de NuGet V3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="50a95-122">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="50a95-123">Eliminación de un paquete</span><span class="sxs-lookup"><span data-stu-id="50a95-123">Delete a package</span></span>

<span data-ttu-id="50a95-124">Eliminar un paquete mediante la [API de extracción y eliminación de NuGet V3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="50a95-124">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="50a95-125">Los servidores NuGet pueden interpretar de forma gratuita una solicitud de eliminación de paquetes como una "eliminación temporal", "eliminación temporal" o "quitar de la lista".</span><span class="sxs-lookup"><span data-stu-id="50a95-125">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="50a95-126">Por ejemplo, nuget.org interpreta la solicitud de eliminación de paquetes como una "unlist".</span><span class="sxs-lookup"><span data-stu-id="50a95-126">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="50a95-127">Para obtener más información acerca de esta práctica, consulte la directiva [eliminar paquetes](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="50a95-127">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="50a95-128">Trabajar con fuentes autenticadas</span><span class="sxs-lookup"><span data-stu-id="50a95-128">Work with authenticated feeds</span></span>

<span data-ttu-id="50a95-129">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) para trabajar con fuentes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="50a95-129">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="50a95-130">NuGet. Packaging</span><span class="sxs-lookup"><span data-stu-id="50a95-130">NuGet.Packaging</span></span>

<span data-ttu-id="50a95-131">Instale el `NuGet.Packaging` paquete para interactuar con `.nupkg` `.nuspec` los archivos y de una secuencia:</span><span class="sxs-lookup"><span data-stu-id="50a95-131">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="50a95-132">Creación de un paquete</span><span class="sxs-lookup"><span data-stu-id="50a95-132">Create a package</span></span>

<span data-ttu-id="50a95-133">Cree un paquete, establezca los metadatos y agregue dependencias mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="50a95-133">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50a95-134">Se recomienda encarecidamente que los paquetes NuGet se creen con las herramientas de NuGet oficiales y **no** se use esta API de bajo nivel.</span><span class="sxs-lookup"><span data-stu-id="50a95-134">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="50a95-135">Hay una variedad de características importantes para un paquete con el formato correcto y la versión más reciente de las herramientas ayuda a incorporar estos procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="50a95-135">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="50a95-136">Para obtener más información sobre la creación de paquetes NuGet, consulte la información general del [flujo de trabajo de creación de paquetes](../create-packages/overview-and-workflow.md) y la documentación de las herramientas oficiales del paquete (por ejemplo, [mediante la CLI de dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="50a95-136">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="50a95-137">Leer un paquete</span><span class="sxs-lookup"><span data-stu-id="50a95-137">Read a package</span></span>

<span data-ttu-id="50a95-138">Lea un paquete de una secuencia de archivos mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="50a95-138">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="50a95-139">Documentación de terceros</span><span class="sxs-lookup"><span data-stu-id="50a95-139">Third-party documentation</span></span>

<span data-ttu-id="50a95-140">Puede encontrar ejemplos y documentación para algunas de las API en la siguiente serie de blog de Dave Glick, publicado 2016:</span><span class="sxs-lookup"><span data-stu-id="50a95-140">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="50a95-141">Exploración de las bibliotecas de NuGet V3, parte 1: introducción y conceptos</span><span class="sxs-lookup"><span data-stu-id="50a95-141">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="50a95-142">Exploración de las bibliotecas de NuGet V3, parte 2: búsqueda de paquetes</span><span class="sxs-lookup"><span data-stu-id="50a95-142">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="50a95-143">Exploración de las bibliotecas de NuGet V3, parte 3: instalación de paquetes</span><span class="sxs-lookup"><span data-stu-id="50a95-143">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="50a95-144">Estas entradas de blog se escribieron poco después de que se publicara la versión **3.4.3** de los paquetes del SDK del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="50a95-144">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="50a95-145">Las versiones más recientes de los paquetes pueden ser incompatibles con la información de las entradas de blog.</span><span class="sxs-lookup"><span data-stu-id="50a95-145">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="50a95-146">Martin Björkström realizó una entrada de blog de seguimiento a la serie de blogs de Dave Glick, donde presenta un enfoque diferente sobre el uso del SDK de cliente de NuGet para instalar paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="50a95-146">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="50a95-147">Revisar las bibliotecas de NuGet V3</span><span class="sxs-lookup"><span data-stu-id="50a95-147">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
