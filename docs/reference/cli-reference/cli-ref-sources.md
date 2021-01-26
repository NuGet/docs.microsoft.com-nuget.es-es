---
title: Comando orígenes de la CLI de NuGet
description: Referencia del comando nuget.exe sources
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780006"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="857cd-103">sources (comando) (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="857cd-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="857cd-104">**Se aplica a: consumo de** paquetes, publicación de &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="857cd-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="857cd-105">Administra la lista de orígenes que se encuentran en el archivo de configuración de ámbito de usuario o en un archivo de configuración especificado.</span><span class="sxs-lookup"><span data-stu-id="857cd-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="857cd-106">El archivo de configuración de ámbito de usuario se encuentra en `%appdata%\NuGet\NuGet.Config` (Windows) y `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="857cd-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="857cd-107">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="857cd-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="857cd-108">Uso</span><span class="sxs-lookup"><span data-stu-id="857cd-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="857cd-109">donde `<operation>` es una de las *listas, agregar, quitar, habilitar, deshabilitar* o *Actualizar*, `<name>` es el nombre del origen y `<source>` es la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="857cd-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="857cd-110">Solo puede trabajar con un origen cada vez.</span><span class="sxs-lookup"><span data-stu-id="857cd-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="857cd-111">Opciones</span><span class="sxs-lookup"><span data-stu-id="857cd-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="857cd-112">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="857cd-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="857cd-113">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="857cd-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="857cd-114">*(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="857cd-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="857cd-115">Se aplica a la `list` acción y puede ser `Detailed` (valor predeterminado) o `Short` .</span><span class="sxs-lookup"><span data-stu-id="857cd-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="857cd-116">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="857cd-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="857cd-117">Nombre del origen.</span><span class="sxs-lookup"><span data-stu-id="857cd-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="857cd-118">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="857cd-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="857cd-119">Especifica la contraseña para autenticarse con el origen.</span><span class="sxs-lookup"><span data-stu-id="857cd-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="857cd-120">Ruta de acceso al origen de los paquetes.</span><span class="sxs-lookup"><span data-stu-id="857cd-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="857cd-121">Indica que se almacene la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenar un formulario cifrado.</span><span class="sxs-lookup"><span data-stu-id="857cd-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="857cd-122">Especifica el nombre de usuario para la autenticación con el origen.</span><span class="sxs-lookup"><span data-stu-id="857cd-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="857cd-123">Lista separada por comas de tipos de autenticación válidos para este origen.</span><span class="sxs-lookup"><span data-stu-id="857cd-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="857cd-124">De forma predeterminada, todos los tipos de autenticación son válidos.</span><span class="sxs-lookup"><span data-stu-id="857cd-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="857cd-125">Ejemplo: `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="857cd-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="857cd-126">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="857cd-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="857cd-127">Asegúrese de agregar la contraseña de los orígenes en el mismo contexto de usuario que el nuget.exe se usa posteriormente para tener acceso al origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="857cd-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="857cd-128">La contraseña se almacenará cifrada en el archivo de configuración y solo se puede descifrar en el mismo contexto de usuario que estaba cifrada.</span><span class="sxs-lookup"><span data-stu-id="857cd-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="857cd-129">Por ejemplo, si usa un servidor de compilación para restaurar paquetes de NuGet, la contraseña debe cifrarse con el mismo usuario de Windows con el que se ejecutará la tarea del servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="857cd-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="857cd-130">Vea también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="857cd-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="857cd-131">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="857cd-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
