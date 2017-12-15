---
title: "NuGet CLI orígenes comando | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Referencia para el nuget.exe orígenes de comando"
keywords: "NuGet orígenes de referencia, orígenes de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="c60a4-104">comando de fuentes (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c60a4-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="c60a4-105">**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="c60a4-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c60a4-106">Administra la lista de orígenes que se encuentran en `%AppData%\NuGet\NuGet.Config` o en el archivo de configuración especificado.</span><span class="sxs-lookup"><span data-stu-id="c60a4-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

## <a name="usage"></a><span data-ttu-id="c60a4-107">Uso</span><span class="sxs-lookup"><span data-stu-id="c60a4-107">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="c60a4-108">donde `<operation>` es uno de los *enumerar, agregar, quitar, habilitar, deshabilitar,* o *actualización*, `<name>` es el nombre del origen, y `<source>` es la dirección URL de la fuente.</span><span class="sxs-lookup"><span data-stu-id="c60a4-108">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>


## <a name="options"></a><span data-ttu-id="c60a4-109">Opciones</span><span class="sxs-lookup"><span data-stu-id="c60a4-109">Options</span></span>

| <span data-ttu-id="c60a4-110">Opción</span><span class="sxs-lookup"><span data-stu-id="c60a4-110">Option</span></span> | <span data-ttu-id="c60a4-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="c60a4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c60a4-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c60a4-112">ConfigFile</span></span> | <span data-ttu-id="c60a4-113">*(2.5 +)*  NuGet el archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="c60a4-113">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="c60a4-114">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="c60a4-114">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="c60a4-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c60a4-115">ForceEnglishOutput</span></span> | <span data-ttu-id="c60a4-116">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="c60a4-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c60a4-117">Formato</span><span class="sxs-lookup"><span data-stu-id="c60a4-117">Format</span></span> | <span data-ttu-id="c60a4-118">Se aplica a la `list` acción y puede ser `Detailed` (valor predeterminado) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="c60a4-118">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="c60a4-119">Ayuda</span><span class="sxs-lookup"><span data-stu-id="c60a4-119">Help</span></span> | <span data-ttu-id="c60a4-120">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="c60a4-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="c60a4-121">No interactivo</span><span class="sxs-lookup"><span data-stu-id="c60a4-121">NonInteractive</span></span> | <span data-ttu-id="c60a4-122">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="c60a4-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c60a4-123">Contraseña</span><span class="sxs-lookup"><span data-stu-id="c60a4-123">Password</span></span> | <span data-ttu-id="c60a4-124">Especifica la contraseña para autenticarse con el origen.</span><span class="sxs-lookup"><span data-stu-id="c60a4-124">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="c60a4-125">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="c60a4-125">StorePasswordInClearText</span></span> | <span data-ttu-id="c60a4-126">Indica que se guarde la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenar de forma cifrada.</span><span class="sxs-lookup"><span data-stu-id="c60a4-126">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="c60a4-127">UserName</span><span class="sxs-lookup"><span data-stu-id="c60a4-127">UserName</span></span> | <span data-ttu-id="c60a4-128">Especifica el nombre de usuario para la autenticación con el origen.</span><span class="sxs-lookup"><span data-stu-id="c60a4-128">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="c60a4-129">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="c60a4-129">Verbosity</span></span> | <span data-ttu-id="c60a4-130">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="c60a4-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="c60a4-131">Asegúrese de agregar la contraseña de los orígenes en el mismo contexto de usuario como el nuget.exe se utiliza posteriormente para tener acceso al origen de paquete.</span><span class="sxs-lookup"><span data-stu-id="c60a4-131">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="c60a4-132">La contraseña se almacenarán cifrados en el archivo de configuración y sólo se puede descifrar en el mismo contexto de usuario tal y como se cifró.</span><span class="sxs-lookup"><span data-stu-id="c60a4-132">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="c60a4-133">Así, por ejemplo cuando usa un servidor de compilación para restaurar los paquetes de NuGet que se debe cifrar la contraseña con el mismo usuario de Windows en la que se ejecutará la tarea de servidor de compilación.</span><span class="sxs-lookup"><span data-stu-id="c60a4-133">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="c60a4-134">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c60a4-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c60a4-135">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c60a4-135">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
