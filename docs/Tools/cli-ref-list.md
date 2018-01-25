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
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="ddb1c-104">comando de lista (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ddb1c-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="ddb1c-105">**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="ddb1c-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ddb1c-106">Muestra una lista de paquetes de un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="ddb1c-107">Si no se especifica ningún origen, todos los orígenes definen en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config`, se utilizan.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="ddb1c-108">Si `NuGet.Config` no especifica ningún origen, a continuación, `list` utiliza la fuente predeterminada (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="ddb1c-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="ddb1c-109">Uso</span><span class="sxs-lookup"><span data-stu-id="ddb1c-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="ddb1c-110">donde los términos de búsqueda opcional filtrará la lista que aparece.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="ddb1c-111">Términos de búsqueda se aplican a los nombres de paquetes, etiquetas y descripciones de paquete.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="ddb1c-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="ddb1c-112">Options</span></span>

| <span data-ttu-id="ddb1c-113">Opción</span><span class="sxs-lookup"><span data-stu-id="ddb1c-113">Option</span></span> | <span data-ttu-id="ddb1c-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="ddb1c-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ddb1c-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="ddb1c-115">AllVersions</span></span> | <span data-ttu-id="ddb1c-116">Enumerar todas las versiones de un paquete.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-116">List all versions of a package.</span></span> <span data-ttu-id="ddb1c-117">De forma predeterminada, se muestra solo la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="ddb1c-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ddb1c-118">ConfigFile</span></span> | <span data-ttu-id="ddb1c-119">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ddb1c-120">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ddb1c-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ddb1c-121">ForceEnglishOutput</span></span> | <span data-ttu-id="ddb1c-122">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ddb1c-123">Ayuda</span><span class="sxs-lookup"><span data-stu-id="ddb1c-123">Help</span></span> | <span data-ttu-id="ddb1c-124">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="ddb1c-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="ddb1c-125">IncludeDelisted</span></span> | <span data-ttu-id="ddb1c-126">*(3.2 +)*  Muestra los paquetes que no figuran en.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="ddb1c-127">No interactivo</span><span class="sxs-lookup"><span data-stu-id="ddb1c-127">NonInteractive</span></span> | <span data-ttu-id="ddb1c-128">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ddb1c-129">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="ddb1c-129">PreRelease</span></span> | <span data-ttu-id="ddb1c-130">Incluye paquetes de versión preliminar en la lista.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="ddb1c-131">Origen</span><span class="sxs-lookup"><span data-stu-id="ddb1c-131">Source</span></span> | <span data-ttu-id="ddb1c-132">Especifica una lista de orígenes de paquetes para buscar.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="ddb1c-133">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="ddb1c-133">Verbosity</span></span> | <span data-ttu-id="ddb1c-134">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="ddb1c-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ddb1c-135">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ddb1c-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ddb1c-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ddb1c-136">Examples</span></span>

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
