---
title: Comando de CLI de NuGet spec
description: Referencia para el comando spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794156"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="9e2dc-103">especificación de comandos (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="9e2dc-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="9e2dc-104">**Se aplica a:** la creación del paquete &bullet; **versiones compatibles:** todas</span><span class="sxs-lookup"><span data-stu-id="9e2dc-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9e2dc-105">Genera un `.nuspec` archivo para un nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="9e2dc-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="9e2dc-106">Si se ejecutan en la misma carpeta que un archivo de proyecto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un con tokens `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="9e2dc-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="9e2dc-107">Para obtener más información, consulte [creación de un paquete](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9e2dc-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9e2dc-108">Uso</span><span class="sxs-lookup"><span data-stu-id="9e2dc-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="9e2dc-109">donde `<packageID>` es un identificador de paquete opcional para guardar en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="9e2dc-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="9e2dc-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="9e2dc-110">Options</span></span>

| <span data-ttu-id="9e2dc-111">Opción</span><span class="sxs-lookup"><span data-stu-id="9e2dc-111">Option</span></span> | <span data-ttu-id="9e2dc-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e2dc-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9e2dc-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="9e2dc-113">AssemblyPath</span></span> | <span data-ttu-id="9e2dc-114">Especifica la ruta de acceso al ensamblado que se usará para los metadatos.</span><span class="sxs-lookup"><span data-stu-id="9e2dc-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="9e2dc-115">Force</span><span class="sxs-lookup"><span data-stu-id="9e2dc-115">Force</span></span> | <span data-ttu-id="9e2dc-116">Sobrescribe cualquier existente `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="9e2dc-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="9e2dc-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9e2dc-117">ForceEnglishOutput</span></span> | <span data-ttu-id="9e2dc-118">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="9e2dc-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9e2dc-119">Ayuda</span><span class="sxs-lookup"><span data-stu-id="9e2dc-119">Help</span></span> | <span data-ttu-id="9e2dc-120">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="9e2dc-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="9e2dc-121">No interactivo</span><span class="sxs-lookup"><span data-stu-id="9e2dc-121">NonInteractive</span></span> | <span data-ttu-id="9e2dc-122">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="9e2dc-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9e2dc-123">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="9e2dc-123">Verbosity</span></span> | <span data-ttu-id="9e2dc-124">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="9e2dc-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9e2dc-125">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9e2dc-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9e2dc-126">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9e2dc-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
