---
title: Comando Add de la CLI de NuGet
description: Referencia del comando Add de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327862"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="e3640-103">Comando add (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="e3640-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="e3640-104">**Se aplica a**: &bullet; **versiones compatibles**de publicación de paquetes: 3.3+</span><span class="sxs-lookup"><span data-stu-id="e3640-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="e3640-105">Agrega un paquete especificado a un origen de paquete no HTTP (una carpeta o ruta de acceso UNC) en un diseño jerárquico, donde se crean las carpetas para el identificador de paquete y el número de versión.</span><span class="sxs-lookup"><span data-stu-id="e3640-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="e3640-106">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e3640-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="e3640-107">Al restaurar o actualizar en el origen del paquete, el diseño jerárquico proporciona un rendimiento significativamente mejor.</span><span class="sxs-lookup"><span data-stu-id="e3640-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="e3640-108">Para expandir todos los archivos del paquete en el origen del paquete de destino, use `-Expand` el modificador.</span><span class="sxs-lookup"><span data-stu-id="e3640-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="e3640-109">Normalmente, esto da lugar `tools` a la aparición de subcarpetas adicionales en el destino, como y. `lib`</span><span class="sxs-lookup"><span data-stu-id="e3640-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="e3640-110">Uso</span><span class="sxs-lookup"><span data-stu-id="e3640-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="e3640-111">donde `<packagePath>` es el directorio del paquete que se va a agregar `<sourcePath>` y especifica el origen del paquete basado en carpeta al que se agregará el paquete.</span><span class="sxs-lookup"><span data-stu-id="e3640-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="e3640-112">No se admiten los orígenes HTTP.</span><span class="sxs-lookup"><span data-stu-id="e3640-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="e3640-113">Opciones</span><span class="sxs-lookup"><span data-stu-id="e3640-113">Options</span></span>

| <span data-ttu-id="e3640-114">Opción</span><span class="sxs-lookup"><span data-stu-id="e3640-114">Option</span></span> | <span data-ttu-id="e3640-115">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="e3640-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3640-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e3640-116">ConfigFile</span></span> | <span data-ttu-id="e3640-117">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="e3640-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e3640-118">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="e3640-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e3640-119">Expand</span><span class="sxs-lookup"><span data-stu-id="e3640-119">Expand</span></span> | <span data-ttu-id="e3640-120">Agrega todos los archivos del paquete al origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="e3640-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="e3640-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e3640-121">ForceEnglishOutput</span></span> | <span data-ttu-id="e3640-122">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="e3640-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e3640-123">Help</span><span class="sxs-lookup"><span data-stu-id="e3640-123">Help</span></span> | <span data-ttu-id="e3640-124">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="e3640-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="e3640-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e3640-125">NonInteractive</span></span> | <span data-ttu-id="e3640-126">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="e3640-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e3640-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="e3640-127">Verbosity</span></span> | <span data-ttu-id="e3640-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="e3640-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e3640-129">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e3640-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e3640-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="e3640-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
