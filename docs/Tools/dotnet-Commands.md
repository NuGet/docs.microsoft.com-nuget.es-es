---
title: comandos de NuGet dotNet | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Una referencia breve para los comandos relacionados con NuGet mediante la interfaz de línea de comandos de dotnet."
keywords: "comandos de NuGet dotnet, dotnet pack, restauración dotnet, variables locales de nuget dotnet, dotnet nuget inserción, dotnet nuget delete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="1601c-104">comandos de dotNet.</span><span class="sxs-lookup"><span data-stu-id="1601c-104">dotNet commands</span></span>

<span data-ttu-id="1601c-105">La interfaz de línea de comandos DotNet, que se ejecuta en Windows, Mac OS X y Linux, proporciona una serie de comandos de nuget.exe esenciales como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="1601c-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="1601c-106">Donde dotnet proporciona los comandos que desee, no es necesario descargar nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="1601c-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="1601c-107">[**módulo de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): el código de los módulos en un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="1601c-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="1601c-108">A partir de NuGet 4.0, se ejecuta el mismo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="1601c-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="1601c-109">[**restauración de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura las dependencias y las herramientas de generación de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="1601c-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="1601c-110">A partir de NuGet 4.0, se ejecuta el mismo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="1601c-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="1601c-111">[**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): borra o listas de recursos locales de NuGet como http-solicitud de caché, caché temporal o carpeta paquetes global de todo el equipo.</span><span class="sxs-lookup"><span data-stu-id="1601c-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="1601c-112">[**inserción de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-push): inserta un paquete en un servidor y lo publica, aplicable a nuget.org, Visual Studio Team Services o los servidores de NuGet de terceros.</span><span class="sxs-lookup"><span data-stu-id="1601c-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="1601c-113">[**eliminar dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): elimina o unlists un paquete desde un servidor, que es aplicable a nuget.org, Visual Studio Team Services o los servidores de NuGet de terceros.</span><span class="sxs-lookup"><span data-stu-id="1601c-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
