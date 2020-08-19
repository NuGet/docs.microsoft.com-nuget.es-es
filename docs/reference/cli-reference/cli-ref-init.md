---
title: Comando init de la CLI de NuGet
description: Referencia del comando nuget.exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623089"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="992c8-103">comando init (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="992c8-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="992c8-104">**Se aplica a:** versiones compatibles de creación de paquetes &bullet; **:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="992c8-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="992c8-105">Copia todos los paquetes de una carpeta plana en una carpeta de destino mediante un diseño jerárquico, tal como se describe en el [comando agregar](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="992c8-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="992c8-106">Es decir, el uso de `init` es equivalente al uso del `add` comando en cada paquete de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="992c8-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="992c8-107">Al igual que con `add` , el destino debe ser una carpeta local o una ruta de acceso UNC; No se admiten repositorios de paquetes HTTP, como nuget.org o servidores privados.</span><span class="sxs-lookup"><span data-stu-id="992c8-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="992c8-108">Uso</span><span class="sxs-lookup"><span data-stu-id="992c8-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="992c8-109">donde `<source>` es la carpeta que contiene los paquetes y `<destination>` es la carpeta local o el directorio UNC en el que se copian los paquetes.</span><span class="sxs-lookup"><span data-stu-id="992c8-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="992c8-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="992c8-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="992c8-111">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="992c8-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="992c8-112">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="992c8-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="992c8-113">Agrega todos los archivos de cada paquete que se agregan al origen del paquete. igual que `-Expand` con el `add` comando.</span><span class="sxs-lookup"><span data-stu-id="992c8-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="992c8-114">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="992c8-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="992c8-115">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="992c8-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="992c8-116">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="992c8-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="992c8-117">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="992c8-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="992c8-118">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="992c8-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="992c8-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="992c8-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
