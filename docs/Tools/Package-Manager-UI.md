---
title: Referencia de interfaz de usuario de administrador de paquetes de NuGet | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: Instrucciones para usando la UI del Administrador de paquetes de NuGet en Visual Studio para trabajar con paquetes de NuGet.
keywords: NuGet UI, el Administrador de paquetes de NuGet UI, NuGet en Visual Studio, administrar paquetes de NuGet, interfaz de usuario de NuGet, Administrador de paquetes de Visual Studio
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0ff60c3cecee5fd9b7f698d2abed7553f5d89c1d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-package-manager-ui"></a>Interfaz de usuario de administrador de paquetes de NuGet

La UI Administrador de paquetes de NuGet en Visual Studio en Windows le permite instalar, desinstalar y actualizar paquetes de NuGet en proyectos y soluciones fácilmente. Para obtener la experiencia en Visual Studio para Mac, consulte [paquete NuGet unos incluidos en el proyecto](/visualstudio/mac/nuget-walkthrough). La UI del Administrador de paquetes no se incluye con Visual Studio Code.

En este tema:

- [Búsqueda e instalación de un paquete (pestaña Examinar)](#finding-and-installing-a-package)
- [Desinstalar un paquete (pestaña instalados)](#uninstalling-a-package)
- [Actualizar un paquete (pestañas instalado y actualizaciones)](#updating-a-package) (incluye el ["Implícitamente al que hace referencia un SDK" o "AutoReferenced" mensaje](#implicit_reference))
- [Administrar paquetes de la solución](#managing-packages-for-the-solution) (trabajar con varios proyectos al mismo tiempo).
- [Orígenes de paquetes](#package-sources)
- [Controlan opciones de administrador de paquetes](#package-manager-options-control)

> [!Note]
> Compruebe si faltan el Administrador de paquetes de NuGet en Visual Studio 2015, **Herramientas > extensiones y actualizaciones...**  y busque el *Administrador de paquetes de NuGet* extensión. Si no puede usar el instalador de extensiones de Visual Studio, descargue la extensión directamente desde [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
>
> En Visual Studio 2017 NuGet y el Administrador de paquetes de NuGet se instalan automáticamente con cualquiera. Cargas de trabajo relacionados con la red. Instalar de forma individual seleccionando la **componentes individuales > herramientas de código > Administrador de paquetes de NuGet** opción en el programa de instalación de Visual Studio de 2017.

## <a name="finding-and-installing-a-package"></a>Búsqueda e instalación de un paquete

1. En **el Explorador de soluciones**, haga **referencias** o un proyecto y seleccione **administrar paquetes de NuGet...** .

    ![Administrar la opción de menú de paquetes de NuGet](media/ManagePackagesUICommand.png)

1. El **examinar** pestaña muestra paquetes por popularidad desde el origen seleccionado actualmente (vea [orígenes del paquete](#package-sources)). Busque un paquete específico mediante el cuadro de búsqueda en la parte superior izquierda. Seleccione un paquete de la lista para mostrar su información, lo que también permite la **instalar** botón junto con una lista desplegable de selección de versión.

    ![Administrar la ficha cuadro de diálogo Examinar de paquetes de NuGet](media/Search.png)

1. Seleccione la versión deseada de la lista desplegable y seleccione **instalar**. Visual Studio instala el paquete y sus dependencias en el proyecto. Se le pedirá que acepte los términos de licencia. Cuando una vez completada la instalación, los paquetes agregados aparecen en la **instalado** ficha. Los paquetes también se enumeran en la **referencias** nodo del explorador de soluciones, que indica que puede hacer referencia a ellas en el proyecto con `using` instrucciones.

    ![Referencias en el Explorador de soluciones](media/References.png)

> [!Tip]
    > Para incluir versiones preliminares en la búsqueda y para que las versiones preliminares estén disponibles en la versión de lista desplegable, seleccione la **incluir versión preliminar** opción.

## <a name="uninstalling-a-package"></a>Desinstalar un paquete

1. En **el Explorador de soluciones**, haga **referencias** o el proyecto que desee y seleccione **administrar paquetes de NuGet...** .
1. Seleccione el **instalado** ficha.
1. Seleccione el paquete para desinstalar (uso de búsqueda para filtrar la lista si es necesario) y seleccione **desinstalar**.

    ![Desinstalar un paquete](media/UninstallPackage.png)

1. Tenga en cuenta que la **incluyen preprelease** y **origen del paquete** controles no tienen ningún efecto cuando se desinstala paquetes.

## <a name="updating-a-package"></a>Actualizar un paquete

1. En **el Explorador de soluciones**, haga **referencias** o el proyecto que desee y seleccione **administrar paquetes de NuGet...** . (En proyectos de sitios web, haga clic en el **Bin** carpeta.)
1. Seleccione el **actualizaciones** pestaña para ver los paquetes que tienen actualizaciones disponibles de los orígenes del paquete seleccionado. Seleccione **incluir versión preliminar** debe incluir paquetes de versión preliminar en la lista de actualizaciones.
1. Seleccione el paquete para actualizar, seleccione la versión deseada de la lista desplegable de la derecha y seleccione **actualizar**.

    ![Actualizar un paquete](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Para algunos de los paquetes, el **actualización** botón está deshabilitado y aparece un mensaje que indica que se está "implícitamente hace referencia a un SDK" (o "AutoReferenced"). El mensaje indica que el paquete, como Microsoft.NETCore.App o Microsoft.NETStandard.Library, forma parte de un marco de trabajo o SDK más grande y no se debe actualizar de forma independiente. (Este tipo packagee internamente se marcan con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Para actualizar el paquete, actualizar el SDK a la que pertenece.

    ![Paquete de ejemplo marcada como implícitamente referencias o AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Para actualizar varios paquetes a sus versiones más recientes, selecciónelas en la lista y seleccione el **actualizar** botón encima de la lista.
1. También puede actualizar un paquete individual desde la **instalado** ficha. En este caso, los detalles para el paquete incluyen un selector de versión (sujeto a la **versión preliminar de inclusión** opción) y un **actualización** botón.

## <a name="managing-packages-for-the-solution"></a>Administrar paquetes de la solución

Administrar paquetes de una solución es un medio cómodo para trabajar con varios proyectos simultáneamente.

1. Seleccione el **Herramientas > Administrador de paquetes de NuGet > Administrar paquetes de NuGet para solución...**  menú de comandos, o haga clic en la solución y seleccione **administrar paquetes de NuGet...** :

    ![Administrar paquetes de NuGet para la solución](media/ManagePackagesSolutionUICommand.png)

1. Al administrar los paquetes para la solución, la interfaz de usuario permite seleccionar los proyectos que se ven afectados por las operaciones:

    ![Selector de proyecto al administrar paquetes de la solución](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Consolidar pestaña

Los desarrolladores normalmente consideran una práctica incorrecta al usar una versión diferente del mismo paquete de NuGet en distintos proyectos de la misma solución. Si decide administrar los paquetes de una solución, la UI del Administrador de paquetes proporciona un **Consolidate** ficha en el que puede ver fácilmente en distintos proyectos de la solución usa los paquetes con números de versión diferentes:

![Pestaña de consolidar de interfaz de usuario de administrador de paquetes](media/ConsolidateTab.png)

En este ejemplo, el proyecto ClassLibrary1 es mediante EntityFramework 6.2.0, mientras que ConsoleApp1 es mediante EntityFramework 6.2.0. Para consolidar las versiones del paquete, haga lo siguiente:

- Seleccione los proyectos para actualizar en la lista de proyectos.
- Seleccione la versión que se va a usar en todos los proyectos en el **versión** control, como EntityFramework 6.2.0.
- Seleccione el **instalar** botón.

El Administrador de paquetes se instala la versión del paquete seleccionado en todos los proyectos seleccionados, después de que el paquete ya no aparece en la **Consolidate** ficha.

## <a name="package-sources"></a>Orígenes de paquetes

Para cambiar el origen desde el que Visual Studio obtiene los paquetes, seleccione uno en el selector de origen:

![Selector de origen de paquete en el Administrador de paquetes de interfaz de usuario](media/PackageSourceDropDown.png)

Para administrar los orígenes de paquetes:

1. Seleccione el **configuración** icono en la UI del Administrador de paquetes que se describen a continuación o use la **Herramientas > opciones** de comandos y desplácese hasta **Administrador de paquetes de NuGet**:

    ![Icono de configuración de interfaz de usuario de administrador de paquetes](media/PackageSourceSettings.png)

1. Seleccione el **orígenes de paquetes** nodo:

    ![Opciones de orígenes de paquetes](media/options.png)

1. Para agregar un origen, seleccione  **+** , edite el nombre, escriba la dirección URL o ruta de acceso en la **origen** control y seleccione **actualización**. El origen ahora aparece en el selector de lista desplegable.
1. Para cambiar un origen del paquete, selecciónelo, efectúe modificaciones en el **nombre** y **origen** cuadros y seleccione **actualización**.
1. Para deshabilitar un origen del paquete, desactive la casilla a la izquierda del nombre de la lista.
1. Para quitar un origen de paquete, selecciónelo y, a continuación, seleccione la **X** botón.
1. Utilice el arriba y abajo botones de flecha para cambiar el orden de prioridad de los orígenes del paquete. Visual Studio busca estos orígenes en el orden de prioridad al restaurar paquetes para un proyecto. Para obtener más información, consulte [restaurar el paquete](../Consume-Packages/Package-Restore.md).

> [!Tip]
> Si vuelve a aparecer un origen del paquete después de eliminarlo, puede aparecer en un nivel de equipo o el nivel de usuario `NuGet.Config` archivos. Vea [NuGet configurar comportamiento](../Consume-Packages/Configuring-NuGet-Behavior.md) para la ubicación de estos archivos, a continuación, quite el origen de la edición de los archivos manualmente o mediante el [nuget orígenes de comando](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Controlan opciones de administrador de paquetes

Cuando se selecciona un paquete, la UI del Administrador de paquetes muestra una pequeña y expandibles **opciones** control debajo el selector de versión (mostrado aquí ambos contraído y expanden). Tenga en cuenta que para algunos proyectos, solo tipos el **Mostrar ventana de vista previa** opción se proporciona.

![Opciones del Administrador de paquetes](media/PackageManagerUIOptions.png)

Las siguientes secciones explican estas opciones.

### <a name="show-preview-window"></a>Mostrar la ventana de vista previa

Cuando se selecciona, una ventana modal que muestra que las dependencias de un paquete elegido antes de instalar el paquete:

![Cuadro de diálogo de vista previa de ejemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Instalar y actualizar opciones

(No disponible para todos los tipos de proyecto).

**Comportamiento de la dependencia** configura cómo NuGet decide qué versiones de los paquetes dependientes para instalar:

- *Pasar por alto las dependencias* omite la instalación de las dependencias, que normalmente se interrumpe el paquete que se va a instalar.
- *Menor* [Default] instala la dependencia con el número de versión mínimo que cumpla los requisitos del paquete primario seleccionado.
- *Revisión mayor* instala la versión con los mismos números de versión principal y secundaria, pero el mayor número de revisión. Por ejemplo, si se especifica la versión 1.2.2 se instalará la versión más reciente que empieza por 1.2
- *Minor mayor* instala la versión con el mismo número de versión principal, pero el número secundario más alto y el número de revisión. Si se especifica la versión 1.2.2, se instalará la versión más reciente que empieza por 1
- *Mayor* instala la versión disponible más alta del paquete.

**Acción de conflictos de archivos** especifica cómo NuGet debe administrar paquetes que ya existen en el proyecto o equipo local:

- *Símbolo del sistema* indica NuGet para preguntar si desea conservar o sobrescribir los paquetes existentes.
- *Omitir todo* indica NuGet para omitir sobrescribir todos los paquetes existentes.
- *Sobrescribir todos* indica NuGet para sobrescribir todos los paquetes existentes.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opciones de desinstalación

(No disponible para todos los tipos de proyecto).

**Quitar las dependencias**: cuando se selecciona, quita todos los paquetes dependientes si no está referencia en otro lugar en el proyecto.

**Forzar la desinstalación aunque tenga dependencias en él**: cuando se selecciona, desinstala un paquete aunque todavía se hace referencia en el proyecto. Normalmente se utiliza en combinación con **quitar dependencias** para quitar un paquete y lo que las dependencias de instalarlo. Con esta opción sin embargo, podría producir un referencias rotas en el proyecto. En tales casos puede que necesite [volver a instalar los otros paquetes](../consume-packages/reinstalling-and-updating-packages.md).
