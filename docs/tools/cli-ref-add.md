---
title: CLI de NuGet Agregar comando
description: Referencia de nuget.exe Agregar comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545839"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="e7040-103">Comando add (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="e7040-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="e7040-104">**Se aplica a**: publicación del paquete &bullet; **versiones compatibles de**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="e7040-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="e7040-105">Agrega un paquete específico a un origen de paquete que no sean HTTP (una carpeta o ruta de acceso UNC) en formato jerárquico, en la que se crean las carpetas para el número de identificador y la versión del paquete.</span><span class="sxs-lookup"><span data-stu-id="e7040-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="e7040-106">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e7040-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="e7040-107">Al restaurar o actualizar en el origen del paquete, formato jerárquico proporciona un rendimiento significativamente mejor.</span><span class="sxs-lookup"><span data-stu-id="e7040-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="e7040-108">Para expandir todos los archivos en el paquete al origen del paquete de destino, use el `-Expand` cambie.</span><span class="sxs-lookup"><span data-stu-id="e7040-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="e7040-109">Esto normalmente da como resultado de las subcarpetas adicionales que aparecen en el destino, como `tools` y `lib`.</span><span class="sxs-lookup"><span data-stu-id="e7040-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="e7040-110">Uso</span><span class="sxs-lookup"><span data-stu-id="e7040-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="e7040-111">donde `<packagePath>` es la ruta de acceso al paquete para agregar, y `<sourcePath>` especifica el origen del paquete basada en la carpeta a la que se agregará el paquete.</span><span class="sxs-lookup"><span data-stu-id="e7040-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="e7040-112">No se admiten orígenes de HTTP.</span><span class="sxs-lookup"><span data-stu-id="e7040-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="e7040-113">Opciones</span><span class="sxs-lookup"><span data-stu-id="e7040-113">Options</span></span>

| <span data-ttu-id="e7040-114">Opción</span><span class="sxs-lookup"><span data-stu-id="e7040-114">Option</span></span> | <span data-ttu-id="e7040-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7040-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7040-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e7040-116">ConfigFile</span></span> | <span data-ttu-id="e7040-117">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="e7040-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e7040-118">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="e7040-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e7040-119">Expand</span><span class="sxs-lookup"><span data-stu-id="e7040-119">Expand</span></span> | <span data-ttu-id="e7040-120">Agrega todos los archivos en el paquete en el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="e7040-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="e7040-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e7040-121">ForceEnglishOutput</span></span> | <span data-ttu-id="e7040-122">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="e7040-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e7040-123">Help</span><span class="sxs-lookup"><span data-stu-id="e7040-123">Help</span></span> | <span data-ttu-id="e7040-124">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="e7040-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="e7040-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e7040-125">NonInteractive</span></span> | <span data-ttu-id="e7040-126">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="e7040-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e7040-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="e7040-127">Verbosity</span></span> | <span data-ttu-id="e7040-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="e7040-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e7040-129">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e7040-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e7040-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="e7040-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
