---
title: Comando variables locales de la CLI de NuGet
description: Referencia del comando de variables locales de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327812"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="9e160-103">Comando locals (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="9e160-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="9e160-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 3.3+</span><span class="sxs-lookup"><span data-stu-id="9e160-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="9e160-105">Borra o muestra los recursos de NuGet locales, como la carpeta *http-cache*, *global-Packages* y la carpeta Temp.</span><span class="sxs-lookup"><span data-stu-id="9e160-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="9e160-106">El `locals` comando también se puede usar para mostrar una lista de esas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="9e160-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="9e160-107">Para obtener más información, vea [administrar paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="9e160-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9e160-108">Uso</span><span class="sxs-lookup"><span data-stu-id="9e160-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="9e160-109">donde `<folder>` es uno de `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 y anteriores)* ,, *(3.4 +)* y *(4.8 +)* .</span><span class="sxs-lookup"><span data-stu-id="9e160-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="9e160-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="9e160-110">Options</span></span>

| <span data-ttu-id="9e160-111">Opción</span><span class="sxs-lookup"><span data-stu-id="9e160-111">Option</span></span> | <span data-ttu-id="9e160-112">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="9e160-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9e160-113">Clear</span><span class="sxs-lookup"><span data-stu-id="9e160-113">Clear</span></span> | <span data-ttu-id="9e160-114">Borra la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="9e160-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="9e160-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9e160-115">ConfigFile</span></span> | <span data-ttu-id="9e160-116">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="9e160-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9e160-117">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9e160-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9e160-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9e160-118">ForceEnglishOutput</span></span> | <span data-ttu-id="9e160-119">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="9e160-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9e160-120">Help</span><span class="sxs-lookup"><span data-stu-id="9e160-120">Help</span></span> | <span data-ttu-id="9e160-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="9e160-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="9e160-122">Enumerar</span><span class="sxs-lookup"><span data-stu-id="9e160-122">List</span></span> | <span data-ttu-id="9e160-123">Muestra la ubicación de la carpeta especificada o las ubicaciones de todas las carpetas cuando se usa con *todos*.</span><span class="sxs-lookup"><span data-stu-id="9e160-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="9e160-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9e160-124">NonInteractive</span></span> | <span data-ttu-id="9e160-125">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="9e160-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9e160-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="9e160-126">Verbosity</span></span> | <span data-ttu-id="9e160-127">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="9e160-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9e160-128">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9e160-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9e160-129">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9e160-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="9e160-130">Para obtener más ejemplos, consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="9e160-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
