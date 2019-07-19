---
title: Comando de ayuda de la CLI de NuGet
description: Referencia del comando de ayuda de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327802"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="3e376-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="3e376-103">help or ?</span></span> <span data-ttu-id="3e376-104">Comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3e376-104">command (NuGet CLI)</span></span>

<span data-ttu-id="3e376-105">**Se aplica a:** todas &bullet; **las versiones compatibles**: todas</span><span class="sxs-lookup"><span data-stu-id="3e376-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="3e376-106">Muestra información de ayuda general e información de ayuda acerca de comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="3e376-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="3e376-107">Uso</span><span class="sxs-lookup"><span data-stu-id="3e376-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="3e376-108">donde [comando] identifica un comando específico para el que se va a mostrar ayuda.</span><span class="sxs-lookup"><span data-stu-id="3e376-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="3e376-109">Con algunos comandos, asegúrese de especificar la *ayuda* primero, como con `nuget help install`, ya que hay un paquete denominado "Help" en Nuget.org. Si proporciona el comando `nuget install help`, no obtendrá ayuda sobre el comando de instalación pero, en su lugar, instalará el paquete denominado help.</span><span class="sxs-lookup"><span data-stu-id="3e376-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="3e376-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="3e376-110">Options</span></span>

| <span data-ttu-id="3e376-111">Opción</span><span class="sxs-lookup"><span data-stu-id="3e376-111">Option</span></span> | <span data-ttu-id="3e376-112">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="3e376-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e376-113">Todo</span><span class="sxs-lookup"><span data-stu-id="3e376-113">All</span></span> | <span data-ttu-id="3e376-114">Imprimir ayuda detallada para todos los comandos disponibles; se omite si se especifica un comando específico.</span><span class="sxs-lookup"><span data-stu-id="3e376-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="3e376-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3e376-115">ConfigFile</span></span> | <span data-ttu-id="3e376-116">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="3e376-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3e376-117">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="3e376-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3e376-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3e376-118">ForceEnglishOutput</span></span> | <span data-ttu-id="3e376-119">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="3e376-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3e376-120">Help</span><span class="sxs-lookup"><span data-stu-id="3e376-120">Help</span></span> | <span data-ttu-id="3e376-121">Muestra información de ayuda para el propio comando de ayuda.</span><span class="sxs-lookup"><span data-stu-id="3e376-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="3e376-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="3e376-122">Markdown</span></span> | <span data-ttu-id="3e376-123">Imprima la ayuda detallada en formato Markdown cuando se `-All`use con.</span><span class="sxs-lookup"><span data-stu-id="3e376-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="3e376-124">Se omite en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="3e376-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="3e376-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3e376-125">NonInteractive</span></span> | <span data-ttu-id="3e376-126">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="3e376-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3e376-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="3e376-127">Verbosity</span></span> | <span data-ttu-id="3e376-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="3e376-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3e376-129">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3e376-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3e376-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="3e376-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
