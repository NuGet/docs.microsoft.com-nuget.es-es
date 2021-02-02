---
title: Instalación y administración de paquetes NuGet mediante la consola en Visual Studio
description: Instrucciones para usar la consola del Administrador de paquetes NuGet en Visual Studio para trabajar con paquetes.
author: JonDouglas
ms.author: jodou
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 119bf32426e5cbc179c3713e60688c691e133c5d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774896"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Instalación y administración de paquetes con la consola del Administrador de paquetes en Visual Studio (PowerShell)

La consola del Administrador de paquetes NuGet le permite usar [comandos de PowerShell de NuGet](../reference/powershell-reference.md) para buscar, instalar, desinstalar y actualizar paquetes NuGet. Usar la consola es necesarios cuando la interfaz de usuario del Administrador de paquetes no ofrece una manera de realizar una operación. Para usar los comandos de la CLI `nuget.exe` en la consola, consulte la sección sobre el [uso de la CLI nuget.exe en la consola](#use-the-nugetexe-cli-in-the-console).

La consola está integrada en Visual Studio en Windows. No se incluye con Visual Studio para Mac ni con Visual Studio Code.

> [!Important]
> Los comandos que se enumeran aquí son específicos de la consola del administrador de paquetes de Visual Studio y difieren de los [comandos del módulo de Administración de paquetes](/powershell/module/packagemanagement/) que están disponibles en un entorno de PowerShell general. En concreto, cada entorno tiene comandos que no están disponibles en el otro entorno, y los comandos con el mismo nombre también pueden tener distintos argumentos específicos. Al usar la consola de Administración de paquetes en Visual Studio, se aplican los comandos y los argumentos que se documentan en este tema.

## <a name="find-and-install-a-package"></a>Búsqueda e instalación de un paquete

Por ejemplo, buscar e instalar un paquete se hace con tres pasos sencillos:

1. Abra el proyecto o la solución en Visual Studio y abra la consola con el comando **Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**.

1. Busque el paquete que quiere instalar. Si ya sabe cuál es, vaya al paso 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Ejecute el comando de instalación:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Todas las operaciones disponibles en la consola también se puede realizar con la [CLI de NuGet](../reference/nuget-exe-cli-reference.md). Sin embargo, los comandos de la consola funcionan dentro del contexto de Visual Studio y una solución o proyecto guardado y, a menudo, logran más que sus comandos de la CLI equivalentes. Por ejemplo, instalar un paquete a través de la consola agrega una referencia al proyecto, mientras que el comando de la CLI no lo hace. Por esta razón, los desarrolladores que trabajan en Visual Studio por lo general prefieren usar la consola en lugar de la CLI.

> [!Tip]
> Muchas operaciones de la consola dependen de tener una solución abierta en Visual Studio con un nombre de ruta de acceso conocido. Si tiene una solución no guardada, o no tiene ninguna solución, es posible que vea el error "La solución no está abierta ni guardada. Asegúrese de tener una solución abierta y guardada". Esto indica que la consola no puede determinar la carpeta de la solución. Al guardar una solución no guardada o al crear y guardar una solución si no hay ninguna abierta se debería corregir el error.

## <a name="opening-the-console-and-console-controls"></a>Apertura de la consola y sus controles

1. Para abrir la consola en Visual Studio, use el comando **Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**. La consola es una ventana de Visual Studio que se puede organizar y posicionar como quiera (consulte [Personalizar los diseños de ventana de Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. De manera predeterminada, los comandos de la consola operan en un proyecto y origen de paquete específico, tal como se establece en el control en la parte superior de la ventana:

    ![Controles de la consola del Administrador de paquetes para un proyecto y origen de paquete](media/PackageManagerConsoleControls1.png)

1. Si selecciona un origen de paquete o un proyecto distinto, estos valores predeterminados se cambian por los comandos subsiguientes. Para invalidar esta configuración sin cambiar los valores predeterminados, la mayoría de los comandos admiten las opciones `-Source` y `-ProjectName`.

1. Para administrar los orígenes de paquete, seleccione el icono de engranaje. Se trata de un acceso directo al cuadro de diálogo **Herramientas > Opciones > Administrador de paquetes NuGet > Orígenes de paquetes** tal como se describe en la página sobre la [interfaz de usuario del Administrador de paquetes](install-use-packages-visual-studio.md#package-sources). Además, el control ubicado a la derecha del selector de proyectos borra el contenido de la consola:

    ![Configuración de la consola del Administrador de paquetes y controles de borrado](media/PackageManagerConsoleControls2.png)

1. El botón que está más a la derecha interrumpe un comando de ejecución de larga duración. Por ejemplo, si ejecuta `Get-Package -ListAvailable -PageSize 500` se muestran los primeros 500 paquetes en el origen predeterminado (como nuget.org), lo que podría tardar varios minutos en ejecutarse.

    ![Control de detención de la consola del Administrador de paquetes](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Instala un paquete.

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Consulte [Install-Package](../reference/ps-reference/ps-ref-install-package.md).

Al instalar un paquete en la consola se llevan a cabo los mismos pasos que se describen en [¿Qué ocurre cuando se instala un paquete?](../concepts/package-installation-process.md) con las siguientes incorporaciones:

- En esta ventana, la consola muestra los términos de licencia con un contrato implícito. Si no está de acuerdo con los términos, debe desinstalar inmediatamente el paquete.
- También se agrega una referencia al paquete en el archivo del proyecto y aparece en el **Explorador de soluciones** en el nodo **Referencias**. Para ver directamente los cambios en el archivo del proyecto, debe guardar el proyecto.

## <a name="uninstall-a-package"></a>Desinstala un paquete.

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Consulte [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md). Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) para ver todos los paquetes que están instalados actualmente en el proyecto predeterminado si necesita buscar un identificador.

Al desinstalar un paquete se llevan a cabo las acciones siguientes:

- Se quitan las referencias al paquete del proyecto (y todos los formatos de administración que estén en uso). Las referencias ya no aparecen en el **Explorador de soluciones**. (Es posible que tenga que recompilar el proyecto para ver que se quitó de la carpeta **Bin**).
- Invierte los cambios realizados en `app.config` o en `web.config` cuando se instaló el paquete.
- Quita las dependencias instaladas previamente si no queda ningún paquete que las use.

## <a name="update-a-package"></a>Actualización de un paquete

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

Consulte [Get-Package](../reference/ps-reference/ps-ref-get-package.md) y [Update-Package](../reference/ps-reference/ps-ref-update-package.md)

## <a name="find-a-package"></a>Búsqueda de un paquete

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

Consulte [Find-Package](../reference/ps-reference/ps-ref-find-package.md). En Visual Studio 2013 y versiones anteriores, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) en su lugar.

## <a name="availability-of-the-console"></a>Disponibilidad de la consola

A partir de Visual Studio 2017, NuGet y el Administrador de paquetes NuGet se instalan automáticamente cuando se selecciona cualquier carga de trabajo relacionada con .NET, también puede instalarla de manera individual si activa la opción **Componentes individuales > Herramientas de código > Administrador de paquetes NuGet** en el instalador de Visual Studio.

Además, si falta el Administrador de paquetes NuGet en Visual Studio 2015 y versiones anteriores, revise **Herramientas > Extensiones y actualizaciones…** y busque la extensión Administrador de paquetes NuGet. Si no puede usar el instalador de extensiones en Visual Studio, puede descargar la extensión directamente de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

Actualmente, la consola del Administrador de paquetes no está disponible con Visual Studio para Mac. Sin embargo, hay comandos equivalentes disponibles a través de la [CLI de NuGet](../reference/nuget-exe-CLI-reference.md). Visual Studio para Mac sí tiene una interfaz de usuario para administrar paquetes de NuGet. Consulte [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough).

La consola del Administrador de paquetes no está incluida en Visual Studio Code.

## <a name="extend-the-package-manager-console"></a>Extensión de la consola del Administrador de paquetes

Algunos paquetes instalan comandos nuevos para la consola. Por ejemplo, `MvcScaffolding` crea comandos como `Scaffold` que se muestra a continuación, el que genera vistas y controladores de MVC de ASP.NET:

![Instalación y uso de MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Configuración de un perfil de PowerShell de NuGet

Un perfil de PowerShell le permite usar los comandos de uso común disponibles cada vez que use PowerShell. NuGet admite un perfil específico de NuGet que habitualmente se encuentra en esta ubicación:

*%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1*

Para buscar el perfil, escriba `$profile` en la consola:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Para más detalles, consulte [Perfiles de Windows PowerShell](/previous-versions//bb613488(v=vs.85)).

## <a name="use-the-nugetexe-cli-in-the-console"></a>Uso de la CLI nuget.exe en la consola

Para que la [CLI `nuget.exe`](../reference/nuget-exe-cli-reference.md) esté disponible en la consola del Administrador de paquetes, instale el paquete [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) desde la consola:

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
