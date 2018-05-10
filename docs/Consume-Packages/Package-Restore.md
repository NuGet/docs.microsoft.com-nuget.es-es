---
title: Restauración de paquetes NuGet
description: Una descripción de cómo NuGet restaura paquetes de los que depende un proyecto, incluido cómo deshabilitar la restauración y la restricción de versiones.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 6a8a2f1c5ced956f18b623f112756cdd2fab22f5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="package-restore"></a>Restauración de paquetes

Para promover un entorno de desarrollo más limpio y reducir el tamaño del repositorio, **Restauración de paquetes** NuGet instala todas las dependencias del proyecto tal y como aparecen en el archivo de proyecto o en `packages.config`. Visual Studio puede restaurar los paquetes automáticamente al compilar un proyecto. Los comandos `dotnet build` y `dotnet run`(.NET Core 2.0 y versiones posteriores) también realizan una restauración automática. También puede restaurar los paquetes siempre que quiera a través de Visual Studio, `nuget restore`, `dotnet restore` y xbuild en Mono.

La restauración de paquetes se asegura de que todas las dependencia de un proyecto estén disponibles sin almacenar los paquetes de control de código fuente. Vea [Paquetes y control de código fuente](../consume-packages/packages-and-source-control.md) sobre cómo configurar el repositorio para excluir los archivos binarios del paquete.

## <a name="package-restore-overview"></a>Información general sobre restauración de paquetes

Al restaurar paquetes, se instalan primero las dependencias directas de un proyecto según sea necesario y luego se instalan todas las dependencias de los paquetes a lo largo del gráfico de dependencias completo.

Si un paquete no está ya instalado, NuGet primero intenta recuperarlo desde la [caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). Si el paquete no está en la memoria caché, NuGet intenta descargarlo y almacenarlo en caché en todos los orígenes habilitados (vea [Configuración del comportamiento de NuGet](Configuring-NuGet-Behavior.md); los orígenes también aparecen en la lista **Herramientas > Opciones > Administrador de paquetes NuGet > Orígenes del paquete** en Visual Studio). Durante la restauración, NuGet omite el orden de los orígenes de paquetes y usará el paquete del origen que primero responda a las solicitudes.

> [!Note]
> NuGet no indica un error al restaurar un paquete hasta que se han comprobado todos los orígenes. En ese momento, NuGet solo informa del error del último origen de la lista. El error implica que el paquete no estaba presente en *ninguno* de los otros orígenes, aunque los errores no se muestran para cada uno de esos orígenes de forma individual.

La restauración de paquetes se activa de las maneras siguientes:

- **CLI de dotnet**: use el comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura los paquetes incluidos en el archivo de proyecto (vea [PackageReference](../consume-packages/package-references-in-project-files.md)). Con .NET Core 2.0 y versiones posteriores, la restauración se realiza automáticamente con `dotnet build` y `dotnet run`.

- **Interfaz de usuario del Administrador de paquetes (Visual Studio en Windows)**: los paquetes se restauran automáticamente al crear un proyecto a partir de una plantilla y al compilar un proyecto (sujeto a la opción descrita en [Habilitar y deshabilitar la restauración de paquetes](#enabling-and-disabling-package-restore)). En NuGet 4.0 y versiones posteriores, la restauración también se produce automáticamente al realizar cambios en un proyecto basado en el SDK de .NET Core.

    Para la restauración manual, haga clic con el botón derecho en la solución en el Explorador de soluciones y seleccione **Restaurar paquetes NuGet**. Si uno o varios paquetes siguen sin estar instalados correctamente (lo que significa que el Explorador de soluciones muestra un icono de error), use la interfaz de usuario del Administrador de paquetes para desinstalar y reinstalar los paquetes afectados. Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md)

    Si ve el error "Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo" o "Uno o varios paquetes de NuGet se deben restaurar, pero no pudieron restaurarse porque no se ha concedido el consentimiento", active la restauración automática mediante las instrucciones descritas en [Habilitar y deshabilitar la restauración de paquetes](#enabling-and-disabling-package-restore). Vea también [Solución de errores de restauración de paquetes](Package-restore-troubleshooting.md).

- **CLI de NuGet**: use el comando [nuget restore](../tools/cli-ref-restore.md), que restaura los paquetes incluidos en el archivo de proyecto o en `packages.config`. También puede especificar un archivo de solución.

- **MSBuild**: use el comando [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), que restaura los paquetes incluidos en el archivo de proyecto (solo PackageReference). Disponible solo en 4.x y versiones posteriores y MSBuild 15.1 y versiones posteriores, que se incluyen con Visual Studio de 2017. `nuget restore` y `dotnet restore` usan este comando para los proyectos aplicables.

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

En algunos casos, es posible que un desarrollador o una empresa quiera habilitar o deshabilitar la restauración de paquetes para todos los usuarios de un equipo. Para ello, agregue la misma configuración anterior al archivo de configuración global de NuGet que se encuentra en `%ProgramData%\NuGet\Config` (Windows, posiblemente en una carpeta `\{IDE}\{Version}\{SKU}\` específica para Visual Studio) o `~/.local/share` (Mac/Linux). Después, los usuarios individuales pueden habilitar la restauración de forma selectiva cuando sea necesario en un nivel de proyecto. Vea [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) para obtener información exacta sobre cómo prioriza NuGet varios archivos de configuración.

> [!Important]
> Si edita el valor `packageRestore` directamente en `nuget.config`, debe reiniciar Visual Studio para que el cuadro de diálogo de opciones muestre los valores actuales.

## <a name="constraining-package-versions-with-restore"></a>Restricción de versiones de paquetes con la restauración

Cuando NuGet restaure paquetes por cualquier método, respetará las restricciones especificadas en `packages.config` o el archivo de proyecto:

- `packages.config`: especifique un intervalo de versiones en la propiedad `allowedVersion` de la dependencia. Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Por ejemplo:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Archivo de proyecto (PackageReference): especifique un intervalo de versiones directamente con el número de versión de la dependencia. Por ejemplo:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

En todos los casos, use la notación que se describe en [Package versioning](../reference/package-versioning.md) (Control de versiones de paquetes).

## <a name="forcing-restore-from-package-sources"></a>Forzamiento de la restauración a partir de orígenes de paquetes

De forma predeterminada, las operaciones de restauración de NuGet usan paquetes de las carpetas *global-packages* y *http-cache*, que se describen en [Administración de paquetes globales y carpetas de caché](managing-the-global-packages-and-cache-folders.md).

Para evitar el uso de la carpeta *global-packages*, realice una de las siguientes acciones:

- Borre la carpeta con `nuget locals global-packages -clear` o `dotnet nuget locals global-packages --clear`.
- Cambie temporalmente la ubicación de la carpeta *global-packages* antes de la operación de restauración con uno de los métodos siguientes:
  - Establezca la variable de entorno NUGET_PACKAGES en otra carpeta.
  - Crear un `NuGet.Config` archivo que establezca `globalPackagesFolder` (si se usa PackageReference) o `repositoryPath` (si se usa `packages.config`) en otra carpeta (vea [valores de configuración](../reference/nuget-config-file.md#config-section)).
  - Solo MSBuild: especifique otra carpeta con la propiedad `RestorePackagesPath`.

Para evitar el uso de la memoria caché para los orígenes HTTP, realice una de las siguientes acciones:

- Use la opción `-NoCache` con `nuget restore` o la opción `--no-cache` con `dotnet restore`. Estas opciones no afectan a las operaciones de restauración a través del la consola o la interfaz de usuario del Administrador de paquetes de Visual Studio.
- Borre la memoria caché con `nuget locals http-cache -clear` o `dotnet nuget locals http-cache --clear`.
- Establezca temporalmente la variable de entorno NUGET_HTTP_CACHE_PATH en otra carpeta.

## <a name="troubleshooting"></a>Solución de problemas

Vea [Solucionar problemas de errores de restauración de paquetes en Visual Studio](package-restore-troubleshooting.md).