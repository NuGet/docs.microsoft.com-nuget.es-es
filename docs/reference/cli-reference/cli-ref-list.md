---
title: Comando list de la CLI de NuGet
description: Referencia del comando de lista Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813343"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="69506-103">List (comando) (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="69506-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="69506-104">**Se aplica a: consumo de** paquetes, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="69506-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="69506-105">Muestra una lista de paquetes de un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="69506-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="69506-106">Si no se especifica ningún origen, se usan todos los orígenes definidos en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="69506-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="69506-107">Si `NuGet.Config` no especifica ningún origen, `list` utiliza la fuente predeterminada (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="69506-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="69506-108">Usage</span><span class="sxs-lookup"><span data-stu-id="69506-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="69506-109">donde los términos de búsqueda opcionales filtrarán la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="69506-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="69506-110">Los términos de búsqueda se aplican a los nombres de los paquetes, etiquetas y descripciones de paquetes tal y como se usan en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="69506-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="69506-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="69506-111">Options</span></span>

| <span data-ttu-id="69506-112">Opción</span><span class="sxs-lookup"><span data-stu-id="69506-112">Option</span></span> | <span data-ttu-id="69506-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="69506-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69506-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="69506-114">AllVersions</span></span> | <span data-ttu-id="69506-115">Enumera todas las versiones de un paquete.</span><span class="sxs-lookup"><span data-stu-id="69506-115">List all versions of a package.</span></span> <span data-ttu-id="69506-116">De forma predeterminada, solo se muestra la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="69506-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="69506-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="69506-117">ConfigFile</span></span> | <span data-ttu-id="69506-118">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="69506-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="69506-119">Si no se especifica, se usa `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="69506-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="69506-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="69506-120">ForceEnglishOutput</span></span> | <span data-ttu-id="69506-121">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="69506-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="69506-122">Ayuda de</span><span class="sxs-lookup"><span data-stu-id="69506-122">Help</span></span> | <span data-ttu-id="69506-123">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="69506-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="69506-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="69506-124">IncludeDelisted</span></span> | <span data-ttu-id="69506-125">*(3,2 +)* Muestra los paquetes que no aparecen en la lista.</span><span class="sxs-lookup"><span data-stu-id="69506-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="69506-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="69506-126">NonInteractive</span></span> | <span data-ttu-id="69506-127">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="69506-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="69506-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="69506-128">PreRelease</span></span> | <span data-ttu-id="69506-129">Incluye paquetes de versiones preliminares en la lista.</span><span class="sxs-lookup"><span data-stu-id="69506-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="69506-130">Origen</span><span class="sxs-lookup"><span data-stu-id="69506-130">Source</span></span> | <span data-ttu-id="69506-131">Especifica una lista de los orígenes de paquetes que se van a buscar.</span><span class="sxs-lookup"><span data-stu-id="69506-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="69506-132">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="69506-132">Verbosity</span></span> | <span data-ttu-id="69506-133">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="69506-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="69506-134">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="69506-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="69506-135">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="69506-135">Examples</span></span>

<span data-ttu-id="69506-136">Enumerar todos los paquetes de las fuentes configuradas:</span><span class="sxs-lookup"><span data-stu-id="69506-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="69506-137">Enumere los paquetes relacionados con Azure con un nivel de detalle detallado:</span><span class="sxs-lookup"><span data-stu-id="69506-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="69506-138">Enumerar todas las versiones de los paquetes relacionados con Azure de las fuentes configuradas:</span><span class="sxs-lookup"><span data-stu-id="69506-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="69506-139">Enumerar todas las versiones de los paquetes relacionados con JSON desde el origen o la fuente especificados:</span><span class="sxs-lookup"><span data-stu-id="69506-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="69506-140">Enumerar los paquetes relacionados con JSON de varios orígenes y fuentes:</span><span class="sxs-lookup"><span data-stu-id="69506-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

