---
title: Comando de eliminación de la CLI de NuGet
description: Referencia del comando de eliminación de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548515"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="36e00-103">eliminar comandos (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="36e00-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="36e00-104">**Se aplica a:** publicación del paquete &bullet; **versiones compatibles:** todas</span><span class="sxs-lookup"><span data-stu-id="36e00-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="36e00-105">Elimina o quita un paquete desde un origen del paquete de la lista.</span><span class="sxs-lookup"><span data-stu-id="36e00-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="36e00-106">Para nuget.org, el comando delete [quita el paquete de la lista](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="36e00-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="36e00-107">Uso</span><span class="sxs-lookup"><span data-stu-id="36e00-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="36e00-108">donde `<packageID>` y `<packageVersion>` identificar el paquete exacto para eliminar o quitar de la lista.</span><span class="sxs-lookup"><span data-stu-id="36e00-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="36e00-109">El comportamiento exacto depende del origen.</span><span class="sxs-lookup"><span data-stu-id="36e00-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="36e00-110">Para las carpetas locales, por ejemplo, se elimina el paquete; para nuget.org, el paquete se da de baja.</span><span class="sxs-lookup"><span data-stu-id="36e00-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="36e00-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="36e00-111">Options</span></span>

| <span data-ttu-id="36e00-112">Opción</span><span class="sxs-lookup"><span data-stu-id="36e00-112">Option</span></span> | <span data-ttu-id="36e00-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="36e00-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36e00-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="36e00-114">ApiKey</span></span> | <span data-ttu-id="36e00-115">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="36e00-115">The API key for the target repository.</span></span> <span data-ttu-id="36e00-116">Si no está presente, se utiliza el especificado en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="36e00-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="36e00-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="36e00-117">ConfigFile</span></span> | <span data-ttu-id="36e00-118">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="36e00-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="36e00-119">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="36e00-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="36e00-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="36e00-120">ForceEnglishOutput</span></span> | <span data-ttu-id="36e00-121">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="36e00-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="36e00-122">Help</span><span class="sxs-lookup"><span data-stu-id="36e00-122">Help</span></span> | <span data-ttu-id="36e00-123">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="36e00-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="36e00-124">No interactivo</span><span class="sxs-lookup"><span data-stu-id="36e00-124">NonInteractive</span></span> | <span data-ttu-id="36e00-125">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="36e00-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="36e00-126">Source</span><span class="sxs-lookup"><span data-stu-id="36e00-126">Source</span></span> | <span data-ttu-id="36e00-127">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="36e00-127">Specifies the server URL.</span></span> <span data-ttu-id="36e00-128">La dirección URL de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="36e00-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="36e00-129">Para fuentes privadas, sustituya el nombre de host, por ejemplo, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="36e00-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="36e00-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="36e00-130">Verbosity</span></span> | <span data-ttu-id="36e00-131">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="36e00-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="36e00-132">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="36e00-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="36e00-133">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="36e00-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
