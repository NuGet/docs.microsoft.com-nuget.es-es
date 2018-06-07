---
title: Comando de NuGet CLI setapikey
description: Referencia para el comando de setapikey nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817689"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="97afe-103">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="97afe-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="97afe-104">**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="97afe-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="97afe-105">Guarda una clave de API para una dirección URL de servidor determinado en `NuGet.Config` para que no es necesario especificar para los comandos siguientes.</span><span class="sxs-lookup"><span data-stu-id="97afe-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="97afe-106">Uso</span><span class="sxs-lookup"><span data-stu-id="97afe-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="97afe-107">donde `<source>` identifica el servidor y `<key>` es la clave o contraseña para guardar.</span><span class="sxs-lookup"><span data-stu-id="97afe-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="97afe-108">Si `<source>` es se omite, se presupone nuget.org.</span><span class="sxs-lookup"><span data-stu-id="97afe-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="97afe-109">Opciones</span><span class="sxs-lookup"><span data-stu-id="97afe-109">Options</span></span>

| <span data-ttu-id="97afe-110">Opción</span><span class="sxs-lookup"><span data-stu-id="97afe-110">Option</span></span> | <span data-ttu-id="97afe-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="97afe-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97afe-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="97afe-112">ConfigFile</span></span> | <span data-ttu-id="97afe-113">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="97afe-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="97afe-114">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="97afe-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="97afe-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="97afe-115">ForceEnglishOutput</span></span> | <span data-ttu-id="97afe-116">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="97afe-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="97afe-117">Ayuda</span><span class="sxs-lookup"><span data-stu-id="97afe-117">Help</span></span> | <span data-ttu-id="97afe-118">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="97afe-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="97afe-119">No interactivo</span><span class="sxs-lookup"><span data-stu-id="97afe-119">NonInteractive</span></span> | <span data-ttu-id="97afe-120">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="97afe-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="97afe-121">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="97afe-121">Verbosity</span></span> | <span data-ttu-id="97afe-122">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="97afe-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="97afe-123">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="97afe-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="97afe-124">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="97afe-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
