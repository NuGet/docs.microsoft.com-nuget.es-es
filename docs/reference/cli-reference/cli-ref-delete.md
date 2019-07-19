---
title: Comando DELETE de la CLI de NuGet
description: Referencia del comando de eliminación de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327842"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="14b22-103">comando DELETE (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="14b22-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="14b22-104">**Se aplica a:** &bullet; **versiones compatibles** de publicación de paquetes: todos</span><span class="sxs-lookup"><span data-stu-id="14b22-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="14b22-105">Elimina o quita de la lista un paquete del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="14b22-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="14b22-106">En el caso de nuget.org, el comando DELETE elimina [el paquete](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="14b22-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="14b22-107">Uso</span><span class="sxs-lookup"><span data-stu-id="14b22-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="14b22-108">Dónde `<packageID>` e`<packageVersion>` identifican el paquete exacto que se va a eliminar o quitar de la lista.</span><span class="sxs-lookup"><span data-stu-id="14b22-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="14b22-109">El comportamiento exacto depende del origen.</span><span class="sxs-lookup"><span data-stu-id="14b22-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="14b22-110">En el caso de las carpetas locales, por ejemplo, se elimina el paquete. para nuget.org, el paquete no está en la lista.</span><span class="sxs-lookup"><span data-stu-id="14b22-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="14b22-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="14b22-111">Options</span></span>

| <span data-ttu-id="14b22-112">Opción</span><span class="sxs-lookup"><span data-stu-id="14b22-112">Option</span></span> | <span data-ttu-id="14b22-113">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="14b22-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="14b22-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="14b22-114">ApiKey</span></span> | <span data-ttu-id="14b22-115">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="14b22-115">The API key for the target repository.</span></span> <span data-ttu-id="14b22-116">Si no está presente, se utiliza el especificado en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="14b22-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="14b22-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="14b22-117">ConfigFile</span></span> | <span data-ttu-id="14b22-118">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="14b22-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="14b22-119">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="14b22-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="14b22-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="14b22-120">ForceEnglishOutput</span></span> | <span data-ttu-id="14b22-121">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="14b22-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="14b22-122">Help</span><span class="sxs-lookup"><span data-stu-id="14b22-122">Help</span></span> | <span data-ttu-id="14b22-123">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="14b22-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="14b22-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="14b22-124">NonInteractive</span></span> | <span data-ttu-id="14b22-125">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="14b22-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="14b22-126">Source</span><span class="sxs-lookup"><span data-stu-id="14b22-126">Source</span></span> | <span data-ttu-id="14b22-127">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="14b22-127">Specifies the server URL.</span></span> <span data-ttu-id="14b22-128">La dirección URL de nuget.org `https://api.nuget.org/v3/index.json`es.</span><span class="sxs-lookup"><span data-stu-id="14b22-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="14b22-129">En el caso de las fuentes privadas, sustituya el nombre de host, por ejemplo, *% hostname%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="14b22-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="14b22-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="14b22-130">Verbosity</span></span> | <span data-ttu-id="14b22-131">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="14b22-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="14b22-132">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="14b22-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="14b22-133">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="14b22-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
