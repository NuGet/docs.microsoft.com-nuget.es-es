---
title: Comando de eliminación de NuGet CLI
description: Referencia para el comando de eliminación nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0f33dd5475521da47972a6f032ac6ea86d98c83
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817183"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="e1159-103">Eliminar comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e1159-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="e1159-104">**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="e1159-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e1159-105">Elimina o unlists un paquete desde un origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="e1159-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="e1159-106">Para nuget.org, el comando delete [unlists el paquete](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e1159-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="e1159-107">Uso</span><span class="sxs-lookup"><span data-stu-id="e1159-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="e1159-108">donde `<packageID>` y `<packageVersion>` identificar el paquete exacto para eliminar u ocultar.</span><span class="sxs-lookup"><span data-stu-id="e1159-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="e1159-109">El comportamiento exacto depende del origen.</span><span class="sxs-lookup"><span data-stu-id="e1159-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="e1159-110">Para las carpetas locales, por ejemplo, se elimina el paquete; para nuget.org es que no figuran en el paquete.</span><span class="sxs-lookup"><span data-stu-id="e1159-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="e1159-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="e1159-111">Options</span></span>

| <span data-ttu-id="e1159-112">Opción</span><span class="sxs-lookup"><span data-stu-id="e1159-112">Option</span></span> | <span data-ttu-id="e1159-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1159-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e1159-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="e1159-114">ApiKey</span></span> | <span data-ttu-id="e1159-115">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="e1159-115">The API key for the target repository.</span></span> <span data-ttu-id="e1159-116">Si no está presente, se utiliza el especificado en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="e1159-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="e1159-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e1159-117">ConfigFile</span></span> | <span data-ttu-id="e1159-118">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="e1159-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e1159-119">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="e1159-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e1159-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e1159-120">ForceEnglishOutput</span></span> | <span data-ttu-id="e1159-121">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="e1159-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e1159-122">Ayuda</span><span class="sxs-lookup"><span data-stu-id="e1159-122">Help</span></span> | <span data-ttu-id="e1159-123">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="e1159-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="e1159-124">No interactivo</span><span class="sxs-lookup"><span data-stu-id="e1159-124">NonInteractive</span></span> | <span data-ttu-id="e1159-125">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="e1159-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e1159-126">Origen</span><span class="sxs-lookup"><span data-stu-id="e1159-126">Source</span></span> | <span data-ttu-id="e1159-127">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="e1159-127">Specifies the server URL.</span></span> <span data-ttu-id="e1159-128">La dirección URL de nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="e1159-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="e1159-129">Para las fuentes privadas, sustituya el nombre de host, por ejemplo, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="e1159-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="e1159-130">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="e1159-130">Verbosity</span></span> | <span data-ttu-id="e1159-131">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="e1159-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e1159-132">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e1159-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e1159-133">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="e1159-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
