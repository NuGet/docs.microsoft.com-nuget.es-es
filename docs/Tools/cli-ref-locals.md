---
title: Comando de variables locales de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia del comando de variables locales nuget.exe
keywords: referencia de variables locales de NuGet, comandos de variables locales
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="d7065-104">comando de variables locales (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d7065-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="d7065-105">**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="d7065-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="d7065-106">Borra o se enumeran los recursos de NuGet locales como el *caché http*, *global paquetes* carpeta y la carpeta temporal.</span><span class="sxs-lookup"><span data-stu-id="d7065-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="d7065-107">El `locals` comando también se puede usar para mostrar una lista de esas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7065-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="d7065-108">Para obtener más información, consulte [administrar los paquetes globales y las carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d7065-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d7065-109">Uso</span><span class="sxs-lookup"><span data-stu-id="d7065-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="d7065-110">donde `<folder>` es uno de los `all`, `http-cache`, `packages-cache` *(3.5 y versiones anteriores)*, `global-packages`, y `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="d7065-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="d7065-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="d7065-111">Options</span></span>

| <span data-ttu-id="d7065-112">Opción</span><span class="sxs-lookup"><span data-stu-id="d7065-112">Option</span></span> | <span data-ttu-id="d7065-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="d7065-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7065-114">Clear</span><span class="sxs-lookup"><span data-stu-id="d7065-114">Clear</span></span> | <span data-ttu-id="d7065-115">Borra la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="d7065-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="d7065-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d7065-116">ConfigFile</span></span> | <span data-ttu-id="d7065-117">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="d7065-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d7065-118">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="d7065-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d7065-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d7065-119">ForceEnglishOutput</span></span> | <span data-ttu-id="d7065-120">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="d7065-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d7065-121">Ayuda</span><span class="sxs-lookup"><span data-stu-id="d7065-121">Help</span></span> | <span data-ttu-id="d7065-122">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="d7065-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="d7065-123">Lista</span><span class="sxs-lookup"><span data-stu-id="d7065-123">List</span></span> | <span data-ttu-id="d7065-124">Muestra la ubicación de la carpeta especificada o las ubicaciones de todas las carpetas cuando se usa con *todos los*.</span><span class="sxs-lookup"><span data-stu-id="d7065-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="d7065-125">No interactivo</span><span class="sxs-lookup"><span data-stu-id="d7065-125">NonInteractive</span></span> | <span data-ttu-id="d7065-126">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="d7065-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d7065-127">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="d7065-127">Verbosity</span></span> | <span data-ttu-id="d7065-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="d7065-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d7065-129">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d7065-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d7065-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d7065-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="d7065-131">Para obtener ejemplos adicionales, vea [administrar los paquetes globales y las carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d7065-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
