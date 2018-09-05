---
title: Comando de reflejo de la CLI de NuGet
description: Referencia del comando de reflejo de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550211"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="8dab9-103">Comando mirror (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="8dab9-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="8dab9-104">**Se aplica a:** publicación del paquete &bullet; **versiones compatibles:** en desuso en 3.2 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="8dab9-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="8dab9-105">Refleja un paquete y sus dependencias de los repositorios de origen especificado en el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="8dab9-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="8dab9-106">Para habilitar este comando para las versiones de NuGet antes 3.2, vaya a [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), seleccione la versión estable más reciente, descargue `NuGet.ServerExtensions.dll` y `Nuget-Signed.exe` en el disco local y el cambio de nombre `Nuget-Signed.exe` a `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="8dab9-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="8dab9-107">Uso</span><span class="sxs-lookup"><span data-stu-id="8dab9-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="8dab9-108">donde `<packageID>` es el paquete para crear el reflejo, o `<configFilePath>` identifica el `packages.config` archivo que enumera los paquetes que se va a reflejar.</span><span class="sxs-lookup"><span data-stu-id="8dab9-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="8dab9-109">El `<listUrlTarget>` especifica el repositorio de origen, y `<publishUrlTarget>` especifica el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="8dab9-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="8dab9-110">Si el repositorio de destino está en `https://machine/repo` que se está ejecutando [NuGet.Server](../hosting-packages/nuget-server.md), las direcciones URL de lista e inserte será `https://machine/repo/nuget` y `https://machine/repo/api/v2/package`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8dab9-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="8dab9-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="8dab9-111">Options</span></span>

| <span data-ttu-id="8dab9-112">Opción</span><span class="sxs-lookup"><span data-stu-id="8dab9-112">Option</span></span> | <span data-ttu-id="8dab9-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="8dab9-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8dab9-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="8dab9-114">ApiKey</span></span> | <span data-ttu-id="8dab9-115">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="8dab9-115">The API key for the target repository.</span></span> <span data-ttu-id="8dab9-116">Si no está presente, el especificado en el archivo de configuración se utiliza (`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="8dab9-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="8dab9-117">Ayuda</span><span class="sxs-lookup"><span data-stu-id="8dab9-117">Help</span></span> | <span data-ttu-id="8dab9-118">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="8dab9-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="8dab9-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="8dab9-119">NoCache</span></span> | <span data-ttu-id="8dab9-120">Impide que NuGet utilice paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="8dab9-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="8dab9-121">Consulte [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="8dab9-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="8dab9-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="8dab9-122">Noop</span></span> | <span data-ttu-id="8dab9-123">Registra qué haría pero no lleva a cabo las acciones; se da por supuesto se realizó correctamente para las operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="8dab9-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="8dab9-124">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="8dab9-124">PreRelease</span></span> | <span data-ttu-id="8dab9-125">Incluye paquetes de versión preliminar de la operación de creación de reflejo.</span><span class="sxs-lookup"><span data-stu-id="8dab9-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="8dab9-126">Origen</span><span class="sxs-lookup"><span data-stu-id="8dab9-126">Source</span></span> | <span data-ttu-id="8dab9-127">Una lista de orígenes de paquetes para crear el reflejo.</span><span class="sxs-lookup"><span data-stu-id="8dab9-127">A list of package sources to mirror.</span></span> <span data-ttu-id="8dab9-128">Si no se especifica ningún origen, los que se definen en el archivo de configuración (consulte ApiKey anterior) se usan de forma predeterminada en nuget.org si se especifica ninguno.</span><span class="sxs-lookup"><span data-stu-id="8dab9-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="8dab9-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="8dab9-129">Timeout</span></span> | <span data-ttu-id="8dab9-130">Especifica el tiempo de espera en segundos, para insertar en un servidor.</span><span class="sxs-lookup"><span data-stu-id="8dab9-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="8dab9-131">El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="8dab9-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="8dab9-132">Versión</span><span class="sxs-lookup"><span data-stu-id="8dab9-132">Version</span></span> | <span data-ttu-id="8dab9-133">La versión del paquete para instalar.</span><span class="sxs-lookup"><span data-stu-id="8dab9-133">The version of the package to install.</span></span> <span data-ttu-id="8dab9-134">Si no se especifica, se refleja la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="8dab9-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="8dab9-135">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8dab9-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8dab9-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="8dab9-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
