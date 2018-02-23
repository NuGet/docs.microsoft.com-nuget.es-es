---
title: comandos de NuGet dotNet | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Una referencia breve para los comandos relacionados con NuGet mediante la interfaz de línea de comandos de dotnet."
keywords: "comandos de NuGet dotnet, dotnet pack, restauración dotnet, variables locales de nuget dotnet, dotnet nuget inserción, dotnet nuget delete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="a5b75-104">comandos de dotNet.</span><span class="sxs-lookup"><span data-stu-id="a5b75-104">dotNet commands</span></span>

<span data-ttu-id="a5b75-105">El `dotnet` interfaz de línea de comandos, que se ejecuta en Windows, Mac OS X y Linux, proporciona una serie de comandos nuget.exe esenciales, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="a5b75-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="a5b75-106">Si dotnet satisface sus necesidades, no es necesario utilizar `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="a5b75-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="a5b75-107">Para obtener información completa sobre `dotnet`, consulte [herramientas de interfaz de línea de comandos (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="a5b75-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="a5b75-108">Consumo de paquete</span><span class="sxs-lookup"><span data-stu-id="a5b75-108">Package consumption</span></span>

- <span data-ttu-id="a5b75-109">[**dotnet Agregar paquete**](/dotnet/core/tools/dotnet-add-package): agrega una referencia de paquete al archivo de proyecto, a continuación, ejecuta `dotnet restore` para instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="a5b75-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="a5b75-110">[**dotnet quitar paquete**](/dotnet/core/tools/dotnet-remove-package): quita una referencia de paquete desde el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="a5b75-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="a5b75-111">[**restauración de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura las dependencias y las herramientas de generación de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="a5b75-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="a5b75-112">A partir de NuGet 4.0, se ejecuta el mismo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="a5b75-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="a5b75-113">[**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): borra o listas de recursos locales de NuGet, como la memoria caché de la solicitud http y la memoria caché temporal, la carpeta paquetes global de todo el equipo.</span><span class="sxs-lookup"><span data-stu-id="a5b75-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="a5b75-114">Creación de paquetes</span><span class="sxs-lookup"><span data-stu-id="a5b75-114">Package creation</span></span>

- <span data-ttu-id="a5b75-115">[**módulo de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): el código de los módulos en un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="a5b75-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="a5b75-116">A partir de NuGet 4.0, se ejecuta el mismo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="a5b75-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="a5b75-117">[**inserción de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-push): inserta un paquete en un servidor y lo publica, aplicables a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.</span><span class="sxs-lookup"><span data-stu-id="a5b75-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="a5b75-118">[**eliminar dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): elimina o unlists un paquete desde un host, se aplica a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.</span><span class="sxs-lookup"><span data-stu-id="a5b75-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
