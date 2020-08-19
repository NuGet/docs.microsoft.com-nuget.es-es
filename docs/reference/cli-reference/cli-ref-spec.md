---
title: Comando de especificación de la CLI de NuGet
description: Referencia del comando nuget.exe Spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622569"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="21f14-103">Spec (comando de la CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="21f14-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="21f14-104">**Se aplica a:** &bullet; **versiones compatibles con** la creación de paquetes: todos</span><span class="sxs-lookup"><span data-stu-id="21f14-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="21f14-105">Genera un `.nuspec` archivo para un nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="21f14-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="21f14-106">Si se ejecuta en la misma carpeta que un archivo de proyecto ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` crea un archivo con tokens `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="21f14-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="21f14-107">Para obtener más información, consulte [crear un paquete](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="21f14-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="21f14-108">Uso</span><span class="sxs-lookup"><span data-stu-id="21f14-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="21f14-109">donde `<packageID>` es un identificador de paquete opcional que se va a guardar en el `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="21f14-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="21f14-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="21f14-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="21f14-111">Especifica la ruta de acceso al ensamblado que se va a usar para los metadatos.</span><span class="sxs-lookup"><span data-stu-id="21f14-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="21f14-112">Sobrescribe cualquier `.nuspec` archivo existente.</span><span class="sxs-lookup"><span data-stu-id="21f14-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="21f14-113">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="21f14-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="21f14-114">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="21f14-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="21f14-115">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="21f14-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="21f14-116">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="21f14-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="21f14-117">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="21f14-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="21f14-118">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="21f14-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
