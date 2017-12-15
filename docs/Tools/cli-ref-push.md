---
title: "Comando de inserción de NuGet CLI | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Referencia del comando de inserción nuget.exe"
keywords: "referencia de inserción de NuGet, el comando de inserción"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="75fba-104">comando de inserción (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="75fba-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="75fba-105">**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** todos; 4.1.0+ necesarios para nuget.org</span><span class="sxs-lookup"><span data-stu-id="75fba-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="75fba-106">Para insertar los paquetes en nuget.org debe usar nuget.exe v4.1.0 +, que implementa los necesarios [protocolos de NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="75fba-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="75fba-107">Inserta un paquete a un origen de paquete y lo publica.</span><span class="sxs-lookup"><span data-stu-id="75fba-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="75fba-108">Configuración predeterminada de NuGet se obtiene mediante la carga de `%AppData%\NuGet\NuGet.Config`, a continuación, cargar alguna `Nuget.Config` o `.nuget\Nuget.Config` archivos a partir de la raíz de unidad y termina en el directorio actual (vea [configuración de comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="75fba-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="75fba-109">Uso</span><span class="sxs-lookup"><span data-stu-id="75fba-109">Usage</span></span>

```
nuget push <packagePath> [options]
```

<span data-ttu-id="75fba-110">donde `<packagePath>` identifica el paquete para insertar en el servidor.</span><span class="sxs-lookup"><span data-stu-id="75fba-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="75fba-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="75fba-111">Options</span></span>

| <span data-ttu-id="75fba-112">Opción</span><span class="sxs-lookup"><span data-stu-id="75fba-112">Option</span></span> | <span data-ttu-id="75fba-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="75fba-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75fba-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="75fba-114">ApiKey</span></span> | <span data-ttu-id="75fba-115">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="75fba-115">The API key for the target repository.</span></span> <span data-ttu-id="75fba-116">Si no está presente, el especificado en *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="75fba-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="75fba-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="75fba-117">ConfigFile</span></span> | <span data-ttu-id="75fba-118">*(2.5 +)*  NuGet el archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="75fba-118">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="75fba-119">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="75fba-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="75fba-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="75fba-120">DisableBuffering</span></span> | <span data-ttu-id="75fba-121">Deshabilita el almacenamiento en búfer cuando se insertan en un servidor HTTP (s) para reducir los usos de la memoria.</span><span class="sxs-lookup"><span data-stu-id="75fba-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="75fba-122">Precaución: cuando se utiliza esta opción, la autenticación integrada de Windows podría no funcionar.</span><span class="sxs-lookup"><span data-stu-id="75fba-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="75fba-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="75fba-123">ForceEnglishOutput</span></span> | <span data-ttu-id="75fba-124">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="75fba-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="75fba-125">Ayuda</span><span class="sxs-lookup"><span data-stu-id="75fba-125">Help</span></span> | <span data-ttu-id="75fba-126">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="75fba-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="75fba-127">No interactivo</span><span class="sxs-lookup"><span data-stu-id="75fba-127">NonInteractive</span></span> | <span data-ttu-id="75fba-128">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="75fba-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="75fba-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="75fba-129">NoSymbols</span></span> | <span data-ttu-id="75fba-130">*(3.5 +)*  Si existe un paquete de símbolos, no se enviarán a un servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="75fba-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="75fba-131">Origen</span><span class="sxs-lookup"><span data-stu-id="75fba-131">Source</span></span> | <span data-ttu-id="75fba-132">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="75fba-132">Specifies the server URL.</span></span> <span data-ttu-id="75fba-133">Con NuGet 2.5 +, NuGet identificará un origen de la carpeta local o UNC y simplemente copie el archivo no existe en lugar de insertar mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="75fba-133">With NuGet 2.5+, NuGet will identify a UNC or local folder source and simply copy the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="75fba-134">Además, a partir de NuGet 3.4.2, esto es un parámetro obligatorio a menos que la `NuGet.Config` archivo especifica un *DefaultPushSource* valor (vea [NuGet configurar comportamiento](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="75fba-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span></span> |
| <span data-ttu-id="75fba-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="75fba-135">SymbolSource</span></span> | <span data-ttu-id="75fba-136">*(3.5 +)*  Especifica la URL del servidor de símbolos; nuget.smbsrc.net se utiliza cuando se realiza la inserción en nuget.org</span><span class="sxs-lookup"><span data-stu-id="75fba-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="75fba-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="75fba-137">SymbolApiKey</span></span> | <span data-ttu-id="75fba-138">*(3.5 +)*  Especifica la clave de API de la dirección URL especificada en `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="75fba-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="75fba-139">Timeout</span><span class="sxs-lookup"><span data-stu-id="75fba-139">Timeout</span></span> | <span data-ttu-id="75fba-140">Especifica el tiempo de espera, en segundos, para insertar a un servidor.</span><span class="sxs-lookup"><span data-stu-id="75fba-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="75fba-141">El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="75fba-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="75fba-142">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="75fba-142">Verbosity</span></span> | <span data-ttu-id="75fba-143">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="75fba-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="75fba-144">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="75fba-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="75fba-145">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="75fba-145">Examples</span></span>

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
