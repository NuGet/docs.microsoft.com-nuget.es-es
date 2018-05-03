---
title: Comandos de la Ayuda de NuGet CLI
description: Referencia para el comando de ayuda nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="718cc-103">¿ayudar a o?</span><span class="sxs-lookup"><span data-stu-id="718cc-103">help or ?</span></span> <span data-ttu-id="718cc-104">comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="718cc-104">command (NuGet CLI)</span></span>

<span data-ttu-id="718cc-105">**Se aplica a:** todos los &bullet; **versiones compatibles**: todos los</span><span class="sxs-lookup"><span data-stu-id="718cc-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="718cc-106">General muestra información de ayuda e información acerca de los comandos específicos de ayuda.</span><span class="sxs-lookup"><span data-stu-id="718cc-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="718cc-107">Uso</span><span class="sxs-lookup"><span data-stu-id="718cc-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="718cc-108">donde [comando] identifica un comando específico para el que se va a mostrar la Ayuda.</span><span class="sxs-lookup"><span data-stu-id="718cc-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="718cc-109">Con algunos comandos, esté atento especificar *ayuda* primero, como con `nuget help install`, porque no hay un paquete denominado "help" en nuget.org. Si se ejecuta el comando `nuget install help`, no obtener ayuda sobre el comando de instalación, pero en su lugar, se instalará el paquete denominado ayuda.</span><span class="sxs-lookup"><span data-stu-id="718cc-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="718cc-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="718cc-110">Options</span></span>

| <span data-ttu-id="718cc-111">Opción</span><span class="sxs-lookup"><span data-stu-id="718cc-111">Option</span></span> | <span data-ttu-id="718cc-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="718cc-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="718cc-113">Todas</span><span class="sxs-lookup"><span data-stu-id="718cc-113">All</span></span> | <span data-ttu-id="718cc-114">Imprimir ayuda detallada acerca de todos los comandos disponibles; se omite si no se especifica un comando específico.</span><span class="sxs-lookup"><span data-stu-id="718cc-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="718cc-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="718cc-115">ConfigFile</span></span> | <span data-ttu-id="718cc-116">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="718cc-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="718cc-117">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="718cc-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="718cc-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="718cc-118">ForceEnglishOutput</span></span> | <span data-ttu-id="718cc-119">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="718cc-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="718cc-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="718cc-120">Help</span></span> | <span data-ttu-id="718cc-121">Muestra información de ayuda para los comandos de la Ayuda.</span><span class="sxs-lookup"><span data-stu-id="718cc-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="718cc-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="718cc-122">Markdown</span></span> | <span data-ttu-id="718cc-123">Imprimir ayuda detallada en formato de marcado cuando se utiliza con `-All`.</span><span class="sxs-lookup"><span data-stu-id="718cc-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="718cc-124">Tecla de método abreviado.</span><span class="sxs-lookup"><span data-stu-id="718cc-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="718cc-125">No interactivo</span><span class="sxs-lookup"><span data-stu-id="718cc-125">NonInteractive</span></span> | <span data-ttu-id="718cc-126">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="718cc-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="718cc-127">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="718cc-127">Verbosity</span></span> | <span data-ttu-id="718cc-128">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="718cc-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="718cc-129">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="718cc-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="718cc-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="718cc-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
