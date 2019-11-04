---
title: Comando list de la CLI de NuGet
description: Referencia del comando de lista Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327742"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="84be6-103">List (comando) (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="84be6-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="84be6-104">**Se aplica a: consumo de** paquetes &bullet; , publicación de **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="84be6-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="84be6-105">Muestra una lista de paquetes de un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="84be6-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="84be6-106">Si no se especifica ningún origen, se usan todos los orígenes definidos en el `%AppData%\NuGet\NuGet.Config` archivo de configuración global `~/.nuget/NuGet/NuGet.Config`, (Windows) o.</span><span class="sxs-lookup"><span data-stu-id="84be6-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="84be6-107">Si `NuGet.Config` no especifica ningún origen `list` , utiliza la fuente predeterminada (Nuget.org).</span><span class="sxs-lookup"><span data-stu-id="84be6-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="84be6-108">Uso</span><span class="sxs-lookup"><span data-stu-id="84be6-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="84be6-109">donde los términos de búsqueda opcionales filtrarán la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="84be6-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="84be6-110">Los términos de búsqueda se aplican a los nombres de los paquetes, etiquetas y descripciones de paquetes tal y como se usan en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="84be6-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="84be6-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="84be6-111">Options</span></span>

| <span data-ttu-id="84be6-112">Opción</span><span class="sxs-lookup"><span data-stu-id="84be6-112">Option</span></span> | <span data-ttu-id="84be6-113">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="84be6-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84be6-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="84be6-114">AllVersions</span></span> | <span data-ttu-id="84be6-115">Enumera todas las versiones de un paquete.</span><span class="sxs-lookup"><span data-stu-id="84be6-115">List all versions of a package.</span></span> <span data-ttu-id="84be6-116">De forma predeterminada, solo se muestra la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="84be6-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="84be6-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="84be6-117">ConfigFile</span></span> | <span data-ttu-id="84be6-118">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="84be6-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="84be6-119">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="84be6-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="84be6-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="84be6-120">ForceEnglishOutput</span></span> | <span data-ttu-id="84be6-121">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="84be6-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="84be6-122">Help</span><span class="sxs-lookup"><span data-stu-id="84be6-122">Help</span></span> | <span data-ttu-id="84be6-123">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="84be6-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="84be6-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="84be6-124">IncludeDelisted</span></span> | <span data-ttu-id="84be6-125">*(3,2 +)* Muestra los paquetes que no aparecen en la lista.</span><span class="sxs-lookup"><span data-stu-id="84be6-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="84be6-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="84be6-126">NonInteractive</span></span> | <span data-ttu-id="84be6-127">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="84be6-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="84be6-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="84be6-128">PreRelease</span></span> | <span data-ttu-id="84be6-129">Incluye paquetes de versiones preliminares en la lista.</span><span class="sxs-lookup"><span data-stu-id="84be6-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="84be6-130">Source</span><span class="sxs-lookup"><span data-stu-id="84be6-130">Source</span></span> | <span data-ttu-id="84be6-131">Especifica una lista de los orígenes de paquetes que se van a buscar.</span><span class="sxs-lookup"><span data-stu-id="84be6-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="84be6-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="84be6-132">Verbosity</span></span> | <span data-ttu-id="84be6-133">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="84be6-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="84be6-134">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="84be6-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="84be6-135">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="84be6-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
