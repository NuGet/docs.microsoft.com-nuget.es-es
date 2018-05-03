---
title: NuGet CLI agregar (comando)
description: Referencia para el nuget.exe agregar (comando)
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="4b89e-103">Agregar comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4b89e-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="4b89e-104">**Se aplica a**: paquete de publicación &bullet; **versiones compatibles**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="4b89e-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="4b89e-105">Agrega un paquete específico a un origen de paquete no son HTTP (una carpeta o ruta de acceso UNC) en un formato jerárquico y en el que se crean las carpetas para el número de identificador y la versión del paquete.</span><span class="sxs-lookup"><span data-stu-id="4b89e-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="4b89e-106">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4b89e-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="4b89e-107">Al restaurar o actualizar en el origen del paquete, formato jerárquico proporciona un rendimiento significativamente mejor.</span><span class="sxs-lookup"><span data-stu-id="4b89e-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="4b89e-108">Para expandir todos los archivos en el paquete en el origen del paquete de destino, use el `-Expand` cambiar.</span><span class="sxs-lookup"><span data-stu-id="4b89e-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="4b89e-109">Normalmente esto tiene como resultado en subcarpetas adicionales que aparecen en el destino, como `tools` y `lib`.</span><span class="sxs-lookup"><span data-stu-id="4b89e-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="4b89e-110">Uso</span><span class="sxs-lookup"><span data-stu-id="4b89e-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="4b89e-111">donde `<packagePath>` es la ruta de acceso al paquete que se agregará y `<sourcePath>` especifica el origen del paquete basada en la carpeta a la que se agregará el paquete.</span><span class="sxs-lookup"><span data-stu-id="4b89e-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="4b89e-112">No se admiten orígenes HTTP.</span><span class="sxs-lookup"><span data-stu-id="4b89e-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="4b89e-113">Opciones</span><span class="sxs-lookup"><span data-stu-id="4b89e-113">Options</span></span>

| <span data-ttu-id="4b89e-114">Opción</span><span class="sxs-lookup"><span data-stu-id="4b89e-114">Option</span></span> | <span data-ttu-id="4b89e-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="4b89e-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b89e-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4b89e-116">ConfigFile</span></span> | <span data-ttu-id="4b89e-117">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="4b89e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4b89e-118">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="4b89e-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4b89e-119">Expand</span><span class="sxs-lookup"><span data-stu-id="4b89e-119">Expand</span></span> | <span data-ttu-id="4b89e-120">Agrega todos los archivos en el paquete en el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="4b89e-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="4b89e-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4b89e-121">ForceEnglishOutput</span></span> | <span data-ttu-id="4b89e-122">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="4b89e-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4b89e-123">Ayuda</span><span class="sxs-lookup"><span data-stu-id="4b89e-123">Help</span></span> | <span data-ttu-id="4b89e-124">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="4b89e-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="4b89e-125">No interactivo</span><span class="sxs-lookup"><span data-stu-id="4b89e-125">NonInteractive</span></span> | <span data-ttu-id="4b89e-126">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="4b89e-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4b89e-127">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="4b89e-127">Verbosity</span></span> | <span data-ttu-id="4b89e-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="4b89e-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4b89e-129">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4b89e-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4b89e-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="4b89e-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
