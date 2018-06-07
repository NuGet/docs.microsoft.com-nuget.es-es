---
title: Comando de lista de NuGet CLI
description: Referencia del comando de lista nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818443"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="43aac-103">comando de lista (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="43aac-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="43aac-104">**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="43aac-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="43aac-105">Muestra una lista de paquetes de un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="43aac-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="43aac-106">Si no se especifica ningún origen, todos los orígenes definen en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, se utilizan.</span><span class="sxs-lookup"><span data-stu-id="43aac-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="43aac-107">Si `NuGet.Config` no especifica ningún origen, a continuación, `list` utiliza la fuente predeterminada (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="43aac-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="43aac-108">Uso</span><span class="sxs-lookup"><span data-stu-id="43aac-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="43aac-109">donde los términos de búsqueda opcional filtrará la lista que aparece.</span><span class="sxs-lookup"><span data-stu-id="43aac-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="43aac-110">Términos de búsqueda se aplican a los nombres de paquetes, etiquetas y descripciones de paquete tal como aparecen cuando se usen en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="43aac-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="43aac-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="43aac-111">Options</span></span>

| <span data-ttu-id="43aac-112">Opción</span><span class="sxs-lookup"><span data-stu-id="43aac-112">Option</span></span> | <span data-ttu-id="43aac-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="43aac-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="43aac-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="43aac-114">AllVersions</span></span> | <span data-ttu-id="43aac-115">Enumerar todas las versiones de un paquete.</span><span class="sxs-lookup"><span data-stu-id="43aac-115">List all versions of a package.</span></span> <span data-ttu-id="43aac-116">De forma predeterminada, se muestra solo la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="43aac-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="43aac-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="43aac-117">ConfigFile</span></span> | <span data-ttu-id="43aac-118">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="43aac-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="43aac-119">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="43aac-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="43aac-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="43aac-120">ForceEnglishOutput</span></span> | <span data-ttu-id="43aac-121">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="43aac-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="43aac-122">Ayuda</span><span class="sxs-lookup"><span data-stu-id="43aac-122">Help</span></span> | <span data-ttu-id="43aac-123">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="43aac-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="43aac-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="43aac-124">IncludeDelisted</span></span> | <span data-ttu-id="43aac-125">*(3.2 +)*  Muestra los paquetes que no figuran en.</span><span class="sxs-lookup"><span data-stu-id="43aac-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="43aac-126">No interactivo</span><span class="sxs-lookup"><span data-stu-id="43aac-126">NonInteractive</span></span> | <span data-ttu-id="43aac-127">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="43aac-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="43aac-128">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="43aac-128">PreRelease</span></span> | <span data-ttu-id="43aac-129">Incluye paquetes de versión preliminar en la lista.</span><span class="sxs-lookup"><span data-stu-id="43aac-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="43aac-130">Origen</span><span class="sxs-lookup"><span data-stu-id="43aac-130">Source</span></span> | <span data-ttu-id="43aac-131">Especifica una lista de orígenes de paquetes para buscar.</span><span class="sxs-lookup"><span data-stu-id="43aac-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="43aac-132">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="43aac-132">Verbosity</span></span> | <span data-ttu-id="43aac-133">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="43aac-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="43aac-134">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="43aac-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="43aac-135">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="43aac-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
