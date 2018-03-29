---
title: Comando de NuGet CLI init | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia del comando de init nuget.exe
keywords: referencia de NuGet init, comando init
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="5af3d-104">comando init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5af3d-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="5af3d-105">**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="5af3d-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="5af3d-106">Copia todos los paquetes de una carpeta sin formato en una carpeta de destino mediante un formato jerárquico como se describe en el [Agregar comando](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="5af3d-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="5af3d-107">Es decir, usando `init` equivale a utilizar el `add` comando en cada paquete en la carpeta.</span><span class="sxs-lookup"><span data-stu-id="5af3d-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="5af3d-108">Al igual que con `add`, el destino debe ser una carpeta local o una ruta de acceso UNC; No se admiten los repositorios de paquete HTTP, como nuget.org %s) privada.</span><span class="sxs-lookup"><span data-stu-id="5af3d-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="5af3d-109">Uso</span><span class="sxs-lookup"><span data-stu-id="5af3d-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="5af3d-110">donde `<source>` es la carpeta que contiene paquetes y `<destination>` es la carpeta local o una ruta de acceso UNC a la que se copian los paquetes.</span><span class="sxs-lookup"><span data-stu-id="5af3d-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="5af3d-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="5af3d-111">Options</span></span>

| <span data-ttu-id="5af3d-112">Opción</span><span class="sxs-lookup"><span data-stu-id="5af3d-112">Option</span></span> | <span data-ttu-id="5af3d-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="5af3d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5af3d-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5af3d-114">ConfigFile</span></span> | <span data-ttu-id="5af3d-115">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="5af3d-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5af3d-116">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="5af3d-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5af3d-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5af3d-117">ForceEnglishOutput</span></span> | <span data-ttu-id="5af3d-118">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="5af3d-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5af3d-119">Expand</span><span class="sxs-lookup"><span data-stu-id="5af3d-119">Expand</span></span> | <span data-ttu-id="5af3d-120">Agrega todos los archivos de cada paquete que se agrega al origen del paquete; igual que `-Expand` con el `add` comando.</span><span class="sxs-lookup"><span data-stu-id="5af3d-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="5af3d-121">Ayuda</span><span class="sxs-lookup"><span data-stu-id="5af3d-121">Help</span></span> | <span data-ttu-id="5af3d-122">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="5af3d-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="5af3d-123">No interactivo</span><span class="sxs-lookup"><span data-stu-id="5af3d-123">NonInteractive</span></span> | <span data-ttu-id="5af3d-124">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="5af3d-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5af3d-125">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="5af3d-125">Verbosity</span></span> | <span data-ttu-id="5af3d-126">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="5af3d-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5af3d-127">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5af3d-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5af3d-128">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5af3d-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
