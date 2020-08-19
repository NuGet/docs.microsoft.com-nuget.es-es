---
title: Comando setapikey de la CLI de NuGet
description: Referencia del comando nuget.exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622816"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="7d348-103">comando setapikey (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="7d348-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="7d348-104">**Se aplica a: consumo de** paquetes, publicación de &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="7d348-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7d348-105">Guarda una clave de API para una dirección URL de servidor determinada en `NuGet.Config` para que no sea necesario especificarla para los comandos subsiguientes.</span><span class="sxs-lookup"><span data-stu-id="7d348-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="7d348-106">Uso</span><span class="sxs-lookup"><span data-stu-id="7d348-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="7d348-107">donde `<source>` identifica el servidor y `<key>` es la clave que se va a guardar.</span><span class="sxs-lookup"><span data-stu-id="7d348-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="7d348-108">Si `<source>` se omite, se supone que es Nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7d348-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="7d348-109">La clave de API no se utiliza para la autenticación con la fuente privada.</span><span class="sxs-lookup"><span data-stu-id="7d348-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="7d348-110">Consulte el [ `nuget sources` comando](../cli-reference/cli-ref-sources.md) para administrar las credenciales para la autenticación con el origen.</span><span class="sxs-lookup"><span data-stu-id="7d348-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="7d348-111">Las claves de API se pueden obtener de los servidores de NuGet individuales.</span><span class="sxs-lookup"><span data-stu-id="7d348-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="7d348-112">Para crear y administrar APIKeys para nuget.org, consulte [adquisición-a-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) .</span><span class="sxs-lookup"><span data-stu-id="7d348-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="7d348-113">Opciones</span><span class="sxs-lookup"><span data-stu-id="7d348-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="7d348-114">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="7d348-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7d348-115">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="7d348-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="7d348-116">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="7d348-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="7d348-117">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="7d348-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="7d348-118">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="7d348-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="7d348-119">Dirección URL del servidor donde la clave de API es válida.</span><span class="sxs-lookup"><span data-stu-id="7d348-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="7d348-120">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="7d348-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="7d348-121">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7d348-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7d348-122">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7d348-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
