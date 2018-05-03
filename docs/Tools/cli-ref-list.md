---
title: Comando de lista de NuGet CLI
description: Referencia del comando de lista nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="4cec0-103">comando de lista (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4cec0-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="4cec0-104">**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="4cec0-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4cec0-105">Muestra una lista de paquetes de un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="4cec0-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="4cec0-106">Si no se especifica ningún origen, todos los orígenes definen en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, se utilizan.</span><span class="sxs-lookup"><span data-stu-id="4cec0-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="4cec0-107">Si `NuGet.Config` no especifica ningún origen, a continuación, `list` utiliza la fuente predeterminada (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="4cec0-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="4cec0-108">Uso</span><span class="sxs-lookup"><span data-stu-id="4cec0-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="4cec0-109">donde los términos de búsqueda opcional filtrará la lista que aparece.</span><span class="sxs-lookup"><span data-stu-id="4cec0-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="4cec0-110">Términos de búsqueda se aplican a los nombres de paquetes, etiquetas y descripciones de paquete tal como aparecen cuando se usen en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4cec0-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="4cec0-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="4cec0-111">Options</span></span>

| <span data-ttu-id="4cec0-112">Opción</span><span class="sxs-lookup"><span data-stu-id="4cec0-112">Option</span></span> | <span data-ttu-id="4cec0-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="4cec0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4cec0-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="4cec0-114">AllVersions</span></span> | <span data-ttu-id="4cec0-115">Enumerar todas las versiones de un paquete.</span><span class="sxs-lookup"><span data-stu-id="4cec0-115">List all versions of a package.</span></span> <span data-ttu-id="4cec0-116">De forma predeterminada, se muestra solo la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="4cec0-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="4cec0-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4cec0-117">ConfigFile</span></span> | <span data-ttu-id="4cec0-118">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="4cec0-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4cec0-119">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="4cec0-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4cec0-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4cec0-120">ForceEnglishOutput</span></span> | <span data-ttu-id="4cec0-121">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="4cec0-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4cec0-122">Ayuda</span><span class="sxs-lookup"><span data-stu-id="4cec0-122">Help</span></span> | <span data-ttu-id="4cec0-123">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="4cec0-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="4cec0-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="4cec0-124">IncludeDelisted</span></span> | <span data-ttu-id="4cec0-125">*(3.2 +)*  Muestra los paquetes que no figuran en.</span><span class="sxs-lookup"><span data-stu-id="4cec0-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="4cec0-126">No interactivo</span><span class="sxs-lookup"><span data-stu-id="4cec0-126">NonInteractive</span></span> | <span data-ttu-id="4cec0-127">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="4cec0-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4cec0-128">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="4cec0-128">PreRelease</span></span> | <span data-ttu-id="4cec0-129">Incluye paquetes de versión preliminar en la lista.</span><span class="sxs-lookup"><span data-stu-id="4cec0-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="4cec0-130">Origen</span><span class="sxs-lookup"><span data-stu-id="4cec0-130">Source</span></span> | <span data-ttu-id="4cec0-131">Especifica una lista de orígenes de paquetes para buscar.</span><span class="sxs-lookup"><span data-stu-id="4cec0-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="4cec0-132">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="4cec0-132">Verbosity</span></span> | <span data-ttu-id="4cec0-133">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="4cec0-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4cec0-134">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4cec0-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4cec0-135">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="4cec0-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
