---
title: Comando de CLI de NuGet setapikey
description: Referencia para el comando setapikey de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549225"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="25947-103">comando setapikey (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="25947-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="25947-104">**Se aplica a:** consumo de paquetes, publicar &bullet; **versiones compatibles:** todas</span><span class="sxs-lookup"><span data-stu-id="25947-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="25947-105">Guarda una clave de API para una dirección URL de servidor determinado en `NuGet.Config` para que los no tiene que escribirse para los comandos siguientes.</span><span class="sxs-lookup"><span data-stu-id="25947-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="25947-106">Uso</span><span class="sxs-lookup"><span data-stu-id="25947-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="25947-107">donde `<source>` identifica el servidor y `<key>` es la clave o contraseña para guardar.</span><span class="sxs-lookup"><span data-stu-id="25947-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="25947-108">Si `<source>` es, nuget.org omite.</span><span class="sxs-lookup"><span data-stu-id="25947-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="25947-109">Opciones</span><span class="sxs-lookup"><span data-stu-id="25947-109">Options</span></span>

| <span data-ttu-id="25947-110">Opción</span><span class="sxs-lookup"><span data-stu-id="25947-110">Option</span></span> | <span data-ttu-id="25947-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="25947-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="25947-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="25947-112">ConfigFile</span></span> | <span data-ttu-id="25947-113">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="25947-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="25947-114">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="25947-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="25947-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="25947-115">ForceEnglishOutput</span></span> | <span data-ttu-id="25947-116">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="25947-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="25947-117">Ayuda</span><span class="sxs-lookup"><span data-stu-id="25947-117">Help</span></span> | <span data-ttu-id="25947-118">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="25947-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="25947-119">No interactivo</span><span class="sxs-lookup"><span data-stu-id="25947-119">NonInteractive</span></span> | <span data-ttu-id="25947-120">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="25947-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="25947-121">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="25947-121">Verbosity</span></span> | <span data-ttu-id="25947-122">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="25947-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="25947-123">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="25947-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="25947-124">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="25947-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
