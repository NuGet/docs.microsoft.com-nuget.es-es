---
title: Comando de NuGet CLI init
description: Referencia del comando de init nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817823"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="fe288-103">comando init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fe288-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="fe288-104">**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="fe288-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="fe288-105">Copia todos los paquetes de una carpeta sin formato en una carpeta de destino mediante un formato jerárquico como se describe en el [Agregar comando](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="fe288-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="fe288-106">Es decir, usando `init` equivale a utilizar el `add` comando en cada paquete en la carpeta.</span><span class="sxs-lookup"><span data-stu-id="fe288-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="fe288-107">Al igual que con `add`, el destino debe ser una carpeta local o una ruta de acceso UNC; No se admiten los repositorios de paquete HTTP, como nuget.org %s) privada.</span><span class="sxs-lookup"><span data-stu-id="fe288-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="fe288-108">Uso</span><span class="sxs-lookup"><span data-stu-id="fe288-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="fe288-109">donde `<source>` es la carpeta que contiene paquetes y `<destination>` es la carpeta local o una ruta de acceso UNC a la que se copian los paquetes.</span><span class="sxs-lookup"><span data-stu-id="fe288-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="fe288-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="fe288-110">Options</span></span>

| <span data-ttu-id="fe288-111">Opción</span><span class="sxs-lookup"><span data-stu-id="fe288-111">Option</span></span> | <span data-ttu-id="fe288-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="fe288-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe288-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fe288-113">ConfigFile</span></span> | <span data-ttu-id="fe288-114">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="fe288-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fe288-115">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="fe288-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fe288-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fe288-116">ForceEnglishOutput</span></span> | <span data-ttu-id="fe288-117">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="fe288-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fe288-118">Expand</span><span class="sxs-lookup"><span data-stu-id="fe288-118">Expand</span></span> | <span data-ttu-id="fe288-119">Agrega todos los archivos de cada paquete que se agrega al origen del paquete; igual que `-Expand` con el `add` comando.</span><span class="sxs-lookup"><span data-stu-id="fe288-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="fe288-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="fe288-120">Help</span></span> | <span data-ttu-id="fe288-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="fe288-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="fe288-122">No interactivo</span><span class="sxs-lookup"><span data-stu-id="fe288-122">NonInteractive</span></span> | <span data-ttu-id="fe288-123">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="fe288-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fe288-124">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="fe288-124">Verbosity</span></span> | <span data-ttu-id="fe288-125">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="fe288-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fe288-126">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fe288-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fe288-127">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="fe288-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
