---
title: Comando config de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia para el comando config de nuget.exe
keywords: "referencia de configuración de NuGet, comando config"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 31abc5c1ade0aff9a2f23ec89ec7082acedb3653
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="a05bf-104">comando config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a05bf-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="a05bf-105">**Se aplica a:** todos los &bullet; **versiones compatibles**: todos los</span><span class="sxs-lookup"><span data-stu-id="a05bf-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="a05bf-106">Obtiene o establece los valores de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="a05bf-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="a05bf-107">Para uso adicionales, consulte [configuración de comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a05bf-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="a05bf-108">Para obtener información detallada sobre los nombres de clave permitidos, consulte la [referencia del archivo de configuración de NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="a05bf-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a05bf-109">Uso</span><span class="sxs-lookup"><span data-stu-id="a05bf-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="a05bf-110">donde `<name>` y `<value>` especificar un par clave-valor que se establecerán en la configuración.</span><span class="sxs-lookup"><span data-stu-id="a05bf-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="a05bf-111">Puede especificar tantos pares según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a05bf-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="a05bf-112">Para quitar un valor, especifique el nombre y la `=` inicio de sesión, pero ningún valor.</span><span class="sxs-lookup"><span data-stu-id="a05bf-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="a05bf-113">Para los nombres de clave permitidos, consulte la [referencia del archivo de configuración de NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="a05bf-113">For allowable key names, see the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

<span data-ttu-id="a05bf-114">En NuGet 3.4 o superior, `<value>` puede usar [variables de entorno](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="a05bf-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="a05bf-115">Opciones</span><span class="sxs-lookup"><span data-stu-id="a05bf-115">Options</span></span>

| <span data-ttu-id="a05bf-116">Opción</span><span class="sxs-lookup"><span data-stu-id="a05bf-116">Option</span></span> | <span data-ttu-id="a05bf-117">Descripción</span><span class="sxs-lookup"><span data-stu-id="a05bf-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a05bf-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="a05bf-118">AsPath</span></span> | <span data-ttu-id="a05bf-119">Devuelve el valor de la configuración como una ruta de acceso, se omite cuando `-Set` se utiliza.</span><span class="sxs-lookup"><span data-stu-id="a05bf-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="a05bf-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a05bf-120">ConfigFile</span></span> | <span data-ttu-id="a05bf-121">El archivo de configuración de NuGet para modificar.</span><span class="sxs-lookup"><span data-stu-id="a05bf-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="a05bf-122">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="a05bf-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a05bf-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a05bf-123">ForceEnglishOutput</span></span> | <span data-ttu-id="a05bf-124">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="a05bf-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a05bf-125">Ayuda</span><span class="sxs-lookup"><span data-stu-id="a05bf-125">Help</span></span> | <span data-ttu-id="a05bf-126">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="a05bf-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="a05bf-127">No interactivo</span><span class="sxs-lookup"><span data-stu-id="a05bf-127">NonInteractive</span></span> | <span data-ttu-id="a05bf-128">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="a05bf-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a05bf-129">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="a05bf-129">Verbosity</span></span> | <span data-ttu-id="a05bf-130">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="a05bf-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a05bf-131">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a05bf-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="a05bf-132">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a05bf-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
