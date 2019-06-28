---
title: Instalar y administrar paquetes de NuGet en Visual Studio
description: Instrucciones para usando la UI de administrador de paquetes de NuGet en Visual Studio para trabajar con paquetes de NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426243"
---
# <a name="install-and-manage-packages-in-visual-studio"></a>Instalar y administrar paquetes en Visual Studio

La UI Administrador de paquetes de NuGet en Visual Studio en Windows le permite instalar, desinstalar y actualizar paquetes de NuGet en proyectos y soluciones con facilidad. Para obtener la experiencia en Visual Studio para Mac, consulte [incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough). El Administrador de paquetes de UI no se incluye con Visual Studio Code.

> [!NOTE]
> Compruebe si faltan el Administrador de paquetes de NuGet en Visual Studio 2015, **Herramientas > extensiones y actualizaciones...**  y busque el *Administrador de paquetes de NuGet* extensión. Si no puede usar el instalador de extensiones de Visual Studio, descargue la extensión directamente desde [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> A partir de Visual Studio 2017, NuGet y el Administrador de paquetes de NuGet se instalan automáticamente con cualquiera. Cargas de trabajo relacionados con la red. Instálelo individualmente seleccionando el **componentes individuales > herramientas de código > Administrador de paquetes de NuGet** opción en el instalador de Visual Studio.

## <a name="finding-and-installing-a-package"></a>Búsqueda e instalación de un paquete

1. En **el Explorador de soluciones**, haga clic en cualquiera **referencias** o un proyecto y seleccione **administrar paquetes NuGet...** .

    ![Administrar la opción de menú de paquetes de NuGet](media/ManagePackagesUICommand.png)

1. El **examinar** pestaña muestra los paquetes por popularidad del origen seleccionado actualmente (vea [orígenes de paquetes](#package-sources)). Busque un paquete específico mediante el cuadro de búsqueda en la parte superior izquierda. Seleccione un paquete de la lista para mostrar su información, lo cual habilita también el **instalar** botón junto con una lista desplegable de selección de versión.

    ![Administrar la ficha cuadro de diálogo Examinar de paquetes de NuGet](media/Search.png)

1. Seleccione la versión deseada de la lista desplegable y seleccione **instalar**. Visual Studio instala el paquete y sus dependencias en el proyecto. Se le pedirá que acepte los términos de licencia. Cuando se complete la instalación, los paquetes agregados aparecen en la **instalado** ficha. Los paquetes también se enumeran en la **referencias** nodo del explorador de soluciones, que indica que puede hacer referencia a ellas en el proyecto con `using` instrucciones.

    ![Referencias en el Explorador de soluciones](media/References.png)

> [!Tip]
> Para incluir versiones preliminares en la búsqueda y para que las versiones preliminares disponibles en la versión lista desplegable, seleccione el **incluir versión preliminar** opción.

## <a name="uninstalling-a-package"></a>Al desinstalar un paquete

1. En **el Explorador de soluciones**, haga clic en cualquiera **referencias** o el proyecto que desee y seleccione **administrar paquetes NuGet...** .
1. Seleccione el **instalado** ficha.
1. Seleccione el paquete para desinstalar (mediante la búsqueda para filtrar la lista si es necesario) y seleccione **desinstalar**.

    ![Al desinstalar un paquete](media/UninstallPackage.png)

1. Tenga en cuenta que el **incluir versión preliminar** y **origen del paquete** controles no tienen ningún efecto cuando se desinstala los paquetes.

## <a name="updating-a-package"></a>Actualizar un paquete

1. En **el Explorador de soluciones**, haga clic en cualquiera **referencias** o el proyecto que desee y seleccione **administrar paquetes NuGet...** . (En proyectos de sitios web, haga clic en el **Bin** carpeta.)
1. Seleccione el **actualizaciones** pestaña para ver los paquetes que tienen actualizaciones disponibles desde los orígenes del paquete seleccionado. Seleccione **incluir versión preliminar** para incluir paquetes de versión preliminar en la lista de actualizaciones.
1. Seleccione el paquete para actualizar, seleccione la versión deseada de la lista desplegable de la derecha y seleccione **actualizar**.

    ![Actualizar un paquete](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Para algunos paquetes, el **actualización** botón está deshabilitado y aparece un mensaje que indica que se "hace referencia implícitamente mediante un SDK" (o "Compatibilidad con AutoReferenced"). Este mensaje indica que el paquete forma parte de un marco de trabajo o SDK más grande y no se debe actualizar de forma independiente. (Estos paquetes internamente se marcan con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Por ejemplo, `Microsoft.NETCore.App` es parte del SDK de .NET Core y la versión del paquete no es igual que la versión de framework en tiempo de ejecución utilizado por la aplicación. Deberá [actualizar su instalación de .NET Core](https://aka.ms/dotnet-download) para obtener nuevas versiones del tiempo de ejecución de ASP.NET Core y .NET Core. [Consulte este documento para obtener más detalles sobre los metapaquetes de .NET Core y control de versiones](/dotnet/core/packages). Esto se aplica a los siguientes paquetes usados:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Paquete de ejemplo marcada como implícitamente las referencias o compatibilidad con AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Para actualizar varios paquetes a sus versiones más recientes, selecciónelos en la lista y seleccione el **actualizar** botón encima de la lista.
1. También puede actualizar un paquete individual desde la **instalado** ficha. En este caso, los detalles para el paquete incluyen un selector de versión (sujeto a la **incluir versión preliminar** opción) y un **actualización** botón.

## <a name="managing-packages-for-the-solution"></a>Administración de paquetes para la solución

Administración de paquetes para una solución es un medio cómodo para trabajar con varios proyectos simultáneamente.

1. Seleccione el **Herramientas > Administrador de paquetes NuGet > Administrar paquetes de NuGet para la solución...**  menú de comandos, o haga clic en la solución y seleccione **administrar paquetes NuGet...** :

    ![Administrar paquetes de NuGet para la solución](media/ManagePackagesSolutionUICommand.png)

1. Al administrar los paquetes para la solución, la interfaz de usuario le permite seleccionar los proyectos que se ven afectados por las operaciones:

    ![Selector de proyecto al administrar los paquetes para la solución](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Consolidar pestaña

Normalmente los desarrolladores consideran mala práctica usar diferentes versiones del mismo paquete de NuGet en los distintos proyectos en la misma solución. Si decide administrar los paquetes para una solución, el Administrador de paquetes de UI proporciona una **consolidar** ficha en el que puede ver fácilmente donde diferentes proyectos de la solución usa los paquetes con números de versión distintos:

![Pestaña consolidar de interfaz de usuario de administrador de paquetes](media/ConsolidateTab.png)

En este ejemplo, el proyecto ClassLibrary1 usa Entity Framework de la 6.2.0, mientras que usa EntityFramework 6.1.0 ConsoleApp1. Para consolidar las versiones del paquete, haga lo siguiente:

- Seleccione los proyectos que se actualizará en la lista de proyectos.
- Seleccione la versión que se usará en todos los proyectos de la **versión** control, como la 6.2.0 EntityFramework.
- Seleccione el **instalar** botón.

El Administrador de paquetes se instala la versión del paquete seleccionado en todos los proyectos seleccionados, después de que el paquete ya no aparece en el **consolidar** ficha.

## <a name="package-sources"></a>Orígenes de paquetes

Para cambiar el origen de los que Visual Studio obtiene los paquetes, seleccione uno en el selector de origen:

![Selector de origen de paquete en el Administrador de paquetes de interfaz de usuario](media/PackageSourceDropDown.png)

Para administrar orígenes de paquetes:

1. Seleccione el **configuración** icono en la UI del Administrador de paquetes que se describen a continuación o usar el **Herramientas > opciones** de comandos y desplácese hasta **Administrador de paquetes de NuGet**:

    ![Icono de configuración de la interfaz de usuario Administrador de paquetes](media/PackageSourceSettings.png)

1. Seleccione el **orígenes de paquetes** nodo:

    ![Opciones de orígenes de paquetes](media/options.png)

1. Para agregar un origen, seleccione **+** , edite el nombre, escriba la dirección URL o ruta de acceso en el **origen** control y seleccione **actualización**. El origen aparece ahora en el selector de lista desplegable.
1. Para cambiar un origen del paquete, selecciónelo, realice modificaciones en el **nombre** y **origen** cuadros y seleccione **actualización**.
1. Para deshabilitar un origen del paquete, desactive la casilla a la izquierda del nombre de la lista.
1. Para quitar un origen del paquete, selecciónelo y, a continuación, seleccione el **X** botón.
1. Usar arriba y flecha abajo botones no cambian el orden de prioridad de los orígenes del paquete. Visual Studio omite el orden de los orígenes de paquetes, mediante el paquete del origen que primero responda a las solicitudes. Para obtener más información, consulte [restauración del paquete](../consume-packages/package-restore.md).

> [!Tip]
> Si se vuelve a aparecer en un origen de paquete después de eliminarlo, pueden mostrarse en un nivel de equipo o el nivel de usuario `NuGet.Config` archivos. Consulte [configuraciones comunes NuGet](../consume-packages/configuring-nuget-behavior.md) para la ubicación de estos archivos, a continuación, quitar el origen de editar manualmente los archivos o usando el [nuget orígenes comando](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Controlan las opciones del Administrador de paquetes

Cuando se selecciona un paquete, el Administrador de paquetes de UI muestra un pequeño expandible **opciones** control debajo el selector de versión (se muestra aquí tanto contraen y expanden). Tenga en cuenta que para algunos proyectos, tipos, solo el **Mostrar ventana de vista previa** opción se proporciona.

![Opciones del Administrador de paquetes](media/PackageManagerUIOptions.png)

Las siguientes secciones explican estas opciones.

### <a name="show-preview-window"></a>Mostrar ventana de vista previa

Cuando se selecciona, una ventana modal muestra que las dependencias de un paquete elegido antes de instalar el paquete:

![Cuadro de diálogo de vista previa de ejemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Instalar y actualizar las opciones

(No disponible para todos los tipos de proyecto).

**Comportamiento de dependencia** configura cómo NuGet decide qué versiones de los paquetes dependientes para instalar:

- *Pasar por alto las dependencias* omite instalar las dependencias, lo que interrumpe normalmente está instalado el paquete.
- *Menor* [predeterminado] la dependencia instala con el número de versión mínima que cumple los requisitos del paquete principal elegido.
- *Revisión mayor* instala la versión con los mismos números de versión principal y secundaria, pero el mayor número de revisión. Por ejemplo, si se especifica la versión 1.2.2 se instalará la versión más reciente que se inicia con 1.2
- *Minor mayor* instala la versión con el mismo número de versión principal, pero el número secundario más alto y el número de revisión. Si se especifica la versión 1.2.2, se instalará la versión más alta que empieza por 1
- *Mayor* instala la versión más alta disponible del paquete.

**Acción de conflictos de archivos** especifica cómo NuGet debe controlar los paquetes que ya existen en el proyecto o equipo local:

- *Símbolo del sistema* indica a NuGet que pregunta si desea conservar o sobrescribir los paquetes existentes.
- *Omitir todo* indica a NuGet que omitir sobrescribir todos los paquetes existentes.
- *Sobrescribir todos* indica a NuGet para sobrescribir todos los paquetes existentes.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opciones de desinstalación

(No disponible para todos los tipos de proyecto).

**Quitar las dependencias**: cuando se selecciona, quita los paquetes dependientes si no hay referencias en otro lugar en el proyecto.

**Forzar la desinstalación incluso si existen dependencias en él**: cuando se selecciona, se desinstala un paquete incluso si se todavía se hace referencia en el proyecto. Esto normalmente se usa en combinación con **quitar las dependencias** para quitar un paquete y lo instala las dependencias. Con esta opción sin embargo, podría dar lugar a referencias erróneas en el proyecto. En tales casos, es posible que deba [reinstalar esos otros paquetes](../consume-packages/reinstalling-and-updating-packages.md).
