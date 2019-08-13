---
title: Comando de reflejo de la CLI de NuGet
description: Referencia del comando de reflejo Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959708"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="2f1c4-103">Comando mirror (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="2f1c4-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="2f1c4-104">**Se aplica a:** &bullet; **versiones compatibles** de publicación de paquetes: desusados en 3,2 +</span><span class="sxs-lookup"><span data-stu-id="2f1c4-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="2f1c4-105">Refleja un paquete y sus dependencias de los repositorios de origen especificados en el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="2f1c4-106">NuGet. ServerExtensions. dll y NuGet-Signed. exe que anteriormente admitían este comando en NuGet 2. x (cambiando el nombre de NuGet-Signed. exe a Nuget. exe) ya no están disponibles para su descarga.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="2f1c4-107">Para usar un comando similar a este, pruebe [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="2f1c4-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="2f1c4-108">Uso</span><span class="sxs-lookup"><span data-stu-id="2f1c4-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="2f1c4-109">donde `<packageID>` es el paquete que se va a `<configFilePath>` reflejar, `packages.config` o identifica el archivo que muestra los paquetes que se van a reflejar.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="2f1c4-110">Especifica el repositorio de origen y `<publishUrlTarget>` especifica el repositorio de destino. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="2f1c4-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="2f1c4-111">Si el repositorio de destino se `https://machine/repo` encuentra en que ejecuta [NuGet. Server](../../hosting-packages/nuget-server.md), la lista y las direcciones URL `https://machine/repo/nuget` de `https://machine/repo/api/v2/package`inserciones serán y, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="2f1c4-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="2f1c4-112">Options</span></span>

| <span data-ttu-id="2f1c4-113">Opción</span><span class="sxs-lookup"><span data-stu-id="2f1c4-113">Option</span></span> | <span data-ttu-id="2f1c4-114">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="2f1c4-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2f1c4-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="2f1c4-115">ApiKey</span></span> | <span data-ttu-id="2f1c4-116">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-116">The API key for the target repository.</span></span> <span data-ttu-id="2f1c4-117">Si no está presente, se usa el especificado en el archivo de configuración`%AppData%\NuGet\NuGet.Config` ((Windows) `~/.nuget/NuGet/NuGet.Config` o (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="2f1c4-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="2f1c4-118">Help</span><span class="sxs-lookup"><span data-stu-id="2f1c4-118">Help</span></span> | <span data-ttu-id="2f1c4-119">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="2f1c4-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="2f1c4-120">NoCache</span></span> | <span data-ttu-id="2f1c4-121">Impide que NuGet use paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="2f1c4-122">Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2f1c4-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="2f1c4-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="2f1c4-123">Noop</span></span> | <span data-ttu-id="2f1c4-124">Registra lo que se haría pero no realiza las acciones; supone que las operaciones de inserciones se han realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="2f1c4-125">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="2f1c4-125">PreRelease</span></span> | <span data-ttu-id="2f1c4-126">Incluye paquetes de versión preliminar en la operación de creación de reflejo.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="2f1c4-127">source</span><span class="sxs-lookup"><span data-stu-id="2f1c4-127">Source</span></span> | <span data-ttu-id="2f1c4-128">Una lista de orígenes de paquetes que se van a reflejar.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-128">A list of package sources to mirror.</span></span> <span data-ttu-id="2f1c4-129">Si no se especifican orígenes, se usan los definidos en el archivo de configuración (vea ApiKey anterior), de forma predeterminada se usa nuget.org si no se especifica ninguno.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="2f1c4-130">Tiempo de espera</span><span class="sxs-lookup"><span data-stu-id="2f1c4-130">Timeout</span></span> | <span data-ttu-id="2f1c4-131">Especifica el tiempo de espera, en segundos, para insertar en un servidor.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="2f1c4-132">El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="2f1c4-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="2f1c4-133">`Version`</span><span class="sxs-lookup"><span data-stu-id="2f1c4-133">Version</span></span> | <span data-ttu-id="2f1c4-134">Versión del paquete que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-134">The version of the package to install.</span></span> <span data-ttu-id="2f1c4-135">Si no se especifica, la versión más reciente está reflejada.</span><span class="sxs-lookup"><span data-stu-id="2f1c4-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="2f1c4-136">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2f1c4-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2f1c4-137">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f1c4-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
