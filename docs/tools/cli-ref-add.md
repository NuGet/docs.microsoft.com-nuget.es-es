---
title: NuGet CLI agregar (comando)
description: Referencia para el nuget.exe agregar (comando)
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817615"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="5da55-103">Comando add (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="5da55-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="5da55-104">**Se aplica a**: paquete de publicación &bullet; **versiones compatibles**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="5da55-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="5da55-105">Agrega un paquete específico a un origen de paquete no son HTTP (una carpeta o ruta de acceso UNC) en un formato jerárquico y en el que se crean las carpetas para el número de identificador y la versión del paquete.</span><span class="sxs-lookup"><span data-stu-id="5da55-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="5da55-106">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5da55-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="5da55-107">Al restaurar o actualizar en el origen del paquete, formato jerárquico proporciona un rendimiento significativamente mejor.</span><span class="sxs-lookup"><span data-stu-id="5da55-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="5da55-108">Para expandir todos los archivos en el paquete en el origen del paquete de destino, use el `-Expand` cambiar.</span><span class="sxs-lookup"><span data-stu-id="5da55-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="5da55-109">Normalmente esto tiene como resultado en subcarpetas adicionales que aparecen en el destino, como `tools` y `lib`.</span><span class="sxs-lookup"><span data-stu-id="5da55-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="5da55-110">Uso</span><span class="sxs-lookup"><span data-stu-id="5da55-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="5da55-111">donde `<packagePath>` es la ruta de acceso al paquete que se agregará y `<sourcePath>` especifica el origen del paquete basada en la carpeta a la que se agregará el paquete.</span><span class="sxs-lookup"><span data-stu-id="5da55-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="5da55-112">No se admiten orígenes HTTP.</span><span class="sxs-lookup"><span data-stu-id="5da55-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="5da55-113">Opciones</span><span class="sxs-lookup"><span data-stu-id="5da55-113">Options</span></span>

| <span data-ttu-id="5da55-114">Opción</span><span class="sxs-lookup"><span data-stu-id="5da55-114">Option</span></span> | <span data-ttu-id="5da55-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="5da55-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5da55-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5da55-116">ConfigFile</span></span> | <span data-ttu-id="5da55-117">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="5da55-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5da55-118">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="5da55-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5da55-119">Expand</span><span class="sxs-lookup"><span data-stu-id="5da55-119">Expand</span></span> | <span data-ttu-id="5da55-120">Agrega todos los archivos en el paquete en el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="5da55-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="5da55-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5da55-121">ForceEnglishOutput</span></span> | <span data-ttu-id="5da55-122">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="5da55-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5da55-123">Ayuda</span><span class="sxs-lookup"><span data-stu-id="5da55-123">Help</span></span> | <span data-ttu-id="5da55-124">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="5da55-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="5da55-125">No interactivo</span><span class="sxs-lookup"><span data-stu-id="5da55-125">NonInteractive</span></span> | <span data-ttu-id="5da55-126">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="5da55-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5da55-127">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="5da55-127">Verbosity</span></span> | <span data-ttu-id="5da55-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="5da55-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5da55-129">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5da55-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5da55-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5da55-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
