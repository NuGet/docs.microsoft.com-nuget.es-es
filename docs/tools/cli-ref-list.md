---
title: Comando de la lista de la CLI de NuGet
description: Referencia del comando de la lista de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549806"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="d00d3-103">comando de lista (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="d00d3-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="d00d3-104">**Se aplica a:** consumo de paquetes, publicar &bullet; **versiones compatibles:** todas</span><span class="sxs-lookup"><span data-stu-id="d00d3-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d00d3-105">Muestra una lista de paquetes desde un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="d00d3-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="d00d3-106">Si no se especifica ningún origen, todos los orígenes definen en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, se usan.</span><span class="sxs-lookup"><span data-stu-id="d00d3-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="d00d3-107">Si `NuGet.Config` no especifica ningún origen, a continuación, `list` utiliza la fuente predeterminada (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="d00d3-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="d00d3-108">Uso</span><span class="sxs-lookup"><span data-stu-id="d00d3-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="d00d3-109">donde los términos de búsqueda opcional filtrarán la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="d00d3-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="d00d3-110">Términos de búsqueda se aplican a los nombres de paquetes, las etiquetas y descripciones de paquetes, tal como aparecen cuando se usen en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d00d3-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="d00d3-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="d00d3-111">Options</span></span>

| <span data-ttu-id="d00d3-112">Opción</span><span class="sxs-lookup"><span data-stu-id="d00d3-112">Option</span></span> | <span data-ttu-id="d00d3-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="d00d3-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d00d3-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="d00d3-114">AllVersions</span></span> | <span data-ttu-id="d00d3-115">Enumerar todas las versiones de un paquete.</span><span class="sxs-lookup"><span data-stu-id="d00d3-115">List all versions of a package.</span></span> <span data-ttu-id="d00d3-116">De forma predeterminada, se muestra solo la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="d00d3-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="d00d3-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d00d3-117">ConfigFile</span></span> | <span data-ttu-id="d00d3-118">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="d00d3-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d00d3-119">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="d00d3-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d00d3-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d00d3-120">ForceEnglishOutput</span></span> | <span data-ttu-id="d00d3-121">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="d00d3-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d00d3-122">Ayuda</span><span class="sxs-lookup"><span data-stu-id="d00d3-122">Help</span></span> | <span data-ttu-id="d00d3-123">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="d00d3-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="d00d3-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="d00d3-124">IncludeDelisted</span></span> | <span data-ttu-id="d00d3-125">*(3.2 y versiones posteriores)*  Muestra los paquetes que están ocultos.</span><span class="sxs-lookup"><span data-stu-id="d00d3-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="d00d3-126">No interactivo</span><span class="sxs-lookup"><span data-stu-id="d00d3-126">NonInteractive</span></span> | <span data-ttu-id="d00d3-127">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="d00d3-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d00d3-128">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="d00d3-128">PreRelease</span></span> | <span data-ttu-id="d00d3-129">Incluye paquetes de versión preliminar en la lista.</span><span class="sxs-lookup"><span data-stu-id="d00d3-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="d00d3-130">Origen</span><span class="sxs-lookup"><span data-stu-id="d00d3-130">Source</span></span> | <span data-ttu-id="d00d3-131">Especifica una lista de los orígenes de paquetes para buscar.</span><span class="sxs-lookup"><span data-stu-id="d00d3-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="d00d3-132">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="d00d3-132">Verbosity</span></span> | <span data-ttu-id="d00d3-133">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="d00d3-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d00d3-134">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d00d3-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d00d3-135">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d00d3-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
