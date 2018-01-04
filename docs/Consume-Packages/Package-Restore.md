---
title: "Restauración de paquetes NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Una descripción de cómo NuGet restaura los paquetes de los que depende un proyecto, incluido cómo deshabilitar la restauración y restringir las versiones."
keywords: "Restauración de paquetes NuGet, instalación de paquetes NuGet, instalación del paquete, restauración de paquetes, versiones de dependencia, deshabilitar la restauración automática, restricción de versiones de paquetes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a>Restauración de paquetes

Para promover un entorno de desarrollo más limpio y reducir el tamaño del repositorio, **Restauración de paquetes** de NuGet instala todos los paquetes a los que se hace referencia antes de compilar un proyecto. Esta característica de uso frecuente garantiza que todas las dependencias están disponibles en un proyecto sin necesidad de almacenar esos paquetes en el control de código fuente (vea [Paquetes y control de código fuente](../consume-packages/packages-and-source-control.md) para obtener información sobre cómo configurar el repositorio para excluir archivos binarios de paquete).

En este tema:
- [Guía rápida de la restauración de paquetes](#quick-guide-to-package-restore)
- [Información general sobre restauración de paquetes](#package-restore-overview)
- [Habilitar y deshabilitar la restauración de paquetes](#enabling-and-disabling-package-restore)
- [Restricción de versiones de paquetes con la restauración](#constraining-package-versions-with-restore)
- [Restauración de línea de comandos](#command-line-restore), para todas las versiones de NuGet
- [Restauración automática en Visual Studio](#automatic-restore-in-visual-studio), para NuGet 2.7 y versiones posteriores.
- [Restauración integrada de MSBuild en Visual Studio](#msbuild-integrated-restore), para NuGet 2.6 y versiones anteriores.
- [Restauración de paquetes con Team Foundation Build](#package-restore-with-team-foundation-build)

El comportamiento de restauración varía según la versión; para comprobar la versión de NuGet, simplemente ejecute `nuget.exe` en la línea de comandos y mire la primera línea de la salida.

Para obtener más detalles sobre la restauración de paquetes en servidores de compilación, vea [Restauración de paquetes con TFBuild](../consume-packages/team-foundation-build.md).

> [!Note]
> Los proyectos configurados para la restauración de paquetes también funcionan con xbuild en Mono.

## <a name="quick-guide-to-package-restore"></a>Guía rápida de la restauración de paquetes

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> Si ve el error "Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo" o "Uno o varios paquetes de NuGet se deben restaurar, pero no pudieron restaurarse porque no se ha concedido el consentimiento", active la restauración automática mediante las instrucciones descritas en [Habilitar y deshabilitar la restauración de paquetes](#enabling-and-disabling-package-restore).

## <a name="package-restore-overview"></a>Información general sobre restauración de paquetes

En primer lugar, las referencias de paquete se mantienen en uno de los formatos de administración de paquetes siguientes, según el tipo de proyecto y la versión de NuGet. (Tenga en cuenta que NuGet 4 y MSBuild 15.1 se instalan con Visual Studio 2017).

| Método | Versión de NuGet | Descripción | 
| --- | --- | --- |
| `packages.config` | 2.x y posterior | Muestra el conjunto completo de dependencias. Los paquetes agregados a `packages.config` también se deben agregar al archivo de proyecto, así como los destinos y propiedades. Este es el método de base de referencia para todas las versiones de NuGet, pero tiene un rendimiento más lento en comparación con las otras opciones. (Vea [esquema packages.config](../schema/packages-config.md)). | 
| `project.json` | 3.x y posteriores | Solo se usa de forma predeterminada con proyectos de UWP, pero los proyectos se pueden convertir desde `packages.config`. `project.json` muestra únicamente las dependencias de nivel superior. Las referencias, destinos y propiedades se agregan de forma dinámica al proyecto durante la compilación, lo que da lugar a un mejor rendimiento en comparación con `packages.config`. (Vea [esquema project.json](../schema/project-json.md)).|
| PackageReference | 4.x y posteriores | Enumera las dependencias directamente en el archivo de proyecto en el nodo `<PackageReference>`, junto a `<Reference>` y `<ProjectReference>`. Funciona de forma similar a `project.json`; vea [Referencias de paquete en archivos de proyecto](../Consume-Packages/Package-References-in-Project-Files.md). |

En segundo lugar, una restauración se inicia con la lista de referencias de varias maneras:

Desde la línea de comandos o la [Consola del Administrador de paquetes](../tools/Package-Manager-Console.md):

| Comando | Escenarios aplicables |
| --- | --- | 
| `nuget restore` | Todas las versiones de NuGet y todos los tipos de referencia. Vea [Restauración de línea de comandos](#command-line-restore) a continuación. | 
| `dotnet restore` | Igual que `nuget restore` para los proyectos de .NET Core. Vea [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore). |
| `msbuild /t:restore` | Solo para NuGet 4.x y versiones posteriores, y MSBuild 15.1 y versiones posteriores con [referencias de paquete en archivos de proyecto](../Consume-Packages/Package-References-in-Project-Files.md). `nuget restore` y `dotnet restore` usan este comando para los proyectos aplicables. Vea [pack y restore de NuGet como destinos de MSBuild: restaurar destino](../schema/msbuild-targets.md#restore-target).|

Visual Studio también restaura paquetes en momentos diferentes:

| Tipo | Cuando se produce la restauración |
| --- | --- |
| Restauración de plantilla | Durante la creación de un proyecto nuevo, dado que algunas plantillas dependen de paquetes externos. |
| Restauración de compilación | Como el primer paso de una compilación. |
| Restauración de la solución | Cuando el usuario hace clic con el botón derecho en una solución y selecciona **Restaurar paquetes NuGet**. |
| Restauración al cambiar el proyecto | *(Solo para NuGet 4.x)* Cuando se usa una proyecto basado en el SDK de .NET Core, incluidos los cambios de estado del proyecto. |

## <a name="enabling-and-disabling-package-restore"></a>Habilitar y deshabilitar la restauración de paquetes

La restauración de paquetes se habilita principalmente a través de **Herramientas > Opciones > Administrador de paquetes NuGet** en Visual Studio:

![Control de los comportamientos de restauración de paquetes a través de las opciones del Administrador de paquetes NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Permitir a NuGet descargar los paquetes que falten**: controla todas las formas de restauración de paquetes cambiando la opción `packageRestore/enabled` en el archivo `%AppData%\NuGet\NuGet.Config` como se muestra a continuación.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  La opción `packageRestore/enabled` se puede invalidar de forma global estableciendo una variable de entorno denominada **EnableNuGetPackageRestore** con un valor de TRUE o FALSE antes de iniciar Visual Studio o una compilación.
    

- **Comprobar automáticamente los paquetes que falten durante la compilación en Visual Studio**: controla la restauración automática para NuGet 2.7 y versiones posteriores cambiando la opción `packageRestore/automatic` en el archivo `%AppData%\NuGet\NuGet.Config` como se muestra a continuación.
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

Como referencia, vea el [archivo de configuración de NuGet: sección packageRestore](../Schema/nuget-config-file.md#packagerestore-section).

En algunos casos, es posible que un desarrollador o una empresa quiera habilitar o deshabilitar la restauración de paquetes en un equipo de forma predeterminada para todos los usuarios. Esto se puede hacer mediante la adición de la misma configuración anterior al archivo de configuración global de NuGet ubicado en `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Después, los usuarios individuales pueden habilitar la restauración de forma selectiva cuando sea necesario en un nivel de proyecto. Vea [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) para obtener información exacta sobre cómo prioriza NuGet varios archivos de configuración.

## <a name="constraining-package-versions-with-restore"></a>Restricción de versiones de paquetes con la restauración

Cuando NuGet restaure paquetes a través de cualquier método, respetará las restricciones especificadas en `packages.config`, `project.json` o el archivo de proyecto:

- `packages.config`: especifique un intervalo de versiones en la propiedad `allowedVersion` de la dependencia. Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Por ejemplo:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: especifique un intervalo de versiones directamente con el número de versión de la dependencia. Por ejemplo:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- Referencias de paquetes en archivos de proyecto: especifique un intervalo de versiones directamente con el número de versión de la dependencia. Por ejemplo:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

En todos los casos, use la notación que se describe en [Package versioning](../reference/package-versioning.md) (Control de versiones de paquetes).

## <a name="command-line-restore"></a>Restauración de línea de comandos

Para NuGet 2.7 y versiones posteriores, use el comando [Restore](../tools/cli-ref-restore.md) para restaurar todos los paquetes de una solución (con independencia de que se use `packages.config`, `project.json` o referencias de paquete en archivos de proyecto). Para una carpeta de proyecto determinada, como `c:\proj\app`, las variaciones comunes siguientes restauran los paquetes:

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

Para NuGet 4.0 y versiones posteriores, y MSBuild 15.1 y versiones posteriores, también se puede usar `MSBuild /t:restore` como se describe en [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md).

## <a name="build-time-restore-in-visual-studio"></a>Restauración en tiempo de compilación en Visual Studio

Visual Studio restaurará automáticamente los paquetes que falten al principio de una compilación de forma predeterminada. Se puede cambiar este comportamiento desactivando **Herramientas > Opciones > Administrador de paquetes NuGet > General > Comprobar automáticamente los paquetes que falten durante la compilación en Visual Studio**.

Cuando se habilita, la restauración automática funciona del siguiente modo:

1. Cuando se inicia una compilación, Visual Studio indica a NuGet que restaure los paquetes.
1. NuGet busca de forma recurrente todos los archivos `packages.config` en la solución, busca `project.json`, o bien busca en el archivo de proyecto.
1. Para cada paquete enumerado en los archivos de referencia, NuGet comprueba si ya existe en la solución (la carpeta `packages`, `project.lock.json` o `project.assets.json` en función de si el proyecto usa `packages.config`, `project.json` o referencias de paquete en archivos de proyecto).
1. Si no se encuentra el paquete, NuGet intenta recuperarlo primero de la memoria caché (vea [Administración de la caché NuGet](../consume-packages/managing-the-nuget-cache.md)). Si el paquete no está en la memoria caché, NuGet intenta descargarlo desde los orígenes habilitados indicados en **Herramientas > Opciones > Administrador de paquetes NuGet > Orígenes de paquetes**, en el orden en que aparecen los orígenes. En este caso, NuGet no indica un error al buscar el paquete hasta que se han comprobado todos los orígenes, momento en el que informa del error solo para el último origen de la lista. Por implicación, este tipo de error también significa que el paquete no estaba presente en ninguno de los otros orígenes, aunque no se mostraran errores para esos orígenes de manera individual.
1. Si la descarga se realiza correctamente, NuGet almacena en caché el paquete y lo instala en la solución (de nuevo, en la carpeta `packages`, `project.lock.json` o `project.assets.json`); de lo contrario, se produce un error de NuGet y de compilación.

Durante este proceso, verá un cuadro de diálogo de progreso con la opción de cancelar la restauración del paquete.

## <a name="package-restore-with-team-foundation-build"></a>Restauración de paquetes con Team Foundation Build

La restauración de paquetes se usa habitualmente al compilar proyectos en servidores de compilación, al igual que con Team Foundation Server (TFS) y Visual Studio Team Services (así como otros sistemas de compilación, que no se tratan aquí).

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Al crear una definición de compilación en Team Services, basta con incluir la tarea Restaurar paquetes NuGet en la definición antes de cualquier tarea de compilación. Esta tarea se incluye de forma predeterminada en una serie de plantillas de compilación.

![Tarea Restaurar paquetes NuGet en una definición de compilación de Visual Studio Team Services](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

Con TFS 2013 y versiones posteriores, los paquetes se restauran automáticamente de forma predeterminada durante la compilación, siempre que se use una plantilla de Team Build para Team Foundation Server 2013 o posterior.

Si usa una versión anterior de plantillas de compilación (como en un proyecto que se ha migrado desde versiones anteriores de TFS), también debe migrar esas plantillas de compilación a TFS 2013. Esto significa, básicamente, volver a crear los elementos personalizados de las plantillas de compilación mediante la plantilla adecuada para el control de código fuente (TFVC o Git).

Para la versión anterior de TFS, simplemente puede incluir un paso de compilación para invocar la [restauración de línea de comandos](#command-line-restore) como se describió anteriormente.

Para obtener más información, vea [Tutorial de restauración de paquetes con Team Foundation Build](../consume-packages/team-foundation-build.md).    
