---
title: Referencia de interfaz de usuario de administrador de paquetes de NuGet | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 62f6962b-7b84-4452-ae0d-a9e1ef1fc6f0
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
description: Instrucciones para usando la UI del Administrador de paquetes de NuGet en Visual Studio para trabajar con paquetes de NuGet.
keywords: NuGet UI, el Administrador de paquetes de NuGet UI, NuGet en Visual Studio, administrar paquetes de NuGet, interfaz de usuario de NuGet, Administrador de paquetes de Visual Studio
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88e987054f3c59a327f71b15330a99eb350449e5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="a56ee-104">Interfaz de usuario de administrador de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="a56ee-104">NuGet Package Manager UI</span></span>

<span data-ttu-id="a56ee-105">La UI Administrador de paquetes de NuGet en Visual Studio en Windows le permite instalar, desinstalar y actualizar paquetes de NuGet en proyectos y soluciones fácilmente.</span><span class="sxs-lookup"><span data-stu-id="a56ee-105">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="a56ee-106">Para obtener la experiencia en Visual Studio para Mac, consulte [paquete NuGet unos incluidos en el proyecto](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="a56ee-106">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="a56ee-107">La UI del Administrador de paquetes no se incluye con Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a56ee-107">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="a56ee-108">En este tema:</span><span class="sxs-lookup"><span data-stu-id="a56ee-108">In this topic:</span></span>

- [<span data-ttu-id="a56ee-109">Búsqueda e instalación de un paquete (pestaña Examinar)</span><span class="sxs-lookup"><span data-stu-id="a56ee-109">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="a56ee-110">Desinstalar un paquete (pestaña instalados)</span><span class="sxs-lookup"><span data-stu-id="a56ee-110">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="a56ee-111">[Actualizar un paquete (pestañas instalado y actualizaciones)](#updating-a-package) (incluye el ["Implícitamente al que hace referencia un SDK" o "AutoReferenced" mensaje](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="a56ee-111">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="a56ee-112">[Administrar paquetes de la solución](#managing-packages-for-the-solution) (trabajar con varios proyectos al mismo tiempo).</span><span class="sxs-lookup"><span data-stu-id="a56ee-112">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="a56ee-113">Orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="a56ee-113">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="a56ee-114">Controlan opciones de administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="a56ee-114">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="a56ee-115">Compruebe si faltan el Administrador de paquetes de NuGet en Visual Studio 2015, **Herramientas > extensiones y actualizaciones...**  y busque el *Administrador de paquetes de NuGet* extensión.</span><span class="sxs-lookup"><span data-stu-id="a56ee-115">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="a56ee-116">Si no puede usar el instalador de extensiones de Visual Studio, descargue la extensión directamente desde [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="a56ee-116">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="a56ee-117">En Visual Studio 2017 NuGet y el Administrador de paquetes de NuGet se instalan automáticamente con cualquiera. Cargas de trabajo relacionados con la red.</span><span class="sxs-lookup"><span data-stu-id="a56ee-117">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="a56ee-118">Instalar individuall seleccionando el **componentes individuales > herramientas de código > Administrador de paquetes de NuGet** opción en el programa de instalación de Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="a56ee-118">Install it individuall by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="a56ee-119">Búsqueda e instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="a56ee-119">Finding and installing a package</span></span>

1. <span data-ttu-id="a56ee-120">En **el Explorador de soluciones**, haga **referencias** o un proyecto y seleccione **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="a56ee-120">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Administrar la opción de menú de paquetes de NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="a56ee-122">El **examinar** pestaña muestra paquetes por popularidad desde el origen seleccionado actualmente (vea [orígenes del paquete](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="a56ee-122">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="a56ee-123">Busque un paquete específico mediante el cuadro de búsqueda en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="a56ee-123">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="a56ee-124">Seleccione un paquete de la lista para mostrar su información, lo que también permite la **instalar** botón junto con una lista desplegable de selección de versión.</span><span class="sxs-lookup"><span data-stu-id="a56ee-124">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Administrar la ficha cuadro de diálogo Examinar de paquetes de NuGet](media/Search.png)

1. <span data-ttu-id="a56ee-126">Seleccione la versión deseada de la lista desplegable y seleccione **instalar**.</span><span class="sxs-lookup"><span data-stu-id="a56ee-126">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="a56ee-127">Visual Studio instala el paquete y sus dependencias en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a56ee-127">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="a56ee-128">Se le pedirá que acepte los términos de licencia.</span><span class="sxs-lookup"><span data-stu-id="a56ee-128">You may be asked to accept license terms.</span></span> <span data-ttu-id="a56ee-129">Cuando una vez completada la instalación, los paquetes agregados aparecen en la **instalado** ficha. Los paquetes también se enumeran en la **referencias** nodo del explorador de soluciones, que indica que puede hacer referencia a ellas en el proyecto con `using` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="a56ee-129">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Referencias en el Explorador de soluciones](media/References.png)

> [!Tip]
    > <span data-ttu-id="a56ee-131">Para incluir versiones preliminares en la búsqueda y para que las versiones preliminares estén disponibles en la versión de lista desplegable, seleccione la **incluir versión preliminar** opción.</span><span class="sxs-lookup"><span data-stu-id="a56ee-131">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="a56ee-132">Desinstalar un paquete</span><span class="sxs-lookup"><span data-stu-id="a56ee-132">Uninstalling a package</span></span>

1. <span data-ttu-id="a56ee-133">En **el Explorador de soluciones**, haga **referencias** o el proyecto que desee y seleccione **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="a56ee-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a56ee-134">Seleccione el **instalado** ficha.</span><span class="sxs-lookup"><span data-stu-id="a56ee-134">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="a56ee-135">Seleccione el paquete para desinstalar (uso de búsqueda para filtrar la lista si es necesario) y seleccione **desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="a56ee-135">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Desinstalar un paquete](media/UninstallPackage.png)

1. <span data-ttu-id="a56ee-137">Tenga en cuenta que la **incluyen preprelease** y **origen del paquete** controles no tienen ningún efecto cuando se desinstala paquetes.</span><span class="sxs-lookup"><span data-stu-id="a56ee-137">Note that the **Include preprelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="a56ee-138">Actualizar un paquete</span><span class="sxs-lookup"><span data-stu-id="a56ee-138">Updating a package</span></span>

1. <span data-ttu-id="a56ee-139">En **el Explorador de soluciones**, haga **referencias** o el proyecto que desee y seleccione **administrar paquetes de NuGet...** . (En proyectos de sitios web, haga clic en el **Bin** carpeta.)</span><span class="sxs-lookup"><span data-stu-id="a56ee-139">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="a56ee-140">Seleccione el **actualizaciones** pestaña para ver los paquetes que tienen actualizaciones disponibles de los orígenes del paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a56ee-140">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="a56ee-141">Seleccione **incluir versión preliminar** debe incluir paquetes de versión preliminar en la lista de actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="a56ee-141">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="a56ee-142">Seleccione el paquete para actualizar, seleccione la versión deseada de la lista desplegable de la derecha y seleccione **actualizar**.</span><span class="sxs-lookup"><span data-stu-id="a56ee-142">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Actualizar un paquete](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="a56ee-144">Para algunos de los paquetes, el **actualización** botón está deshabilitado y aparece un mensaje que indica que se está "implícitamente hace referencia a un SDK" (o "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="a56ee-144">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="a56ee-145">El mensaje indica que el paquete, como Microsoft.NETCore.App o Microsoft.NETStandard.Library, forma parte de un marco de trabajo o SDK más grande y no se debe actualizar de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="a56ee-145">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="a56ee-146">(Este tipo packagee internamente se marcan con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Para actualizar el paquete, actualizar el SDK a la que pertenece.</span><span class="sxs-lookup"><span data-stu-id="a56ee-146">(Such packagee are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs.</span></span>

    ![Paquete de ejemplo marcada como implícitamente referencias o AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="a56ee-148">Para actualizar varios paquetes a sus versiones más recientes, selecciónelas en la lista y seleccione el **actualizar** botón encima de la lista.</span><span class="sxs-lookup"><span data-stu-id="a56ee-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="a56ee-149">También puede actualizar un paquete individual desde la **instalado** ficha. En este caso, los detalles para el paquete incluyen un selector de versión (sujeto a la **versión preliminar de inclusión** opción) y un **actualización** botón.</span><span class="sxs-lookup"><span data-stu-id="a56ee-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="a56ee-150">Administrar paquetes de la solución</span><span class="sxs-lookup"><span data-stu-id="a56ee-150">Managing packages for the solution</span></span>

<span data-ttu-id="a56ee-151">Administrar paquetes de una solución es un medio cómodo para trabajar con varios proyectos simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="a56ee-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="a56ee-152">Seleccione el **Herramientas > Administrador de paquetes de NuGet > Administrar paquetes de NuGet para solución...**  menú de comandos, o haga clic en la solución y seleccione **administrar paquetes de NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="a56ee-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Administrar paquetes de NuGet para la solución](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="a56ee-154">Al administrar los paquetes para la solución, la interfaz de usuario permite seleccionar los proyectos que se ven afectados por las operaciones:</span><span class="sxs-lookup"><span data-stu-id="a56ee-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selector de proyecto al administrar paquetes de la solución](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="a56ee-156">Consolidar pestaña</span><span class="sxs-lookup"><span data-stu-id="a56ee-156">Consolidate tab</span></span>

<span data-ttu-id="a56ee-157">Los desarrolladores normalmente consideran una práctica incorrecta al usar una versión diferente del mismo paquete de NuGet en distintos proyectos de la misma solución.</span><span class="sxs-lookup"><span data-stu-id="a56ee-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="a56ee-158">Si decide administrar los paquetes de una solución, la UI del Administrador de paquetes proporciona un **Consolidate** ficha en el que puede ver fácilmente en distintos proyectos de la solución usa los paquetes con números de versión diferentes:</span><span class="sxs-lookup"><span data-stu-id="a56ee-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Pestaña de consolidar de interfaz de usuario de administrador de paquetes](media/ConsolidateTab.png)

<span data-ttu-id="a56ee-160">En este ejemplo, el proyecto ClassLibrary1 es mediante EntityFramework 6.2.0, mientras que ConsoleApp1 es mediante EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="a56ee-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.2.0.</span></span> <span data-ttu-id="a56ee-161">Para consolidar las versiones del paquete, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a56ee-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="a56ee-162">Seleccione los proyectos para actualizar en la lista de proyectos.</span><span class="sxs-lookup"><span data-stu-id="a56ee-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="a56ee-163">Seleccione la versión que se va a usar en todos los proyectos en el **versión** control, como EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="a56ee-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="a56ee-164">Seleccione el **instalar** botón.</span><span class="sxs-lookup"><span data-stu-id="a56ee-164">Select the **Install** button.</span></span>

<span data-ttu-id="a56ee-165">El Administrador de paquetes se instala la versión del paquete seleccionado en todos los proyectos seleccionados, después de que el paquete ya no aparece en la **Consolidate** ficha.</span><span class="sxs-lookup"><span data-stu-id="a56ee-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="a56ee-166">Orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="a56ee-166">Package sources</span></span>

<span data-ttu-id="a56ee-167">Para cambiar el origen desde el que Visual Studio obtiene los paquetes, seleccione uno en el selector de origen:</span><span class="sxs-lookup"><span data-stu-id="a56ee-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selector de origen de paquete en el Administrador de paquetes de interfaz de usuario](media/PackageSourceDropDown.png)

<span data-ttu-id="a56ee-169">Para administrar los orígenes de paquetes:</span><span class="sxs-lookup"><span data-stu-id="a56ee-169">To manage package sources:</span></span>

1. <span data-ttu-id="a56ee-170">Seleccione el **configuración** icono en la UI del Administrador de paquetes que se describen a continuación o use la **Herramientas > opciones** de comandos y desplácese hasta **Administrador de paquetes de NuGet**:</span><span class="sxs-lookup"><span data-stu-id="a56ee-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Icono de configuración de interfaz de usuario de administrador de paquetes](media/PackageSourceSettings.png)

1. <span data-ttu-id="a56ee-172">Seleccione el **orígenes de paquetes** nodo:</span><span class="sxs-lookup"><span data-stu-id="a56ee-172">Select the **Package Sources** node:</span></span>

    ![Opciones de orígenes de paquetes](media/options.png)

1. <span data-ttu-id="a56ee-174">Para agregar un origen, seleccione  **+** , edite el nombre, escriba la dirección URL o ruta de acceso en la **origen** control y seleccione **actualización**.</span><span class="sxs-lookup"><span data-stu-id="a56ee-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="a56ee-175">El origen ahora aparece en el selector de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="a56ee-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="a56ee-176">Para cambiar un origen del paquete, selecciónelo, efectúe modificaciones en el **nombre** y **origen** cuadros y seleccione **actualización**.</span><span class="sxs-lookup"><span data-stu-id="a56ee-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="a56ee-177">Para deshabilitar un origen del paquete, desactive la casilla a la izquierda del nombre de la lista.</span><span class="sxs-lookup"><span data-stu-id="a56ee-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="a56ee-178">Para quitar un origen de paquete, selecciónelo y, a continuación, seleccione la **X** botón.</span><span class="sxs-lookup"><span data-stu-id="a56ee-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="a56ee-179">Utilice el arriba y abajo botones de flecha para cambiar el orden de prioridad de los orígenes del paquete.</span><span class="sxs-lookup"><span data-stu-id="a56ee-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="a56ee-180">Visual Studio busca estos orígenes en el orden de prioridad al restaurar paquetes para un proyecto.</span><span class="sxs-lookup"><span data-stu-id="a56ee-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="a56ee-181">Para obtener más información, consulte [restaurar el paquete](../Consume-Packages/Package-Restore.md).</span><span class="sxs-lookup"><span data-stu-id="a56ee-181">For more information, see [Package restore](../Consume-Packages/Package-Restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="a56ee-182">Si vuelve a aparecer un origen del paquete después de eliminarlo, puede aparecer en un nivel de equipo o el nivel de usuario `NuGet.Config` archivos.</span><span class="sxs-lookup"><span data-stu-id="a56ee-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="a56ee-183">Vea [NuGet configurar comportamiento](../Consume-Packages/Configuring-NuGet-Behavior.md) para la ubicación de estos archivos, a continuación, quite el origen de la edición de los archivos manualmente o mediante el [nuget orígenes de comando](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a56ee-183">See [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="a56ee-184">Controlan opciones de administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="a56ee-184">Package manager Options control</span></span>

<span data-ttu-id="a56ee-185">Cuando se selecciona un paquete, la UI del Administrador de paquetes muestra una pequeña y expandibles **opciones** control debajo el selector de versión (mostrado aquí ambos contraído y expanden).</span><span class="sxs-lookup"><span data-stu-id="a56ee-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="a56ee-186">Tenga en cuenta que para algunos proyectos de tipos, como .NET Core y los usuarios que utilicen el `project.json` formato de referencia, solo el **Mostrar ventana de vista previa** opción se proporciona.</span><span class="sxs-lookup"><span data-stu-id="a56ee-186">Note that for some project types, such as .NET Core and those using the `project.json` reference format, only the **Show preview window** option is provided.</span></span>

![Opciones del Administrador de paquetes](media/PackageManagerUIOptions.png)

<span data-ttu-id="a56ee-188">Las siguientes secciones explican estas opciones.</span><span class="sxs-lookup"><span data-stu-id="a56ee-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="a56ee-189">Mostrar la ventana de vista previa</span><span class="sxs-lookup"><span data-stu-id="a56ee-189">Show preview window</span></span>

<span data-ttu-id="a56ee-190">Cuando se selecciona, una ventana modal que muestra que las dependencias de un paquete elegido antes de instalar el paquete:</span><span class="sxs-lookup"><span data-stu-id="a56ee-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Cuadro de diálogo de vista previa de ejemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="a56ee-192">Instalar y actualizar opciones</span><span class="sxs-lookup"><span data-stu-id="a56ee-192">Install and Update Options</span></span>

<span data-ttu-id="a56ee-193">(No disponible para todos los tipos de proyecto).</span><span class="sxs-lookup"><span data-stu-id="a56ee-193">(Not available for all project types.)</span></span>

<span data-ttu-id="a56ee-194">**Comportamiento de la dependencia** configura cómo NuGet decide qué versiones de los paquetes dependientes para instalar:</span><span class="sxs-lookup"><span data-stu-id="a56ee-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="a56ee-195">*Pasar por alto las dependencias* omite la instalación de las dependencias, que normalmente se interrumpe el paquete que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="a56ee-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="a56ee-196">*Menor* [Default] instala la dependencia con el número de versión mínimo que cumpla los requisitos del paquete primario seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a56ee-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="a56ee-197">*Revisión mayor* instala la versión con los mismos números de versión principal y secundaria, pero el mayor número de revisión.</span><span class="sxs-lookup"><span data-stu-id="a56ee-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="a56ee-198">Por ejemplo, si se especifica la versión 1.2.2 se instalará la versión más reciente que empieza por 1.2</span><span class="sxs-lookup"><span data-stu-id="a56ee-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="a56ee-199">*Minor mayor* instala la versión con el mismo número de versión principal, pero el número secundario más alto y el número de revisión.</span><span class="sxs-lookup"><span data-stu-id="a56ee-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="a56ee-200">Si se especifica la versión 1.2.2, se instalará la versión más reciente que empieza por 1</span><span class="sxs-lookup"><span data-stu-id="a56ee-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="a56ee-201">*Mayor* instala la versión disponible más alta del paquete.</span><span class="sxs-lookup"><span data-stu-id="a56ee-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="a56ee-202">**Acción de conflictos de archivos** especifica cómo NuGet debe administrar paquetes que ya existen en el proyecto o equipo local:</span><span class="sxs-lookup"><span data-stu-id="a56ee-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="a56ee-203">*Símbolo del sistema* indica NuGet para preguntar si desea conservar o sobrescribir los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="a56ee-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="a56ee-204">*Omitir todo* indica NuGet para omitir sobrescribir todos los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="a56ee-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="a56ee-205">*Sobrescribir todos* indica NuGet para sobrescribir todos los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="a56ee-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="a56ee-206">Opciones de desinstalación</span><span class="sxs-lookup"><span data-stu-id="a56ee-206">Uninstall Options</span></span>

<span data-ttu-id="a56ee-207">(No disponible para todos los tipos de proyecto).</span><span class="sxs-lookup"><span data-stu-id="a56ee-207">(Not available for all project types.)</span></span>

<span data-ttu-id="a56ee-208">**Quitar las dependencias**: cuando se selecciona, quita todos los paquetes dependientes si no está referencia en otro lugar en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a56ee-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="a56ee-209">**Forzar la desinstalación aunque tenga dependencias en él**: cuando se selecciona, desinstala un paquete aunque todavía se hace referencia en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a56ee-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="a56ee-210">Normalmente se utiliza en combinación con **quitar dependencias** para quitar un paquete y lo que las dependencias de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="a56ee-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="a56ee-211">Con esta opción sin embargo, podría producir un referencias rotas en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a56ee-211">Using this option may, however, lead to a broken references in the project.</span></span> <span data-ttu-id="a56ee-212">En tales casos puede que necesite [volver a instalar los otros paquetes](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a56ee-212">In such cases you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
