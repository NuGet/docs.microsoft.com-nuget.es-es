---
title: comandos de NuGet de la CLI de dotnet
description: Una referencia breve para los comandos relacionados con NuGet mediante la interfaz de línea de comandos de dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426002"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="89077-103">comandos de la CLI de dotnet</span><span class="sxs-lookup"><span data-stu-id="89077-103">dotnet CLI commands</span></span>

<span data-ttu-id="89077-104">El `dotnet` interfaz de línea de comandos (CLI), que se ejecuta en Windows, Mac OS X y Linux, proporciona una serie de comandos esenciales como la instalación, restauración y publicación de paquetes.</span><span class="sxs-lookup"><span data-stu-id="89077-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="89077-105">Si dotnet satisface sus necesidades, no es necesario usar `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="89077-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="89077-106">Para obtener ejemplos del uso de estos comandos para consumir paquetes, vea [instalar y administrar paquetes mediante la CLI de dotnet](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="89077-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="89077-107">Para obtener ejemplos del uso de estos comandos para crear paquetes, vea [crear y publicar un paquete con la CLI de dotnet]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="89077-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="89077-108">Para la referencia de comandos completa en `dotnet` CLI, consulte [herramientas de interfaz de línea de comandos (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="89077-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="89077-109">Consumo de paquetes</span><span class="sxs-lookup"><span data-stu-id="89077-109">Package consumption</span></span>

- <span data-ttu-id="89077-110">[**dotnet Agregar paquete**](/dotnet/core/tools/dotnet-add-package): Agrega una referencia de paquete al archivo de proyecto, a continuación, ejecuta `dotnet restore` para instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="89077-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="89077-111">[**dotnet quitar paquete**](/dotnet/core/tools/dotnet-remove-package): Quita una referencia de paquete desde el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="89077-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="89077-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restaura las dependencias y las herramientas de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="89077-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="89077-113">A partir de NuGet 4.0, se ejecuta el mismo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="89077-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="89077-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Se enumeran las ubicaciones de la *global-packages*, *http-cache*, y *temp* carpetas y borra el contenido de esas carpetas.</span><span class="sxs-lookup"><span data-stu-id="89077-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="89077-115">Creación de paquetes</span><span class="sxs-lookup"><span data-stu-id="89077-115">Package creation</span></span>

- <span data-ttu-id="89077-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Empaqueta el código en un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="89077-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="89077-117">A partir de NuGet 4.0, se ejecuta el mismo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="89077-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="89077-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Inserta un paquete en un servidor y lo publica, aplicables a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.</span><span class="sxs-lookup"><span data-stu-id="89077-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="89077-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o quita de la lista un paquete desde un host, se aplica a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.</span><span class="sxs-lookup"><span data-stu-id="89077-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
