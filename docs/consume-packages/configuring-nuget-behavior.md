---
title: Configuraciones comunes de NuGet
description: Los archivos NuGet.Config controlan el comportamiento de NuGet, tanto global como por proyecto, y se modifican con el comando nuget config.
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 35339626b0a20ccfceafa89fef94fb3187013fd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774862"
---
# <a name="common-nuget-configurations"></a><span data-ttu-id="e9c53-103">Configuraciones comunes de NuGet</span><span class="sxs-lookup"><span data-stu-id="e9c53-103">Common NuGet configurations</span></span>

<span data-ttu-id="e9c53-104">El comportamiento de NuGet se controla mediante la configuración acumulada en uno o varios archivos `NuGet.Config` (XML) que pueden existir en los niveles del proyecto, usuario y todo el equipo.</span><span class="sxs-lookup"><span data-stu-id="e9c53-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="e9c53-105">Un archivo `NuGetDefaults.Config` global configura también los orígenes de paquetes de forma específica.</span><span class="sxs-lookup"><span data-stu-id="e9c53-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="e9c53-106">La configuración se aplica a todos los comandos emitidos en la CLI, la consola del Administrador de paquetes y la interfaz de usuario del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e9c53-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="e9c53-107">Usos y ubicaciones de los archivos de configuración</span><span class="sxs-lookup"><span data-stu-id="e9c53-107">Config file locations and uses</span></span>

| <span data-ttu-id="e9c53-108">Ámbito</span><span class="sxs-lookup"><span data-stu-id="e9c53-108">Scope</span></span> | <span data-ttu-id="e9c53-109">Ubicación del archivo NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="e9c53-109">NuGet.Config file location</span></span> | <span data-ttu-id="e9c53-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="e9c53-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e9c53-111">Soluciones</span><span class="sxs-lookup"><span data-stu-id="e9c53-111">Solution</span></span> | <span data-ttu-id="e9c53-112">Carpeta actual (también denominada carpeta de soluciones) o cualquier carpeta hasta la raíz de la unidad.</span><span class="sxs-lookup"><span data-stu-id="e9c53-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="e9c53-113">En una carpeta de soluciones, la configuración se aplica a todos los proyectos de las subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="e9c53-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="e9c53-114">Tenga en cuenta que si se coloca un archivo de configuración en una carpeta de proyecto, no tiene ningún efecto en ese proyecto.</span><span class="sxs-lookup"><span data-stu-id="e9c53-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="e9c53-115">Usuario</span><span class="sxs-lookup"><span data-stu-id="e9c53-115">User</span></span> | <span data-ttu-id="e9c53-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="e9c53-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="e9c53-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` o `~/.nuget/NuGet/NuGet.Config` (varía según la distribución del SO)</span><span class="sxs-lookup"><span data-stu-id="e9c53-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> <br/><span data-ttu-id="e9c53-118">Se admiten configuraciones adicionales en todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="e9c53-118">Additional configs are supported on all platforms.</span></span> <span data-ttu-id="e9c53-119">Estas configuraciones no se pueden editar con las herramientas.</span><span class="sxs-lookup"><span data-stu-id="e9c53-119">These configs cannot be edited by the tooling.</span></span> </br> <span data-ttu-id="e9c53-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span><span class="sxs-lookup"><span data-stu-id="e9c53-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span></span> <br/><span data-ttu-id="e9c53-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` o `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="e9c53-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> | <span data-ttu-id="e9c53-122">La configuración se aplica a todas las operaciones, pero se reemplaza por la configuración de nivel de proyecto.</span><span class="sxs-lookup"><span data-stu-id="e9c53-122">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="e9c53-123">Computer</span><span class="sxs-lookup"><span data-stu-id="e9c53-123">Computer</span></span> | <span data-ttu-id="e9c53-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="e9c53-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="e9c53-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="e9c53-126">Si `$XDG_DATA_HOME` es null o está vacío, se usará `~/.local/share` o `/usr/local/share` (varía según la distribución del SO)</span><span class="sxs-lookup"><span data-stu-id="e9c53-126">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="e9c53-127">La configuración se aplica a todas las operaciones en el equipo, pero se reemplaza por cualquier configuración de nivel de proyecto o de usuario.</span><span class="sxs-lookup"><span data-stu-id="e9c53-127">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="e9c53-128">Notas para versiones anteriores de NuGet:</span><span class="sxs-lookup"><span data-stu-id="e9c53-128">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="e9c53-129">En NuGet 3.3 y versiones anteriores se usaba una carpeta `.nuget` para la configuración de toda la solución.</span><span class="sxs-lookup"><span data-stu-id="e9c53-129">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="e9c53-130">Esta carpeta no se usa en NuGet 3.4 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="e9c53-130">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="e9c53-131">Para NuGet 2.6 a 3.x, el archivo de configuración de nivel de equipo en Windows se encontraba en %ProgramData%\NuGet\Config[\\{IDE}[\\{Versión}[\\{SKU}]]]\NuGet.Config, donde *{IDE}* podía ser *VisualStudio*, *{Versión}* era la versión de Visual Studio como *14.0* y *{SKU}* era *Community*, *Pro* o *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="e9c53-131">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="e9c53-132">Para migrar la configuración a NuGet 4.0 y versiones posteriores, simplemente copie el archivo de configuración a %ProgramFiles(x86)%\NuGet\Config. Esta ubicación anterior era /etc/opt, en Linux, y /Biblioteca/Application Support, en Mac.</span><span class="sxs-lookup"><span data-stu-id="e9c53-132">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="e9c53-133">Cambiar los valores de configuración</span><span class="sxs-lookup"><span data-stu-id="e9c53-133">Changing config settings</span></span>

<span data-ttu-id="e9c53-134">Un archivo `NuGet.Config` es un archivo de texto XML simple que contiene pares de clave y valor como se describe en el tema [Opciones de configuración de NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="e9c53-134">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="e9c53-135">La configuración se administra mediante el [comando config](../reference/cli-reference/cli-ref-config.md) de la CLI de NuGet:</span><span class="sxs-lookup"><span data-stu-id="e9c53-135">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="e9c53-136">De forma predeterminada, los cambios se realizan en el archivo de configuración de nivel de usuario.</span><span class="sxs-lookup"><span data-stu-id="e9c53-136">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="e9c53-137">Para cambiar la configuración en un archivo diferente, use el modificador `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-137">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="e9c53-138">En este caso, se puede usar cualquier nombre de archivo en los archivos.</span><span class="sxs-lookup"><span data-stu-id="e9c53-138">In this case files can use any filename.</span></span>
- <span data-ttu-id="e9c53-139">Las claves siempre distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e9c53-139">Keys are always case sensitive.</span></span>
- <span data-ttu-id="e9c53-140">Es necesaria la elevación para cambiar la configuración en el archivo de configuración de nivel de equipo.</span><span class="sxs-lookup"><span data-stu-id="e9c53-140">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="e9c53-141">Aunque puede modificar el archivo en cualquier editor de texto, NuGet (v3.4.3 y versiones posteriores) ignora automáticamente el archivo de configuración completo si contiene código XML con formato incorrecto (etiquetas que no coinciden, comillas no válidas, etc.)</span><span class="sxs-lookup"><span data-stu-id="e9c53-141">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="e9c53-142">Por este motivo se prefiere administrar la configuración mediante `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-142">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="e9c53-143">Establecer un valor</span><span class="sxs-lookup"><span data-stu-id="e9c53-143">Setting a value</span></span>

<span data-ttu-id="e9c53-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="e9c53-144">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="e9c53-145">Mac o Linux:</span><span class="sxs-lookup"><span data-stu-id="e9c53-145">Mac/Linux:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="e9c53-146">En NuGet 3.4 y versiones posteriores puede usar variables de entorno en cualquier valor, como en `repositoryPath=%PACKAGEHOME%` (Windows) y `repositoryPath=$PACKAGEHOME` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="e9c53-146">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="e9c53-147">Quitar un valor</span><span class="sxs-lookup"><span data-stu-id="e9c53-147">Removing a value</span></span>

<span data-ttu-id="e9c53-148">Para quitar un valor, especifique una clave con un valor vacío.</span><span class="sxs-lookup"><span data-stu-id="e9c53-148">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="e9c53-149">Creación de un archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="e9c53-149">Creating a new config file</span></span>

<span data-ttu-id="e9c53-150">Copie la plantilla siguiente en el archivo nuevo y, después, use `nuget config -configFile <filename>` para establecer los valores:</span><span class="sxs-lookup"><span data-stu-id="e9c53-150">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="e9c53-151">Cómo se aplica la configuración</span><span class="sxs-lookup"><span data-stu-id="e9c53-151">How settings are applied</span></span>

<span data-ttu-id="e9c53-152">Varios archivos `NuGet.Config` permiten almacenar la configuración en ubicaciones diferentes para que se aplique a un único proyecto, a un grupo de proyectos o a todos los proyectos.</span><span class="sxs-lookup"><span data-stu-id="e9c53-152">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="e9c53-153">Colectivamente, esta configuración se aplica a cualquier operación de NuGet que se invoca desde la línea de comandos o desde Visual Studio, y tiene prioridad la configuración que existe "más cerca" de un proyecto o la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="e9c53-153">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="e9c53-154">En concreto, NuGet carga la configuración desde los diferentes archivos de configuración en el orden siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9c53-154">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="e9c53-155">El [archivo NuGetDefaults.Config](#nuget-defaults-file), que contiene los valores relacionados solamente con orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e9c53-155">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="e9c53-156">El archivo de nivel de equipo.</span><span class="sxs-lookup"><span data-stu-id="e9c53-156">The computer-level file.</span></span>
1. <span data-ttu-id="e9c53-157">El archivo de nivel de usuario.</span><span class="sxs-lookup"><span data-stu-id="e9c53-157">The user-level file.</span></span>
1. <span data-ttu-id="e9c53-158">El archivo especificado con `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-158">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="e9c53-159">Los archivos que se encuentran en todas las carpetas en la ruta de acceso desde la raíz de la unidad a la carpeta actual (donde se invoca nuget.exe o la carpeta que contiene el proyecto de Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="e9c53-159">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="e9c53-160">Por ejemplo, si se invoca un comando en c:\A\B\C, NuGet busca y carga los archivos de configuración en c:\,, después c:\A, después c:\A\B y, por último, c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="e9c53-160">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="e9c53-161">Cuando NuGet encuentra la configuración en estos archivos, se aplica como sigue:</span><span class="sxs-lookup"><span data-stu-id="e9c53-161">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="e9c53-162">Para elementos de un solo elemento, NuGet reemplaza cualquier valor encontrado anteriormente para la misma clave.</span><span class="sxs-lookup"><span data-stu-id="e9c53-162">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="e9c53-163">Esto significa que la configuración "más cercana" a la carpeta o proyecto actual reemplaza a cualquier otra encontrada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e9c53-163">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="e9c53-164">Por ejemplo, el valor `defaultPushSource` en `NuGetDefaults.Config` se reemplaza si se encuentra en cualquier otro archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="e9c53-164">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="e9c53-165">Para elementos de colección (como `<packageSources>`), NuGet combina los valores de todos los archivos de configuración en una sola colección.</span><span class="sxs-lookup"><span data-stu-id="e9c53-165">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="e9c53-166">Cuando `<clear />` está presente para un nodo determinado, NuGet ignora los valores de configuración definidos previamente para ese nodo.</span><span class="sxs-lookup"><span data-stu-id="e9c53-166">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="e9c53-167">Tutorial de configuración</span><span class="sxs-lookup"><span data-stu-id="e9c53-167">Settings walkthrough</span></span>

<span data-ttu-id="e9c53-168">Supongamos que tiene la siguiente estructura de carpetas en dos unidades independientes:</span><span class="sxs-lookup"><span data-stu-id="e9c53-168">Let's say you have the following folder structure on two separate drives:</span></span>

```
disk_drive_1
    User
disk_drive_2
    Project1
        Source
    Project2
        Source
    tmp
```

<span data-ttu-id="e9c53-169">Tiene cuatro archivos `NuGet.Config` en las ubicaciones siguientes con el contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="e9c53-169">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="e9c53-170">(El archivo de nivel de equipo no está incluido en este ejemplo, pero se comportaría igual que el archivo de nivel de usuario).</span><span class="sxs-lookup"><span data-stu-id="e9c53-170">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="e9c53-171">Archivo A. Archivo de nivel de usuario (`%appdata%\NuGet\NuGet.Config` en Windows, `~/.config/NuGet/NuGet.Config` en Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="e9c53-171">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="e9c53-172">Archivo B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="e9c53-172">File B. disk_drive_2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="e9c53-173">Archivo C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="e9c53-173">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="e9c53-174">Archivo D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="e9c53-174">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="e9c53-175">Después, NuGet carga y aplica la configuración como se indica a continuación, en función de dónde se invoque:</span><span class="sxs-lookup"><span data-stu-id="e9c53-175">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="e9c53-176">**Se invoca desde disk_drive_1/users/**: solo se usa el repositorio predeterminado que aparece en el archivo de configuración de nivel de usuario (A), ya que es el único archivo encontrado en disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="e9c53-176">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="e9c53-177">**Se invoca desde disk_drive_2/ o disk_drive_/tmp**: en primer lugar se carga el archivo de nivel de usuario (A) y después NuGet se desplaza a la raíz de disk_drive_2 y busca el archivo (B).</span><span class="sxs-lookup"><span data-stu-id="e9c53-177">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="e9c53-178">NuGet también busca un archivo de configuración en/tmp pero no lo encuentra.</span><span class="sxs-lookup"><span data-stu-id="e9c53-178">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="e9c53-179">Como resultado, se usa el repositorio predeterminado en nuget.org, se habilita la restauración de paquetes y los paquetes se expanden en disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="e9c53-179">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="e9c53-180">**Se invoca desde disk_drive_2/Project1 o disk_drive_2/Project1/Source**: primero se carga el archivo de nivel de usuario (A), después NuGet carga el archivo (B) desde la raíz de disk_drive_2, seguido del archivo (C).</span><span class="sxs-lookup"><span data-stu-id="e9c53-180">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="e9c53-181">La configuración de (C) invalida la de (B) y (A), por lo que la `repositoryPath` donde se instalan los paquetes es disk_drive_2/Project1/External/Packages en lugar de *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="e9c53-181">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="e9c53-182">Además, dado que borra (C) `<packageSources>`, nuget.org ya no está disponible como un origen, lo que solo deja `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-182">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="e9c53-183">**Se invoca desde disk_drive_2/Project2 o disk_drive_2/Project2/Source**: primero se carga el archivo de nivel de usuario (A), seguido del archivo (B) y el archivo (D).</span><span class="sxs-lookup"><span data-stu-id="e9c53-183">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="e9c53-184">Dado que `packageSources` no se borra, `nuget.org` y `https://MyPrivateRepo/DQ/nuget` están disponibles como orígenes.</span><span class="sxs-lookup"><span data-stu-id="e9c53-184">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="e9c53-185">Los paquetes se expanden en disk_drive_2/tmp, como se especifica en (B).</span><span class="sxs-lookup"><span data-stu-id="e9c53-185">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="additional-user-wide-configuration"></a><span data-ttu-id="e9c53-186">Configuración adicional para todos los usuarios</span><span class="sxs-lookup"><span data-stu-id="e9c53-186">Additional user wide configuration</span></span>

<span data-ttu-id="e9c53-187">A partir de la versión 5.7, NuGet ha agregado compatibilidad con archivos de configuración adicional para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e9c53-187">Starting with 5.7, NuGet has added support for additional user wide configuration files.</span></span> <span data-ttu-id="e9c53-188">Esto permite a los proveedores externos agregar archivos de configuración de usuario adicional sin elevación.</span><span class="sxs-lookup"><span data-stu-id="e9c53-188">This allows third-party vendors to add additional user configuration files without elevation.</span></span>
<span data-ttu-id="e9c53-189">Estos archivos de configuración se encuentran en la carpeta de configuración estándar de todos los usuarios en una subcarpeta `config`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-189">These configuration files are found in the standard user wide configuration folder within a `config` subfolder.</span></span>
<span data-ttu-id="e9c53-190">Se tendrán en cuenta todos los archivos que terminen en `.config` o `.Config`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-190">All files ending with `.config` or `.Config` will be considered.</span></span>
<span data-ttu-id="e9c53-191">Estos archivos no se pueden editar con las herramientas estándar.</span><span class="sxs-lookup"><span data-stu-id="e9c53-191">These files cannot be edited by the standard tooling.</span></span>

| <span data-ttu-id="e9c53-192">Plataforma de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e9c53-192">OS Platform</span></span>  | <span data-ttu-id="e9c53-193">Configuración adicional</span><span class="sxs-lookup"><span data-stu-id="e9c53-193">Additional Configurations</span></span> |
| --- | --- |
| <span data-ttu-id="e9c53-194">Windows</span><span class="sxs-lookup"><span data-stu-id="e9c53-194">Windows</span></span>      | `%appdata%\NuGet\config\*.Config` |
| <span data-ttu-id="e9c53-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="e9c53-195">Mac/Linux</span></span>    | <span data-ttu-id="e9c53-196">`~/.config/NuGet/config/*.config` o `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="e9c53-196">`~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> |

## <a name="nuget-defaults-file"></a><span data-ttu-id="e9c53-197">Archivo de valores predeterminados de NuGet</span><span class="sxs-lookup"><span data-stu-id="e9c53-197">NuGet defaults file</span></span>

<span data-ttu-id="e9c53-198">El archivo `NuGetDefaults.Config` existe para especificar los orígenes de paquete desde los que se instalan y actualizan los paquetes, y para controlar el destino predeterminado para la publicación de paquetes con `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-198">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="e9c53-199">Como los administradores pueden implementar de forma cómoda (mediante la directiva de grupo, por ejemplo) archivos `NuGetDefaults.Config` coherentes para equipos de desarrollo y compilación, pueden garantizar que todos los usuarios de la organización usen los orígenes de paquete correctos en lugar de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e9c53-199">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="e9c53-200">El archivo `NuGetDefaults.Config` nunca hace que un origen de paquete se quite de la configuración de NuGet del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="e9c53-200">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="e9c53-201">Esto significa que si el desarrollador ya ha usado NuGet y, por tanto, tiene registrado el origen del paquete de nuget.org, no se eliminará después de la creación de un archivo `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-201">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="e9c53-202">Además, ni `NuGetDefaults.Config` ni ningún otro mecanismo de NuGet puede impedir el acceso a orígenes de paquetes como nuget.org. Si una organización quiere bloquear ese acceso, debe usar otros medios, como firewalls, para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="e9c53-202">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="e9c53-203">Ubicación de NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="e9c53-203">NuGetDefaults.Config location</span></span>

<span data-ttu-id="e9c53-204">En esta tabla se describe dónde debe almacenarse el archivo `NuGetDefaults.Config`, según el sistema operativo de destino:</span><span class="sxs-lookup"><span data-stu-id="e9c53-204">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="e9c53-205">Plataforma de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e9c53-205">OS Platform</span></span>  | <span data-ttu-id="e9c53-206">Ubicación de NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="e9c53-206">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="e9c53-207">Windows</span><span class="sxs-lookup"><span data-stu-id="e9c53-207">Windows</span></span>      | <span data-ttu-id="e9c53-208">**Visual Studio 2017 o NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="e9c53-208">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="e9c53-209">**Visual Studio 2015 y versiones anteriores o NuGet 3.x y versiones anteriores:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="e9c53-209">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="e9c53-210">Mac o Linux:</span><span class="sxs-lookup"><span data-stu-id="e9c53-210">Mac/Linux</span></span>    | <span data-ttu-id="e9c53-211">`$XDG_DATA_HOME` (normalmente `~/.local/share` o `/usr/local/share`, dependiendo de la distribución del SO)</span><span class="sxs-lookup"><span data-stu-id="e9c53-211">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="e9c53-212">Configuración de NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="e9c53-212">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="e9c53-213">`packageSources`: esta colección tiene el mismo significado que `packageSources` en los archivos de configuración normales y especifica los orígenes predeterminados.</span><span class="sxs-lookup"><span data-stu-id="e9c53-213">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="e9c53-214">NuGet usa los orígenes por su orden al instalar o actualizar paquetes en proyectos que usan el formato de administración `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="e9c53-214">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="e9c53-215">Para los proyectos que usan el formato PackageReference, NuGet usa primero orígenes locales y luego orígenes en recursos compartidos de red. Después, orígenes HTTP, independientemente del orden de los archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="e9c53-215">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="e9c53-216">NuGet siempre omite el orden de los orígenes de las operaciones de restauración.</span><span class="sxs-lookup"><span data-stu-id="e9c53-216">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="e9c53-217">`disabledPackageSources`: esta colección también tiene el mismo significado que en los archivos `NuGet.Config`, donde cada origen afectado se enumera por su nombre y un valor de true o false que indica si está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="e9c53-217">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="e9c53-218">Esto permite que el nombre y la dirección URL del origen se mantengan en `packageSources` sin tenerlo activado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e9c53-218">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="e9c53-219">Después, cada desarrollador puede volver a habilitar el origen estableciendo el valor del origen en false en otros archivos `NuGet.Config` sin tener que volver a buscar la dirección URL correcta.</span><span class="sxs-lookup"><span data-stu-id="e9c53-219">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="e9c53-220">Esto también es útil para proporcionar a los desarrolladores una lista completa de las direcciones URL de orígenes internos para una organización mientras solo se habilita el origen de un equipo individual de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e9c53-220">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="e9c53-221">`defaultPushSource`: especifica el destino predeterminado para las operaciones `nuget push`, lo que invalida el valor predeterminado integrado de nuget.org. Los administradores pueden implementar esta opción para evitar la publicación de paquetes internos en nuget.org por accidente, ya que los desarrolladores deben usar específicamente `nuget push -Source` para publicar en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e9c53-221">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="e9c53-222">Archivo NuGetDefaults.Config y aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e9c53-222">Example NuGetDefaults.Config and application</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
