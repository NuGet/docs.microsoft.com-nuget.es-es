---
title: Cómo administrar las carpetas de paquetes globales, de caché y temporales en NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Vea cómo administrar la carpeta de instalación de paquetes globales, la caché de paquetes y las carpetas temporales que existen en un equipo, que se utilizan al instalar, restaurar y actualizar paquetes.
keywords: carpeta de paquetes globales NuGet, memoria caché de paquetes NuGet, almacenamiento en caché de paquetes, carpeta de instalación de paquetes, memorias caché de NuGet, administrar memorias caché, memoria caché local de NuGet, memoria caché global de NuGet, comando locals de NuGet, borrar una memoria caché
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e9f4383a3f1700b96e3d6fe9ea4c0a7c24daa45a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Administración de las carpetas de paquetes globales, de caché y temporales

Cada vez que instala, actualiza o restaura un paquete, NuGet administra los paquetes y la información de paquete en varias externas a la estructura del proyecto:

| nombre | Descripción y ubicación (por usuario)|
| --- | --- |
| global‑packages | La carpeta *global-packages* es donde NuGet instala los paquetes que se descargan. Cada paquete se expande totalmente en una subcarpeta que coincida con el identificador y el número de versión del paquete. Los proyectos con el formato PackageReference siempre usan los paquetes directamente de esta carpeta. Cuando se usa `packages.config`, los paquetes se instalan en la carpeta *global-packages* y luego se copian en la carpeta `packages` del proyecto.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Se invalida mediante la variable de entorno NUGET_PACKAGES, las [opciones de configuración](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` o `repositoryPath` (cuando se usa PackageReference y `packages.config`, respectivamente) o la propiedad `RestorePackagesPath` de MSBuild (solo MSBuild). La variable de entorno tiene prioridad sobre la opción de configuración.</li></ul> |
| http-cache | El Administrador de paquetes de Visual Studio (NuGet 3.x y versiones posteriores) y la herramienta `dotnet` almacenan copias de los paquetes descargados en esta caché (guardados como archivos `.dat`), organizados en subcarpetas para cada origen de paquete. Los paquetes no se expanden y la caché tiene un plazo de expiración de 30 minutos.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Se invalida mediante la variable de entorno NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Carpeta donde NuGet almacena los archivos temporales durante sus diversas operaciones.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |

> [!Note]
> NuGet 3.5 y versiones anteriores utilizan *packages-cache* en lugar de *http-cache*, que se encuentra en `%localappdata%\NuGet\Cache`.

Mediante las carpetas *global-packages* y de caché, NuGet generalmente evita descargar paquetes que ya existen en el equipo, lo que mejora el rendimiento de las operaciones de instalación, actualización y restauración. Cuando se usa PackageReference, la carpeta *global-packages* también evita mantener paquetes descargados dentro de carpetas de proyecto, donde podrían accidentalmente agregarse al control de código fuente, y reduce el impacto general de NuGet en el almacenamiento en el equipo.

Cuando se le pide que recupere un paquete, NuGet busca primero en la carpeta *global-packages*. Si la versión exacta del paquete no está, NuGet comprueba todos los orígenes de paquetes que no sean HTTP. Si todavía no se encuentra el paquete, NuGet lo busca en *http-cache* a menos que especifique `--no-cache` con comandos `dotnet.exe` o `-NoCache` con comandos `nuget.exe`. Si el paquete no está en la caché o esta no se usa, NuGet recupera luego el paquete por HTTP.

Para más información, vea [¿Qué ocurre cuando se instala un paquete?](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).

## <a name="viewing-folder-locations"></a>Visualización de ubicaciones de carpeta

Puede ver las ubicaciones de carpeta mediante el [comando dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):

```cli
dotnet nuget locals all --list
```

Salida típica (Mac/Linux; "user1" es el nombre de usuario actual):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

Para mostrar la ubicación de una sola carpeta, use `http-cache`, `global-packages` o `temp` en lugar de `all`. 

También se ven ubicaciones mediante el [comando nuget locals](../tools/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

Salida típica (Windows; "user1" es el nombre de usuario actual):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

(`package-cache` se utiliza en NuGet 2.x y aparece con NuGet 3.5 y versiones anteriores).

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

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Los paquetes que se usen en proyectos que están actualmente abiertos en Visual Studio no se borran de la carpeta *global-packages*.

En Visual Studio, utilice el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes** y luego seleccione **Borrar todas las cachés de NuGet**. La administración de la memoria caché no está actualmente disponible a través de la consola del Administrador de paquetes.

![Comando de opciones de NuGet para borrar memorias caché](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Solución de problemas de errores

Se pueden producir los siguientes errores al usar `nuget locals` o `dotnet nuget locals`:

- *Error: El proceso no puede obtener acceso al archivo porque otro proceso <package> lo está utilizando* o *Error al borrar los recursos locales: no se pueden eliminar uno o varios archivos*.

    Uno o varios archivos de la carpeta están en uso por otro proceso; por ejemplo, se abre un proyecto de Visual Studio que hace referencia a paquetes de la carpeta *global-packages*. Cierre los procesos y e inténtelo de nuevo.

- *Error: se ha denegado el acceso a la ruta de acceso <path>* o *el directorio no está vacío*.

    No tiene permiso para eliminar archivos en la caché. Si es posible, cambie los permisos de carpeta e inténtelo de nuevo. Si no, póngase en contacto con el administrador del sistema.

- *Error: la ruta de acceso especificada, el nombre de archivo o ambos son demasiado largos. El nombre de archivo completo debe ser inferior a 260 caracteres y el nombre del directorio debe ser inferior a 248*.

    Acorte los nombres de carpeta e inténtelo de nuevo.
