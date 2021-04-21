---
title: Solución de problemas de paquetes instalados
description: Cómo buscar qué origen de paquete se usó para paquetes individuales
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387536"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="9338b-103">Solución de problemas de paquetes instalados</span><span class="sxs-lookup"><span data-stu-id="9338b-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="9338b-104">En ocasiones, es posible que quiera validar desde qué origen se instaló un paquete específico.</span><span class="sxs-lookup"><span data-stu-id="9338b-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="9338b-105">Estas son algunas de las formas de comprobarlo.</span><span class="sxs-lookup"><span data-stu-id="9338b-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="9338b-106">Algunos orígenes de paquetes admiten un concepto conocido como orígenes ascendentes.</span><span class="sxs-lookup"><span data-stu-id="9338b-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="9338b-107">Por ejemplo, los [orígenes ascendentes de Azure Artifacts](/azure/devops/artifacts/concepts/upstream-sources).</span><span class="sxs-lookup"><span data-stu-id="9338b-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="9338b-108">Los clientes NuGet no saben si un paquete provenía de un origen ascendente.</span><span class="sxs-lookup"><span data-stu-id="9338b-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="9338b-109">Por lo tanto, cualquier registro del origen del paquete mostrará el origen configurado, no el origen ascendente.</span><span class="sxs-lookup"><span data-stu-id="9338b-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="9338b-110">Archivo `.nupkg.metadata` de la carpeta global-packages</span><span class="sxs-lookup"><span data-stu-id="9338b-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="9338b-111">Cuando se extrae un paquete en la carpeta *global-packages*, se escribe un archivo `.nupkg.metadata`.</span><span class="sxs-lookup"><span data-stu-id="9338b-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="9338b-112">A partir de NuGet 5.9.0, se agrega el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="9338b-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="9338b-113">Consulte a continuación para asignar versiones de NuGet a versiones de Visual Studio o del SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="9338b-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="9338b-114">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9338b-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="9338b-115">Si en la carpeta *global-packages* se han extraído paquetes antes de que actualice a una versión más reciente de herramientas que tenga NuGet 5.9.0, el archivo `.nupkg.metadata` tendrá la versión 1 y no contendrá el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="9338b-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="9338b-116">Puede [borrar la carpeta *global-packages*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) para que todos los paquetes contengan el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="9338b-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="9338b-117">NuGet escribe el archivo `.nupkg.metadata` solo en la carpeta *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="9338b-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="9338b-118">Los proyectos que usan `packages.config` emplean una carpeta de paquetes de solución, que no crea un archivo `.nupkg.metadata`.</span><span class="sxs-lookup"><span data-stu-id="9338b-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="9338b-119">Mensaje de registro del paquete instalado</span><span class="sxs-lookup"><span data-stu-id="9338b-119">Installed package log message</span></span>

<span data-ttu-id="9338b-120">A partir de NuGet 5.9.0, el origen del paquete se genera en el mensaje de restauración que informa de que se ha instalado un paquete.</span><span class="sxs-lookup"><span data-stu-id="9338b-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="9338b-121">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9338b-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="9338b-122">Este mensaje se genera en el nivel de detalle normal o informativo.</span><span class="sxs-lookup"><span data-stu-id="9338b-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="9338b-123">Visual Studio y la CLI de `dotnet` tienen como valor predeterminado el nivel de detalle mínimo, por lo que este mensaje no estará visible de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9338b-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="9338b-124">Las herramientas de la CLI `msbuild` y `nuget` tienen como valor predeterminado el nivel de detalle normal, por lo que este mensaje estará visible de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9338b-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="9338b-125">Mensaje de registro HTTP</span><span class="sxs-lookup"><span data-stu-id="9338b-125">HTTP log message</span></span>

<span data-ttu-id="9338b-126">Cuando un paquete no está disponible localmente, ya sea en la carpeta *global-packages*, en una carpeta de reserva o en un origen de archivo local, NuGet lo descarga de cualquier origen de paquete configurado a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9338b-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="9338b-127">Las solicitudes y respuestas HTTP se registran en el nivel de detalle normal y solo debería ver una solicitud y respuesta por versión del paquete.</span><span class="sxs-lookup"><span data-stu-id="9338b-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="9338b-128">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9338b-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="9338b-129">Si los archivos se descargaron recientemente, podrían recuperarse de *http-cache* de NuGet.</span><span class="sxs-lookup"><span data-stu-id="9338b-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="9338b-130">El formato de dirección URL puede ser diferente para las distintas implementaciones de servidor HTTP de NuGet y según si implementa el protocolo HTTP NuGet V2 o V3.</span><span class="sxs-lookup"><span data-stu-id="9338b-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="9338b-131">Si `nuget.config` tiene varios orígenes HTTP definidos, verá varias solicitudes al archivo `index.json` de cada paquete, una para cada origen.</span><span class="sxs-lookup"><span data-stu-id="9338b-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="9338b-132">Sin embargo, solo habrá una descarga `nupkg` para cada versión del paquete.</span><span class="sxs-lookup"><span data-stu-id="9338b-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="9338b-133">Mensaje de registro de firma de paquete</span><span class="sxs-lookup"><span data-stu-id="9338b-133">Package signature log message</span></span>

<span data-ttu-id="9338b-134">Si el paquete que se descarga está firmado, NuGet validará la firma y registrará el mensaje siguiente en el nivel de detalle pormenorizado:</span><span class="sxs-lookup"><span data-stu-id="9338b-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="9338b-135">Este mensaje se mostrará si el paquete se descargó de un origen de paquete HTTP o se copió de un origen de paquete local.</span><span class="sxs-lookup"><span data-stu-id="9338b-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="9338b-136">No se mostrará si el paquete ya está disponible en la carpeta *global-packages* o en una carpeta de reserva.</span><span class="sxs-lookup"><span data-stu-id="9338b-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="9338b-137">Debido a la [eliminación de la confianza de la entidad de certificación VeriSign](https://github.com/dotnet/announcements/issues/180), NuGet ha deshabilitado la comprobación de paquetes firmados en determinadas plataformas, en determinadas versiones de NuGet y en el SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="9338b-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="9338b-138">Por lo tanto, es posible que los mismos paquetes tengan registros `PackageSignatureVerificationLog` o que falten esos registros, en función de la plataforma en la que se ejecute la restauración y de la versión de .NET o NuGet que se use.</span><span class="sxs-lookup"><span data-stu-id="9338b-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="9338b-139">Asignación de versiones de NuGet</span><span class="sxs-lookup"><span data-stu-id="9338b-139">NuGet Version Map</span></span>

<span data-ttu-id="9338b-140">Las siguientes versiones de NuGet tienen cambios importantes relacionados con el registro del origen del paquete:</span><span class="sxs-lookup"><span data-stu-id="9338b-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="9338b-141">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="9338b-141">NuGet Version</span></span>|<span data-ttu-id="9338b-142">Versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9338b-142">Visual Studio Version</span></span>|<span data-ttu-id="9338b-143">Versión del SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="9338b-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="9338b-144">NuGet 5.9.0</span><span class="sxs-lookup"><span data-stu-id="9338b-144">NuGet 5.9.0</span></span>|<span data-ttu-id="9338b-145">Visual Studio 2019 16.9.0</span><span class="sxs-lookup"><span data-stu-id="9338b-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="9338b-146">SDK de .NET 5 5.0.200</span><span class="sxs-lookup"><span data-stu-id="9338b-146">.NET 5 SDK 5.0.200</span></span>|
