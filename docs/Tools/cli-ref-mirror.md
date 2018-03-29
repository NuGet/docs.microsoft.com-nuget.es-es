---
title: Comando de NuGet CLI reflejado | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia del comando de reflejado nuget.exe
keywords: referencia de reflejado de NuGet, comando espejo
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="c7258-104">comando reflejado (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c7258-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="c7258-105">**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** en desuso en 3.2 +</span><span class="sxs-lookup"><span data-stu-id="c7258-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="c7258-106">Refleja un paquete y sus dependencias de los repositorios de origen especificada en el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="c7258-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="c7258-107">Para habilitar este comando para las versiones de NuGet antes 3.2, vaya a [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), seleccione la versión estable más reciente, descargue `NuGet.ServerExtensions.dll` y `Nuget-Signed.exe` en el disco local y el cambio de nombre `Nuget-Signed.exe` a `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="c7258-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="c7258-108">Uso</span><span class="sxs-lookup"><span data-stu-id="c7258-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="c7258-109">donde `<packageID>` es el paquete para reflejar, o `<configFilePath>` identifica el `packages.config` archivo que enumera los paquetes que se va a reflejar.</span><span class="sxs-lookup"><span data-stu-id="c7258-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="c7258-110">El `<listUrlTarget>` especifica el repositorio de origen, y `<publishUrlTarget>` especifica el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="c7258-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="c7258-111">Si el repositorio de destino está en `https://machine/repo` que se esté ejecutando [NuGet.Server](../hosting-packages/nuget-server.md), las direcciones URL lista e inserte será `https://machine/repo/nuget` y `https://machine/repo/api/v2/package`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c7258-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c7258-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="c7258-112">Options</span></span>

| <span data-ttu-id="c7258-113">Opción</span><span class="sxs-lookup"><span data-stu-id="c7258-113">Option</span></span> | <span data-ttu-id="c7258-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="c7258-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7258-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="c7258-115">ApiKey</span></span> | <span data-ttu-id="c7258-116">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="c7258-116">The API key for the target repository.</span></span> <span data-ttu-id="c7258-117">Si no está presente, se especificó en el archivo de configuración se usa (`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux)).</span><span class="sxs-lookup"><span data-stu-id="c7258-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="c7258-118">Ayuda</span><span class="sxs-lookup"><span data-stu-id="c7258-118">Help</span></span> | <span data-ttu-id="c7258-119">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="c7258-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="c7258-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="c7258-120">NoCache</span></span> | <span data-ttu-id="c7258-121">Impide que NuGet use paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="c7258-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="c7258-122">Vea [administrar los paquetes globales y las carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c7258-122">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c7258-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="c7258-123">Noop</span></span> | <span data-ttu-id="c7258-124">Registra qué están a cargo pero no lleva a cabo las acciones; se da por supuesto se realizó correctamente para las operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="c7258-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="c7258-125">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="c7258-125">PreRelease</span></span> | <span data-ttu-id="c7258-126">Incluye paquetes de versión preliminar de la operación de creación de reflejo.</span><span class="sxs-lookup"><span data-stu-id="c7258-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="c7258-127">Origen</span><span class="sxs-lookup"><span data-stu-id="c7258-127">Source</span></span> | <span data-ttu-id="c7258-128">Una lista de orígenes de paquetes para crear el reflejo.</span><span class="sxs-lookup"><span data-stu-id="c7258-128">A list of package sources to mirror.</span></span> <span data-ttu-id="c7258-129">Si no se especifica ningún origen de los definen en el archivo de configuración (vea ApiKey anterior) se usan, volverá al valor predeterminado nuget.org si no se especifica ninguno.</span><span class="sxs-lookup"><span data-stu-id="c7258-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="c7258-130">Timeout</span><span class="sxs-lookup"><span data-stu-id="c7258-130">Timeout</span></span> | <span data-ttu-id="c7258-131">Especifica el tiempo de espera, en segundos, para insertar a un servidor.</span><span class="sxs-lookup"><span data-stu-id="c7258-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="c7258-132">El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="c7258-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="c7258-133">Versión</span><span class="sxs-lookup"><span data-stu-id="c7258-133">Version</span></span> | <span data-ttu-id="c7258-134">La versión del paquete para instalar.</span><span class="sxs-lookup"><span data-stu-id="c7258-134">The version of the package to install.</span></span> <span data-ttu-id="c7258-135">Si no se especifica, se refleja la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="c7258-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="c7258-136">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c7258-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c7258-137">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c7258-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
