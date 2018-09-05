---
title: Comando de CLI de NuGet locals
description: Referencia para el comando locals de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545033"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="840cc-103">Comando locals (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="840cc-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="840cc-104">**Se aplica a:** consumo de paquetes &bullet; **versiones compatibles:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="840cc-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="840cc-105">Borra o enumera recursos locales de NuGet, como el *http-cache*, *global-packages* carpeta y la carpeta temporal.</span><span class="sxs-lookup"><span data-stu-id="840cc-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="840cc-106">El `locals` también se puede usar el comando para mostrar una lista de esas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="840cc-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="840cc-107">Para obtener más información, consulte [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="840cc-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="840cc-108">Uso</span><span class="sxs-lookup"><span data-stu-id="840cc-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="840cc-109">donde `<folder>` es uno de `all`, `http-cache`, `packages-cache` *(3.5 y anteriores)*, `global-packages`, `temp` *(3.4 y versiones posteriores)*, y `plugins-cache` *(4.8)*.</span><span class="sxs-lookup"><span data-stu-id="840cc-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="840cc-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="840cc-110">Options</span></span>

| <span data-ttu-id="840cc-111">Opción</span><span class="sxs-lookup"><span data-stu-id="840cc-111">Option</span></span> | <span data-ttu-id="840cc-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="840cc-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="840cc-113">Clear</span><span class="sxs-lookup"><span data-stu-id="840cc-113">Clear</span></span> | <span data-ttu-id="840cc-114">Borra la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="840cc-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="840cc-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="840cc-115">ConfigFile</span></span> | <span data-ttu-id="840cc-116">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="840cc-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="840cc-117">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="840cc-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="840cc-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="840cc-118">ForceEnglishOutput</span></span> | <span data-ttu-id="840cc-119">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="840cc-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="840cc-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="840cc-120">Help</span></span> | <span data-ttu-id="840cc-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="840cc-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="840cc-122">Lista</span><span class="sxs-lookup"><span data-stu-id="840cc-122">List</span></span> | <span data-ttu-id="840cc-123">Muestra la ubicación de la carpeta especificada, o las ubicaciones de todas las carpetas cuando se usa con *todas*.</span><span class="sxs-lookup"><span data-stu-id="840cc-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="840cc-124">No interactivo</span><span class="sxs-lookup"><span data-stu-id="840cc-124">NonInteractive</span></span> | <span data-ttu-id="840cc-125">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="840cc-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="840cc-126">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="840cc-126">Verbosity</span></span> | <span data-ttu-id="840cc-127">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="840cc-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="840cc-128">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="840cc-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="840cc-129">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="840cc-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="840cc-130">Para obtener ejemplos adicionales, consulte [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="840cc-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
