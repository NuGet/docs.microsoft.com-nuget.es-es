---
title: Comando de NuGet CLI variables locales
description: Referencia del comando de variables locales nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818206"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="866aa-103">Comando locals (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="866aa-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="866aa-104">**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="866aa-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="866aa-105">Borra o se enumeran los recursos de NuGet locales como el *caché http*, *global paquetes* carpeta y la carpeta temporal.</span><span class="sxs-lookup"><span data-stu-id="866aa-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="866aa-106">El `locals` comando también se puede usar para mostrar una lista de esas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="866aa-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="866aa-107">Para obtener más información, consulte [administrar los paquetes globales y las carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="866aa-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="866aa-108">Uso</span><span class="sxs-lookup"><span data-stu-id="866aa-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="866aa-109">donde `<folder>` es uno de los `all`, `http-cache`, `packages-cache` *(3.5 y versiones anteriores)*, `global-packages`, y `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="866aa-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="866aa-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="866aa-110">Options</span></span>

| <span data-ttu-id="866aa-111">Opción</span><span class="sxs-lookup"><span data-stu-id="866aa-111">Option</span></span> | <span data-ttu-id="866aa-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="866aa-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="866aa-113">Clear</span><span class="sxs-lookup"><span data-stu-id="866aa-113">Clear</span></span> | <span data-ttu-id="866aa-114">Borra la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="866aa-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="866aa-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="866aa-115">ConfigFile</span></span> | <span data-ttu-id="866aa-116">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="866aa-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="866aa-117">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="866aa-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="866aa-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="866aa-118">ForceEnglishOutput</span></span> | <span data-ttu-id="866aa-119">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="866aa-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="866aa-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="866aa-120">Help</span></span> | <span data-ttu-id="866aa-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="866aa-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="866aa-122">Lista</span><span class="sxs-lookup"><span data-stu-id="866aa-122">List</span></span> | <span data-ttu-id="866aa-123">Muestra la ubicación de la carpeta especificada o las ubicaciones de todas las carpetas cuando se usa con *todos los*.</span><span class="sxs-lookup"><span data-stu-id="866aa-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="866aa-124">No interactivo</span><span class="sxs-lookup"><span data-stu-id="866aa-124">NonInteractive</span></span> | <span data-ttu-id="866aa-125">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="866aa-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="866aa-126">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="866aa-126">Verbosity</span></span> | <span data-ttu-id="866aa-127">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="866aa-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="866aa-128">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="866aa-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="866aa-129">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="866aa-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="866aa-130">Para obtener ejemplos adicionales, vea [administrar los paquetes globales y las carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="866aa-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
