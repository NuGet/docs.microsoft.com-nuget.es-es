---
title: Comando de orígenes de la CLI de NuGet
description: Comando de orígenes de referencia de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548113"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="03c3f-103">Comando sources (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="03c3f-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="03c3f-104">**Se aplica a:** consumo de paquetes, publicar &bullet; **versiones compatibles:** todas</span><span class="sxs-lookup"><span data-stu-id="03c3f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="03c3f-105">Administra la lista de orígenes que se encuentra en el archivo de configuración de ámbito de usuario o un archivo de configuración especificado.</span><span class="sxs-lookup"><span data-stu-id="03c3f-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="03c3f-106">El archivo de configuración de ámbito de usuario se encuentra en `%appdata%\NuGet\NuGet.Config` (Windows) y `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="03c3f-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="03c3f-107">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="03c3f-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="03c3f-108">Uso</span><span class="sxs-lookup"><span data-stu-id="03c3f-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="03c3f-109">donde `<operation>` es uno de *enumerar, agregar, quitar, habilitar, deshabilitar* o *actualización*, `<name>` es el nombre del origen, y `<source>` es la dirección URL de origen.</span><span class="sxs-lookup"><span data-stu-id="03c3f-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="03c3f-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="03c3f-110">Options</span></span>

| <span data-ttu-id="03c3f-111">Opción</span><span class="sxs-lookup"><span data-stu-id="03c3f-111">Option</span></span> | <span data-ttu-id="03c3f-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="03c3f-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="03c3f-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="03c3f-113">ConfigFile</span></span> | <span data-ttu-id="03c3f-114">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="03c3f-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="03c3f-115">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="03c3f-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="03c3f-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="03c3f-116">ForceEnglishOutput</span></span> | <span data-ttu-id="03c3f-117">*(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="03c3f-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="03c3f-118">Formato</span><span class="sxs-lookup"><span data-stu-id="03c3f-118">Format</span></span> | <span data-ttu-id="03c3f-119">Se aplica a la `list` acción y puede ser `Detailed` (valor predeterminado) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="03c3f-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="03c3f-120">Ayuda</span><span class="sxs-lookup"><span data-stu-id="03c3f-120">Help</span></span> | <span data-ttu-id="03c3f-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="03c3f-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="03c3f-122">No interactivo</span><span class="sxs-lookup"><span data-stu-id="03c3f-122">NonInteractive</span></span> | <span data-ttu-id="03c3f-123">Suprime los mensajes para confirmaciones o intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="03c3f-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="03c3f-124">Contraseña</span><span class="sxs-lookup"><span data-stu-id="03c3f-124">Password</span></span> | <span data-ttu-id="03c3f-125">Especifica la contraseña para autenticarse con el origen.</span><span class="sxs-lookup"><span data-stu-id="03c3f-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="03c3f-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="03c3f-126">StorePasswordInClearText</span></span> | <span data-ttu-id="03c3f-127">Indica que se almacene la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenamiento de forma cifrada.</span><span class="sxs-lookup"><span data-stu-id="03c3f-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="03c3f-128">UserName</span><span class="sxs-lookup"><span data-stu-id="03c3f-128">UserName</span></span> | <span data-ttu-id="03c3f-129">Especifica el nombre de usuario para autenticar con el origen.</span><span class="sxs-lookup"><span data-stu-id="03c3f-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="03c3f-130">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="03c3f-130">Verbosity</span></span> | <span data-ttu-id="03c3f-131">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="03c3f-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="03c3f-132">No olvide agregar la contraseña de la de los orígenes en el mismo contexto de usuario como nuget.exe se utiliza posteriormente para tener acceso al origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="03c3f-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="03c3f-133">La contraseña se almacenan cifradas en el archivo de configuración y sólo puede descifrar en el mismo contexto de usuario cuando se cifró.</span><span class="sxs-lookup"><span data-stu-id="03c3f-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="03c3f-134">Por ejemplo al utilizar un servidor de compilación para restaurar los paquetes de NuGet que se debe cifrar la contraseña con el mismo usuario de Windows bajo la que se ejecutará la tarea de servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="03c3f-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="03c3f-135">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="03c3f-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="03c3f-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="03c3f-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
