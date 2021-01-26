---
title: Comando Add de la CLI de NuGet
description: Referencia del comando nuget.exe Add
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776094"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="da4af-103">Add (comando) (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="da4af-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="da4af-104">**Se aplica a**: &bullet; **versiones compatibles** de publicación de paquetes: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="da4af-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="da4af-105">Agrega un paquete especificado a un origen de paquete no HTTP (una carpeta o ruta de acceso UNC) en un diseño jerárquico, donde se crean las carpetas para el identificador de paquete y el número de versión.</span><span class="sxs-lookup"><span data-stu-id="da4af-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="da4af-106">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="da4af-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="da4af-107">Al restaurar o actualizar en el origen del paquete, el diseño jerárquico proporciona un rendimiento significativamente mejor.</span><span class="sxs-lookup"><span data-stu-id="da4af-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="da4af-108">Para expandir todos los archivos del paquete en el origen del paquete de destino, use el `-Expand` modificador.</span><span class="sxs-lookup"><span data-stu-id="da4af-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="da4af-109">Normalmente, esto da lugar a la aparición de subcarpetas adicionales en el destino, como `tools` y `lib` .</span><span class="sxs-lookup"><span data-stu-id="da4af-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="da4af-110">Uso</span><span class="sxs-lookup"><span data-stu-id="da4af-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="da4af-111">donde `<packagePath>` es el directorio del paquete que se va a agregar y `<sourcePath>` especifica el origen del paquete basado en carpeta al que se agregará el paquete.</span><span class="sxs-lookup"><span data-stu-id="da4af-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="da4af-112">No se admiten los orígenes HTTP.</span><span class="sxs-lookup"><span data-stu-id="da4af-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="da4af-113">Opciones</span><span class="sxs-lookup"><span data-stu-id="da4af-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="da4af-114">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="da4af-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="da4af-115">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="da4af-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="da4af-116">Agrega todos los archivos del paquete al origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="da4af-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="da4af-117">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="da4af-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="da4af-118">Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="da4af-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="da4af-119">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="da4af-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="da4af-120">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="da4af-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="da4af-121">Especifica el origen del paquete, que es una carpeta o un recurso compartido UNC, al que se agregará el nupkg.</span><span class="sxs-lookup"><span data-stu-id="da4af-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="da4af-122">No se admiten los orígenes http.</span><span class="sxs-lookup"><span data-stu-id="da4af-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="da4af-123">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="da4af-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="da4af-124">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="da4af-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="da4af-125">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="da4af-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
