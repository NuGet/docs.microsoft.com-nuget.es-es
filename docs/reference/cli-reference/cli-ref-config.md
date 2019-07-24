---
title: Comando de configuración de la CLI de NuGet
description: Referencia del comando de configuración de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433312"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="7d308-103">comando config (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="7d308-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="7d308-104">**Se aplica a:** todas &bullet; **las versiones compatibles**: todas</span><span class="sxs-lookup"><span data-stu-id="7d308-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="7d308-105">Obtiene o establece los valores de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d308-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="7d308-106">Para obtener más uso, consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7d308-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="7d308-107">Para obtener más información sobre los nombres de clave permitidos, consulte la [Referencia del archivo de configuración de NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="7d308-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7d308-108">Uso</span><span class="sxs-lookup"><span data-stu-id="7d308-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="7d308-109">donde `<name>` y`<value>` especifican un par clave-valor que se establecerá en la configuración.</span><span class="sxs-lookup"><span data-stu-id="7d308-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="7d308-110">Puede especificar tantos pares como desee.</span><span class="sxs-lookup"><span data-stu-id="7d308-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="7d308-111">Para quitar un valor, especifique el nombre y el `=` signo pero no el valor.</span><span class="sxs-lookup"><span data-stu-id="7d308-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="7d308-112">Para ver los nombres de clave permitidos, consulte la [Referencia del archivo de configuración de NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="7d308-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="7d308-113">En NuGet 3.4 +, `<value>` puede usar [variables de entorno](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="7d308-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="7d308-114">Opciones</span><span class="sxs-lookup"><span data-stu-id="7d308-114">Options</span></span>

| <span data-ttu-id="7d308-115">Opción</span><span class="sxs-lookup"><span data-stu-id="7d308-115">Option</span></span> | <span data-ttu-id="7d308-116">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="7d308-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7d308-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="7d308-117">AsPath</span></span> | <span data-ttu-id="7d308-118">Devuelve el valor de configuración como una ruta de acceso `-Set` , que se omite cuando se usa.</span><span class="sxs-lookup"><span data-stu-id="7d308-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="7d308-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7d308-119">ConfigFile</span></span> | <span data-ttu-id="7d308-120">El archivo de configuración de NuGet que se va a modificar.</span><span class="sxs-lookup"><span data-stu-id="7d308-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="7d308-121">Si no se especifica, se usa el archivo predeterminado`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.config/NuGet/NuGet.Config` (Mac/Linux) o `~/.nuget/NuGet/NuGet.Config` (varía según la distribución del SO).</span><span class="sxs-lookup"><span data-stu-id="7d308-121">If not specified, the default file is used -`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.config/NuGet/NuGet.Config`  (Mac/Linux) or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution).</span></span>|
| <span data-ttu-id="7d308-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7d308-122">ForceEnglishOutput</span></span> | <span data-ttu-id="7d308-123">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="7d308-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7d308-124">Help</span><span class="sxs-lookup"><span data-stu-id="7d308-124">Help</span></span> | <span data-ttu-id="7d308-125">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="7d308-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="7d308-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7d308-126">NonInteractive</span></span> | <span data-ttu-id="7d308-127">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="7d308-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7d308-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="7d308-128">Verbosity</span></span> | <span data-ttu-id="7d308-129">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="7d308-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7d308-130">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7d308-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="7d308-131">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7d308-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
