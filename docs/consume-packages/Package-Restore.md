---
title: Restauración de paquetes NuGet
description: Descripción de la manera en que NuGet restaura los paquetes de los que depende un proyecto, incluida la forma de deshabilitar la restauración y la restricción de versiones.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 3b64c035886818496339fe1bdd8f9abce060278a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467796"
---
# <a name="package-restore"></a>Restauración de paquetes

Para promover un entorno de desarrollo más limpio y reducir el tamaño del repositorio, la **Restauración de paquetes** NuGet instala todas las dependencias del proyecto que aparecen en el archivo de proyecto o en `packages.config`. Los comandos `dotnet build` y `dotnet run` de .NET Core 2.0 y versiones posteriores llevan a cabo una restauración de paquetes automática. Visual Studio puede restaurar los paquetes automáticamente cuando compila un proyecto, de modo que usted puede restaurar los paquetes en cualquier momento a través de Visual Studio, `nuget restore`, `dotnet restore` y xbuild en Mono.

La Restauración de paquetes garantiza que todas las dependencias de un proyecto estén disponibles sin necesidad de almacenarlas en el código fuente. Si quiere configurar el repositorio de control de código fuente para excluir los archivos binarios del paquete, vea el artículo sobre los [paquetes y el control de código fuente](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Información general sobre la restauración de paquetes

La Restauración de paquetes primero instala las dependencias directas de un proyecto según sea necesario y, luego, instala todas las dependencias de los paquetes a lo largo del gráfico de dependencias completo.

Si un paquete todavía no está instalado, NuGet primero intenta recuperarlo de la [caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). Si el paquete no está en la caché, NuGet intenta descargarlo de todos los orígenes habilitados en la lista de **Herramientas** > **Opciones** > **Administrador de paquetes NuGet**  > **Orígenes de paquetes** en Visual Studio. Durante la restauración, NuGet omite el orden de los orígenes de paquetes y usa el paquete del origen que primero responda a las solicitudes. Para obtener más información sobre el comportamiento de NuGet, consulte las [configuraciones comunes de NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet no indica un error al restaurar un paquete hasta que se han comprobado todos los orígenes. En ese momento, NuGet solo informa del error del último origen de la lista. El error implica que el paquete no estaba presente en *ninguno* de los demás orígenes, aunque los errores no se muestran para cada uno de esos orígenes de forma individual.

Puede desencadenar la Restauración de paquetes de cualquiera de las maneras siguientes:

- **CLI de dotnet**: use el comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) para restaurar los paquetes incluidos en el archivo de proyecto con [PackageReference](../consume-packages/package-references-in-project-files.md). Con .NET Core 2.0 y versiones posteriores, la restauración se realiza automáticamente con los comandos `dotnet build` y `dotnet run`.  

- **Administrador de paquetes**: en Visual Studio en Windows, la Restauración de paquetes se realiza automáticamente al crear un proyecto a partir de una plantilla o un proyecto de compilación, según las opciones indicadas en [Habilitación y deshabilitación de la Restauración de paquetes](#enable-and-disable-package-restore). En NuGet 4.0 y versiones posteriores, la restauración también se produce automáticamente al realizar cambios en un proyecto basado en el SDK de .NET Core.

    Para restaurar los paquetes de forma manual, haga clic con el botón derecho en la solución en el **Explorador de soluciones** y seleccione **Restaurar paquetes NuGet**. Si uno o varios paquetes no se instalan correctamente, se mostrará un icono de error en el **Explorador de soluciones**. Haga clic con el botón derecho, seleccione **Administrar paquetes NuGet** y use el **Administrador de paquetes** para desinstalar y reinstalar los paquetes afectados. Para obtener más información, consulte [Cómo volver a instalar y actualizar paquetes](../consume-packages/reinstalling-and-updating-packages.md).

    Si ve el error "Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo" o "Uno o varios paquetes de NuGet se deben restaurar, pero no pudieron restaurarse porque no se ha concedido el consentimiento", [habilite la restauración automática](#enable-and-disable-package-restore). Vea también [Solución de errores de restauración de paquetes](Package-restore-troubleshooting.md).

- **CLI de nuget.exe**: use el comando [nuget restore](../tools/cli-ref-restore.md) para restaurar los paquetes incluidos en un archivo de proyecto o solución, o en `packages.config`. 

- **MSBuild**: use el comando [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) para restaurar los paquetes incluidos en el archivo de proyecto con PackageReference. Este comando está disponible solo en NuGet 4.x y versiones posteriores y en MSBuild 15.1 y versiones posteriores, que se incluyen con Visual Studio 2017 y versiones posteriores. Tanto `nuget restore` como `dotnet restore` usan este comando para los proyectos aplicables.

- **Azure Pipelines**: al crear una definición de compilación en Azure Pipelines, incluya la tarea [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) de NuGet o [restore](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages) de .NET Core en la definición antes de cualquier tarea de compilación. Algunas plantillas de compilación incluyen la tarea restore de forma predeterminada.

- **Azure DevOps Server**: tanto Azure DevOps Server como TFS 2013 y versiones posteriores restauran los paquetes automáticamente durante la compilación, siempre y cuando use una plantilla de Team Build para TFS 2013 o versiones posteriores. En el caso de versiones anteriores de TFS, puede incluir un paso de compilación para ejecutar una opción de restauración de la línea de comandos, o bien migrar la plantilla de compilación a una versión posterior. Para obtener más información, consulte [Configurar la restauración de paquetes con Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore"></a>Habilitación y deshabilitación de la Restauración de paquetes

En Visual Studio, la Restauración de paquetes se controla principalmente a través de **Herramientas** > **Opciones** > **Administrador de paquetes NuGet**:

![Control de la Restauración de paquetes a través de las opciones del Administrador de paquetes NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Permitir a NuGet descargar los paquetes que falten** controla todas las formas de restauración de paquetes mediante la modificación de la opción `packageRestore/enabled` en la [sección packageRestore](../reference/nuget-config-file.md#packagerestore-section) del archivo `NuGet.Config`, en `%AppData%\NuGet\` en Windows y en `~/.nuget/NuGet/` en Mac/Linux. Esta opción también habilita el comando **Restaurar paquetes NuGet** en el menú contextual de la solución en Visual Studio.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > Para invalidar de forma global la opción `packageRestore/enabled`, establezca la variable de entorno **EnableNuGetPackageRestore** con un valor de True o False antes de iniciar Visual Studio o una compilación.

- **Comprobar automáticamente los paquetes que falten durante la compilación en Visual Studio** controla la restauración automática mediante la modificación del ajuste `packageRestore/automatic` en la [sección packageRestore](../reference/nuget-config-file.md#packagerestore-section) del archivo `NuGet.Config`. Cuando esta opción se establece en True, al ejecutar una compilación de Visual Studio se restauran automáticamente todos los paquetes que falten. Esta configuración no afecta a las compilaciones que se ejecutan desde la línea de comandos de MSBuild.

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

Para habilitar o deshabilitar la Restauración de paquetes para todos los usuarios de un equipo, un desarrollador o una empresa pueden agregar los valores de configuración al archivo global `nuget.config`. El archivo global `nuget.config` se encuentra en Windows en `%ProgramData%\NuGet\Config`, a veces en una carpeta `\{IDE}\{Version}\{SKU}\` determinada de Visual Studio, o en Mac/Linux en `~/.local/share`. Después, los usuarios individuales pueden habilitar la restauración de forma selectiva cuando sea necesario en un nivel de proyecto. Para obtener más información sobre la manera en que NuGet prioriza varios archivos de configuración, consulte las [configuraciones comunes de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Si edita el valor `packageRestore` directamente en `nuget.config`, debe reiniciar Visual Studio para que en el cuadro de diálogo **Opciones** se muestren los valores actuales.

## <a name="constrain-package-versions-with-restore"></a>Restricción de versiones de paquetes con la restauración

Cuando NuGet restaure paquetes con cualquier método, respetará las restricciones que haya especificado en `packages.config` o en el archivo de proyecto:

- En `packages.config`, puede especificar un intervalo de versiones en la propiedad `allowedVersion` de la dependencia. Consulte [Restringir las versiones de actualización](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) para obtener más información. Por ejemplo:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- En un archivo de proyecto, puede usar PackageReference para especificar directamente el intervalo de una dependencia. Por ejemplo:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

En todos los casos, use la notación que se describe en [Package versioning](../reference/package-versioning.md) (Control de versiones de paquetes).

## <a name="force-restore-from-package-sources"></a>Restauración forzada a partir de orígenes de paquetes

De forma predeterminada, las operaciones de restauración de NuGet usan paquetes de las carpetas *global-packages* y *http-cache*, que se describen en [Administración de las carpetas de paquetes globales, de caché y temporales](managing-the-global-packages-and-cache-folders.md).

Para evitar el uso de la carpeta *global-packages*, realice una de las siguientes acciones:

- Borre la carpeta con `nuget locals global-packages -clear` o `dotnet nuget locals global-packages --clear`.
- Cambie temporalmente la ubicación de la carpeta *global-packages* antes de la operación de restauración con uno de los métodos siguientes:
  - Establezca la variable de entorno NUGET_PACKAGES en otra carpeta.
  - Cree un archivo `NuGet.Config` que establezca `globalPackagesFolder` (si usa PackageReference) o `repositoryPath` (si usa `packages.config`) en otra carpeta. Para obtener más información, vea los [valores de configuración](../reference/nuget-config-file.md#config-section).
  - Solo MSBuild: especifique otra carpeta con la propiedad `RestorePackagesPath`.

Para evitar el uso de la memoria caché para los orígenes HTTP, realice una de las siguientes acciones:

- Use la opción `-NoCache` con `nuget restore`, o bien la opción `--no-cache` con `dotnet restore`. Estas opciones no afectan a las operaciones de restauración mediante la consola o el Administrador de paquetes de Visual Studio.
- Borre la memoria caché con `nuget locals http-cache -clear` o `dotnet nuget locals http-cache --clear`.
- Establezca temporalmente la variable de entorno NUGET_HTTP_CACHE_PATH en otra carpeta.

## <a name="troubleshooting"></a>Solución de problemas

Vea [Solución de errores de restauración de paquetes](package-restore-troubleshooting.md).
