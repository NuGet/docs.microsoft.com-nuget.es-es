---
title: Comando de NuGet CLI spec | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia para el comando spec nuget.exe
keywords: "referencia de especificación de NuGet, especificaciones de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="88a49-104">comando spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="88a49-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="88a49-105">**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="88a49-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="88a49-106">Genera un `.nuspec` archivo para un nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="88a49-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="88a49-107">Si se ejecutan en la misma carpeta que un archivo de proyecto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un con tokens `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="88a49-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="88a49-108">Para obtener más información, consulte [crear un paquete](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="88a49-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="88a49-109">Uso</span><span class="sxs-lookup"><span data-stu-id="88a49-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="88a49-110">donde `<packageID>` es un identificador de paquete opcional para guardar en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="88a49-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="88a49-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="88a49-111">Options</span></span>

| <span data-ttu-id="88a49-112">Opción</span><span class="sxs-lookup"><span data-stu-id="88a49-112">Option</span></span> | <span data-ttu-id="88a49-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="88a49-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88a49-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="88a49-114">AssemblyPath</span></span> | <span data-ttu-id="88a49-115">Especifica la ruta de acceso al ensamblado que se va a usar para los metadatos.</span><span class="sxs-lookup"><span data-stu-id="88a49-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="88a49-116">Force</span><span class="sxs-lookup"><span data-stu-id="88a49-116">Force</span></span> | <span data-ttu-id="88a49-117">Sobrescribe cualquier existente `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="88a49-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="88a49-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="88a49-118">ForceEnglishOutput</span></span> | <span data-ttu-id="88a49-119">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="88a49-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="88a49-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="88a49-120">Help</span></span> | <span data-ttu-id="88a49-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="88a49-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="88a49-122">No interactivo</span><span class="sxs-lookup"><span data-stu-id="88a49-122">NonInteractive</span></span> | <span data-ttu-id="88a49-123">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="88a49-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="88a49-124">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="88a49-124">Verbosity</span></span> | <span data-ttu-id="88a49-125">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="88a49-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="88a49-126">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="88a49-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="88a49-127">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="88a49-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
