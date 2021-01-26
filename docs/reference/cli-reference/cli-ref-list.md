---
title: Comando list de la CLI de NuGet
description: Referencia del comando list de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780054"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="5cfdd-103">List (comando) (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="5cfdd-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="5cfdd-104">**Se aplica a: consumo de** paquetes, publicación de &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="5cfdd-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5cfdd-105">Muestra una lista de paquetes de un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="5cfdd-106">Si no se especifica ningún origen, se usan todos los orígenes definidos en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="5cfdd-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="5cfdd-107">Si `NuGet.Config` no especifica ningún origen, `list` utiliza la fuente predeterminada (Nuget.org).</span><span class="sxs-lookup"><span data-stu-id="5cfdd-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="5cfdd-108">Uso</span><span class="sxs-lookup"><span data-stu-id="5cfdd-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="5cfdd-109">donde los términos de búsqueda opcionales filtrarán la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="5cfdd-110">Los [términos de búsqueda](../../consume-packages/finding-and-choosing-packages.md#search-syntax) se aplican a los nombres de los paquetes, etiquetas y descripciones de paquetes tal y como se usan en Nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="5cfdd-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="5cfdd-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="5cfdd-112">Enumera todas las versiones de un paquete.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-112">List all versions of a package.</span></span> <span data-ttu-id="5cfdd-113">De forma predeterminada, solo se muestra la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="5cfdd-114">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5cfdd-115">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5cfdd-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="5cfdd-116">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="5cfdd-117">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="5cfdd-118">*(3,2 +)* Muestra los paquetes que no aparecen en la lista.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="5cfdd-119">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="5cfdd-120">Incluye paquetes de versiones preliminares en la lista.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="5cfdd-121">Origen del paquete que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-121">The package source to search.</span></span> <span data-ttu-id="5cfdd-122">Puede especificar varios orígenes mediante la `-Source` opción varias veces.</span><span class="sxs-lookup"><span data-stu-id="5cfdd-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="5cfdd-123">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="5cfdd-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="5cfdd-124">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5cfdd-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5cfdd-125">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5cfdd-125">Examples</span></span>

<span data-ttu-id="5cfdd-126">Enumerar todos los paquetes de las fuentes configuradas:</span><span class="sxs-lookup"><span data-stu-id="5cfdd-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="5cfdd-127">Enumere los paquetes relacionados con Azure con un nivel de detalle detallado:</span><span class="sxs-lookup"><span data-stu-id="5cfdd-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="5cfdd-128">Enumerar todas las versiones de los paquetes relacionados con Azure de las fuentes configuradas:</span><span class="sxs-lookup"><span data-stu-id="5cfdd-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="5cfdd-129">Enumerar todas las versiones de los paquetes relacionados con JSON desde el origen o la fuente especificados:</span><span class="sxs-lookup"><span data-stu-id="5cfdd-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="5cfdd-130">Enumerar los paquetes relacionados con JSON de varios orígenes y fuentes:</span><span class="sxs-lookup"><span data-stu-id="5cfdd-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
