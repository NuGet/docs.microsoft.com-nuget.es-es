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
# <a name="install-and-manage-packages-in-visual-studio"></a><span data-ttu-id="13350-103">Instalar y administrar paquetes en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13350-103">Install and manage packages in Visual Studio</span></span>

<span data-ttu-id="13350-104">La UI Administrador de paquetes de NuGet en Visual Studio en Windows le permite instalar, desinstalar y actualizar paquetes de NuGet en proyectos y soluciones con facilidad.</span><span class="sxs-lookup"><span data-stu-id="13350-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="13350-105">Para obtener la experiencia en Visual Studio para Mac, consulte [incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="13350-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="13350-106">El Administrador de paquetes de UI no se incluye con Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="13350-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="13350-107">Compruebe si faltan el Administrador de paquetes de NuGet en Visual Studio 2015, **Herramientas > extensiones y actualizaciones...**  y busque el *Administrador de paquetes de NuGet* extensión.</span><span class="sxs-lookup"><span data-stu-id="13350-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="13350-108">Si no puede usar el instalador de extensiones de Visual Studio, descargue la extensión directamente desde [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="13350-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="13350-109">A partir de Visual Studio 2017, NuGet y el Administrador de paquetes de NuGet se instalan automáticamente con cualquiera. Cargas de trabajo relacionados con la red.</span><span class="sxs-lookup"><span data-stu-id="13350-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="13350-110">Instálelo individualmente seleccionando el **componentes individuales > herramientas de código > Administrador de paquetes de NuGet** opción en el instalador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13350-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="13350-111">Búsqueda e instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="13350-111">Finding and installing a package</span></span>

1. <span data-ttu-id="13350-112">En **el Explorador de soluciones**, haga clic en cualquiera **referencias** o un proyecto y seleccione **administrar paquetes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="13350-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Administrar la opción de menú de paquetes de NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="13350-114">El **examinar** pestaña muestra los paquetes por popularidad del origen seleccionado actualmente (vea [orígenes de paquetes](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="13350-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="13350-115">Busque un paquete específico mediante el cuadro de búsqueda en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="13350-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="13350-116">Seleccione un paquete de la lista para mostrar su información, lo cual habilita también el **instalar** botón junto con una lista desplegable de selección de versión.</span><span class="sxs-lookup"><span data-stu-id="13350-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Administrar la ficha cuadro de diálogo Examinar de paquetes de NuGet](media/Search.png)

1. <span data-ttu-id="13350-118">Seleccione la versión deseada de la lista desplegable y seleccione **instalar**.</span><span class="sxs-lookup"><span data-stu-id="13350-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="13350-119">Visual Studio instala el paquete y sus dependencias en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="13350-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="13350-120">Se le pedirá que acepte los términos de licencia.</span><span class="sxs-lookup"><span data-stu-id="13350-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="13350-121">Cuando se complete la instalación, los paquetes agregados aparecen en la **instalado** ficha. Los paquetes también se enumeran en la **referencias** nodo del explorador de soluciones, que indica que puede hacer referencia a ellas en el proyecto con `using` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="13350-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Referencias en el Explorador de soluciones](media/References.png)

> [!Tip]
> <span data-ttu-id="13350-123">Para incluir versiones preliminares en la búsqueda y para que las versiones preliminares disponibles en la versión lista desplegable, seleccione el **incluir versión preliminar** opción.</span><span class="sxs-lookup"><span data-stu-id="13350-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="13350-124">Al desinstalar un paquete</span><span class="sxs-lookup"><span data-stu-id="13350-124">Uninstalling a package</span></span>

1. <span data-ttu-id="13350-125">En **el Explorador de soluciones**, haga clic en cualquiera **referencias** o el proyecto que desee y seleccione **administrar paquetes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="13350-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="13350-126">Seleccione el **instalado** ficha.</span><span class="sxs-lookup"><span data-stu-id="13350-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="13350-127">Seleccione el paquete para desinstalar (mediante la búsqueda para filtrar la lista si es necesario) y seleccione **desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="13350-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Al desinstalar un paquete](media/UninstallPackage.png)

1. <span data-ttu-id="13350-129">Tenga en cuenta que el **incluir versión preliminar** y **origen del paquete** controles no tienen ningún efecto cuando se desinstala los paquetes.</span><span class="sxs-lookup"><span data-stu-id="13350-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="13350-130">Actualizar un paquete</span><span class="sxs-lookup"><span data-stu-id="13350-130">Updating a package</span></span>

1. <span data-ttu-id="13350-131">En **el Explorador de soluciones**, haga clic en cualquiera **referencias** o el proyecto que desee y seleccione **administrar paquetes NuGet...** . (En proyectos de sitios web, haga clic en el **Bin** carpeta.)</span><span class="sxs-lookup"><span data-stu-id="13350-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="13350-132">Seleccione el **actualizaciones** pestaña para ver los paquetes que tienen actualizaciones disponibles desde los orígenes del paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="13350-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="13350-133">Seleccione **incluir versión preliminar** para incluir paquetes de versión preliminar en la lista de actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="13350-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="13350-134">Seleccione el paquete para actualizar, seleccione la versión deseada de la lista desplegable de la derecha y seleccione **actualizar**.</span><span class="sxs-lookup"><span data-stu-id="13350-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Actualizar un paquete](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="13350-136">Para algunos paquetes, el **actualización** botón está deshabilitado y aparece un mensaje que indica que se "hace referencia implícitamente mediante un SDK" (o "Compatibilidad con AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="13350-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="13350-137">Este mensaje indica que el paquete forma parte de un marco de trabajo o SDK más grande y no se debe actualizar de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="13350-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="13350-138">(Estos paquetes internamente se marcan con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Por ejemplo, `Microsoft.NETCore.App` es parte del SDK de .NET Core y la versión del paquete no es igual que la versión de framework en tiempo de ejecución utilizado por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="13350-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="13350-139">Deberá [actualizar su instalación de .NET Core](https://aka.ms/dotnet-download) para obtener nuevas versiones del tiempo de ejecución de ASP.NET Core y .NET Core.</span><span class="sxs-lookup"><span data-stu-id="13350-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="13350-140">[Consulte este documento para obtener más detalles sobre los metapaquetes de .NET Core y control de versiones](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="13350-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="13350-141">Esto se aplica a los siguientes paquetes usados:</span><span class="sxs-lookup"><span data-stu-id="13350-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="13350-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="13350-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="13350-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="13350-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="13350-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="13350-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="13350-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="13350-145">NETStandard.Library</span></span>

    ![Paquete de ejemplo marcada como implícitamente las referencias o compatibilidad con AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="13350-147">Para actualizar varios paquetes a sus versiones más recientes, selecciónelos en la lista y seleccione el **actualizar** botón encima de la lista.</span><span class="sxs-lookup"><span data-stu-id="13350-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="13350-148">También puede actualizar un paquete individual desde la **instalado** ficha. En este caso, los detalles para el paquete incluyen un selector de versión (sujeto a la **incluir versión preliminar** opción) y un **actualización** botón.</span><span class="sxs-lookup"><span data-stu-id="13350-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="13350-149">Administración de paquetes para la solución</span><span class="sxs-lookup"><span data-stu-id="13350-149">Managing packages for the solution</span></span>

<span data-ttu-id="13350-150">Administración de paquetes para una solución es un medio cómodo para trabajar con varios proyectos simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="13350-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="13350-151">Seleccione el **Herramientas > Administrador de paquetes NuGet > Administrar paquetes de NuGet para la solución...**  menú de comandos, o haga clic en la solución y seleccione **administrar paquetes NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="13350-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Administrar paquetes de NuGet para la solución](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="13350-153">Al administrar los paquetes para la solución, la interfaz de usuario le permite seleccionar los proyectos que se ven afectados por las operaciones:</span><span class="sxs-lookup"><span data-stu-id="13350-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selector de proyecto al administrar los paquetes para la solución](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="13350-155">Consolidar pestaña</span><span class="sxs-lookup"><span data-stu-id="13350-155">Consolidate tab</span></span>

<span data-ttu-id="13350-156">Normalmente los desarrolladores consideran mala práctica usar diferentes versiones del mismo paquete de NuGet en los distintos proyectos en la misma solución.</span><span class="sxs-lookup"><span data-stu-id="13350-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="13350-157">Si decide administrar los paquetes para una solución, el Administrador de paquetes de UI proporciona una **consolidar** ficha en el que puede ver fácilmente donde diferentes proyectos de la solución usa los paquetes con números de versión distintos:</span><span class="sxs-lookup"><span data-stu-id="13350-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Pestaña consolidar de interfaz de usuario de administrador de paquetes](media/ConsolidateTab.png)

<span data-ttu-id="13350-159">En este ejemplo, el proyecto ClassLibrary1 usa Entity Framework de la 6.2.0, mientras que usa EntityFramework 6.1.0 ConsoleApp1.</span><span class="sxs-lookup"><span data-stu-id="13350-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="13350-160">Para consolidar las versiones del paquete, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="13350-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="13350-161">Seleccione los proyectos que se actualizará en la lista de proyectos.</span><span class="sxs-lookup"><span data-stu-id="13350-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="13350-162">Seleccione la versión que se usará en todos los proyectos de la **versión** control, como la 6.2.0 EntityFramework.</span><span class="sxs-lookup"><span data-stu-id="13350-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="13350-163">Seleccione el **instalar** botón.</span><span class="sxs-lookup"><span data-stu-id="13350-163">Select the **Install** button.</span></span>

<span data-ttu-id="13350-164">El Administrador de paquetes se instala la versión del paquete seleccionado en todos los proyectos seleccionados, después de que el paquete ya no aparece en el **consolidar** ficha.</span><span class="sxs-lookup"><span data-stu-id="13350-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="13350-165">Orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="13350-165">Package sources</span></span>

<span data-ttu-id="13350-166">Para cambiar el origen de los que Visual Studio obtiene los paquetes, seleccione uno en el selector de origen:</span><span class="sxs-lookup"><span data-stu-id="13350-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selector de origen de paquete en el Administrador de paquetes de interfaz de usuario](media/PackageSourceDropDown.png)

<span data-ttu-id="13350-168">Para administrar orígenes de paquetes:</span><span class="sxs-lookup"><span data-stu-id="13350-168">To manage package sources:</span></span>

1. <span data-ttu-id="13350-169">Seleccione el **configuración** icono en la UI del Administrador de paquetes que se describen a continuación o usar el **Herramientas > opciones** de comandos y desplácese hasta **Administrador de paquetes de NuGet**:</span><span class="sxs-lookup"><span data-stu-id="13350-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Icono de configuración de la interfaz de usuario Administrador de paquetes](media/PackageSourceSettings.png)

1. <span data-ttu-id="13350-171">Seleccione el **orígenes de paquetes** nodo:</span><span class="sxs-lookup"><span data-stu-id="13350-171">Select the **Package Sources** node:</span></span>

    ![Opciones de orígenes de paquetes](media/options.png)

1. <span data-ttu-id="13350-173">Para agregar un origen, seleccione **+** , edite el nombre, escriba la dirección URL o ruta de acceso en el **origen** control y seleccione **actualización**.</span><span class="sxs-lookup"><span data-stu-id="13350-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="13350-174">El origen aparece ahora en el selector de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="13350-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="13350-175">Para cambiar un origen del paquete, selecciónelo, realice modificaciones en el **nombre** y **origen** cuadros y seleccione **actualización**.</span><span class="sxs-lookup"><span data-stu-id="13350-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="13350-176">Para deshabilitar un origen del paquete, desactive la casilla a la izquierda del nombre de la lista.</span><span class="sxs-lookup"><span data-stu-id="13350-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="13350-177">Para quitar un origen del paquete, selecciónelo y, a continuación, seleccione el **X** botón.</span><span class="sxs-lookup"><span data-stu-id="13350-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="13350-178">Usar arriba y flecha abajo botones no cambian el orden de prioridad de los orígenes del paquete.</span><span class="sxs-lookup"><span data-stu-id="13350-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="13350-179">Visual Studio omite el orden de los orígenes de paquetes, mediante el paquete del origen que primero responda a las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="13350-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="13350-180">Para obtener más información, consulte [restauración del paquete](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="13350-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="13350-181">Si se vuelve a aparecer en un origen de paquete después de eliminarlo, pueden mostrarse en un nivel de equipo o el nivel de usuario `NuGet.Config` archivos.</span><span class="sxs-lookup"><span data-stu-id="13350-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="13350-182">Consulte [configuraciones comunes NuGet](../consume-packages/configuring-nuget-behavior.md) para la ubicación de estos archivos, a continuación, quitar el origen de editar manualmente los archivos o usando el [nuget orígenes comando](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="13350-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="13350-183">Controlan las opciones del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="13350-183">Package manager Options control</span></span>

<span data-ttu-id="13350-184">Cuando se selecciona un paquete, el Administrador de paquetes de UI muestra un pequeño expandible **opciones** control debajo el selector de versión (se muestra aquí tanto contraen y expanden).</span><span class="sxs-lookup"><span data-stu-id="13350-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="13350-185">Tenga en cuenta que para algunos proyectos, tipos, solo el **Mostrar ventana de vista previa** opción se proporciona.</span><span class="sxs-lookup"><span data-stu-id="13350-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opciones del Administrador de paquetes](media/PackageManagerUIOptions.png)

<span data-ttu-id="13350-187">Las siguientes secciones explican estas opciones.</span><span class="sxs-lookup"><span data-stu-id="13350-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="13350-188">Mostrar ventana de vista previa</span><span class="sxs-lookup"><span data-stu-id="13350-188">Show preview window</span></span>

<span data-ttu-id="13350-189">Cuando se selecciona, una ventana modal muestra que las dependencias de un paquete elegido antes de instalar el paquete:</span><span class="sxs-lookup"><span data-stu-id="13350-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Cuadro de diálogo de vista previa de ejemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="13350-191">Instalar y actualizar las opciones</span><span class="sxs-lookup"><span data-stu-id="13350-191">Install and Update Options</span></span>

<span data-ttu-id="13350-192">(No disponible para todos los tipos de proyecto).</span><span class="sxs-lookup"><span data-stu-id="13350-192">(Not available for all project types.)</span></span>

<span data-ttu-id="13350-193">**Comportamiento de dependencia** configura cómo NuGet decide qué versiones de los paquetes dependientes para instalar:</span><span class="sxs-lookup"><span data-stu-id="13350-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="13350-194">*Pasar por alto las dependencias* omite instalar las dependencias, lo que interrumpe normalmente está instalado el paquete.</span><span class="sxs-lookup"><span data-stu-id="13350-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="13350-195">*Menor* [predeterminado] la dependencia instala con el número de versión mínima que cumple los requisitos del paquete principal elegido.</span><span class="sxs-lookup"><span data-stu-id="13350-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="13350-196">*Revisión mayor* instala la versión con los mismos números de versión principal y secundaria, pero el mayor número de revisión.</span><span class="sxs-lookup"><span data-stu-id="13350-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="13350-197">Por ejemplo, si se especifica la versión 1.2.2 se instalará la versión más reciente que se inicia con 1.2</span><span class="sxs-lookup"><span data-stu-id="13350-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="13350-198">*Minor mayor* instala la versión con el mismo número de versión principal, pero el número secundario más alto y el número de revisión.</span><span class="sxs-lookup"><span data-stu-id="13350-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="13350-199">Si se especifica la versión 1.2.2, se instalará la versión más alta que empieza por 1</span><span class="sxs-lookup"><span data-stu-id="13350-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="13350-200">*Mayor* instala la versión más alta disponible del paquete.</span><span class="sxs-lookup"><span data-stu-id="13350-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="13350-201">**Acción de conflictos de archivos** especifica cómo NuGet debe controlar los paquetes que ya existen en el proyecto o equipo local:</span><span class="sxs-lookup"><span data-stu-id="13350-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="13350-202">*Símbolo del sistema* indica a NuGet que pregunta si desea conservar o sobrescribir los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="13350-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="13350-203">*Omitir todo* indica a NuGet que omitir sobrescribir todos los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="13350-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="13350-204">*Sobrescribir todos* indica a NuGet para sobrescribir todos los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="13350-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="13350-205">Opciones de desinstalación</span><span class="sxs-lookup"><span data-stu-id="13350-205">Uninstall Options</span></span>

<span data-ttu-id="13350-206">(No disponible para todos los tipos de proyecto).</span><span class="sxs-lookup"><span data-stu-id="13350-206">(Not available for all project types.)</span></span>

<span data-ttu-id="13350-207">**Quitar las dependencias**: cuando se selecciona, quita los paquetes dependientes si no hay referencias en otro lugar en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="13350-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="13350-208">**Forzar la desinstalación incluso si existen dependencias en él**: cuando se selecciona, se desinstala un paquete incluso si se todavía se hace referencia en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="13350-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="13350-209">Esto normalmente se usa en combinación con **quitar las dependencias** para quitar un paquete y lo instala las dependencias.</span><span class="sxs-lookup"><span data-stu-id="13350-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="13350-210">Con esta opción sin embargo, podría dar lugar a referencias erróneas en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="13350-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="13350-211">En tales casos, es posible que deba [reinstalar esos otros paquetes](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="13350-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
