---
title: Comando setapikey de la CLI de NuGet
description: Referencia del comando setapikey de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383974"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="d123f-103">comando setapikey (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="d123f-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="d123f-104">**Se aplica a: consumo de** paquetes, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="d123f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d123f-105">Guarda una clave de API para una dirección URL de servidor determinada en `NuGet.Config` para que no sea necesario especificarla para los comandos posteriores.</span><span class="sxs-lookup"><span data-stu-id="d123f-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="d123f-106">Usage</span><span class="sxs-lookup"><span data-stu-id="d123f-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="d123f-107">donde `<source>` identifica el servidor y `<key>` es la clave o contraseña que se va a guardar.</span><span class="sxs-lookup"><span data-stu-id="d123f-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="d123f-108">Si se omite `<source>`, se supone que es nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d123f-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="d123f-109">La clave de API no se utiliza para la autenticación con la fuente privada.</span><span class="sxs-lookup"><span data-stu-id="d123f-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="d123f-110">Consulte [`nuget sources` comando](../cli-reference/cli-ref-sources.md) para administrar las credenciales para la autenticación con el origen.</span><span class="sxs-lookup"><span data-stu-id="d123f-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="d123f-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="d123f-111">Options</span></span>

| <span data-ttu-id="d123f-112">Opción</span><span class="sxs-lookup"><span data-stu-id="d123f-112">Option</span></span> | <span data-ttu-id="d123f-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="d123f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d123f-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d123f-114">ConfigFile</span></span> | <span data-ttu-id="d123f-115">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="d123f-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d123f-116">Si no se especifica, se usa `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="d123f-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d123f-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d123f-117">ForceEnglishOutput</span></span> | <span data-ttu-id="d123f-118">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="d123f-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d123f-119">Ayuda de</span><span class="sxs-lookup"><span data-stu-id="d123f-119">Help</span></span> | <span data-ttu-id="d123f-120">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="d123f-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="d123f-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d123f-121">NonInteractive</span></span> | <span data-ttu-id="d123f-122">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="d123f-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d123f-123">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="d123f-123">Verbosity</span></span> | <span data-ttu-id="d123f-124">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="d123f-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d123f-125">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d123f-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d123f-126">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d123f-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
