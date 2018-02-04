---
title: Comando de variables locales de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia del comando de variables locales nuget.exe
keywords: referencia de variables locales de NuGet, comandos de variables locales
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="a343f-104">comando de variables locales (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a343f-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="a343f-105">**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="a343f-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="a343f-106">Borra o listas de recursos locales de NuGet, como la memoria caché de la solicitud http y caché de paquetes, la carpeta paquetes global de todo el equipo.</span><span class="sxs-lookup"><span data-stu-id="a343f-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="a343f-107">El `locals` comando también se puede usar para mostrar una lista de esas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="a343f-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="a343f-108">Para obtener más información, consulte [administrar la memoria NuGet caché](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="a343f-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a343f-109">Uso</span><span class="sxs-lookup"><span data-stu-id="a343f-109">Usage</span></span>

```cli
nuget locals <cache> [options]
```

<span data-ttu-id="a343f-110">donde `<cache>` es uno de los `all`, `http-cache`, `packages-cache`, `global-packages`, y `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="a343f-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="a343f-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="a343f-111">Options</span></span>

| <span data-ttu-id="a343f-112">Opción</span><span class="sxs-lookup"><span data-stu-id="a343f-112">Option</span></span> | <span data-ttu-id="a343f-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="a343f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a343f-114">Clear</span><span class="sxs-lookup"><span data-stu-id="a343f-114">Clear</span></span> | <span data-ttu-id="a343f-115">Borra la memoria caché especificada.</span><span class="sxs-lookup"><span data-stu-id="a343f-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="a343f-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a343f-116">ConfigFile</span></span> | <span data-ttu-id="a343f-117">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="a343f-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a343f-118">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="a343f-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a343f-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a343f-119">ForceEnglishOutput</span></span> | <span data-ttu-id="a343f-120">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="a343f-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a343f-121">Ayuda</span><span class="sxs-lookup"><span data-stu-id="a343f-121">Help</span></span> | <span data-ttu-id="a343f-122">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="a343f-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="a343f-123">Lista</span><span class="sxs-lookup"><span data-stu-id="a343f-123">List</span></span> | <span data-ttu-id="a343f-124">Muestra la ubicación de la memoria caché especificada o las ubicaciones de todas las memorias caché cuando se usa con *todos los*.</span><span class="sxs-lookup"><span data-stu-id="a343f-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="a343f-125">No interactivo</span><span class="sxs-lookup"><span data-stu-id="a343f-125">NonInteractive</span></span> | <span data-ttu-id="a343f-126">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="a343f-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a343f-127">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="a343f-127">Verbosity</span></span> | <span data-ttu-id="a343f-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="a343f-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a343f-129">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a343f-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a343f-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a343f-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```
