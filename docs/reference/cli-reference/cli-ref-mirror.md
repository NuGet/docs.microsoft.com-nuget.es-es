---
title: Comando de reflejo de la CLI de NuGet
description: Referencia del comando de reflejo Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327672"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="43151-103">Comando mirror (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="43151-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="43151-104">**Se aplica a:** &bullet; **versiones compatibles** de publicación de paquetes: desusados en 3,2 +</span><span class="sxs-lookup"><span data-stu-id="43151-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="43151-105">Refleja un paquete y sus dependencias de los repositorios de origen especificados en el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="43151-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="43151-106">Para habilitar este comando para las versiones de NuGet anteriores a 3,2 [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), vaya a, seleccione la versión estable `NuGet.ServerExtensions.dll` más `Nuget-Signed.exe` reciente, descargue y en el disco `Nuget-Signed.exe` local `nuget.exe` y cambie el nombre a.</span><span class="sxs-lookup"><span data-stu-id="43151-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="43151-107">Uso</span><span class="sxs-lookup"><span data-stu-id="43151-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="43151-108">donde `<packageID>` es el paquete que se va a `<configFilePath>` reflejar, `packages.config` o identifica el archivo que muestra los paquetes que se van a reflejar.</span><span class="sxs-lookup"><span data-stu-id="43151-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="43151-109">Especifica el repositorio de origen y `<publishUrlTarget>` especifica el repositorio de destino. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="43151-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="43151-110">Si el repositorio de destino se `https://machine/repo` encuentra en que ejecuta [NuGet. Server](../../hosting-packages/nuget-server.md), la lista y las direcciones URL `https://machine/repo/nuget` de `https://machine/repo/api/v2/package`inserciones serán y, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="43151-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="43151-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="43151-111">Options</span></span>

| <span data-ttu-id="43151-112">Opción</span><span class="sxs-lookup"><span data-stu-id="43151-112">Option</span></span> | <span data-ttu-id="43151-113">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="43151-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="43151-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="43151-114">ApiKey</span></span> | <span data-ttu-id="43151-115">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="43151-115">The API key for the target repository.</span></span> <span data-ttu-id="43151-116">Si no está presente, se usa el especificado en el archivo de configuración`%AppData%\NuGet\NuGet.Config` ((Windows) `~/.nuget/NuGet/NuGet.Config` o (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="43151-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="43151-117">Help</span><span class="sxs-lookup"><span data-stu-id="43151-117">Help</span></span> | <span data-ttu-id="43151-118">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="43151-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="43151-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="43151-119">NoCache</span></span> | <span data-ttu-id="43151-120">Impide que NuGet use paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="43151-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="43151-121">Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="43151-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="43151-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="43151-122">Noop</span></span> | <span data-ttu-id="43151-123">Registra lo que se haría pero no realiza las acciones; supone que las operaciones de inserciones se han realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="43151-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="43151-124">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="43151-124">PreRelease</span></span> | <span data-ttu-id="43151-125">Incluye paquetes de versión preliminar en la operación de creación de reflejo.</span><span class="sxs-lookup"><span data-stu-id="43151-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="43151-126">source</span><span class="sxs-lookup"><span data-stu-id="43151-126">Source</span></span> | <span data-ttu-id="43151-127">Una lista de orígenes de paquetes que se van a reflejar.</span><span class="sxs-lookup"><span data-stu-id="43151-127">A list of package sources to mirror.</span></span> <span data-ttu-id="43151-128">Si no se especifican orígenes, se usan los definidos en el archivo de configuración (vea ApiKey anterior), de forma predeterminada se usa nuget.org si no se especifica ninguno.</span><span class="sxs-lookup"><span data-stu-id="43151-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="43151-129">Tiempo de espera</span><span class="sxs-lookup"><span data-stu-id="43151-129">Timeout</span></span> | <span data-ttu-id="43151-130">Especifica el tiempo de espera, en segundos, para insertar en un servidor.</span><span class="sxs-lookup"><span data-stu-id="43151-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="43151-131">El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="43151-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="43151-132">`Version`</span><span class="sxs-lookup"><span data-stu-id="43151-132">Version</span></span> | <span data-ttu-id="43151-133">Versión del paquete que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="43151-133">The version of the package to install.</span></span> <span data-ttu-id="43151-134">Si no se especifica, la versión más reciente está reflejada.</span><span class="sxs-lookup"><span data-stu-id="43151-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="43151-135">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="43151-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="43151-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="43151-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
