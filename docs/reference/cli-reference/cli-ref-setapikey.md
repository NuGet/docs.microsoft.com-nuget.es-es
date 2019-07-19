---
title: Comando setapikey de la CLI de NuGet
description: Referencia del comando setapikey de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327612"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="f586f-103">comando setapikey (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="f586f-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="f586f-104">**Se aplica a: consumo de** paquetes &bullet; , publicación de **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="f586f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f586f-105">Guarda una clave de API para una dirección URL de `NuGet.Config` servidor determinada en para que no sea necesario especificarla para los comandos subsiguientes.</span><span class="sxs-lookup"><span data-stu-id="f586f-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="f586f-106">Uso</span><span class="sxs-lookup"><span data-stu-id="f586f-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="f586f-107">donde `<source>` identifica el servidor y `<key>` es la clave o contraseña que se va a guardar.</span><span class="sxs-lookup"><span data-stu-id="f586f-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="f586f-108">Si `<source>` se omite, se supone que es Nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f586f-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="f586f-109">Opciones</span><span class="sxs-lookup"><span data-stu-id="f586f-109">Options</span></span>

| <span data-ttu-id="f586f-110">Opción</span><span class="sxs-lookup"><span data-stu-id="f586f-110">Option</span></span> | <span data-ttu-id="f586f-111">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="f586f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f586f-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f586f-112">ConfigFile</span></span> | <span data-ttu-id="f586f-113">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="f586f-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f586f-114">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f586f-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f586f-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f586f-115">ForceEnglishOutput</span></span> | <span data-ttu-id="f586f-116">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="f586f-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f586f-117">Help</span><span class="sxs-lookup"><span data-stu-id="f586f-117">Help</span></span> | <span data-ttu-id="f586f-118">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="f586f-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="f586f-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f586f-119">NonInteractive</span></span> | <span data-ttu-id="f586f-120">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="f586f-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f586f-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f586f-121">Verbosity</span></span> | <span data-ttu-id="f586f-122">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="f586f-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f586f-123">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f586f-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f586f-124">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f586f-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
