---
title: Comando variables locales de la CLI de NuGet
description: Referencia del comando nuget.exe variables locales
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779197"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="af91b-103">comando variables locales (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="af91b-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="af91b-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="af91b-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="af91b-105">Borra o muestra los recursos de NuGet locales, como la carpeta *http-cache*, *global-Packages* y la carpeta Temp.</span><span class="sxs-lookup"><span data-stu-id="af91b-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="af91b-106">El `locals` comando también se puede usar para mostrar una lista de esas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="af91b-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="af91b-107">Para obtener más información, vea [administrar paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="af91b-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="af91b-108">Uso</span><span class="sxs-lookup"><span data-stu-id="af91b-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="af91b-109">donde `<folder>` es uno de `all` , `http-cache` , `packages-cache` *(3,5 y anteriores)*, `global-packages` , `temp` *(3.4 +)* y `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="af91b-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="af91b-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="af91b-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="af91b-111">Borra la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="af91b-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="af91b-112">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="af91b-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="af91b-113">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="af91b-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="af91b-114">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="af91b-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="af91b-115">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="af91b-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="af91b-116">Muestra la ubicación de la carpeta especificada o las ubicaciones de todas las carpetas cuando se usa con *todos*.</span><span class="sxs-lookup"><span data-stu-id="af91b-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="af91b-117">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="af91b-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="af91b-118">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="af91b-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="af91b-119">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="af91b-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="af91b-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="af91b-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="af91b-121">Para obtener más ejemplos, consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="af91b-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
