---
title: SDK de cliente de NuGet
description: La API está evolucionando y aún no se ha documentado, pero los ejemplos están disponibles en el blog de David Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924606"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="39b52-103">SDK de cliente de NuGet</span><span class="sxs-lookup"><span data-stu-id="39b52-103">NuGet Client SDK</span></span>

<span data-ttu-id="39b52-104">El *SDK de cliente de Nuget* hace referencia a un grupo de paquetes de Nuget centrados en [Nuget. Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget. Packaging](https://www.nuget.org/packages/NuGet.Packaging)y [Nuget. Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="39b52-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="39b52-105">Estos paquetes reemplazan a la biblioteca [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) anterior.</span><span class="sxs-lookup"><span data-stu-id="39b52-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="39b52-106">Para obtener documentación sobre el protocolo de servidor NuGet, consulte la [API del servidor de Nuget](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="39b52-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="39b52-107">Código fuente</span><span class="sxs-lookup"><span data-stu-id="39b52-107">Source code</span></span>

<span data-ttu-id="39b52-108">El código fuente se publica en GitHub en el proyecto [Nuget/Nuget. Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="39b52-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="39b52-109">Documentación de terceros</span><span class="sxs-lookup"><span data-stu-id="39b52-109">Third-party documentation</span></span>

<span data-ttu-id="39b52-110">Puede encontrar ejemplos y documentación para algunas de las API en la siguiente serie de blog de Dave Glick, publicado 2016:</span><span class="sxs-lookup"><span data-stu-id="39b52-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="39b52-111">Exploración de las bibliotecas de NuGet V3, parte 1: introducción y conceptos</span><span class="sxs-lookup"><span data-stu-id="39b52-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="39b52-112">Exploración de las bibliotecas de NuGet V3, parte 2: búsqueda de paquetes</span><span class="sxs-lookup"><span data-stu-id="39b52-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="39b52-113">Exploración de las bibliotecas de NuGet V3, parte 3: instalación de paquetes</span><span class="sxs-lookup"><span data-stu-id="39b52-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="39b52-114">Estas entradas de blog se escribieron poco después de que se publicara la versión **3.4.3** de los paquetes del SDK del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="39b52-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="39b52-115">Las versiones más recientes de los paquetes pueden ser incompatibles con la información de las entradas de blog.</span><span class="sxs-lookup"><span data-stu-id="39b52-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="39b52-116">Martin Björkström realizó una entrada de blog de seguimiento a la serie de blogs de Dave Glick, donde presenta un enfoque diferente sobre el uso del SDK de cliente de NuGet para la instalación de paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="39b52-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="39b52-117">Revisar las bibliotecas de NuGet V3</span><span class="sxs-lookup"><span data-stu-id="39b52-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
