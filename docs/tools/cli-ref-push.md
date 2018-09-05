---
title: Comando de CLI de NuGet push
description: Referencia del comando de inserción de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548348"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="415ce-103">inserción de comandos (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="415ce-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="415ce-104">**Se aplica a:** publicación del paquete &bullet; **versiones compatibles:** todos; 4.1.0 necesarios para nuget.org</span><span class="sxs-lookup"><span data-stu-id="415ce-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="415ce-105">Para insertar paquetes en nuget.org debe usar nuget.exe 4.1.0 +, que implementa la requiere [protocolos de NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="415ce-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="415ce-106">Inserta un paquete a un origen de paquete y lo publica.</span><span class="sxs-lookup"><span data-stu-id="415ce-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="415ce-107">Configuración predeterminada de NuGet se obtiene mediante la carga `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), a continuación, cargar cualquier `Nuget.Config` o `.nuget\Nuget.Config` archivos a partir de la raíz de la unidad y finalizando en el directorio actual (consulte [configuración Comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="415ce-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="415ce-108">Uso</span><span class="sxs-lookup"><span data-stu-id="415ce-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="415ce-109">donde `<packagePath>` identifica el paquete para insertar en el servidor.</span><span class="sxs-lookup"><span data-stu-id="415ce-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="415ce-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="415ce-110">Options</span></span>

| <span data-ttu-id="415ce-111">Opción</span><span class="sxs-lookup"><span data-stu-id="415ce-111">Option</span></span> | <span data-ttu-id="415ce-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="415ce-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="415ce-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="415ce-113">ApiKey</span></span> | <span data-ttu-id="415ce-114">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="415ce-114">The API key for the target repository.</span></span> <span data-ttu-id="415ce-115">Si no está presente, se utiliza el especificado en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="415ce-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="415ce-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="415ce-116">ConfigFile</span></span> | <span data-ttu-id="415ce-117">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="415ce-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="415ce-118">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="415ce-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="415ce-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="415ce-119">DisableBuffering</span></span> | <span data-ttu-id="415ce-120">Deshabilita el almacenamiento en búfer al insertar en un servidor HTTP (s) para disminuir los usos de la memoria.</span><span class="sxs-lookup"><span data-stu-id="415ce-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="415ce-121">Precaución: cuando se usa esta opción, la autenticación integrada de Windows podría no funcionar.</span><span class="sxs-lookup"><span data-stu-id="415ce-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="415ce-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="415ce-122">ForceEnglishOutput</span></span> | <span data-ttu-id="415ce-123">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="415ce-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="415ce-124">Ayuda</span><span class="sxs-lookup"><span data-stu-id="415ce-124">Help</span></span> | <span data-ttu-id="415ce-125">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="415ce-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="415ce-126">No interactivo</span><span class="sxs-lookup"><span data-stu-id="415ce-126">NonInteractive</span></span> | <span data-ttu-id="415ce-127">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="415ce-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="415ce-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="415ce-128">NoSymbols</span></span> | <span data-ttu-id="415ce-129">*(3.5 y versiones posteriores)*  Si existe un paquete de símbolos, no se podrán realizar en un servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="415ce-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="415ce-130">Origen</span><span class="sxs-lookup"><span data-stu-id="415ce-130">Source</span></span> | <span data-ttu-id="415ce-131">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="415ce-131">Specifies the server URL.</span></span> <span data-ttu-id="415ce-132">NuGet identifica un origen de la carpeta local o UNC y simplemente copia el archivo existe en lugar de insertar mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="415ce-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="415ce-133">Además, a partir de NuGet 3.4.2, esto es un parámetro obligatorio a menos que el `NuGet.Config` archivo especifica un *DefaultPushSource* valor (consulte [del comportamiento de configuración de NuGet](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="415ce-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="415ce-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="415ce-134">SymbolSource</span></span> | <span data-ttu-id="415ce-135">*(3.5 y versiones posteriores)*  Especifica la URL del servidor de símbolos; nuget.smbsrc.net se utiliza al realizar inserciones en nuget.org</span><span class="sxs-lookup"><span data-stu-id="415ce-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="415ce-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="415ce-136">SymbolApiKey</span></span> | <span data-ttu-id="415ce-137">*(3.5 y versiones posteriores)*  Especifica la clave de API de la dirección URL especificada en `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="415ce-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="415ce-138">Timeout</span><span class="sxs-lookup"><span data-stu-id="415ce-138">Timeout</span></span> | <span data-ttu-id="415ce-139">Especifica el tiempo de espera en segundos, para insertar en un servidor.</span><span class="sxs-lookup"><span data-stu-id="415ce-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="415ce-140">El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="415ce-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="415ce-141">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="415ce-141">Verbosity</span></span> | <span data-ttu-id="415ce-142">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="415ce-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="415ce-143">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="415ce-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="415ce-144">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="415ce-144">Examples</span></span>

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
