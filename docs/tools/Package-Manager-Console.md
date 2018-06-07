---
title: Guía de consola de administrador de paquetes de NuGet
description: Instrucciones para usar la consola de administrador de paquetes de NuGet en Visual Studio para trabajar con paquetes.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 06c525cab2dac61c92c4596533173f1d93493d9a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817663"
---
# <a name="package-manager-console"></a>Consola del Administrador de paquetes

La consola de administrador de paquetes de NuGet se compila en Visual Studio en Windows 2012 y versiones posteriores. (No se incluye con Visual Studio para Mac o código de Visual Studio).

La consola le permite usar [comandos de NuGet PowerShell](../tools/powershell-reference.md) para buscar, instalar, desinstalar y actualizar paquetes de NuGet. Es necesario en casos donde la UI del Administrador de paquetes no proporciona una manera de realizar una operación mediante la consola. Usar `nuget.exe` comandos en la consola, consulte [mediante la CLI nuget.exe en la consola de](#using-the-nugetexe-cli-in-the-console).

Por ejemplo, la búsqueda e instalación de un paquete se realiza con tres sencillos pasos:

1. Abra el proyecto o la solución en Visual Studio y abra la consola utilizando la **Herramientas > Administrador de paquetes de NuGet > Package Manager Console** comando.

1. Busque el paquete que desea instalar. Si ya sabe esto, vaya al paso 3.

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
> Todas las operaciones que están disponibles en la consola también pueden realizarse con el [NuGet CLI](../tools/nuget-exe-cli-reference.md). Sin embargo, comandos de la consola operan dentro del contexto de Visual Studio y una proyecto o solución guardada y a menudo llevar más de sus comandos CLI equivalente. Por ejemplo, instalando un paquete mediante la consola de, agrega una referencia al proyecto, mientras que el comando CLI no. Por este motivo, los desarrolladores que trabajan en Visual Studio normalmente prefieren mediante la consola de la CLI.

> [!Tip]
> Muchas operaciones de consola dependen de tener una solución abierta en Visual Studio con un nombre de ruta de acceso conocida. Si tiene una solución que no haya guardado o no hay ninguna solución, puede ver el error, "solución no está abierta o no guardada. Asegúrese de que dispone de una solución abierta y guardada." Esto indica que la consola no puede determinar la carpeta de soluciones. Guardar una solución que no haya guardado, o crear y guardar una solución si no dispone de uno abierto, debe corregir el error.

## <a name="opening-the-console-and-console-controls"></a>Abra la consola y los controles de la consola

1. Abra la consola en Visual Studio mediante el **Herramientas > Administrador de paquetes de NuGet > Package Manager Console** comando. La consola es una ventana de Visual Studio que se pueden organizan y coloca sin embargo igual (vea [personalizar diseños de ventana de Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. De forma predeterminada, los comandos de consola operan en un origen de paquete específico y un proyecto como se establece en el control en la parte superior de la ventana:

    ![Controles de la consola de administrador de paquetes de origen del paquete y proyecto](media/PackageManagerConsoleControls1.png)

1. Al seleccionar un origen de otro paquete o proyecto cambia los valores predeterminados para los comandos siguientes. Admite la mayoría de los comandos anular estos valores sin cambiar los valores predeterminados, `-Source` y `-ProjectName` opciones.

1. Para administrar orígenes de paquetes, seleccione el icono de engranaje. Se trata de un acceso directo a la **Herramientas > Opciones > Administrador de paquetes de NuGet > orígenes de paquetes** cuadro de diálogo tal como se describe en el [UI del Administrador de paquetes](package-manager-ui.md#package-sources) página. Además, el control a la derecha del selector de proyecto borra el contenido de la consola:

    ![Configuración de la consola de administrador de paquetes y desactive los controles](media/PackageManagerConsoleControls2.png)

1. El botón situado interrumpe un comando de ejecución prolongada. Por ejemplo, ejecutar `Get-Package -ListAvailable -PageSize 500` enumera los paquetes de 500 principales en el origen predeterminado (por ejemplo, nuget.org), que puede tardar varios minutos en ejecutarse.

    ![Control de detención de la consola de administrador de paquetes](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Instalar un paquete

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Vea [Install-Package](../tools/ps-ref-install-package.md).

Instalar un paquete en la consola realiza los mismos pasos tal como se describe en [¿qué ocurre cuando se instala un paquete](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), con las siguientes adiciones:

- La consola muestra los términos de licencia aplicables en su ventana con un acuerdo implícito. Si no acepta los términos, debe desinstalar el paquete inmediatamente.
- También una referencia al paquete se agrega al archivo de proyecto y aparece en **el Explorador de soluciones** en el **referencias** nodo, debe guardar el proyecto para ver los cambios en el archivo de proyecto directamente.

## <a name="uninstalling-a-package"></a>Desinstalar un paquete

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Vea [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Use [Get-Package](../tools/ps-ref-get-package.md) para ver todos los paquetes instalados actualmente en el proyecto predeterminado si fuese necesario encontrar un identificador.

Desinstalar un paquete realiza las siguientes acciones:

- Quita las referencias a los paquetes del proyecto (y cualquier formato de administración está en uso). Las referencias ya no aparecen en **el Explorador de soluciones**. (Es posible que deba volver a generar el proyecto para verlo quita de la **Bin** carpeta.)
- Invierte los cambios realizados en `app.config` o `web.config` cuando se instaló el paquete.
- Quita instaladas con anterioridad dependencias si no hay paquetes restantes usan esas dependencias.

## <a name="updating-a-package"></a>Actualizar un paquete

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

Vea [Get-Package](../tools/ps-ref-get-package.md) y [paquete de actualización](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Buscar un paquete

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

Vea [Find-Package](../tools/ps-ref-find-package.md). En Visual Studio 2013 y versiones anteriores, utilice [Get-Package](../tools/ps-ref-get-package.md) en su lugar.

## <a name="availability-of-the-console"></a>Disponibilidad de la consola

En Visual Studio 2017 NuGet y el Administrador de paquetes de NuGet se instalan automáticamente cuando se selecciona cualquiera. Cargas de trabajo relacionados con NET; También puede instalarlo por separado mediante la comprobación de la **componentes individuales > herramientas de código > Administrador de paquetes de NuGet** opción en el programa de instalación de Visual Studio de 2017.

Además, compruebe si faltan el Administrador de paquetes de NuGet en Visual Studio 2015 y versiones anteriores, **Herramientas > extensiones y actualizaciones...**  y busque la extensión del Administrador de paquetes de NuGet. Si no puede usar el instalador de extensiones de Visual Studio, puede descargar la extensión directamente desde [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

La consola de administrador de paquetes no está actualmente disponible con Visual Studio para Mac. Los comandos equivalentes, sin embargo, están disponibles a través de la [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio para Mac tiene una interfaz de usuario para administrar paquetes de NuGet. Vea [paquete NuGet unos incluidos en el proyecto](/visualstudio/mac/nuget-walkthrough).

La consola de administrador de paquetes no se incluye con Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Extender la consola de administrador de paquetes

Algunos paquetes instalarán nuevos comandos para la consola. Por ejemplo, `MvcScaffolding` crea comandos como `Scaffold` se muestra a continuación, lo cual genera ASP.NET MVC controladores y vistas:

![Instalar y usar MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Cómo configurar un perfil de NuGet PowerShell

Un perfil de PowerShell le permite disponer de los comandos usados con frecuencia siempre que utilice PowerShell. NuGet es compatible con un perfil específico de NuGet que normalmente se encuentran en la siguiente ubicación:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Para encontrar el perfil, escriba `$profile` en la consola:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Para obtener más información, consulte [perfiles de Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Uso de la CLI nuget.exe en la consola de

Para realizar la [ `nuget.exe` CLI](nuget-exe-cli-reference.md) disponibles en la consola de administrador de paquetes, instale el [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) paquete desde la consola:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
