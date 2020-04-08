---
title: Cómo administrar las carpetas de paquetes globales, de caché y temporales en NuGet
description: Vea cómo administrar la carpeta de instalación de paquetes globales, la caché de paquetes y las carpetas temporales que existen en un equipo, que se utilizan al instalar, restaurar y actualizar paquetes.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428592"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Administración de las carpetas de paquetes globales, de caché y temporales

Cada vez que instala, actualiza o restaura un paquete, NuGet administra los paquetes y la información de paquete en varias externas a la estructura del proyecto:

| NOMBRE | Descripción y ubicación (por usuario)|
| --- | --- |
| global‑packages | La carpeta *global-packages* es donde NuGet instala los paquetes que se descargan. Cada paquete se expande totalmente en una subcarpeta que coincida con el identificador y el número de versión del paquete. Los proyectos con el formato [PackageReference](package-references-in-project-files.md) siempre usan los paquetes directamente de esta carpeta. Cuando se usa [packages.config](../reference/packages-config.md), los paquetes se instalan en la carpeta *global-packages* y luego se copian en la carpeta `packages` del proyecto.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Se invalida mediante la variable de entorno NUGET_PACKAGES, las [opciones de configuración](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` o `repositoryPath` (cuando se usa PackageReference y `packages.config`, respectivamente) o la propiedad `RestorePackagesPath` de MSBuild (solo MSBuild). La variable de entorno tiene prioridad sobre la opción de configuración.</li></ul> |
| http-cache | El Administrador de paquetes de Visual Studio (NuGet 3.x y versiones posteriores) y la herramienta `dotnet` almacenan copias de los paquetes descargados en esta caché (guardados como archivos `.dat`), organizados en subcarpetas para cada origen de paquete. Los paquetes no se expanden y la caché tiene un plazo de expiración de 30 minutos.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Se invalida mediante la variable de entorno NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Carpeta donde NuGet almacena los archivos temporales durante sus diversas operaciones.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| plugins-cache **4.8+** | Carpeta en la que NuGet almacena los resultados de la solicitud de notificaciones de la operación.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>Se invalida mediante la variable de entorno NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> NuGet 3.5 y versiones anteriores utilizan *packages-cache* en lugar de *http-cache*, que se encuentra en `%localappdata%\NuGet\Cache`.

Mediante las carpetas *global-packages* y de caché, NuGet generalmente evita descargar paquetes que ya existen en el equipo, lo que mejora el rendimiento de las operaciones de instalación, actualización y restauración. Cuando se usa PackageReference, la carpeta *global-packages* también evita mantener paquetes descargados dentro de carpetas de proyecto, donde podrían accidentalmente agregarse al control de código fuente, y reduce el impacto general de NuGet en el almacenamiento en el equipo.

Cuando se le pide que recupere un paquete, NuGet busca primero en la carpeta *global-packages*. Si la versión exacta del paquete no está, NuGet comprueba todos los orígenes de paquetes que no sean HTTP. Si todavía no se encuentra el paquete, NuGet lo busca en *http-cache* a menos que especifique `--no-cache` con comandos `dotnet.exe` o `-NoCache` con comandos `nuget.exe`. Si el paquete no está en la caché o esta no se usa, NuGet recupera luego el paquete por HTTP.

Para obtener más información, vea [¿Qué ocurre cuando se instala un paquete?](../concepts/package-installation-process.md)

## <a name="viewing-folder-locations"></a>Visualización de ubicaciones de carpeta

Puede ver las ubicaciones mediante el [comando nuget locals](../reference/cli-reference/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Salida típica (Windows; "user1" es el nombre de usuario actual):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` se utiliza en NuGet 2.x y aparece con NuGet 3.5 y versiones anteriores).

También puede ver las ubicaciones de carpeta mediante el [comando dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):

```dotnetcli
dotnet nuget locals all --list
```

Salida típica (Mac/Linux; "user1" es el nombre de usuario actual):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Para mostrar la ubicación de una sola carpeta, use `http-cache`, `global-packages`, `temp` o `plugins-cache` en lugar de `all`.

## <a name="clearing-local-folders"></a>Borrado de carpetas locales

Si detecta problemas de instalación de paquetes o quiere asegurarse de que está instalando paquetes de una galería remota, use la opción `locals --clear` (dotnet.exe) o `locals -clear` (nuget.exe) para especificar la carpeta que quiere borrar o `all` para borrar todas las carpetas:

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Los paquetes que se usen en proyectos que están actualmente abiertos en Visual Studio no se borran de la carpeta *global-packages*.

A partir de Visual Studio 2017, use el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes** y, luego, seleccione **Borrar todas las cachés de NuGet**. La administración de la memoria caché no está actualmente disponible a través de la consola del Administrador de paquetes. En Visual Studio 2015, en su lugar use los comandos de la CLI.

![Comando de opciones de NuGet para borrar memorias caché](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Solución de problemas de errores

Se pueden producir los siguientes errores al usar `nuget locals` o `dotnet nuget locals`:

- *Error: El proceso no puede acceder al archivo <package> porque otro proceso lo está usando* o *Error al borrar los recursos locales: no se pueden eliminar uno o varios archivos*.

    Uno o varios archivos de la carpeta están en uso por otro proceso; por ejemplo, se abre un proyecto de Visual Studio que hace referencia a paquetes de la carpeta *global-packages*. Cierre los procesos y e inténtelo de nuevo.

- *Error: Se ha denegado el acceso a la ruta <path>* o *El directorio no está vacío*.

    No tiene permiso para eliminar archivos en la caché. Si es posible, cambie los permisos de carpeta e inténtelo de nuevo. Si no, póngase en contacto con el administrador del sistema.

- *Error: La ruta de acceso especificada, el nombre de archivo o ambos son demasiado largos. El nombre de archivo completo debe ser inferior a 260 caracteres y el nombre del directorio debe ser inferior a 248*.

    Acorte los nombres de carpeta e inténtelo de nuevo.
