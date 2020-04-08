---
title: Restauración de paquetes NuGet
description: Descripción de la manera en que NuGet restaura los paquetes de los que depende un proyecto, incluida la forma de deshabilitar la restauración y la restricción de versiones.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: c1f1957c58839ac763238938b476eb0882c56a59
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428442"
---
# <a name="restore-packages-using-package-restore"></a>Restauración de paquetes

Para promover un entorno de desarrollo más limpio y reducir el tamaño del repositorio, la **Restauración de paquetes** NuGet instala todas las dependencias del proyecto que aparecen en el archivo de proyecto o en `packages.config`. Los comandos `dotnet build` y `dotnet run` de .NET Core 2.0 y versiones posteriores llevan a cabo una restauración de paquetes automática. Visual Studio puede restaurar los paquetes automáticamente cuando compila un proyecto, de modo que usted puede restaurar los paquetes en cualquier momento a través de Visual Studio, `nuget restore`, `dotnet restore` y xbuild en Mono.

La Restauración de paquetes garantiza que todas las dependencias de un proyecto estén disponibles sin necesidad de almacenarlas en el código fuente. Si quiere configurar el repositorio de control de código fuente para excluir los archivos binarios del paquete, vea el artículo sobre los [paquetes y el control de código fuente](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Información general sobre la restauración de paquetes

La Restauración de paquetes primero instala las dependencias directas de un proyecto según sea necesario y, luego, instala todas las dependencias de los paquetes a lo largo del gráfico de dependencias completo.

Si un paquete todavía no está instalado, NuGet primero intenta recuperarlo de la [caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). Si el paquete no está en la caché, NuGet intenta descargarlo de todos los orígenes habilitados en la lista de **Herramientas** > **Opciones** > **Administrador de paquetes NuGet**  > **Orígenes de paquetes** en Visual Studio. Durante la restauración, NuGet omite el orden de los orígenes de paquetes y usa el paquete del origen que primero responda a las solicitudes. Para obtener más información sobre el comportamiento de NuGet, consulte las [configuraciones comunes de NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet no indica un error al restaurar un paquete hasta que se han comprobado todos los orígenes. En ese momento, NuGet solo informa del error del último origen de la lista. El error implica que el paquete no estaba presente en *ninguno* de los demás orígenes, aunque los errores no se muestran para cada uno de esos orígenes de forma individual.

## <a name="restore-packages"></a>Restaurar paquetes

La restauración de paquetes intenta instalar todas las dependencias de paquete en el estado correcto que coincida con las referencias del paquete en el archivo de proyecto ( *.csproj*) o el archivo *packages.config*. (En Visual Studio, las referencias aparecen en Explorador de soluciones en el nodo**Dependencias \ NuGet** o **Referencias**).

1. Si las referencias del paquete en el archivo del proyecto son correctas, use la herramienta que prefiera para restaurar los paquetes.

   - [Visual Studio](#restore-using-visual-studio) ([restauración automática](#restore-packages-automatically-using-visual-studio) o [restauración manual](#restore-packages-manually-using-visual-studio))
   - [CLI de dotnet](#restore-using-the-dotnet-cli)
   - [CLI de nuget.exe](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Si las referencias del paquete en el archivo de proyecto ( *.csproj*) o el archivo *packages.config* son incorrectos (no coinciden con el estado deseado después de la restauración de paquetes), debe instalar o actualizar los paquetes en su lugar.

   En el caso de los proyectos que usan PackageReference, después de una restauración correcta, el paquete debe estar presente en la carpeta *global-packages* y el archivo `obj/project.assets.json` se vuelve a crear. En el caso de los proyectos que usan `packages.config`, el paquete debe aparecer en la carpeta del proyecto `packages`. Ahora el proyecto debería compilarse correctamente. 

2. Tras ejecutar la restauración de paquetes, si sigue teniendo errores relacionados con los paquetes (como iconos de error en el Explorador de soluciones de Visual Studio) o faltan paquetes, es posible que deba seguir las instrucciones descritas en [Solución de errores de restauración de paquetes](package-restore-troubleshooting.md). Si lo prefiere, puede [reinstalar y actualizar los paquetes](../consume-packages/reinstalling-and-updating-packages.md).

   En Visual Studio, la consola del administrador de paquetes proporciona varias opciones flexibles para volver a instalar los paquetes. Consulte [Uso de Package-Update](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Restauración con Visual Studio

En Visual Studio en Windows, o bien:

- Restaure los paquetes de forma automática, o bien

- Restaure los paquetes de forma manual

### <a name="restore-packages-automatically-using-visual-studio"></a>Restauración automática de paquetes con Visual Studio

La restauración de paquetes se produce automáticamente al crear un proyecto a partir de una plantilla o al compilar un proyecto, según las opciones indicadas en [Habilitación y deshabilitación de la restauración de paquetes](#enable-and-disable-package-restore-in-visual-studio). En NuGet 4.0 y versiones posteriores, la restauración también se produce automáticamente al realizar cambios en un proyecto del estilo de SDK (normalmente un proyecto .NET Core o .NET Standard).

1. Habilite la restauración automática de paquetes ; para ello, elija **Herramientas** > **Opciones** > **Administrador de paquetes NuGet** y, a continuación, seleccione **Comprobar automáticamente los paquetes que faltan durante la compilación en Visual Studio** en **Restauración de paquetes**.

   En el caso de los proyectos que no son de estilo SDK, primero debe seleccionar **Permitir a NuGet descargar los paquetes que falten** para habilitar la opción de restauración automática.

1. Compile el proyecto.

   Si uno o varios paquetes no se instalan correctamente, se mostrará un icono de error en el **Explorador de soluciones**. Haga clic con el botón derecho, seleccione **Administrar paquetes NuGet** y use el **Administrador de paquetes** para desinstalar y reinstalar los paquetes afectados. Para obtener más información, consulte [Cómo volver a instalar y actualizar paquetes](../consume-packages/reinstalling-and-updating-packages.md).

   Si ve el error "Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo" o "Uno o varios paquetes de NuGet se deben restaurar, pero no pudieron restaurarse porque no se ha concedido el consentimiento", [habilite la restauración automática](#enable-and-disable-package-restore-in-visual-studio). Para los proyectos anteriores, consulte también [Migración a la restauración automática de paquetes](#migrate-to-automatic-package-restore-visual-studio). Vea también [Solución de errores de restauración de paquetes](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Restauración manual de paquetes con Visual Studio

1. Habilite la restauración de paquetes; para ello, elija **Herramientas** > **Opciones** > **Administrador de paquetes NuGet**. En las opciones de **Restauración de paquetes**, seleccione **Permitir a NuGet descargar los paquetes que falten**.

1. En el **Explorador de soluciones** haga clic con el botón derecho en la solución y seleccione **Restaurar paquetes NuGet**.

   Si uno o varios paquetes no se instalan correctamente, se mostrará un icono de error en el **Explorador de soluciones**. Haga clic con el botón derecho, seleccione **Administrar paquetes NuGet** y use el **Administrador de paquetes** para desinstalar y reinstalar los paquetes afectados. Para obtener más información, consulte [Cómo volver a instalar y actualizar paquetes](../consume-packages/reinstalling-and-updating-packages.md).

   Si ve el error "Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo" o "Uno o varios paquetes de NuGet se deben restaurar, pero no pudieron restaurarse porque no se ha concedido el consentimiento", [habilite la restauración automática](#enable-and-disable-package-restore-in-visual-studio). Para los proyectos anteriores, consulte también [Migración a la restauración automática de paquetes](#migrate-to-automatic-package-restore-visual-studio). Vea también [Solución de errores de restauración de paquetes](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Habilitación y deshabilitación de la restauración de paquetes en Visual Studio

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

### <a name="choose-default-package-management-format"></a>Elección del formato predeterminado de administración de paquetes

![Control del formato predeterminado de administración de paquetes a través de las opciones del Administrador de paquetes de NuGet](media/Restore-02-PackageFormatOptions.png)

NuGet dispone de dos formatos en los que un proyecto puede usar paquetes: [`PackageReference`](package-references-in-project-files.md) y [`packages.config`](../reference/packages-config.md). El formato predeterminado se puede seleccionar en la lista desplegable situada debajo del encabezado **Administración de paquetes**. También está disponible una opción que le preguntará cuando el primer paquete esté instalado en un proyecto.

> [!Note]
> Si un proyecto no admite ambos formatos de administración de paquetes, el formato de administración de paquetes utilizado será el que sea compatible con el proyecto y, por lo tanto, puede que no sea el conjunto predeterminado en las opciones. Además, NuGet no solicitará que se seleccione en la primera instalación del paquete, aunque la opción esté seleccionada en la ventana Opciones.
>
> Si se usa la consola del Administrador de paquetes para instalar el primer paquete en un proyecto, NuGet no solicitará la selección de formato, aunque la opción esté seleccionada en la ventana Opciones.

## <a name="restore-using-the-dotnet-cli"></a>Restauración mediante la CLI de dotnet

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Para agregar una referencia de paquete que falta al archivo del proyecto, use [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), que también ejecuta el comando `restore`.

## <a name="restore-using-the-nugetexe-cli"></a>Restauración con la CLI de nuget.exe

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> El comando `restore`no modifica un archivo del proyecto o *packages.config*. Para agregar una dependencia, puede agregar un paquete mediante la interfaz de usuario del Administrador de paquetes o la consola en Visual Studio, o bien modificar *packages.config* y, luego, ejecutar `install` o `restore`.

## <a name="restore-using-msbuild"></a>Restauración con MSBuild

Para restaurar los paquetes mostrados en el archivo del proyecto con PackageReference, utilice el comando [msbuild -t:restore](../reference/msbuild-targets.md#restore-target). Este comando está disponible solo en NuGet 4.x y versiones posteriores y en MSBuild 15.1 y versiones posteriores, que se incluyen con Visual Studio 2017 y versiones posteriores. Tanto `nuget restore` como `dotnet restore` usan este comando para los proyectos aplicables.

1. Abra un símbolo del sistema para desarrolladores (en el cuadro **Búsqueda**, escriba **Símbolo del sistema para desarrolladores**).

   Normalmente, es preferible iniciar el símbolo del sistema para desarrolladores de Visual Studio en el menú **Inicio**, ya que se configurará con todas las rutas de acceso necesarias para MSBuild.

2. Cambie a la carpeta que contiene el archivo del proyecto y escriba el siguiente comando.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Escriba el siguiente comando para recompilar el proyecto.

   ```cmd
   msbuild
   ```

   Asegúrese de que la salida de MSBuild indica que la compilación se ha completado correctamente.

## <a name="restore-using-azure-pipelines"></a>Restauración con Azure Pipelines

Al crear una definición de compilación en Azure Pipelines, incluya la tarea [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) de NuGet o [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) de .NET Core en la definición antes de cualquier tarea de compilación. Algunas plantillas de compilación incluyen la tarea restore de forma predeterminada.

## <a name="restore-using-azure-devops-server"></a>Restauración con Azure DevOps Server

Tanto Azure DevOps Server como TFS 2013 y versiones posteriores restauran los paquetes automáticamente durante la compilación, siempre y cuando use una plantilla de Team Build para TFS 2013 o versiones posteriores. En el caso de versiones anteriores de TFS, puede incluir un paso de compilación para ejecutar una opción de restauración de la línea de comandos, o bien migrar la plantilla de compilación a una versión posterior. Para obtener más información, consulte [Configurar la restauración de paquetes con Team Foundation Build](../consume-packages/team-foundation-build.md).

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

En todos los casos, use la notación que se describe en [Package versioning](../concepts/package-versioning.md) (Control de versiones de paquetes).

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

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migración a la restauración automática de paquetes (Visual Studio)

En NuGet 2.6 y versiones anteriores se permitía una restauración de paquetes integrada en MSBuild, pero eso ya no es así. (Normalmente se habilitaba haciendo clic con el botón derecho en una solución en Visual Studio y seleccionando **Habilitar restauración de paquetes NuGet**). Si el proyecto usa la restauración de paquetes integrada en MSBuild en desuso, migre a la restauración automática de paquetes.

Los proyectos que usan la restauración de paquetes integrada en MSBuild normalmente contienen una carpeta *.nuget* con tres archivos: *NuGet.config*, *nuget.exe* y *NuGet.targets*. La presencia de un archivo *NuGet.targets* determina si NuGet seguirá usando el enfoque integrado en MSBuild, por lo que este archivo debe quitarse durante la migración.

Para migrar a la restauración automática de paquetes, realice lo siguiente:

1. Cierre Visual Studio.
2. Elimine los archivos *.nuget/nuget.exe* y *.nuget/NuGet.targets*.
3. Para cada archivo del proyecto, quite el elemento `<RestorePackages>` y todas las referencias a *NuGet.targets*.

Para probar la restauración automática de paquetes, realice lo siguiente:

1. Quite la carpeta *paquetes* de la solución.
2. Abra la solución en Visual Studio e inicie una compilación.

   La restauración automática de paquetes debe descargar e instalar los paquetes de dependencia, sin agregarlos al control de código fuente.

## <a name="troubleshooting"></a>Solución de problemas

Vea [Solución de errores de restauración de paquetes](package-restore-troubleshooting.md).
