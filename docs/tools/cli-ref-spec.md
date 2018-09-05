---
title: Comando de CLI de NuGet spec
description: Referencia para el comando spec nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546454"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="d6db0-103">especificación de comandos (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="d6db0-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="d6db0-104">**Se aplica a:** la creación del paquete &bullet; **versiones compatibles:** todas</span><span class="sxs-lookup"><span data-stu-id="d6db0-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d6db0-105">Genera un `.nuspec` archivo para un nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="d6db0-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="d6db0-106">Si se ejecutan en la misma carpeta que un archivo de proyecto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un con tokens `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="d6db0-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="d6db0-107">Para obtener más información, consulte [creación de un paquete](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d6db0-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d6db0-108">Uso</span><span class="sxs-lookup"><span data-stu-id="d6db0-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="d6db0-109">donde `<packageID>` es un identificador de paquete opcional para guardar en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="d6db0-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="d6db0-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="d6db0-110">Options</span></span>

| <span data-ttu-id="d6db0-111">Opción</span><span class="sxs-lookup"><span data-stu-id="d6db0-111">Option</span></span> | <span data-ttu-id="d6db0-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="d6db0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d6db0-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="d6db0-113">AssemblyPath</span></span> | <span data-ttu-id="d6db0-114">Especifica la ruta de acceso al ensamblado que se usará para los metadatos.</span><span class="sxs-lookup"><span data-stu-id="d6db0-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="d6db0-115">Force</span><span class="sxs-lookup"><span data-stu-id="d6db0-115">Force</span></span> | <span data-ttu-id="d6db0-116">Sobrescribe cualquier existente `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="d6db0-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="d6db0-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d6db0-117">ForceEnglishOutput</span></span> | <span data-ttu-id="d6db0-118">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="d6db0-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d6db0-119">Ayuda</span><span class="sxs-lookup"><span data-stu-id="d6db0-119">Help</span></span> | <span data-ttu-id="d6db0-120">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="d6db0-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="d6db0-121">No interactivo</span><span class="sxs-lookup"><span data-stu-id="d6db0-121">NonInteractive</span></span> | <span data-ttu-id="d6db0-122">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="d6db0-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d6db0-123">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="d6db0-123">Verbosity</span></span> | <span data-ttu-id="d6db0-124">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="d6db0-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d6db0-125">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d6db0-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d6db0-126">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d6db0-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
