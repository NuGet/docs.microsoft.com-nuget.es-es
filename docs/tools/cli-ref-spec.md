---
title: Comando spec NuGet CLI
description: Referencia para el comando spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817091"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="cf258-103">comando spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cf258-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="cf258-104">**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="cf258-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="cf258-105">Genera un `.nuspec` archivo para un nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="cf258-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="cf258-106">Si se ejecutan en la misma carpeta que un archivo de proyecto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un con tokens `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="cf258-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="cf258-107">Para obtener más información, consulte [crear un paquete](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="cf258-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="cf258-108">Uso</span><span class="sxs-lookup"><span data-stu-id="cf258-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="cf258-109">donde `<packageID>` es un identificador de paquete opcional para guardar en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="cf258-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="cf258-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="cf258-110">Options</span></span>

| <span data-ttu-id="cf258-111">Opción</span><span class="sxs-lookup"><span data-stu-id="cf258-111">Option</span></span> | <span data-ttu-id="cf258-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="cf258-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf258-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="cf258-113">AssemblyPath</span></span> | <span data-ttu-id="cf258-114">Especifica la ruta de acceso al ensamblado que se va a usar para los metadatos.</span><span class="sxs-lookup"><span data-stu-id="cf258-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="cf258-115">Force</span><span class="sxs-lookup"><span data-stu-id="cf258-115">Force</span></span> | <span data-ttu-id="cf258-116">Sobrescribe cualquier existente `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="cf258-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="cf258-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cf258-117">ForceEnglishOutput</span></span> | <span data-ttu-id="cf258-118">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="cf258-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cf258-119">Ayuda</span><span class="sxs-lookup"><span data-stu-id="cf258-119">Help</span></span> | <span data-ttu-id="cf258-120">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="cf258-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="cf258-121">No interactivo</span><span class="sxs-lookup"><span data-stu-id="cf258-121">NonInteractive</span></span> | <span data-ttu-id="cf258-122">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="cf258-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cf258-123">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="cf258-123">Verbosity</span></span> | <span data-ttu-id="cf258-124">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="cf258-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cf258-125">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cf258-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cf258-126">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="cf258-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
