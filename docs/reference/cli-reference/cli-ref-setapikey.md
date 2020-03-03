---
title: Comando setapikey de la CLI de NuGet
description: Referencia del comando setapikey de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231232"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="212d6-103">comando setapikey (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="212d6-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="212d6-104">**Se aplica a: consumo de** paquetes, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="212d6-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="212d6-105">Guarda una clave de API para una dirección URL de servidor determinada en `NuGet.Config` para que no sea necesario especificarla para los comandos posteriores.</span><span class="sxs-lookup"><span data-stu-id="212d6-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="212d6-106">Uso</span><span class="sxs-lookup"><span data-stu-id="212d6-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="212d6-107">donde `<source>` identifica el servidor y `<key>` es la clave que se va a guardar.</span><span class="sxs-lookup"><span data-stu-id="212d6-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="212d6-108">Si se omite `<source>`, se supone que es nuget.org.</span><span class="sxs-lookup"><span data-stu-id="212d6-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="212d6-109">La clave de API no se utiliza para la autenticación con la fuente privada.</span><span class="sxs-lookup"><span data-stu-id="212d6-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="212d6-110">Consulte [`nuget sources` comando](../cli-reference/cli-ref-sources.md) para administrar las credenciales para la autenticación con el origen.</span><span class="sxs-lookup"><span data-stu-id="212d6-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="212d6-111">Las claves de API se pueden obtener de los servidores de NuGet individuales.</span><span class="sxs-lookup"><span data-stu-id="212d6-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="212d6-112">Para crear y administrar APIKeys para nuget.org, consulte [Publish-API-Key](../../quickstart/includes/publish-api-key.md) .</span><span class="sxs-lookup"><span data-stu-id="212d6-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="212d6-113">Opciones</span><span class="sxs-lookup"><span data-stu-id="212d6-113">Options</span></span>

| <span data-ttu-id="212d6-114">Opción</span><span class="sxs-lookup"><span data-stu-id="212d6-114">Option</span></span> | <span data-ttu-id="212d6-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="212d6-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="212d6-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="212d6-116">ConfigFile</span></span> | <span data-ttu-id="212d6-117">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="212d6-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="212d6-118">Si no se especifica, se usa `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="212d6-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="212d6-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="212d6-119">ForceEnglishOutput</span></span> | <span data-ttu-id="212d6-120">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="212d6-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="212d6-121">Help</span><span class="sxs-lookup"><span data-stu-id="212d6-121">Help</span></span> | <span data-ttu-id="212d6-122">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="212d6-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="212d6-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="212d6-123">NonInteractive</span></span> | <span data-ttu-id="212d6-124">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="212d6-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="212d6-125">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="212d6-125">Verbosity</span></span> | <span data-ttu-id="212d6-126">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="212d6-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="212d6-127">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="212d6-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="212d6-128">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="212d6-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
