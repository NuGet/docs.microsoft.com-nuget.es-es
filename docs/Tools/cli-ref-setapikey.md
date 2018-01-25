---
title: Comando de NuGet CLI setapikey | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia para el comando de setapikey nuget.exe
keywords: referencia de setapikey de NuGet, comando setapikey
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="a0136-104">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a0136-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="a0136-105">**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="a0136-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a0136-106">Guarda una clave de API para una dirección URL de servidor determinado en `NuGet.Config` para que no es necesario especificar para los comandos siguientes.</span><span class="sxs-lookup"><span data-stu-id="a0136-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="a0136-107">Uso</span><span class="sxs-lookup"><span data-stu-id="a0136-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="a0136-108">donde `<source>` identifica el servidor y `<key>` es la clave o contraseña para guardar.</span><span class="sxs-lookup"><span data-stu-id="a0136-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="a0136-109">Si `<source>` es se omite, se presupone nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a0136-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="a0136-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="a0136-110">Options</span></span>

| <span data-ttu-id="a0136-111">Opción</span><span class="sxs-lookup"><span data-stu-id="a0136-111">Option</span></span> | <span data-ttu-id="a0136-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="a0136-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0136-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a0136-113">ConfigFile</span></span> | <span data-ttu-id="a0136-114">El archivo de configuración de NuGet para modificar.</span><span class="sxs-lookup"><span data-stu-id="a0136-114">The NuGet configuration file to modify.</span></span> <span data-ttu-id="a0136-115">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="a0136-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a0136-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a0136-116">ForceEnglishOutput</span></span> | <span data-ttu-id="a0136-117">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="a0136-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a0136-118">Ayuda</span><span class="sxs-lookup"><span data-stu-id="a0136-118">Help</span></span> | <span data-ttu-id="a0136-119">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="a0136-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="a0136-120">No interactivo</span><span class="sxs-lookup"><span data-stu-id="a0136-120">NonInteractive</span></span> | <span data-ttu-id="a0136-121">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="a0136-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a0136-122">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="a0136-122">Verbosity</span></span> | <span data-ttu-id="a0136-123">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="a0136-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a0136-124">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a0136-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a0136-125">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a0136-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
