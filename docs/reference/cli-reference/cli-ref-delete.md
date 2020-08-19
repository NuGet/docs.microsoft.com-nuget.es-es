---
title: Comando DELETE de la CLI de NuGet
description: Referencia del comando nuget.exe Delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622868"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="33d61-103">comando DELETE (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="33d61-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="33d61-104">**Se aplica a:** versiones compatibles de publicación de paquetes &bullet; **:** todos</span><span class="sxs-lookup"><span data-stu-id="33d61-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="33d61-105">Elimina o quita de la lista un paquete del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="33d61-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="33d61-106">En el caso de nuget.org, el comando DELETE elimina [el paquete](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="33d61-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="33d61-107">Uso</span><span class="sxs-lookup"><span data-stu-id="33d61-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="33d61-108">Dónde `<packageID>` e `<packageVersion>` identifican el paquete exacto que se va a eliminar o quitar de la lista.</span><span class="sxs-lookup"><span data-stu-id="33d61-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="33d61-109">El comportamiento exacto depende del origen.</span><span class="sxs-lookup"><span data-stu-id="33d61-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="33d61-110">En el caso de las carpetas locales, por ejemplo, se elimina el paquete. para nuget.org, el paquete no está en la lista.</span><span class="sxs-lookup"><span data-stu-id="33d61-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="33d61-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="33d61-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="33d61-112">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="33d61-112">The API key for the target repository.</span></span> <span data-ttu-id="33d61-113">Si no está presente, se utiliza el especificado en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="33d61-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="33d61-114">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="33d61-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="33d61-115">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="33d61-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="33d61-116">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="33d61-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="33d61-117">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="33d61-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="33d61-118">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="33d61-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="33d61-119">No preguntar al eliminar.</span><span class="sxs-lookup"><span data-stu-id="33d61-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="33d61-120">**`-NoServiceEndpoint`** No anexa "API/V2/packages" a la dirección URL de origen.</span><span class="sxs-lookup"><span data-stu-id="33d61-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="33d61-121">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="33d61-121">Specifies the server URL.</span></span> <span data-ttu-id="33d61-122">La dirección URL de nuget.org es `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="33d61-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="33d61-123">En el caso de las fuentes privadas, sustituya el nombre de host, por ejemplo, *% hostname%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="33d61-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="33d61-124">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="33d61-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="33d61-125">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="33d61-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="33d61-126">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="33d61-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
