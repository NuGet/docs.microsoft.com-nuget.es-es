---
title: Comando de CLI de NuGet init
description: Referencia del comando de init de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551415"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="8087c-103">Init comandos (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="8087c-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="8087c-104">**Se aplica a:** la creación del paquete &bullet; **versiones compatibles:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="8087c-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="8087c-105">Copia todos los paquetes de una carpeta sin formato en una carpeta de destino mediante un formato jerárquico como se describió para la [Agregar comando](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="8087c-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="8087c-106">Es decir, usando `init` equivale a usar el `add` comando en cada paquete en la carpeta.</span><span class="sxs-lookup"><span data-stu-id="8087c-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="8087c-107">Igual que con `add`, el destino debe ser una carpeta local o una ruta de acceso UNC; No se admiten los repositorios de paquetes HTTP como nuget.org o servidores privados.</span><span class="sxs-lookup"><span data-stu-id="8087c-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="8087c-108">Uso</span><span class="sxs-lookup"><span data-stu-id="8087c-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="8087c-109">donde `<source>` es la carpeta que contiene paquetes y `<destination>` es la carpeta local o una ruta de acceso UNC a la que se copian los paquetes.</span><span class="sxs-lookup"><span data-stu-id="8087c-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="8087c-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="8087c-110">Options</span></span>

| <span data-ttu-id="8087c-111">Opción</span><span class="sxs-lookup"><span data-stu-id="8087c-111">Option</span></span> | <span data-ttu-id="8087c-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="8087c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8087c-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8087c-113">ConfigFile</span></span> | <span data-ttu-id="8087c-114">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="8087c-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8087c-115">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="8087c-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8087c-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8087c-116">ForceEnglishOutput</span></span> | <span data-ttu-id="8087c-117">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="8087c-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8087c-118">Expand</span><span class="sxs-lookup"><span data-stu-id="8087c-118">Expand</span></span> | <span data-ttu-id="8087c-119">Agrega todos los archivos de cada paquete que se agrega al origen del paquete; igual que `-Expand` con el `add` comando.</span><span class="sxs-lookup"><span data-stu-id="8087c-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="8087c-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="8087c-120">Help</span></span> | <span data-ttu-id="8087c-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="8087c-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="8087c-122">No interactivo</span><span class="sxs-lookup"><span data-stu-id="8087c-122">NonInteractive</span></span> | <span data-ttu-id="8087c-123">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="8087c-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8087c-124">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="8087c-124">Verbosity</span></span> | <span data-ttu-id="8087c-125">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="8087c-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8087c-126">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8087c-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8087c-127">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="8087c-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
