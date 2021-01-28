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
# <a name="common-nuget-configurations"></a>Configuraciones comunes de NuGet

El comportamiento de NuGet se controla mediante la configuración acumulada en uno o varios archivos `NuGet.Config` (XML) que pueden existir en los niveles del proyecto, usuario y todo el equipo. Un archivo `NuGetDefaults.Config` global configura también los orígenes de paquetes de forma específica. La configuración se aplica a todos los comandos emitidos en la CLI, la consola del Administrador de paquetes y la interfaz de usuario del Administrador de paquetes.

## <a name="config-file-locations-and-uses"></a>Usos y ubicaciones de los archivos de configuración

| Ámbito | Ubicación del archivo NuGet.Config | Descripción |
| --- | --- | --- |
| Soluciones | Carpeta actual (también denominada carpeta de soluciones) o cualquier carpeta hasta la raíz de la unidad.| En una carpeta de soluciones, la configuración se aplica a todos los proyectos de las subcarpetas. Tenga en cuenta que si se coloca un archivo de configuración en una carpeta de proyecto, no tiene ningún efecto en ese proyecto. |
| Usuario | **Windows:** `%appdata%\NuGet\NuGet.Config`<br/>**Mac/Linux:** `~/.config/NuGet/NuGet.Config` o `~/.nuget/NuGet/NuGet.Config` (varía según la distribución del SO) <br/>Se admiten configuraciones adicionales en todas las plataformas. Estas configuraciones no se pueden editar con las herramientas. </br> **Windows:** `%appdata%\NuGet\config\*.Config` <br/>**Mac/Linux:** `~/.config/NuGet/config/*.config` o `~/.nuget/config/*.config` | La configuración se aplica a todas las operaciones, pero se reemplaza por la configuración de nivel de proyecto. |
| Computer | **Windows:** `%ProgramFiles(x86)%\NuGet\Config`<br/>**Mac/Linux:** `$XDG_DATA_HOME`. Si `$XDG_DATA_HOME` es null o está vacío, se usará `~/.local/share` o `/usr/local/share` (varía según la distribución del SO)  | La configuración se aplica a todas las operaciones en el equipo, pero se reemplaza por cualquier configuración de nivel de proyecto o de usuario. |

Notas para versiones anteriores de NuGet:
- En NuGet 3.3 y versiones anteriores se usaba una carpeta `.nuget` para la configuración de toda la solución. Esta carpeta no se usa en NuGet 3.4 y versiones posteriores.
- Para NuGet 2.6 a 3.x, el archivo de configuración de nivel de equipo en Windows se encontraba en %ProgramData%\NuGet\Config[\\{IDE}[\\{Versión}[\\{SKU}]]]\NuGet.Config, donde *{IDE}* podía ser *VisualStudio*, *{Versión}* era la versión de Visual Studio como *14.0* y *{SKU}* era *Community*, *Pro* o *Enterprise*. Para migrar la configuración a NuGet 4.0 y versiones posteriores, simplemente copie el archivo de configuración a %ProgramFiles(x86)%\NuGet\Config. Esta ubicación anterior era /etc/opt, en Linux, y /Biblioteca/Application Support, en Mac.

## <a name="changing-config-settings"></a>Cambiar los valores de configuración

Un archivo `NuGet.Config` es un archivo de texto XML simple que contiene pares de clave y valor como se describe en el tema [Opciones de configuración de NuGet](../reference/nuget-config-file.md).

La configuración se administra mediante el [comando config](../reference/cli-reference/cli-ref-config.md) de la CLI de NuGet:
- De forma predeterminada, los cambios se realizan en el archivo de configuración de nivel de usuario.
- Para cambiar la configuración en un archivo diferente, use el modificador `-configFile`. En este caso, se puede usar cualquier nombre de archivo en los archivos.
- Las claves siempre distinguen mayúsculas de minúsculas.
- Es necesaria la elevación para cambiar la configuración en el archivo de configuración de nivel de equipo.

> [!Warning]
> Aunque puede modificar el archivo en cualquier editor de texto, NuGet (v3.4.3 y versiones posteriores) ignora automáticamente el archivo de configuración completo si contiene código XML con formato incorrecto (etiquetas que no coinciden, comillas no válidas, etc.) Por este motivo se prefiere administrar la configuración mediante `nuget config`.

### <a name="setting-a-value"></a>Establecer un valor

Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

Mac o Linux:

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
> En NuGet 3.4 y versiones posteriores puede usar variables de entorno en cualquier valor, como en `repositoryPath=%PACKAGEHOME%` (Windows) y `repositoryPath=$PACKAGEHOME` (Mac o Linux).

### <a name="removing-a-value"></a>Quitar un valor

Para quitar un valor, especifique una clave con un valor vacío.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Creación de un archivo de configuración

Copie la plantilla siguiente en el archivo nuevo y, después, use `nuget config -configFile <filename>` para establecer los valores:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Cómo se aplica la configuración

Varios archivos `NuGet.Config` permiten almacenar la configuración en ubicaciones diferentes para que se aplique a un único proyecto, a un grupo de proyectos o a todos los proyectos. Colectivamente, esta configuración se aplica a cualquier operación de NuGet que se invoca desde la línea de comandos o desde Visual Studio, y tiene prioridad la configuración que existe "más cerca" de un proyecto o la carpeta actual.

En concreto, NuGet carga la configuración desde los diferentes archivos de configuración en el orden siguiente:

1. El [archivo NuGetDefaults.Config](#nuget-defaults-file), que contiene los valores relacionados solamente con orígenes de paquetes.
1. El archivo de nivel de equipo.
1. El archivo de nivel de usuario.
1. El archivo especificado con `-configFile`.
1. Los archivos que se encuentran en todas las carpetas en la ruta de acceso desde la raíz de la unidad a la carpeta actual (donde se invoca nuget.exe o la carpeta que contiene el proyecto de Visual Studio). Por ejemplo, si se invoca un comando en c:\A\B\C, NuGet busca y carga los archivos de configuración en c:\,, después c:\A, después c:\A\B y, por último, c:\A\B\C.

Cuando NuGet encuentra la configuración en estos archivos, se aplica como sigue:

1. Para elementos de un solo elemento, NuGet reemplaza cualquier valor encontrado anteriormente para la misma clave. Esto significa que la configuración "más cercana" a la carpeta o proyecto actual reemplaza a cualquier otra encontrada anteriormente. Por ejemplo, el valor `defaultPushSource` en `NuGetDefaults.Config` se reemplaza si se encuentra en cualquier otro archivo de configuración.

1. Para elementos de colección (como `<packageSources>`), NuGet combina los valores de todos los archivos de configuración en una sola colección.

1. Cuando `<clear />` está presente para un nodo determinado, NuGet ignora los valores de configuración definidos previamente para ese nodo.

### <a name="settings-walkthrough"></a>Tutorial de configuración

Supongamos que tiene la siguiente estructura de carpetas en dos unidades independientes:

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

Tiene cuatro archivos `NuGet.Config` en las ubicaciones siguientes con el contenido especificado. (El archivo de nivel de equipo no está incluido en este ejemplo, pero se comportaría igual que el archivo de nivel de usuario).

Archivo A. Archivo de nivel de usuario (`%appdata%\NuGet\NuGet.Config` en Windows, `~/.config/NuGet/NuGet.Config` en Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Archivo B. disk_drive_2/NuGet.Config:

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

Archivo C. disk_drive_2/Project1/NuGet.Config:

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

Archivo D. disk_drive_2/Project2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

Después, NuGet carga y aplica la configuración como se indica a continuación, en función de dónde se invoque:

- **Se invoca desde disk_drive_1/users/**: solo se usa el repositorio predeterminado que aparece en el archivo de configuración de nivel de usuario (A), ya que es el único archivo encontrado en disk_drive_1.

- **Se invoca desde disk_drive_2/ o disk_drive_/tmp**: en primer lugar se carga el archivo de nivel de usuario (A) y después NuGet se desplaza a la raíz de disk_drive_2 y busca el archivo (B). NuGet también busca un archivo de configuración en/tmp pero no lo encuentra. Como resultado, se usa el repositorio predeterminado en nuget.org, se habilita la restauración de paquetes y los paquetes se expanden en disk_drive_2/tmp.

- **Se invoca desde disk_drive_2/Project1 o disk_drive_2/Project1/Source**: primero se carga el archivo de nivel de usuario (A), después NuGet carga el archivo (B) desde la raíz de disk_drive_2, seguido del archivo (C). La configuración de (C) invalida la de (B) y (A), por lo que la `repositoryPath` donde se instalan los paquetes es disk_drive_2/Project1/External/Packages en lugar de *disk_drive_2/tmp*. Además, dado que borra (C) `<packageSources>`, nuget.org ya no está disponible como un origen, lo que solo deja `https://MyPrivateRepo/ES/nuget`.

- **Se invoca desde disk_drive_2/Project2 o disk_drive_2/Project2/Source**: primero se carga el archivo de nivel de usuario (A), seguido del archivo (B) y el archivo (D). Dado que `packageSources` no se borra, `nuget.org` y `https://MyPrivateRepo/DQ/nuget` están disponibles como orígenes. Los paquetes se expanden en disk_drive_2/tmp, como se especifica en (B).

## <a name="additional-user-wide-configuration"></a>Configuración adicional para todos los usuarios

A partir de la versión 5.7, NuGet ha agregado compatibilidad con archivos de configuración adicional para todos los usuarios. Esto permite a los proveedores externos agregar archivos de configuración de usuario adicional sin elevación.
Estos archivos de configuración se encuentran en la carpeta de configuración estándar de todos los usuarios en una subcarpeta `config`.
Se tendrán en cuenta todos los archivos que terminen en `.config` o `.Config`.
Estos archivos no se pueden editar con las herramientas estándar.

| Plataforma de sistema operativo  | Configuración adicional |
| --- | --- |
| Windows      | `%appdata%\NuGet\config\*.Config` |
| Mac/Linux    | `~/.config/NuGet/config/*.config` o `~/.nuget/config/*.config` |

## <a name="nuget-defaults-file"></a>Archivo de valores predeterminados de NuGet

El archivo `NuGetDefaults.Config` existe para especificar los orígenes de paquete desde los que se instalan y actualizan los paquetes, y para controlar el destino predeterminado para la publicación de paquetes con `nuget push`. Como los administradores pueden implementar de forma cómoda (mediante la directiva de grupo, por ejemplo) archivos `NuGetDefaults.Config` coherentes para equipos de desarrollo y compilación, pueden garantizar que todos los usuarios de la organización usen los orígenes de paquete correctos en lugar de nuget.org.

> [!Important]
> El archivo `NuGetDefaults.Config` nunca hace que un origen de paquete se quite de la configuración de NuGet del desarrollador. Esto significa que si el desarrollador ya ha usado NuGet y, por tanto, tiene registrado el origen del paquete de nuget.org, no se eliminará después de la creación de un archivo `NuGetDefaults.Config`.
>
> Además, ni `NuGetDefaults.Config` ni ningún otro mecanismo de NuGet puede impedir el acceso a orígenes de paquetes como nuget.org. Si una organización quiere bloquear ese acceso, debe usar otros medios, como firewalls, para hacerlo.

### <a name="nugetdefaultsconfig-location"></a>Ubicación de NuGetDefaults.Config

En esta tabla se describe dónde debe almacenarse el archivo `NuGetDefaults.Config`, según el sistema operativo de destino:

| Plataforma de sistema operativo  | Ubicación de NuGetDefaults.Config |
| --- | --- |
| Windows      | **Visual Studio 2017 o NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 y versiones anteriores o NuGet 3.x y versiones anteriores:** `%PROGRAMDATA%\NuGet` |
| Mac o Linux:    | `$XDG_DATA_HOME` (normalmente `~/.local/share` o `/usr/local/share`, dependiendo de la distribución del SO)|

### <a name="nugetdefaultsconfig-settings"></a>Configuración de NuGetDefaults.Config

- `packageSources`: esta colección tiene el mismo significado que `packageSources` en los archivos de configuración normales y especifica los orígenes predeterminados. NuGet usa los orígenes por su orden al instalar o actualizar paquetes en proyectos que usan el formato de administración `packages.config`. Para los proyectos que usan el formato PackageReference, NuGet usa primero orígenes locales y luego orígenes en recursos compartidos de red. Después, orígenes HTTP, independientemente del orden de los archivos de configuración. NuGet siempre omite el orden de los orígenes de las operaciones de restauración.

- `disabledPackageSources`: esta colección también tiene el mismo significado que en los archivos `NuGet.Config`, donde cada origen afectado se enumera por su nombre y un valor de true o false que indica si está deshabilitado. Esto permite que el nombre y la dirección URL del origen se mantengan en `packageSources` sin tenerlo activado de forma predeterminada. Después, cada desarrollador puede volver a habilitar el origen estableciendo el valor del origen en false en otros archivos `NuGet.Config` sin tener que volver a buscar la dirección URL correcta. Esto también es útil para proporcionar a los desarrolladores una lista completa de las direcciones URL de orígenes internos para una organización mientras solo se habilita el origen de un equipo individual de forma predeterminada.

- `defaultPushSource`: especifica el destino predeterminado para las operaciones `nuget push`, lo que invalida el valor predeterminado integrado de nuget.org. Los administradores pueden implementar esta opción para evitar la publicación de paquetes internos en nuget.org por accidente, ya que los desarrolladores deben usar específicamente `nuget push -Source` para publicar en nuget.org.

### <a name="example-nugetdefaultsconfig-and-application"></a>Archivo NuGetDefaults.Config y aplicación de ejemplo

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
