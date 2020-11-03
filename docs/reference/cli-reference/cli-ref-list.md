---
title: Comando list de la CLI de NuGet
description: Referencia del comando list de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a6a4ee434c43ad4865dba12f039b5d545a90d3c4
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238171"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="9695a-103">List (comando) (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="9695a-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="9695a-104">**Se aplica a: consumo de** paquetes, publicación de &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="9695a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9695a-105">Muestra una lista de paquetes de un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="9695a-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="9695a-106">Si no se especifica ningún origen, se usan todos los orígenes definidos en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="9695a-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="9695a-107">Si `NuGet.Config` no especifica ningún origen, `list` utiliza la fuente predeterminada (Nuget.org).</span><span class="sxs-lookup"><span data-stu-id="9695a-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="9695a-108">Uso</span><span class="sxs-lookup"><span data-stu-id="9695a-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="9695a-109">donde los términos de búsqueda opcionales filtrarán la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="9695a-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="9695a-110">Los [términos de búsqueda](../../consume-packages/finding-and-choosing-packages.md#search-syntax) se aplican a los nombres de los paquetes, etiquetas y descripciones de paquetes tal y como se usan en Nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9695a-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="9695a-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="9695a-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="9695a-112">Enumera todas las versiones de un paquete.</span><span class="sxs-lookup"><span data-stu-id="9695a-112">List all versions of a package.</span></span> <span data-ttu-id="9695a-113">De forma predeterminada, solo se muestra la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="9695a-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="9695a-114">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="9695a-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9695a-115">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9695a-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="9695a-116">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="9695a-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="9695a-117">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="9695a-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="9695a-118">*(3,2 +)* Muestra los paquetes que no aparecen en la lista.</span><span class="sxs-lookup"><span data-stu-id="9695a-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="9695a-119">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="9695a-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="9695a-120">Incluye paquetes de versiones preliminares en la lista.</span><span class="sxs-lookup"><span data-stu-id="9695a-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="9695a-121">Especifica una lista de los orígenes de paquetes que se van a buscar.</span><span class="sxs-lookup"><span data-stu-id="9695a-121">Specifies a list of packages sources to search.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="9695a-122">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="9695a-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="9695a-123">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9695a-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9695a-124">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9695a-124">Examples</span></span>

<span data-ttu-id="9695a-125">Enumerar todos los paquetes de las fuentes configuradas:</span><span class="sxs-lookup"><span data-stu-id="9695a-125">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="9695a-126">Enumere los paquetes relacionados con Azure con un nivel de detalle detallado:</span><span class="sxs-lookup"><span data-stu-id="9695a-126">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="9695a-127">Enumerar todas las versiones de los paquetes relacionados con Azure de las fuentes configuradas:</span><span class="sxs-lookup"><span data-stu-id="9695a-127">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="9695a-128">Enumerar todas las versiones de los paquetes relacionados con JSON desde el origen o la fuente especificados:</span><span class="sxs-lookup"><span data-stu-id="9695a-128">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="9695a-129">Enumerar los paquetes relacionados con JSON de varios orígenes y fuentes:</span><span class="sxs-lookup"><span data-stu-id="9695a-129">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```