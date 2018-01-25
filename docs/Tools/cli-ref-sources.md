---
title: "NuGet CLI orígenes comando | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referencia para el nuget.exe orígenes de comando"
keywords: "NuGet orígenes de referencia, orígenes de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c1cd909c0c35d52f0269d267367669df46f9db55
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="921f1-104">comando de fuentes (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="921f1-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="921f1-105">**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="921f1-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="921f1-106">Administra la lista de orígenes que se encuentran en `%AppData%\NuGet\NuGet.Config` o en el archivo de configuración especificado.</span><span class="sxs-lookup"><span data-stu-id="921f1-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="921f1-107">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="921f1-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="921f1-108">Uso</span><span class="sxs-lookup"><span data-stu-id="921f1-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="921f1-109">donde `<operation>` es uno de los *enumerar, agregar, quitar, habilitar, deshabilitar,* o *actualización*, `<name>` es el nombre del origen, y `<source>` es la dirección URL de la fuente.</span><span class="sxs-lookup"><span data-stu-id="921f1-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="921f1-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="921f1-110">Options</span></span>

| <span data-ttu-id="921f1-111">Opción</span><span class="sxs-lookup"><span data-stu-id="921f1-111">Option</span></span> | <span data-ttu-id="921f1-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="921f1-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="921f1-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="921f1-113">ConfigFile</span></span> | <span data-ttu-id="921f1-114">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="921f1-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="921f1-115">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="921f1-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="921f1-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="921f1-116">ForceEnglishOutput</span></span> | <span data-ttu-id="921f1-117">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="921f1-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="921f1-118">Formato</span><span class="sxs-lookup"><span data-stu-id="921f1-118">Format</span></span> | <span data-ttu-id="921f1-119">Se aplica a la `list` acción y puede ser `Detailed` (valor predeterminado) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="921f1-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="921f1-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="921f1-120">Help</span></span> | <span data-ttu-id="921f1-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="921f1-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="921f1-122">No interactivo</span><span class="sxs-lookup"><span data-stu-id="921f1-122">NonInteractive</span></span> | <span data-ttu-id="921f1-123">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="921f1-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="921f1-124">Contraseña</span><span class="sxs-lookup"><span data-stu-id="921f1-124">Password</span></span> | <span data-ttu-id="921f1-125">Especifica la contraseña para autenticarse con el origen.</span><span class="sxs-lookup"><span data-stu-id="921f1-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="921f1-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="921f1-126">StorePasswordInClearText</span></span> | <span data-ttu-id="921f1-127">Indica que se guarde la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenar de forma cifrada.</span><span class="sxs-lookup"><span data-stu-id="921f1-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="921f1-128">UserName</span><span class="sxs-lookup"><span data-stu-id="921f1-128">UserName</span></span> | <span data-ttu-id="921f1-129">Especifica el nombre de usuario para la autenticación con el origen.</span><span class="sxs-lookup"><span data-stu-id="921f1-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="921f1-130">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="921f1-130">Verbosity</span></span> | <span data-ttu-id="921f1-131">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="921f1-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="921f1-132">Asegúrese de agregar la contraseña de los orígenes en el mismo contexto de usuario como el nuget.exe se utiliza posteriormente para tener acceso al origen de paquete.</span><span class="sxs-lookup"><span data-stu-id="921f1-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="921f1-133">La contraseña se almacenarán cifrados en el archivo de configuración y sólo se puede descifrar en el mismo contexto de usuario tal y como se cifró.</span><span class="sxs-lookup"><span data-stu-id="921f1-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="921f1-134">Así, por ejemplo cuando usa un servidor de compilación para restaurar los paquetes de NuGet que se debe cifrar la contraseña con el mismo usuario de Windows en la que se ejecutará la tarea de servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="921f1-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="921f1-135">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="921f1-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="921f1-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="921f1-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
