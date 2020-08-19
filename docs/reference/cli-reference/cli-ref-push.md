---
title: Comando de instalación de CLI de NuGet
description: Referencia de la nuget.exe comando de extracción
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622851"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="dcf7a-103">comando de extracción (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="dcf7a-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="dcf7a-104">**Se aplica a:** &bullet; **versiones admitidas** de publicación de paquetes: ALL; 4.1.0 + requerido para Nuget.org</span><span class="sxs-lookup"><span data-stu-id="dcf7a-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="dcf7a-105">Para enviar paquetes a nuget.org, debe usar nuget.exe v 4.1.0 +, que implementa los protocolos de [Nuget](../../api/nuget-protocols.md)necesarios.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="dcf7a-106">Envía un paquete a un origen de paquete y lo publica.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="dcf7a-107">La configuración predeterminada de NuGet se obtiene mediante la carga de `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), la carga `Nuget.Config` de los archivos o a partir de la `.nuget\Nuget.Config` raíz de la unidad y la finalización en el directorio actual (consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="dcf7a-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="dcf7a-108">Uso</span><span class="sxs-lookup"><span data-stu-id="dcf7a-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="dcf7a-109">donde `<packagePath>` identifica el paquete que se va a enviar al servidor.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="dcf7a-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="dcf7a-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="dcf7a-111">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-111">The API key for the target repository.</span></span> <span data-ttu-id="dcf7a-112">Si no está presente, se utiliza el especificado en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="dcf7a-113">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dcf7a-114">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="dcf7a-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="dcf7a-115">Deshabilita el almacenamiento en búfer al insertar en un servidor HTTP (s) para reducir los usos de memoria.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="dcf7a-116">PRECAUCIÓN: cuando se usa esta opción, es posible que la autenticación integrada de Windows no funcione.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="dcf7a-117">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="dcf7a-118">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="dcf7a-119">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="dcf7a-120">No se anexa `api/v2/packages` a la dirección URL de origen.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="dcf7a-121">*(3.5 +)* Si existe un paquete de símbolos, no se insertará en un servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="dcf7a-122">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-122">Specifies the server URL.</span></span> <span data-ttu-id="dcf7a-123">NuGet identifica un origen de carpeta local o UNC y simplemente copia el archivo allí en lugar de insertarlo mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="dcf7a-124">Además, a partir de NuGet 3.4.2, se trata de un parámetro obligatorio, a menos que el `NuGet.Config` archivo especifique un valor de *DefaultPushSource* (consulte [configuración del comportamiento de NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="dcf7a-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="dcf7a-125">*(5.1 +)* Si ya existe un paquete y una versión, omítalo y continúe con el siguiente paquete de la extracción, si existe.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="dcf7a-126">*(3.5 +)* Especifica la dirección URL del servidor de símbolos; nuget.smbsrc.net se usa al insertar en nuget.org</span><span class="sxs-lookup"><span data-stu-id="dcf7a-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="dcf7a-127">*(3.5 +)* Especifica la clave de API de la dirección URL especificada en `-SymbolSource` .</span><span class="sxs-lookup"><span data-stu-id="dcf7a-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="dcf7a-128">Especifica el tiempo de espera, en segundos, para insertar en un servidor.</span><span class="sxs-lookup"><span data-stu-id="dcf7a-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="dcf7a-129"> El valor predeterminado es 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="dcf7a-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="dcf7a-130">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="dcf7a-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="dcf7a-131">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dcf7a-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dcf7a-132">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="dcf7a-132">Examples</span></span>

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
