---
title: "Restauración de paquetes NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Una descripción de cómo NuGet restaura paquetes de los que depende un proyecto, incluido cómo deshabilitar la restauración y la restricción de versiones."
keywords: "Restauración de paquetes NuGet, instalación de paquetes NuGet, instalación del paquete, restauración de paquetes, versiones de dependencia, deshabilitar la restauración automática, restricción de versiones de paquetes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a>Restauración de paquetes

Para promover un entorno de desarrollo más limpio y reducir el tamaño del repositorio, **Restauración de paquetes** de NuGet instala todos los paquetes a los que se hace referencia antes de compilar un proyecto. Esta característica de uso frecuente (disponible en Visual Studio, .NET Core 2.0 y versiones posteriores y xbuild en Mono) garantiza que todas las dependencias están disponibles en un proyecto sin necesidad de almacenar esos paquetes en el control de código fuente (vea [Paquetes y control de código fuente](../consume-packages/packages-and-source-control.md) para obtener información sobre cómo configurar el repositorio para excluir archivos binarios de paquete). También puede restaurar paquetes manualmente en cualquier momento.

Para obtener más detalles sobre la restauración de paquetes en servidores de compilación, vea [Restauración de paquetes con TFBuild](../consume-packages/team-foundation-build.md).

## <a name="package-restore-overview"></a>Información general sobre restauración de paquetes

Al restaurar paquetes, se instalan primero las dependencias directas de un proyecto según sea necesario y, luego, se instalarán todas las dependencias de los paquetes a lo largo del gráfico de dependencias completo.

Si un paquete no está ya instalado, NuGet primero intenta recuperarlo desde la [caché](../consume-packages/managing-the-nuget-cache.md). Si el paquete no está en la memoria caché, NuGet intenta descargar el paquete (y almacenarlo en caché) desde todos los orígenes habilitados (vea [Configuración del comportamiento de NuGet](Configuring-NuGet-Behavior.md)); los orígenes también aparecen en la lista **Herramientas > Opciones > Administrador de paquetes NuGet > Orígenes del paquete** en Visual Studio). NuGet omite el orden de los orígenes del paquete, usando el paquete del origen que primero responda a las solicitudes.

> [!Note]
> NuGet no indica un error al restaurar un paquete hasta que se han comprobado todos los orígenes. En ese momento, NuGet informa del error solo para el último origen de la lista. El error implica que el paquete no estaba presente en *ninguno* de los otros orígenes, aunque los errores no se muestran para cada uno de esos orígenes de forma individual.

La restauración de paquetes se activa de las maneras siguientes:

- **CLI de dotnet**: use el comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura los paquetes incluidos en el archivo de proyecto (vea [PackageReference](../consume-packages/package-references-in-project-files.md)). Con .NET Core 2.0 y versiones posteriores, la restauración se realiza automáticamente con `dotnet build` y `dotnet run`.

- **Interfaz de usuario del Administrador de paquetes (Visual Studio en Windows)**: los paquetes se restauran automáticamente al crear un proyecto a partir de una plantilla y al compilar un proyecto (sujeto a la opción descrita en [Habilitar y deshabilitar la restauración de paquetes](#enabling-and-disabling-package-restore)). En NuGet 4.0 y versiones posteriores, la restauración también se produce automáticamente al realizar cambios en un proyecto basado en el SDK de .NET Core.

    Para la restauración manual, haga clic con el botón derecho en la solución en el Explorador de soluciones y seleccione **Restaurar paquetes NuGet**. Si uno o varios paquetes siguen sin estar instalados correctamente (lo que significa que el Explorador de soluciones muestra un icono de error), use la interfaz de usuario del Administrador de paquetes para desinstalar y reinstalar los paquetes afectados. Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md)

    Si ve el error "Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo" o "Uno o varios paquetes de NuGet se deben restaurar, pero no pudieron restaurarse porque no se ha concedido el consentimiento", active la restauración automática mediante las instrucciones descritas en [Habilitar y deshabilitar la restauración de paquetes](#enabling-and-disabling-package-restore).

- **CLI de NuGet**: use el comando [nuget restore](../tools/cli-ref-restore.md), que restaura los paquetes incluidos en el archivo de proyecto (vea [PackageReference](../consume-packages/package-references-in-project-files.md)) o en un archivo [packages.config](../reference/packages-config.md). También puede especificar un archivo de solución.

- **MSBuild**: use el comando [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), que restaura los paquetes incluidos en el archivo de proyecto (vea [PackageReference](../consume-packages/package-references-in-project-files.md)). Disponible solo en 4.x y versiones posteriores y MSBuild 15.1 y versiones posteriores, que se incluyen con Visual Studio de 2017. `nuget restore` y `dotnet restore` usan este comando para los proyectos aplicables.

- **Visual Studio Team Services**: al crear una definición de compilación en Team Services, incluya la tarea [Restaurar NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) o [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) (Restaurar .NET Core) en la definición antes de cualquier tarea de compilación. Esta tarea se incluye de forma predeterminada en una serie de plantillas de compilación.

- **Team Foundation Server**: TFS 2013 con TFS 2013 y versiones posteriores, los paquetes se restauran automáticamente de forma predeterminada durante la compilación, siempre que se use una plantilla de Team Build para TFS 2013 o posterior. Para la versión anterior de TFS, puede incluir un paso de compilación que invoque una de las opciones de restauración de línea de comandos anteriores. También tiene la posibilidad de migrar la plantilla de compilación a TFS 2013. Para obtener más información, vea el [tutorial sobre restauración de paquetes con Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Habilitar y deshabilitar la restauración de paquetes

La restauración de paquetes se habilita principalmente a través de **Herramientas > Opciones > Administrador de paquetes NuGet** en Visual Studio:

![Control de los comportamientos de restauración de paquetes a través de las opciones del Administrador de paquetes NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Permitir a NuGet descargar los paquetes que falten**: controla todas las formas de restauración de paquetes cambiando la opción `packageRestore/enabled` en el archivo `NuGet.Config` como se muestra aquí (`%AppData%\NuGet\NuGet.Config` en Windows, `~/.nuget/NuGet/NuGet.Config` en Mac/Linux). En Visual Studio, este valor permite que funcione el comando **Restaurar paquetes NuGet** en el menú contextual de la solución.

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

- **Comprobar automáticamente los paquetes que falten durante la compilación en Visual Studio**: controla la restauración automática cambiando el ajuste `packageRestore/automatic` en el archivo `NuGet.Config` tal y como se muestra aquí (`%AppData%\NuGet\NuGet.Config` en Windows, `~/.nuget/NuGet/NuGet.Config` en Mac/Linux). Cuando se establece esta opción, al ejecutar una compilación de Visual Studio se restauran automáticamente todos los paquetes que falten. La opción no afecta a las compilaciones que se ejecutan desde la línea de comandos con MSBuild.

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

Como referencia, vea el [archivo de configuración de NuGet: sección packageRestore](../reference/nuget-config-file.md#packagerestore-section).

En algunos casos, es posible que un desarrollador o una empresa quiera habilitar o deshabilitar la restauración de paquetes para todos los usuarios de un equipo. Para ello, agregue la misma configuración anterior al archivo de configuración global de NuGet que se encuentra en `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Después, los usuarios individuales pueden habilitar la restauración de forma selectiva cuando sea necesario en un nivel de proyecto. Vea [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) para obtener información exacta sobre cómo prioriza NuGet varios archivos de configuración.

## <a name="constraining-package-versions-with-restore"></a>Restricción de versiones de paquetes con la restauración

Cuando NuGet restaure paquetes por cualquier método, respetará las restricciones especificadas en `packages.config` o el archivo de proyecto:

- `packages.config`: especifique un intervalo de versiones en la propiedad `allowedVersion` de la dependencia. Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Por ejemplo:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- PackageReference: especifique un intervalo de versiones directamente con el número de versión de la dependencia. Por ejemplo:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

En todos los casos, use la notación que se describe en [Package versioning](../reference/package-versioning.md) (Control de versiones de paquetes).

## <a name="troubleshooting"></a>Solución de problemas

Vea [Solucionar problemas de errores de restauración de paquetes en Visual Studio](package-restore-troubleshooting.md).