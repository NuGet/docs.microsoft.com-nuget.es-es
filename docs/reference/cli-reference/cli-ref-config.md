---
title: Comando de configuración de la CLI de NuGet
description: Referencia del comando nuget.exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622881"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="c30f0-103">comando config (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="c30f0-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="c30f0-104">**Se aplica a:** todas &bullet; **las versiones compatibles**: todas</span><span class="sxs-lookup"><span data-stu-id="c30f0-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="c30f0-105">Obtiene o establece los valores de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="c30f0-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="c30f0-106">Para obtener más uso, consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c30f0-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="c30f0-107">Para obtener más información sobre los nombres de clave permitidos, consulte la [Referencia del archivo de configuración de NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="c30f0-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c30f0-108">Uso</span><span class="sxs-lookup"><span data-stu-id="c30f0-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="c30f0-109">donde `<name>` y `<value>` especifican un par clave-valor que se establecerá en la configuración.</span><span class="sxs-lookup"><span data-stu-id="c30f0-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="c30f0-110">Puede especificar tantos pares como desee.</span><span class="sxs-lookup"><span data-stu-id="c30f0-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="c30f0-111">Para quitar un valor, especifique el nombre y el `=` signo pero no el valor.</span><span class="sxs-lookup"><span data-stu-id="c30f0-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="c30f0-112">Para ver los nombres de clave permitidos, consulte la [Referencia del archivo de configuración de NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="c30f0-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="c30f0-113">En NuGet 3.4 +, `<value>` puede usar [variables de entorno](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c30f0-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="c30f0-114">Opciones</span><span class="sxs-lookup"><span data-stu-id="c30f0-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="c30f0-115">Devuelve el valor de configuración como una ruta de acceso, que se omite cuando `-Set` se usa.</span><span class="sxs-lookup"><span data-stu-id="c30f0-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c30f0-116">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="c30f0-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c30f0-117">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c30f0-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c30f0-118">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="c30f0-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c30f0-119">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="c30f0-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c30f0-120">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="c30f0-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="c30f0-121">Uno en más pares clave-valor que se establecerá en la configuración.</span><span class="sxs-lookup"><span data-stu-id="c30f0-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c30f0-122">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c30f0-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="c30f0-123">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c30f0-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="c30f0-124">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c30f0-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
