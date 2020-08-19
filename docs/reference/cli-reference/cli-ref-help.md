---
title: Comando de ayuda de la CLI de NuGet
description: Referencia del comando ayuda de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623115"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="9a0d7-103">help o ?</span><span class="sxs-lookup"><span data-stu-id="9a0d7-103">help or ?</span></span> <span data-ttu-id="9a0d7-104">comando (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="9a0d7-104">command (NuGet CLI)</span></span>

<span data-ttu-id="9a0d7-105">**Se aplica a:** todas &bullet; **las versiones compatibles**: todas</span><span class="sxs-lookup"><span data-stu-id="9a0d7-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="9a0d7-106">Muestra información de ayuda general e información de ayuda acerca de comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="9a0d7-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="9a0d7-107">Uso</span><span class="sxs-lookup"><span data-stu-id="9a0d7-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="9a0d7-108">donde [comando] identifica un comando específico para el que se va a mostrar ayuda.</span><span class="sxs-lookup"><span data-stu-id="9a0d7-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="9a0d7-109">Con algunos comandos, asegúrese de especificar la *ayuda* primero, como con `nuget help install` , ya que hay un paquete denominado "help" en Nuget.org. Si proporciona el comando `nuget install help` , no obtendrá ayuda sobre el comando de instalación pero, en su lugar, instalará el paquete denominado help.</span><span class="sxs-lookup"><span data-stu-id="9a0d7-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="9a0d7-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="9a0d7-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="9a0d7-111">Imprimir ayuda detallada para todos los comandos disponibles; se omite si se especifica un comando específico.</span><span class="sxs-lookup"><span data-stu-id="9a0d7-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="9a0d7-112">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="9a0d7-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9a0d7-113">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9a0d7-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="9a0d7-114">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="9a0d7-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="9a0d7-115">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="9a0d7-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="9a0d7-116">Imprima la ayuda detallada en formato Markdown cuando se use con `-All` .</span><span class="sxs-lookup"><span data-stu-id="9a0d7-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="9a0d7-117">Se omite en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="9a0d7-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="9a0d7-118">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="9a0d7-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="9a0d7-119">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="9a0d7-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="9a0d7-120">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9a0d7-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9a0d7-121">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9a0d7-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
