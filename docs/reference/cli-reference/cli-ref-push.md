---
title: Comando de instalación de CLI de NuGet
description: Referencia del comando de instalación de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327632"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="fcd7c-103">comando de extracción (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="fcd7c-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="fcd7c-104">**Se aplica a:** versiones &bullet; admitidas de publicación de paquetes **:** All; 4.1.0 + requerido para Nuget.org</span><span class="sxs-lookup"><span data-stu-id="fcd7c-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="fcd7c-105">Para enviar paquetes a nuget.org, debe usar Nuget. exe v 4.1.0 +, que implementa los protocolos de [Nuget](../../api/nuget-protocols.md)necesarios.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="fcd7c-106">Envía un paquete a un origen de paquete y lo publica.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="fcd7c-107">La configuración predeterminada de NuGet se obtiene mediante `%AppData%\NuGet\NuGet.Config` la carga de ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux), `Nuget.Config` la `.nuget\Nuget.Config` carga de los archivos o a partir de la raíz de la unidad y la finalización en el directorio actual (consulte [NuGet común). configuraciones](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="fcd7c-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="fcd7c-108">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd7c-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="fcd7c-109">donde `<packagePath>` identifica el paquete que se va a enviar al servidor.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="fcd7c-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="fcd7c-110">Options</span></span>

| <span data-ttu-id="fcd7c-111">Opción</span><span class="sxs-lookup"><span data-stu-id="fcd7c-111">Option</span></span> | <span data-ttu-id="fcd7c-112">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="fcd7c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fcd7c-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="fcd7c-113">ApiKey</span></span> | <span data-ttu-id="fcd7c-114">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-114">The API key for the target repository.</span></span> <span data-ttu-id="fcd7c-115">Si no está presente, se utiliza el especificado en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="fcd7c-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fcd7c-116">ConfigFile</span></span> | <span data-ttu-id="fcd7c-117">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fcd7c-118">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fcd7c-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fcd7c-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="fcd7c-119">DisableBuffering</span></span> | <span data-ttu-id="fcd7c-120">Deshabilita el almacenamiento en búfer al insertar en un servidor HTTP (s) para reducir los usos de memoria.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="fcd7c-121">PRECAUCIÓN: cuando se usa esta opción, es posible que la autenticación integrada de Windows no funcione.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="fcd7c-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fcd7c-122">ForceEnglishOutput</span></span> | <span data-ttu-id="fcd7c-123">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fcd7c-124">Help</span><span class="sxs-lookup"><span data-stu-id="fcd7c-124">Help</span></span> | <span data-ttu-id="fcd7c-125">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="fcd7c-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fcd7c-126">NonInteractive</span></span> | <span data-ttu-id="fcd7c-127">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fcd7c-128">Nosymbols</span><span class="sxs-lookup"><span data-stu-id="fcd7c-128">NoSymbols</span></span> | <span data-ttu-id="fcd7c-129">*(3.5 +)* Si existe un paquete de símbolos, no se insertará en un servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="fcd7c-130">source</span><span class="sxs-lookup"><span data-stu-id="fcd7c-130">Source</span></span> | <span data-ttu-id="fcd7c-131">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-131">Specifies the server URL.</span></span> <span data-ttu-id="fcd7c-132">NuGet identifica un origen de carpeta local o UNC y simplemente copia el archivo allí en lugar de insertarlo mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="fcd7c-133">Además, a partir de NuGet 3.4.2, se trata de un parámetro obligatorio `NuGet.Config` , a menos que el archivo especifique un valor de *DefaultPushSource* (consulte [configuración del comportamiento de NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="fcd7c-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="fcd7c-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="fcd7c-134">SkipDuplicate</span></span> | <span data-ttu-id="fcd7c-135">*(5.1 +)* Si ya existe un paquete y una versión, omítalo y continúe con el siguiente paquete de la extracción, si existe.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="fcd7c-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="fcd7c-136">SymbolSource</span></span> | <span data-ttu-id="fcd7c-137">*(3.5 +)* Especifica la dirección URL del servidor de símbolos; nuget.smbsrc.net se usa al insertar en nuget.org</span><span class="sxs-lookup"><span data-stu-id="fcd7c-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="fcd7c-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="fcd7c-138">SymbolApiKey</span></span> | <span data-ttu-id="fcd7c-139">*(3.5 +)* Especifica la clave de API de la dirección URL `-SymbolSource`especificada en.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="fcd7c-140">Tiempo de espera</span><span class="sxs-lookup"><span data-stu-id="fcd7c-140">Timeout</span></span> | <span data-ttu-id="fcd7c-141">Especifica el tiempo de espera, en segundos, para insertar en un servidor.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="fcd7c-142">El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="fcd7c-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="fcd7c-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="fcd7c-143">Verbosity</span></span> | <span data-ttu-id="fcd7c-144">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="fcd7c-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fcd7c-145">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fcd7c-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fcd7c-146">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="fcd7c-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
