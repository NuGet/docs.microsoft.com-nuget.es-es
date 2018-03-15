---
title: Comando de lista de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia del comando de lista nuget.exe
keywords: paquetes de lista de referencia de la lista de NuGet, comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7e0945b9e64a15a839f62bde0a0ef8f3d83335d4
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="b0da2-104">comando de lista (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b0da2-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="b0da2-105">**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="b0da2-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b0da2-106">Muestra una lista de paquetes de un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="b0da2-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="b0da2-107">Si no se especifica ningún origen, todos los orígenes definen en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, se utilizan.</span><span class="sxs-lookup"><span data-stu-id="b0da2-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="b0da2-108">Si `NuGet.Config` no especifica ningún origen, a continuación, `list` utiliza la fuente predeterminada (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="b0da2-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="b0da2-109">Uso</span><span class="sxs-lookup"><span data-stu-id="b0da2-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="b0da2-110">donde los términos de búsqueda opcional filtrará la lista que aparece.</span><span class="sxs-lookup"><span data-stu-id="b0da2-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="b0da2-111">Términos de búsqueda se aplican a los nombres de paquetes, etiquetas y descripciones de paquete tal como aparecen cuando se usen en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b0da2-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="b0da2-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="b0da2-112">Options</span></span>

| <span data-ttu-id="b0da2-113">Opción</span><span class="sxs-lookup"><span data-stu-id="b0da2-113">Option</span></span> | <span data-ttu-id="b0da2-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="b0da2-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0da2-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="b0da2-115">AllVersions</span></span> | <span data-ttu-id="b0da2-116">Enumerar todas las versiones de un paquete.</span><span class="sxs-lookup"><span data-stu-id="b0da2-116">List all versions of a package.</span></span> <span data-ttu-id="b0da2-117">De forma predeterminada, se muestra solo la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="b0da2-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="b0da2-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b0da2-118">ConfigFile</span></span> | <span data-ttu-id="b0da2-119">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="b0da2-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b0da2-120">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="b0da2-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b0da2-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b0da2-121">ForceEnglishOutput</span></span> | <span data-ttu-id="b0da2-122">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="b0da2-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b0da2-123">Ayuda</span><span class="sxs-lookup"><span data-stu-id="b0da2-123">Help</span></span> | <span data-ttu-id="b0da2-124">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="b0da2-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="b0da2-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="b0da2-125">IncludeDelisted</span></span> | <span data-ttu-id="b0da2-126">*(3.2 +)*  Muestra los paquetes que no figuran en.</span><span class="sxs-lookup"><span data-stu-id="b0da2-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="b0da2-127">No interactivo</span><span class="sxs-lookup"><span data-stu-id="b0da2-127">NonInteractive</span></span> | <span data-ttu-id="b0da2-128">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="b0da2-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b0da2-129">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="b0da2-129">PreRelease</span></span> | <span data-ttu-id="b0da2-130">Incluye paquetes de versión preliminar en la lista.</span><span class="sxs-lookup"><span data-stu-id="b0da2-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="b0da2-131">Origen</span><span class="sxs-lookup"><span data-stu-id="b0da2-131">Source</span></span> | <span data-ttu-id="b0da2-132">Especifica una lista de orígenes de paquetes para buscar.</span><span class="sxs-lookup"><span data-stu-id="b0da2-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="b0da2-133">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="b0da2-133">Verbosity</span></span> | <span data-ttu-id="b0da2-134">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="b0da2-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b0da2-135">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b0da2-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b0da2-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="b0da2-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
