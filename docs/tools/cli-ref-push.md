---
title: Comando de inserción de NuGet CLI
description: Referencia del comando de inserción nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817196"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="93955-103">comando de inserción (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="93955-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="93955-104">**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** todos; 4.1.0+ necesarios para nuget.org</span><span class="sxs-lookup"><span data-stu-id="93955-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="93955-105">Para insertar los paquetes en nuget.org debe usar nuget.exe v4.1.0 +, que implementa los necesarios [protocolos de NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="93955-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="93955-106">Inserta un paquete a un origen de paquete y lo publica.</span><span class="sxs-lookup"><span data-stu-id="93955-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="93955-107">Configuración predeterminada de NuGet se obtiene mediante la carga de `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux), a continuación, cargar cualquier `Nuget.Config` o `.nuget\Nuget.Config` archivos a partir de la raíz de unidad y termina en el directorio actual (vea [configuración Comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="93955-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="93955-108">Uso</span><span class="sxs-lookup"><span data-stu-id="93955-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="93955-109">donde `<packagePath>` identifica el paquete para insertar en el servidor.</span><span class="sxs-lookup"><span data-stu-id="93955-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="93955-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="93955-110">Options</span></span>

| <span data-ttu-id="93955-111">Opción</span><span class="sxs-lookup"><span data-stu-id="93955-111">Option</span></span> | <span data-ttu-id="93955-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="93955-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93955-113">apiKey</span><span class="sxs-lookup"><span data-stu-id="93955-113">ApiKey</span></span> | <span data-ttu-id="93955-114">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="93955-114">The API key for the target repository.</span></span> <span data-ttu-id="93955-115">Si no está presente, se utiliza el especificado en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="93955-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="93955-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="93955-116">ConfigFile</span></span> | <span data-ttu-id="93955-117">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="93955-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="93955-118">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="93955-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="93955-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="93955-119">DisableBuffering</span></span> | <span data-ttu-id="93955-120">Deshabilita el almacenamiento en búfer cuando se insertan en un servidor HTTP (s) para reducir los usos de la memoria.</span><span class="sxs-lookup"><span data-stu-id="93955-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="93955-121">Precaución: cuando se utiliza esta opción, la autenticación integrada de Windows podría no funcionar.</span><span class="sxs-lookup"><span data-stu-id="93955-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="93955-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="93955-122">ForceEnglishOutput</span></span> | <span data-ttu-id="93955-123">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="93955-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="93955-124">Ayuda</span><span class="sxs-lookup"><span data-stu-id="93955-124">Help</span></span> | <span data-ttu-id="93955-125">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="93955-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="93955-126">No interactivo</span><span class="sxs-lookup"><span data-stu-id="93955-126">NonInteractive</span></span> | <span data-ttu-id="93955-127">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="93955-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="93955-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="93955-128">NoSymbols</span></span> | <span data-ttu-id="93955-129">*(3.5 +)*  Si existe un paquete de símbolos, no se enviarán a un servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="93955-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="93955-130">Origen</span><span class="sxs-lookup"><span data-stu-id="93955-130">Source</span></span> | <span data-ttu-id="93955-131">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="93955-131">Specifies the server URL.</span></span> <span data-ttu-id="93955-132">NuGet identifica un origen de la carpeta local o UNC y simplemente copia el archivo no existe en lugar de insertar mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="93955-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="93955-133">Además, a partir de NuGet 3.4.2, esto es un parámetro obligatorio a menos que la `NuGet.Config` archivo especifica un *DefaultPushSource* valor (vea [NuGet configurar comportamiento](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="93955-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="93955-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="93955-134">SymbolSource</span></span> | <span data-ttu-id="93955-135">*(3.5 +)*  Especifica la URL del servidor de símbolos; nuget.smbsrc.net se utiliza cuando se realiza la inserción en nuget.org</span><span class="sxs-lookup"><span data-stu-id="93955-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="93955-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="93955-136">SymbolApiKey</span></span> | <span data-ttu-id="93955-137">*(3.5 +)*  Especifica la clave de API de la dirección URL especificada en `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="93955-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="93955-138">Timeout</span><span class="sxs-lookup"><span data-stu-id="93955-138">Timeout</span></span> | <span data-ttu-id="93955-139">Especifica el tiempo de espera, en segundos, para insertar a un servidor.</span><span class="sxs-lookup"><span data-stu-id="93955-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="93955-140">El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="93955-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="93955-141">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="93955-141">Verbosity</span></span> | <span data-ttu-id="93955-142">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="93955-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="93955-143">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="93955-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="93955-144">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="93955-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
