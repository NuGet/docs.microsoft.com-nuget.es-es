---
title: Comando de especificación de la CLI de NuGet
description: Referencia del comando de especificación de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327572"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="af00d-103">Spec (comando de la CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="af00d-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="af00d-104">**Se aplica a:** &bullet; **versiones compatibles con** la creación de paquetes: todos</span><span class="sxs-lookup"><span data-stu-id="af00d-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="af00d-105">Genera un `.nuspec` archivo para un nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="af00d-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="af00d-106">Si se ejecuta en la misma carpeta que un archivo de`.csproj`proyecto `.vbproj`( `.fsproj`,, `spec` ), crea un `.nuspec` archivo con tokens.</span><span class="sxs-lookup"><span data-stu-id="af00d-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="af00d-107">Para obtener más información, consulte [crear un paquete](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="af00d-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="af00d-108">Uso</span><span class="sxs-lookup"><span data-stu-id="af00d-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="af00d-109">donde `<packageID>` es un identificador de paquete opcional que se va a `.nuspec` guardar en el archivo.</span><span class="sxs-lookup"><span data-stu-id="af00d-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="af00d-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="af00d-110">Options</span></span>

| <span data-ttu-id="af00d-111">Opción</span><span class="sxs-lookup"><span data-stu-id="af00d-111">Option</span></span> | <span data-ttu-id="af00d-112">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="af00d-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="af00d-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="af00d-113">AssemblyPath</span></span> | <span data-ttu-id="af00d-114">Especifica la ruta de acceso al ensamblado que se va a usar para los metadatos.</span><span class="sxs-lookup"><span data-stu-id="af00d-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="af00d-115">Aplica</span><span class="sxs-lookup"><span data-stu-id="af00d-115">Force</span></span> | <span data-ttu-id="af00d-116">Sobrescribe cualquier archivo existente `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="af00d-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="af00d-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="af00d-117">ForceEnglishOutput</span></span> | <span data-ttu-id="af00d-118">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="af00d-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="af00d-119">Help</span><span class="sxs-lookup"><span data-stu-id="af00d-119">Help</span></span> | <span data-ttu-id="af00d-120">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="af00d-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="af00d-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="af00d-121">NonInteractive</span></span> | <span data-ttu-id="af00d-122">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="af00d-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="af00d-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="af00d-123">Verbosity</span></span> | <span data-ttu-id="af00d-124">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="af00d-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="af00d-125">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="af00d-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="af00d-126">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="af00d-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
