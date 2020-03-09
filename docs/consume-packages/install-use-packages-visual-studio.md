---
title: Instalación y administración de paquetes NuGet en Visual Studio
description: Instrucciones para usar la interfaz de usuario del Administrador de paquetes NuGet en Visual Studio para trabajar con paquetes NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231012"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Instalación y administración de paquetes en Visual Studio con el Administrador de paquetes NuGet

La interfaz de usuario del Administrador de paquetes NuGet en Visual Studio de Windows le permite instalar, desinstalar y actualizar fácilmente paquetes NuGet en proyectos y soluciones. Si necesita información sobre la experiencia en Visual Studio para Mac, consulte [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json). La interfaz de usuario del Administrador de paquetes no está incluida en Visual Studio Code.

> [!NOTE]
> Si falta el Administrador de paquetes NuGet en Visual Studio 2015, revise **Herramientas > Extensiones y actualizaciones…** y busque la extensión *Administrador de paquetes NuGet*. Si no puede usar el instalador de extensiones en Visual Studio, descargue la extensión directamente de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
>
> A partir de Visual Studio 2017, NuGet y el Administrador de paquetes NuGet están instalados automáticamente con cualquier carga de trabajo relacionada con .NET. Para instalarlo individualmente, seleccione la opción **Componentes individuales > Herramientas de código > Administrador de paquetes NuGet** en el instalador de Visual Studio.

## <a name="find-and-install-a-package"></a>Búsqueda e instalación de un paquete

1. En el **Explorador de soluciones**, haga clic con el botón derecho en **Referencias** o en un proyecto y seleccione **Administrar paquetes NuGet…** .

    ![Opción de menú Administrar paquetes NuGet](media/ManagePackagesUICommand.png)

1. La pestaña **Examinar** muestra los paquetes del origen seleccionado (consulte los [orígenes de paquetes](#package-sources)) ordenados por popularidad. Busque un paquete específico en el cuadro de búsqueda que se encuentra en la esquina superior izquierda. Seleccione un paquete de la lista para mostrar su información, lo que también habilita el botón **Instalar** junto con un menú desplegable para seleccionar la versión.

    ![Pestaña Examinar del cuadro de diálogo Administrar paquetes NuGet](media/Search.png)

1. Seleccione la versión deseada en el menú desplegable y seleccione **Instalar**. Visual Studio instala el paquete y sus dependencias en el proyecto. Es posible que se le pida aceptar los términos de licencia. Una vez que se complete la instalación, los paquetes agregados aparecerán en la pestaña **Instalado**. Los paquetes también aparecen en el nodo **Referencias** del Explorador de soluciones, lo que indica que es posible hace referencia a ellos en el proyecto con instrucciones `using`.

    ![Referencias en el Explorador de soluciones](media/References.png)

> [!Tip]
> Para incluir las versiones preliminares en la búsqueda y hacer que estén disponibles en el menú desplegable de las versiones, seleccione la opción **Incluir versión preliminar**.

> [!Note]
> NuGet dispone de dos formatos en los que un proyecto puede usar paquetes: [`PackageReference`](package-references-in-project-files.md) y [`packages.config`](../reference/packages-config.md). [El valor predeterminado se puede establecer en la ventana Opciones de Visual Studio](Package-Restore.md#choose-default-package-management-format).

## <a name="uninstall-a-package"></a>Desinstala un paquete.

1. En el **Explorador de soluciones**, haga clic con el botón derecho en **Referencias** o en el proyecto deseado y seleccione **Administrar paquetes NuGet…** .
1. Seleccione la pestaña **Instalado**.
1. Seleccione el paquete que se va a desinstalar (use la búsqueda para filtrar la lista si es necesario) y seleccione **Desinstalar**.

    ![Desinstalación de un paquete](media/UninstallPackage.png)

1. Observe que los controles **Incluir versión preliminar** y **Origen del paquete** no tienen efecto al desinstalar los paquetes.

## <a name="update-a-package"></a>Actualización de un paquete

1. En el **Explorador de soluciones**, haga clic con el botón derecho en **Referencias** o en el proyecto deseado y seleccione **Administrar paquetes NuGet…** . (En proyectos de sitio web, haga clic con el botón derecho en la carpeta **Bin**).
1. Seleccione la pestaña **Actualizaciones** para ver los paquetes que tienen actualizaciones disponibles de los orígenes de paquetes seleccionados. Seleccione **Incluir versión preliminar** para incluir los paquetes de versión preliminar en la lista de actualizaciones.
1. Seleccione el paquete que se va a actualizar, la versión deseada en el menú desplegable de la derecha y, luego, seleccione **Actualizar**.

    ![Actualización de un paquete](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>En algunos paquetes, el botón **Actualizar** está deshabilitado y aparece un mensaje que indica que un SDK hace referencia de forma implícita al paquete en cuestión (o que hay una referencia automática). Este mensaje indica que el paquete forma parte de un marco o SDK más grande y que no se debe actualizar por separado. (Dichos paquetes están marcados internamente con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`). Por ejemplo, `Microsoft.NETCore.App` forma parte del SDK de .NET Core y la versión del paquete no es igual que la versión del marco de runtime que la aplicación usa. Necesita [actualizar la instalación de .NET Core](https://aka.ms/dotnet-download) para obtener versiones nuevas del runtime de ASP.NET Core y .NET Core. [Consulte este documento para ver más detalles sobre los metapaquetes y el control de versiones de .NET Core](/dotnet/core/packages). Esto se aplica a los siguientes paquetes de uso común:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Paquete de ejemplo marcado como Hace referencia de forma implícita o Con referencia automática](media/PackageManagerUIAutoReferenced.png)

1. Para actualizar varios paquetes a sus versiones más recientes, selecciónelos en la lista y seleccione el botón **Actualizar** que está encima de la lista.
1. También puede actualizar un paquete individual desde la pestaña **Instalado**. En este caso, los detalles del paquete incluyen un selector de versión (sujeto a la opción **Incluir versión preliminar**) y un botón **Actualizar**.

## <a name="manage-packages-for-the-solution"></a>Administración de paquetes para la solución

Administrar los paquetes de una solución es un medio cómodo para trabajar con varios proyectos a la vez.

1. Seleccione el comando de menú **Herramientas > Administrador de paquetes NuGet > Administrar paquetes NuGet para la solución…** o haga clic con el botón derecho en la solución y seleccione **Administrar paquetes NuGet…** :

    ![Administrar paquetes NuGet para la solución](media/ManagePackagesSolutionUICommand.png)

1. Cuando administra paquetes para la solución, la interfaz de usuario le permite seleccionar los proyectos que se ven afectados por las operaciones:

    ![Selector de proyectos al administrar los paquetes para la solución](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Pestaña Consolidar

Por lo general, los desarrolladores consideran como una práctica incorrecta usar versiones distintas del mismo paquete NuGet en diferentes proyectos de la misma solución. Cuando elige administrar los paquetes de una solución, la interfaz de usuario del Administrador de paquetes proporciona una pestaña **Consolidar** donde puede ver fácilmente dónde los distintos proyectos de la solución usan paquetes con distintos números de versión:

![Pestaña Consolidar de la interfaz de usuario del Administrador de paquetes](media/ConsolidateTab.png)

En este ejemplo, el proyecto ClassLibrary1 usa EntityFramework 6.2.0, mientras que ConsoleApp1 usa EntityFramework 6.1.0. Para consolidar las versiones de los paquetes, haga lo siguiente:

- Seleccione los proyectos que se van a actualizar en la lista de proyectos.
- Seleccione la versión que se usará en todos esos proyectos en el control **Versión**, como EntityFramework 6.2.0.
- Seleccione el botón **Instalar**.

El Administrador de paquetes instala la versión de paquete seleccionada en todos los proyectos seleccionados, después de lo cual el paquete deja de aparecer en la pestaña **Consolidar**.

## <a name="package-sources"></a>Orígenes de paquetes

Para cambiar el origen desde donde Visual Studio obtiene los paquetes, seleccione uno en el selector de origen:

![Selector de origen del paquete en la interfaz de usuario del Administrador de paquetes](media/PackageSourceDropDown.png)

Para administrar los orígenes de paquetes:

1. Seleccione el icono **Configuración** en la interfaz de usuario del Administrador de paquetes que se describe a continuación o use el comando **Herramientas > Opciones** y desplácese hasta **Administrador de paquetes NuGet**:

    ![Icono de configuración de la interfaz de usuario del Administrador de paquetes](media/PackageSourceSettings.png)

1. Seleccione el nodo **Orígenes de paquetes**:

    ![Opciones de Orígenes de paquetes](media/options.png)

1. Para agregar un origen, seleccione **+** , edite el nombre, escriba la dirección URL o la ruta de acceso en el control **Origen** y seleccione **Actualizar**. El origen ahora aparece en el menú desplegable del selector.
1. Para cambiar un origen de paquete, selecciónelo, realice las modificaciones en los cuadros **Nombre** y **Origen** y seleccione **Actualizar**.
1. Para deshabilitar un origen de paquete, desactive la casilla que está a la izquierda del nombre en la lista.
1. Para quitar un origen de paquete, selecciónelo y, luego, seleccione el botón **X**.
1. El uso de los botones de flecha arriba y flecha abajo no cambia el orden de prioridad de los orígenes de paquetes. Visual Studio omite el orden de los orígenes de paquetes, usando el paquete del origen que primero responda a las solicitudes. Para más información, consulte [Restauración de paquetes](../consume-packages/package-restore.md).

> [!Tip]
> Si un origen de paquete vuelve a aparecer después de eliminarlo, es posible que aparezca en los archivos `NuGet.Config` en un nivel de equipo o de usuario. Consulte [Configuraciones comunes de NuGet](../consume-packages/configuring-nuget-behavior.md) para ver la ubicación de estos archivos y, luego, quite el origen al editar los archivos de manera manual o mediante el [comando nuget sources](../reference/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Control de opciones del Administrador de paquetes

Cuando se selecciona un paquete, la interfaz de usuario del Administrador de paquetes muestra un pequeño control **Opciones** que se puede expandir debajo del selector de versión (que aquí se muestra tanto contraído como expandido). Tenga en cuenta que, para algunos tipos de proyecto, solo se proporciona la opción **Mostrar ventana de vista previa**.

![Opciones del Administrador de paquetes](media/PackageManagerUIOptions.png)

Estas opciones se explican en las secciones siguientes.

### <a name="show-preview-window"></a>Mostrar ventana de vista previa

Cuando se selecciona esta opción, una ventana modal muestra cuáles son las dependencias de un paquete elegido antes de que se instale el paquete:

![Cuadro de diálogo de vista previa de ejemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Opciones de Instalar y actualizar

(No disponibles para todos los tipos de proyectos).

**Comportamiento de dependencia**: configura cómo NuGet decide qué versiones de los paquetes dependientes se van a instalar:

- *Omitir dependencias*: omite la instalación de cualquier dependencia, lo que habitualmente interrumpe el paquete que se está instalando.
- *Mínima* [valor predeterminado]: instala la dependencia con el número de versión mínimo que cumple los requisitos del paquete principal escogido.
- *Revisión superior*: instala la versión con los mismos números de versión principal y secundaria, pero con el número de revisión superior. Por ejemplo, si se especifica la versión 1.2.2, se instalará la versión superior que empieza con 1.2.
- *Secundaria superior*: instala la versión con el mismo número de versión principal, pero el número de revisión y de versión secundaria superior. Si se especifica la versión 1.2.2, se instalará la versión superior que empieza con 1.
- *Superior*: instala la versión superior disponible del paquete.

**Acción de conflicto de archivos**: especifica cómo NuGet debe administrar los paquetes que ya existen en la máquina local o en el proyecto:

- *Petición*: indica a NuGet si debe conservar o sobrescribir los paquetes existentes.
- *Omitir todo*: indica a NuGet que omita sobrescribir cualquier paquete existente.
- *Sobrescribir todo*: indica a NuGet que sobrescriba cualquier paquete existente.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opciones de desinstalación

(No disponibles para todos los tipos de proyectos).

**Quitar dependencia**: cuando se selecciona, esta opción quita todos los paquetes dependientes si no se hace referencia a ellos en alguna otra parte del proyecto.

**Forzar la desinstalación incluso si hay dependencias**: cuando se selecciona, esta opción desinstala un paquete incluso si se hace referencia a él en el proyecto. Por lo general, se usa en combinación con **Quitar dependencias** para quitar un paquete y todas las dependencias que instaló. Sin embargo, usar esta opción puede generar referencias rotas en el proyecto. En tales casos, es posible que tenga que [volver a instalar esos otros paquetes](../consume-packages/reinstalling-and-updating-packages.md).
