---
title: Comandos de la Ayuda de NuGet CLI
description: Referencia para el comando de ayuda nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818261"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="5e3e5-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="5e3e5-103">help or ?</span></span> <span data-ttu-id="5e3e5-104">Comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5e3e5-104">command (NuGet CLI)</span></span>

<span data-ttu-id="5e3e5-105">**Se aplica a:** todos los &bullet; **versiones compatibles**: todos los</span><span class="sxs-lookup"><span data-stu-id="5e3e5-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="5e3e5-106">General muestra información de ayuda e información acerca de los comandos específicos de ayuda.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="5e3e5-107">Uso</span><span class="sxs-lookup"><span data-stu-id="5e3e5-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="5e3e5-108">donde [comando] identifica un comando específico para el que se va a mostrar la Ayuda.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="5e3e5-109">Con algunos comandos, esté atento especificar *ayuda* primero, como con `nuget help install`, porque no hay un paquete denominado "help" en nuget.org. Si se ejecuta el comando `nuget install help`, no obtener ayuda sobre el comando de instalación, pero en su lugar, se instalará el paquete denominado ayuda.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="5e3e5-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="5e3e5-110">Options</span></span>

| <span data-ttu-id="5e3e5-111">Opción</span><span class="sxs-lookup"><span data-stu-id="5e3e5-111">Option</span></span> | <span data-ttu-id="5e3e5-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="5e3e5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5e3e5-113">Todas</span><span class="sxs-lookup"><span data-stu-id="5e3e5-113">All</span></span> | <span data-ttu-id="5e3e5-114">Imprimir ayuda detallada acerca de todos los comandos disponibles; se omite si no se especifica un comando específico.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="5e3e5-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5e3e5-115">ConfigFile</span></span> | <span data-ttu-id="5e3e5-116">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5e3e5-117">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5e3e5-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5e3e5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="5e3e5-119">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5e3e5-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="5e3e5-120">Help</span></span> | <span data-ttu-id="5e3e5-121">Muestra información de ayuda para los comandos de la Ayuda.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="5e3e5-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="5e3e5-122">Markdown</span></span> | <span data-ttu-id="5e3e5-123">Imprimir ayuda detallada en formato de marcado cuando se utiliza con `-All`.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="5e3e5-124">Tecla de método abreviado.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="5e3e5-125">No interactivo</span><span class="sxs-lookup"><span data-stu-id="5e3e5-125">NonInteractive</span></span> | <span data-ttu-id="5e3e5-126">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5e3e5-127">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="5e3e5-127">Verbosity</span></span> | <span data-ttu-id="5e3e5-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="5e3e5-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5e3e5-129">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5e3e5-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5e3e5-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5e3e5-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
