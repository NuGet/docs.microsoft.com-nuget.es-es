---
title: Comando de NuGet CLI delete | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia para el comando de eliminación nuget.exe
keywords: NuGet eliminar referencia, eliminar comando paquete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9445042c46ef41721def1fbbb8dcebf4afc14d1b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="3ef00-104">Eliminar comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3ef00-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="3ef00-105">**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="3ef00-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3ef00-106">Elimina o unlists un paquete desde un origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="3ef00-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="3ef00-107">Para nuget.org, el comando delete [unlists el paquete](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="3ef00-107">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="3ef00-108">Uso</span><span class="sxs-lookup"><span data-stu-id="3ef00-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="3ef00-109">donde `<packageID>` y `<packageVersion>` identificar el paquete exacto para eliminar u ocultar.</span><span class="sxs-lookup"><span data-stu-id="3ef00-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="3ef00-110">El comportamiento exacto depende del origen.</span><span class="sxs-lookup"><span data-stu-id="3ef00-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="3ef00-111">Para las carpetas locales, por ejemplo, se elimina el paquete; para nuget.org es que no figuran en el paquete.</span><span class="sxs-lookup"><span data-stu-id="3ef00-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="3ef00-112">Opciones</span><span class="sxs-lookup"><span data-stu-id="3ef00-112">Options</span></span>

| <span data-ttu-id="3ef00-113">Opción</span><span class="sxs-lookup"><span data-stu-id="3ef00-113">Option</span></span> | <span data-ttu-id="3ef00-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="3ef00-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3ef00-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="3ef00-115">ApiKey</span></span> | <span data-ttu-id="3ef00-116">La clave de API para el repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="3ef00-116">The API key for the target repository.</span></span> <span data-ttu-id="3ef00-117">Si no está presente, se utiliza el especificado en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="3ef00-117">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="3ef00-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3ef00-118">ConfigFile</span></span> | <span data-ttu-id="3ef00-119">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="3ef00-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3ef00-120">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="3ef00-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3ef00-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3ef00-121">ForceEnglishOutput</span></span> | <span data-ttu-id="3ef00-122">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="3ef00-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3ef00-123">Ayuda</span><span class="sxs-lookup"><span data-stu-id="3ef00-123">Help</span></span> | <span data-ttu-id="3ef00-124">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="3ef00-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="3ef00-125">No interactivo</span><span class="sxs-lookup"><span data-stu-id="3ef00-125">NonInteractive</span></span> | <span data-ttu-id="3ef00-126">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="3ef00-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3ef00-127">Origen</span><span class="sxs-lookup"><span data-stu-id="3ef00-127">Source</span></span> | <span data-ttu-id="3ef00-128">Especifica la dirección URL del servidor.</span><span class="sxs-lookup"><span data-stu-id="3ef00-128">Specifies the server URL.</span></span> <span data-ttu-id="3ef00-129">La dirección URL de nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="3ef00-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="3ef00-130">Para las fuentes privadas, sustituya el nombre de host, por ejemplo, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="3ef00-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="3ef00-131">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="3ef00-131">Verbosity</span></span> | <span data-ttu-id="3ef00-132">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="3ef00-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3ef00-133">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3ef00-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3ef00-134">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="3ef00-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
