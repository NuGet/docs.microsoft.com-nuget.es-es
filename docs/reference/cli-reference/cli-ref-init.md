---
title: Comando init de la CLI de NuGet
description: Referencia del comando de inicialización de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327782"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="147f1-103">comando init (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="147f1-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="147f1-104">**Se aplica a:** &bullet; **versiones compatibles con** la creación de paquetes: 3.3+</span><span class="sxs-lookup"><span data-stu-id="147f1-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="147f1-105">Copia todos los paquetes de una carpeta plana en una carpeta de destino mediante un diseño jerárquico, tal como se describe en el [comando agregar](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="147f1-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="147f1-106">Es decir, el `init` uso de es equivalente al `add` uso del comando en cada paquete de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="147f1-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="147f1-107">Al igual `add`que con, el destino debe ser una carpeta local o una ruta de acceso UNC; No se admiten repositorios de paquetes HTTP, como nuget.org o servidores privados.</span><span class="sxs-lookup"><span data-stu-id="147f1-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="147f1-108">Uso</span><span class="sxs-lookup"><span data-stu-id="147f1-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="147f1-109">donde `<source>` es la carpeta que contiene los `<destination>` paquetes y es la carpeta local o el directorio UNC en el que se copian los paquetes.</span><span class="sxs-lookup"><span data-stu-id="147f1-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="147f1-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="147f1-110">Options</span></span>

| <span data-ttu-id="147f1-111">Opción</span><span class="sxs-lookup"><span data-stu-id="147f1-111">Option</span></span> | <span data-ttu-id="147f1-112">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="147f1-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="147f1-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="147f1-113">ConfigFile</span></span> | <span data-ttu-id="147f1-114">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="147f1-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="147f1-115">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="147f1-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="147f1-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="147f1-116">ForceEnglishOutput</span></span> | <span data-ttu-id="147f1-117">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="147f1-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="147f1-118">Expand</span><span class="sxs-lookup"><span data-stu-id="147f1-118">Expand</span></span> | <span data-ttu-id="147f1-119">Agrega todos los archivos de cada paquete que se agregan al origen del paquete. igual que `-Expand` con el `add` comando.</span><span class="sxs-lookup"><span data-stu-id="147f1-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="147f1-120">Help</span><span class="sxs-lookup"><span data-stu-id="147f1-120">Help</span></span> | <span data-ttu-id="147f1-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="147f1-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="147f1-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="147f1-122">NonInteractive</span></span> | <span data-ttu-id="147f1-123">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="147f1-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="147f1-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="147f1-124">Verbosity</span></span> | <span data-ttu-id="147f1-125">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="147f1-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="147f1-126">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="147f1-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="147f1-127">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="147f1-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
