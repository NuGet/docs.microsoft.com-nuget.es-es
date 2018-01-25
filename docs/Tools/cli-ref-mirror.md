---
title: Comando de NuGet CLI reflejado | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia del comando de reflejado nuget.exe
keywords: referencia de reflejado de NuGet, comando espejo
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff5f1c1a915943e8a2eb9c6d6ab09a850968371
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="90567-104">comando reflejado (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="90567-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="90567-105">**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** en desuso en 3.2 +</span><span class="sxs-lookup"><span data-stu-id="90567-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="90567-106">Refleja un paquete y sus dependencias de los repositorios de origen especificada en el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="90567-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="90567-107">Para habilitar este comando para las versiones de NuGet antes 3.2, vaya a [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), seleccione la versión estable más reciente, descargue `NuGet.ServerExtensions.dll` y `Nuget-Signed.exe` en el disco local y el nombre `Nuget-Signed.exe` a `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="90567-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="90567-108">Uso</span><span class="sxs-lookup"><span data-stu-id="90567-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="90567-109">donde `<packageID>` es el paquete para reflejar, o `<configFilePath>` identifica el `packages.config` archivo que enumera los paquetes que se va a reflejar.</span><span class="sxs-lookup"><span data-stu-id="90567-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="90567-110">El `<listUrlTarget>` especifica el repositorio de origen, y `<publishUrlTarget>` especifica el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="90567-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="90567-111">Si el repositorio de destino está en `https://machine/repo` que se esté ejecutando [NuGet.Server](../hosting-packages/NuGet-Server.md), las direcciones URL lista e inserte será `https://machine/repo/nuget` y `https://machine/repo/api/v2/package`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="90567-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/NuGet-Server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="90567-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="90567-112">Options</span></span>

| <span data-ttu-id="90567-113">Opción</span><span class="sxs-lookup"><span data-stu-id="90567-113">Option</span></span> | <span data-ttu-id="90567-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="90567-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="90567-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="90567-115">ApiKey</span></span> | <span data-ttu-id="90567-116">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="90567-116">The API key for the target repository.</span></span> <span data-ttu-id="90567-117">Si no está presente, el especificado en *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="90567-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="90567-118">Ayuda</span><span class="sxs-lookup"><span data-stu-id="90567-118">Help</span></span> | <span data-ttu-id="90567-119">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="90567-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="90567-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="90567-120">NoCache</span></span> | <span data-ttu-id="90567-121">Impide que NuGet use paquetes de memorias caché del equipo local.</span><span class="sxs-lookup"><span data-stu-id="90567-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="90567-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="90567-122">Noop</span></span> | <span data-ttu-id="90567-123">Registra qué están a cargo pero no lleva a cabo las acciones; se da por supuesto se realizó correctamente para las operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="90567-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="90567-124">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="90567-124">PreRelease</span></span> | <span data-ttu-id="90567-125">Incluye paquetes de versión preliminar de la operación de creación de reflejo.</span><span class="sxs-lookup"><span data-stu-id="90567-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="90567-126">Origen</span><span class="sxs-lookup"><span data-stu-id="90567-126">Source</span></span> | <span data-ttu-id="90567-127">Una lista de orígenes de paquetes para crear el reflejo.</span><span class="sxs-lookup"><span data-stu-id="90567-127">A list of package sources to mirror.</span></span> <span data-ttu-id="90567-128">Si no se especifica ningún origen de los definen en *%AppData%\NuGet\NuGet.Config* se usan, volverá al valor predeterminado nuget.org si no se especifica ninguno.</span><span class="sxs-lookup"><span data-stu-id="90567-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="90567-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="90567-129">Timeout</span></span> | <span data-ttu-id="90567-130">Especifica el tiempo de espera, en segundos, para insertar a un servidor.</span><span class="sxs-lookup"><span data-stu-id="90567-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="90567-131">El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="90567-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="90567-132">Versión</span><span class="sxs-lookup"><span data-stu-id="90567-132">Version</span></span> | <span data-ttu-id="90567-133">La versión del paquete para instalar.</span><span class="sxs-lookup"><span data-stu-id="90567-133">The version of the package to install.</span></span> <span data-ttu-id="90567-134">Si no se especifica, se refleja la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="90567-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="90567-135">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="90567-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="90567-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="90567-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
