---
title: Comando orígenes de la CLI de NuGet
description: Referencia del comando de orígenes de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327602"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="da3e3-103">Comando sources (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="da3e3-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="da3e3-104">**Se aplica a: consumo de** paquetes &bullet; , publicación de **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="da3e3-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="da3e3-105">Administra la lista de orígenes que se encuentran en el archivo de configuración de ámbito de usuario o en un archivo de configuración especificado.</span><span class="sxs-lookup"><span data-stu-id="da3e3-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="da3e3-106">El archivo de configuración de ámbito de usuario `%appdata%\NuGet\NuGet.Config` se encuentra en ( `~/.nuget/NuGet/NuGet.Config` Windows) y (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="da3e3-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="da3e3-107">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="da3e3-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="da3e3-108">Uso</span><span class="sxs-lookup"><span data-stu-id="da3e3-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="da3e3-109">donde `<operation>` es una de las *listas, agregar, quitar, habilitar, deshabilitar* o *Actualizar*, `<name>` es el nombre del origen y `<source>` es la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="da3e3-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="da3e3-110">Solo puede trabajar con un origen cada vez.</span><span class="sxs-lookup"><span data-stu-id="da3e3-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="da3e3-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="da3e3-111">Options</span></span>

| <span data-ttu-id="da3e3-112">Opción</span><span class="sxs-lookup"><span data-stu-id="da3e3-112">Option</span></span> | <span data-ttu-id="da3e3-113">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="da3e3-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da3e3-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="da3e3-114">ConfigFile</span></span> | <span data-ttu-id="da3e3-115">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="da3e3-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="da3e3-116">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="da3e3-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="da3e3-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="da3e3-117">ForceEnglishOutput</span></span> | <span data-ttu-id="da3e3-118">*(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="da3e3-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="da3e3-119">Formato</span><span class="sxs-lookup"><span data-stu-id="da3e3-119">Format</span></span> | <span data-ttu-id="da3e3-120">Se aplica a `list` la acción y puede `Detailed` ser (valor predeterminado) `Short`o.</span><span class="sxs-lookup"><span data-stu-id="da3e3-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="da3e3-121">Help</span><span class="sxs-lookup"><span data-stu-id="da3e3-121">Help</span></span> | <span data-ttu-id="da3e3-122">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="da3e3-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="da3e3-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="da3e3-123">NonInteractive</span></span> | <span data-ttu-id="da3e3-124">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="da3e3-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="da3e3-125">Contraseña</span><span class="sxs-lookup"><span data-stu-id="da3e3-125">Password</span></span> | <span data-ttu-id="da3e3-126">Especifica la contraseña para autenticarse con el origen.</span><span class="sxs-lookup"><span data-stu-id="da3e3-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="da3e3-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="da3e3-127">StorePasswordInClearText</span></span> | <span data-ttu-id="da3e3-128">Indica que se almacene la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenar un formulario cifrado.</span><span class="sxs-lookup"><span data-stu-id="da3e3-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="da3e3-129">UserName</span><span class="sxs-lookup"><span data-stu-id="da3e3-129">UserName</span></span> | <span data-ttu-id="da3e3-130">Especifica el nombre de usuario para la autenticación con el origen.</span><span class="sxs-lookup"><span data-stu-id="da3e3-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="da3e3-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="da3e3-131">Verbosity</span></span> | <span data-ttu-id="da3e3-132">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="da3e3-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="da3e3-133">Asegúrese de agregar la contraseña de orígenes en el mismo contexto de usuario que el archivo Nuget. exe se usa más adelante para obtener acceso al origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="da3e3-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="da3e3-134">La contraseña se almacenará cifrada en el archivo de configuración y solo se puede descifrar en el mismo contexto de usuario que estaba cifrada.</span><span class="sxs-lookup"><span data-stu-id="da3e3-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="da3e3-135">Por ejemplo, si usa un servidor de compilación para restaurar paquetes de NuGet, la contraseña debe cifrarse con el mismo usuario de Windows con el que se ejecutará la tarea del servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="da3e3-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="da3e3-136">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="da3e3-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="da3e3-137">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="da3e3-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
