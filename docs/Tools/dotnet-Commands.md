---
title: comandos de NuGet dotnet.
description: Una referencia breve para los comandos relacionados con NuGet mediante la interfaz de línea de comandos de dotnet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="6596c-103">comandos de dotnet</span><span class="sxs-lookup"><span data-stu-id="6596c-103">dotnet commands</span></span>

<span data-ttu-id="6596c-104">El `dotnet` interfaz de línea de comandos, que se ejecuta en Windows, Mac OS X y Linux, proporciona una serie de comandos nuget.exe esenciales, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6596c-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="6596c-105">Si dotnet satisface sus necesidades, no es necesario utilizar `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="6596c-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="6596c-106">Para obtener información completa sobre `dotnet`, consulte [herramientas de interfaz de línea de comandos (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="6596c-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="6596c-107">Consumo de paquete</span><span class="sxs-lookup"><span data-stu-id="6596c-107">Package consumption</span></span>

- <span data-ttu-id="6596c-108">[**dotnet Agregar paquete**](/dotnet/core/tools/dotnet-add-package): agrega una referencia de paquete al archivo de proyecto, a continuación, ejecuta `dotnet restore` para instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="6596c-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="6596c-109">[**dotnet quitar paquete**](/dotnet/core/tools/dotnet-remove-package): quita una referencia de paquete desde el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="6596c-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="6596c-110">[**restauración de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura las dependencias y las herramientas de generación de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="6596c-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="6596c-111">A partir de NuGet 4.0, se ejecuta el mismo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="6596c-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="6596c-112">[**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): enumera las ubicaciones de la *global paquetes*, *caché http*, y *temp* carpetas y borra el contenido de esas carpetas.</span><span class="sxs-lookup"><span data-stu-id="6596c-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="6596c-113">Creación de paquetes</span><span class="sxs-lookup"><span data-stu-id="6596c-113">Package creation</span></span>

- <span data-ttu-id="6596c-114">[**módulo de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): el código de los módulos en un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="6596c-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="6596c-115">A partir de NuGet 4.0, se ejecuta el mismo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="6596c-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="6596c-116">[**inserción de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-push): inserta un paquete en un servidor y lo publica, aplicables a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.</span><span class="sxs-lookup"><span data-stu-id="6596c-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="6596c-117">[**eliminar dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): elimina o unlists un paquete desde un host, se aplica a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.</span><span class="sxs-lookup"><span data-stu-id="6596c-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
