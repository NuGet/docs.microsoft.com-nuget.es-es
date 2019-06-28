---
title: Comando de CLI de NuGet config
description: Referencia para el comando config de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426070"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="8fddc-103">comando config (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="8fddc-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="8fddc-104">**Se aplica a:** todas &bullet; **versiones compatibles de**: todas</span><span class="sxs-lookup"><span data-stu-id="8fddc-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="8fddc-105">Obtiene o establece los valores de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="8fddc-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="8fddc-106">Para el uso adicional, consulte [configuraciones comunes NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8fddc-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="8fddc-107">Para más información sobre los nombres de clave permitidos, consulte el [referencia del archivo de configuración de NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="8fddc-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8fddc-108">Uso</span><span class="sxs-lookup"><span data-stu-id="8fddc-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="8fddc-109">donde `<name>` y `<value>` especificar un par de clave y valor debe establecerse en la configuración.</span><span class="sxs-lookup"><span data-stu-id="8fddc-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="8fddc-110">Puede especificar tantos pares según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8fddc-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="8fddc-111">Para quitar un valor, especifique el nombre y la `=` inicio de sesión, pero ningún valor.</span><span class="sxs-lookup"><span data-stu-id="8fddc-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="8fddc-112">Para los nombres de clave permitidos, consulte el [referencia del archivo de configuración de NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="8fddc-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="8fddc-113">En NuGet 3.4 y versiones posteriores, `<value>` puede usar [variables de entorno](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="8fddc-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="8fddc-114">Opciones</span><span class="sxs-lookup"><span data-stu-id="8fddc-114">Options</span></span>

| <span data-ttu-id="8fddc-115">Opción</span><span class="sxs-lookup"><span data-stu-id="8fddc-115">Option</span></span> | <span data-ttu-id="8fddc-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="8fddc-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8fddc-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="8fddc-117">AsPath</span></span> | <span data-ttu-id="8fddc-118">Devuelve el valor de la configuración como una ruta de acceso, se omite cuando `-Set` se utiliza.</span><span class="sxs-lookup"><span data-stu-id="8fddc-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="8fddc-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8fddc-119">ConfigFile</span></span> | <span data-ttu-id="8fddc-120">El archivo de configuración para modificar.</span><span class="sxs-lookup"><span data-stu-id="8fddc-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="8fddc-121">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="8fddc-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8fddc-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8fddc-122">ForceEnglishOutput</span></span> | <span data-ttu-id="8fddc-123">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="8fddc-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8fddc-124">Help</span><span class="sxs-lookup"><span data-stu-id="8fddc-124">Help</span></span> | <span data-ttu-id="8fddc-125">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="8fddc-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="8fddc-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8fddc-126">NonInteractive</span></span> | <span data-ttu-id="8fddc-127">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="8fddc-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8fddc-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="8fddc-128">Verbosity</span></span> | <span data-ttu-id="8fddc-129">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="8fddc-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8fddc-130">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8fddc-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="8fddc-131">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="8fddc-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
