---
title: Comando de Ayuda de la CLI de NuGet
description: Referencia del comando de Ayuda de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546568"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="fcd19-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="fcd19-103">help or ?</span></span> <span data-ttu-id="fcd19-104">Comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fcd19-104">command (NuGet CLI)</span></span>

<span data-ttu-id="fcd19-105">**Se aplica a:** todas &bullet; **versiones compatibles de**: todas</span><span class="sxs-lookup"><span data-stu-id="fcd19-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="fcd19-106">General muestra información de ayuda e información acerca de los comandos específicos de ayuda.</span><span class="sxs-lookup"><span data-stu-id="fcd19-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="fcd19-107">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd19-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="fcd19-108">donde [comando] identifica un comando específico para el que se va a mostrar la Ayuda.</span><span class="sxs-lookup"><span data-stu-id="fcd19-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="fcd19-109">Con algunos comandos, esté atento especificar *ayuda* primero, como ocurre con `nuget help install`, porque no hay un paquete denominado "Ayuda" en nuget.org. Si se ejecuta el comando `nuget install help`, no obtener ayuda sobre el comando de instalación, pero en su lugar, se instalará el paquete denominado ayuda.</span><span class="sxs-lookup"><span data-stu-id="fcd19-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="fcd19-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="fcd19-110">Options</span></span>

| <span data-ttu-id="fcd19-111">Opción</span><span class="sxs-lookup"><span data-stu-id="fcd19-111">Option</span></span> | <span data-ttu-id="fcd19-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="fcd19-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fcd19-113">Todas</span><span class="sxs-lookup"><span data-stu-id="fcd19-113">All</span></span> | <span data-ttu-id="fcd19-114">Imprime la ayuda detallada de todos los comandos disponibles; se omite si no se especifica un comando específico.</span><span class="sxs-lookup"><span data-stu-id="fcd19-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="fcd19-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fcd19-115">ConfigFile</span></span> | <span data-ttu-id="fcd19-116">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="fcd19-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fcd19-117">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="fcd19-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fcd19-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fcd19-118">ForceEnglishOutput</span></span> | <span data-ttu-id="fcd19-119">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="fcd19-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fcd19-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="fcd19-120">Help</span></span> | <span data-ttu-id="fcd19-121">Muestra información de ayuda para el propio comando de ayuda.</span><span class="sxs-lookup"><span data-stu-id="fcd19-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="fcd19-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="fcd19-122">Markdown</span></span> | <span data-ttu-id="fcd19-123">Imprimir ayuda detallada en formato de marcado cuando se usa con `-All`.</span><span class="sxs-lookup"><span data-stu-id="fcd19-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="fcd19-124">Pasa por alto en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="fcd19-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="fcd19-125">No interactivo</span><span class="sxs-lookup"><span data-stu-id="fcd19-125">NonInteractive</span></span> | <span data-ttu-id="fcd19-126">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="fcd19-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fcd19-127">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="fcd19-127">Verbosity</span></span> | <span data-ttu-id="fcd19-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="fcd19-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fcd19-129">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fcd19-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fcd19-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="fcd19-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
