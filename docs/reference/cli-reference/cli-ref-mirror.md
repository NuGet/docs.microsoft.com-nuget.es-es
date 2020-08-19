---
title: Comando de reflejo de la CLI de NuGet
description: Referencia del comando nuget.exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622972"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="53559-103">comando Mirror (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="53559-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="53559-104">**Se aplica a:** &bullet; **versiones compatibles** de publicación de paquetes: desusados en 3,2 +</span><span class="sxs-lookup"><span data-stu-id="53559-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="53559-105">Refleja un paquete y sus dependencias de los repositorios de origen especificados en el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="53559-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="53559-106">Los NuGet.ServerExtensions.dll y NuGet-Signed.exe que anteriormente admitían este comando en NuGet 2. x (cambiando el nombre de NuGet-Signed.exe a nuget.exe) ya no están disponibles para su descarga.</span><span class="sxs-lookup"><span data-stu-id="53559-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="53559-107">Para usar un comando similar a este, pruebe [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="53559-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="53559-108">Uso</span><span class="sxs-lookup"><span data-stu-id="53559-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="53559-109">donde `<packageID>` es el paquete que se va a reflejar, o `<configFilePath>` identifica el `packages.config` archivo que muestra los paquetes que se van a reflejar.</span><span class="sxs-lookup"><span data-stu-id="53559-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="53559-110">`<listUrlTarget>`Especifica el repositorio de origen y `<publishUrlTarget>` especifica el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="53559-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="53559-111">Si el repositorio de destino se encuentra en `https://machine/repo` que ejecuta [NuGet. Server](../../hosting-packages/nuget-server.md), la lista y las direcciones URL de inserciones serán `https://machine/repo/nuget` y `https://machine/repo/api/v2/package` , respectivamente.</span><span class="sxs-lookup"><span data-stu-id="53559-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="53559-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="53559-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="53559-113">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="53559-113">The API key for the target repository.</span></span> <span data-ttu-id="53559-114">Si no está presente, se usa el especificado en el archivo de configuración ( `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="53559-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="53559-115">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="53559-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="53559-116">Impide que NuGet use paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="53559-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="53559-117">Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="53559-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="53559-118">Registra lo que se haría pero no realiza las acciones; supone que las operaciones de inserciones se han realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="53559-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="53559-119">Incluye paquetes de versión preliminar en la operación de creación de reflejo.</span><span class="sxs-lookup"><span data-stu-id="53559-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="53559-120">Una lista de orígenes de paquetes que se van a reflejar.</span><span class="sxs-lookup"><span data-stu-id="53559-120">A list of package sources to mirror.</span></span> <span data-ttu-id="53559-121">Si no se especifican orígenes, se usan los definidos en el archivo de configuración (vea ApiKey anterior), de forma predeterminada se usa nuget.org si no se especifica ninguno.</span><span class="sxs-lookup"><span data-stu-id="53559-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="53559-122">Especifica el tiempo de espera, en segundos, para insertar en un servidor.</span><span class="sxs-lookup"><span data-stu-id="53559-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="53559-123"> El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="53559-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="53559-124">Versión del paquete que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="53559-124">The version of the package to install.</span></span> <span data-ttu-id="53559-125">Si no se especifica, la versión más reciente está reflejada.</span><span class="sxs-lookup"><span data-stu-id="53559-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="53559-126">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="53559-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="53559-127">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="53559-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
