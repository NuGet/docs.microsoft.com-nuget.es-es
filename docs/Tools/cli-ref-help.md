---
title: Comandos de la Ayuda de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: Referencia para el comando de ayuda nuget.exe
keywords: NuGet ayuda referencia, comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="c2f27-104">¿ayudar a o?</span><span class="sxs-lookup"><span data-stu-id="c2f27-104">help or ?</span></span> <span data-ttu-id="c2f27-105">comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c2f27-105">command (NuGet CLI)</span></span>

<span data-ttu-id="c2f27-106">**Se aplica a:** todos los &bullet; **versiones compatibles**: todos los</span><span class="sxs-lookup"><span data-stu-id="c2f27-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="c2f27-107">General muestra información de ayuda e información acerca de los comandos específicos de ayuda.</span><span class="sxs-lookup"><span data-stu-id="c2f27-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="c2f27-108">Uso</span><span class="sxs-lookup"><span data-stu-id="c2f27-108">Usage</span></span>

```
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="c2f27-109">donde [comando] identifica un comando específico para el que se va a mostrar la Ayuda.</span><span class="sxs-lookup"><span data-stu-id="c2f27-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="c2f27-110">Con algunos comandos, esté atento especificar *ayuda* primero, como con `nuget help install`, porque no hay un paquete denominado "help" en nuget.org. Si se ejecuta el comando `nuget install help`, no se podrá obtener ayuda sobre el comando de instalación, pero en su lugar, se instalará el paquete denominado ayuda.</span><span class="sxs-lookup"><span data-stu-id="c2f27-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you'll not get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="c2f27-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="c2f27-111">Options</span></span>

| <span data-ttu-id="c2f27-112">Opción</span><span class="sxs-lookup"><span data-stu-id="c2f27-112">Option</span></span> | <span data-ttu-id="c2f27-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="c2f27-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2f27-114">Todas</span><span class="sxs-lookup"><span data-stu-id="c2f27-114">All</span></span> | <span data-ttu-id="c2f27-115">Imprimir ayuda detallada acerca de todos los comandos disponibles; se omite si no se especifica un comando específico.</span><span class="sxs-lookup"><span data-stu-id="c2f27-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="c2f27-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c2f27-116">ConfigFile</span></span> | <span data-ttu-id="c2f27-117">*(2.5 +)*  NuGet el archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="c2f27-117">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="c2f27-118">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="c2f27-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="c2f27-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c2f27-119">ForceEnglishOutput</span></span> | <span data-ttu-id="c2f27-120">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="c2f27-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c2f27-121">Ayuda</span><span class="sxs-lookup"><span data-stu-id="c2f27-121">Help</span></span> | <span data-ttu-id="c2f27-122">Muestra información de ayuda para los comandos de la Ayuda.</span><span class="sxs-lookup"><span data-stu-id="c2f27-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="c2f27-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="c2f27-123">Markdown</span></span> | <span data-ttu-id="c2f27-124">Imprimir ayuda detallada en formato de marcado cuando se utiliza con `-All`.</span><span class="sxs-lookup"><span data-stu-id="c2f27-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="c2f27-125">Tecla de método abreviado.</span><span class="sxs-lookup"><span data-stu-id="c2f27-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="c2f27-126">No interactivo</span><span class="sxs-lookup"><span data-stu-id="c2f27-126">NonInteractive</span></span> | <span data-ttu-id="c2f27-127">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="c2f27-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c2f27-128">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="c2f27-128">Verbosity</span></span> | <span data-ttu-id="c2f27-129">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="c2f27-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="c2f27-130">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c2f27-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c2f27-131">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c2f27-131">Examples</span></span>

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
