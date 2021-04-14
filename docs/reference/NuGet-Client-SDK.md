---
title: SDK cliente de NuGet
description: La API está evolucionando y aún no está documentada, pero hay ejemplos disponibles en el blog de Dave Quek.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387392"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="67866-103">SDK cliente de NuGet</span><span class="sxs-lookup"><span data-stu-id="67866-103">NuGet Client SDK</span></span>

<span data-ttu-id="67866-104">El *SDK de cliente de NuGet* hace referencia a un grupo de paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="67866-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="67866-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Se usa para interactuar con fuentes De NuGet basadas en archivos y HTTP</span><span class="sxs-lookup"><span data-stu-id="67866-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="67866-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : se usa para interactuar con paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="67866-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="67866-107">`NuGet.Protocol` depende de este paquete</span><span class="sxs-lookup"><span data-stu-id="67866-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="67866-108">Puede encontrar el código fuente de estos paquetes en el [repositorio NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) de GitHub.</span><span class="sxs-lookup"><span data-stu-id="67866-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="67866-109">Puede encontrar el código fuente de estos ejemplos en el proyecto [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="67866-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="67866-110">Para obtener documentación sobre el protocolo de servidor NuGet, consulte la [API del servidor NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="67866-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="67866-111">NuGet.Protocol</span><span class="sxs-lookup"><span data-stu-id="67866-111">NuGet.Protocol</span></span>

<span data-ttu-id="67866-112">Instale el `NuGet.Protocol` paquete para interactuar con fuentes de paquetes NuGet basadas en carpetas y HTTP:</span><span class="sxs-lookup"><span data-stu-id="67866-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="67866-113">`Repository.Factory` se define en el espacio `NuGet.Protocol.Core.Types` de nombres y el método es un método de extensión definido en el espacio de nombres `GetCoreV3` `NuGet.Protocol` .</span><span class="sxs-lookup"><span data-stu-id="67866-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="67866-114">Por lo tanto, deberá agregar instrucciones `using` para ambos espacios de nombres.</span><span class="sxs-lookup"><span data-stu-id="67866-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="67866-115">Enumeración de versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="67866-115">List package versions</span></span>

<span data-ttu-id="67866-116">Busque todas las versiones de Newtonsoft.Jssobre el uso de La API de contenido del paquete [NuGet V3:](../api/package-base-address-resource.md#enumerate-package-versions)</span><span class="sxs-lookup"><span data-stu-id="67866-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="67866-117">Descarga de un paquete</span><span class="sxs-lookup"><span data-stu-id="67866-117">Download a package</span></span>

<span data-ttu-id="67866-118">Descargue Newtonsoft.Jsen v12.0.1 mediante la API de contenido del paquete [NuGet V3:](../api/package-base-address-resource.md)</span><span class="sxs-lookup"><span data-stu-id="67866-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="67866-119">Obtener metadatos del paquete</span><span class="sxs-lookup"><span data-stu-id="67866-119">Get package metadata</span></span>

<span data-ttu-id="67866-120">Obtenga los metadatos del paquete "Newtonsoft.Js" mediante la API de metadatos del paquete [NuGet V3:](../api/registration-base-url-resource.md)</span><span class="sxs-lookup"><span data-stu-id="67866-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="67866-121">Buscar paquetes</span><span class="sxs-lookup"><span data-stu-id="67866-121">Search packages</span></span>

<span data-ttu-id="67866-122">Busque paquetes "json" mediante La API de búsqueda [de NuGet V3:](../api/search-query-service-resource.md)</span><span class="sxs-lookup"><span data-stu-id="67866-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="67866-123">Inserción de un paquete</span><span class="sxs-lookup"><span data-stu-id="67866-123">Push a package</span></span>

<span data-ttu-id="67866-124">Insertar un paquete mediante la [API de inserción y eliminación de NuGet V3:](../api/package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="67866-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="67866-125">Eliminación de un paquete</span><span class="sxs-lookup"><span data-stu-id="67866-125">Delete a package</span></span>

<span data-ttu-id="67866-126">Elimine un paquete mediante la API de [inserción y eliminación de NuGet V3:](../api/package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="67866-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="67866-127">Los servidores NuGet pueden interpretar una solicitud de eliminación de paquetes como una "eliminación permanente", "eliminación flexible" o "eliminación de la lista".</span><span class="sxs-lookup"><span data-stu-id="67866-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="67866-128">Por ejemplo, nuget.org interpreta la solicitud de eliminación del paquete como "no lista".</span><span class="sxs-lookup"><span data-stu-id="67866-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="67866-129">Para obtener más información sobre esta práctica, vea [la directiva Eliminar paquetes.](../nuget-org/policies/deleting-packages.md)</span><span class="sxs-lookup"><span data-stu-id="67866-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="67866-130">Trabajo con fuentes autenticadas</span><span class="sxs-lookup"><span data-stu-id="67866-130">Work with authenticated feeds</span></span>

<span data-ttu-id="67866-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) para trabajar con fuentes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="67866-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="67866-132">NuGet.Packaging</span><span class="sxs-lookup"><span data-stu-id="67866-132">NuGet.Packaging</span></span>

<span data-ttu-id="67866-133">Instale el `NuGet.Packaging` paquete para interactuar con los archivos y desde una `.nupkg` `.nuspec` secuencia:</span><span class="sxs-lookup"><span data-stu-id="67866-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="67866-134">Creación de un paquete</span><span class="sxs-lookup"><span data-stu-id="67866-134">Create a package</span></span>

<span data-ttu-id="67866-135">Cree un paquete, establezca metadatos y agregue dependencias mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="67866-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67866-136">Se recomienda encarecidamente crear paquetes NuGet mediante las  herramientas oficiales de NuGet y no usar esta API de bajo nivel.</span><span class="sxs-lookup"><span data-stu-id="67866-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="67866-137">Hay una variedad de características importantes para un paquete bien formado y la versión más reciente de las herramientas ayuda a incorporar estos procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="67866-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="67866-138">Para obtener más información sobre cómo crear [](../create-packages/overview-and-workflow.md) paquetes NuGet, consulte la información general del flujo de trabajo de creación de paquetes y la documentación de las herramientas de paquetes oficiales (por ejemplo, mediante la [CLI de dotnet).](../create-packages/creating-a-package-dotnet-cli.md)</span><span class="sxs-lookup"><span data-stu-id="67866-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="67866-139">Leer un paquete</span><span class="sxs-lookup"><span data-stu-id="67866-139">Read a package</span></span>

<span data-ttu-id="67866-140">Lea un paquete de una secuencia de archivos mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="67866-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="67866-141">Documentación de terceros</span><span class="sxs-lookup"><span data-stu-id="67866-141">Third-party documentation</span></span>

<span data-ttu-id="67866-142">Puede encontrar ejemplos y documentación para algunas de las API en la siguiente serie de blogs de Dave Blok, publicada en 2016:</span><span class="sxs-lookup"><span data-stu-id="67866-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="67866-143">Exploración de las bibliotecas de NuGet v3, Parte 1: Introducción y conceptos</span><span class="sxs-lookup"><span data-stu-id="67866-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="67866-144">Exploración de las bibliotecas de NuGet v3, Parte 2: Búsqueda de paquetes</span><span class="sxs-lookup"><span data-stu-id="67866-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="67866-145">Exploración de las bibliotecas de NuGet v3, Parte 3: Instalación de paquetes</span><span class="sxs-lookup"><span data-stu-id="67866-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="67866-146">Estas entradas de blog se escribieron poco después de que se publicara la versión **3.4.3** de los paquetes del SDK de cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="67866-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="67866-147">Las versiones más recientes de los paquetes pueden ser incompatibles con la información de las entradas de blog.</span><span class="sxs-lookup"><span data-stu-id="67866-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="67866-148">Martin Packsörkström hizo una entrada de blog de seguimiento de la serie de blogs de DaveChak en la que presenta un enfoque diferente sobre el uso del SDK de cliente de NuGet para instalar paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="67866-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="67866-149">Revisión de las bibliotecas de NuGet v3</span><span class="sxs-lookup"><span data-stu-id="67866-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
