---
title: Referencia de la interfaz de usuario del Administrador de paquetes de NuGet
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
ms.openlocfilehash: 1de6ddeca6295c621a90409807af198bc3c7a068
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981189"
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="d860c-103">Interfaz de usuario del Administrador de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="d860c-103">NuGet Package Manager UI</span></span>

<span data-ttu-id="d860c-104">La UI Administrador de paquetes de NuGet en Visual Studio en Windows le permite instalar, desinstalar y actualizar paquetes de NuGet en proyectos y soluciones con facilidad.</span><span class="sxs-lookup"><span data-stu-id="d860c-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="d860c-105">Para obtener la experiencia en Visual Studio para Mac, consulte [incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="d860c-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="d860c-106">El Administrador de paquetes de UI no se incluye con Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d860c-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="d860c-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="d860c-107">In this topic:</span></span>

- [<span data-ttu-id="d860c-108">Búsqueda e instalación de un paquete (pestaña Examinar)</span><span class="sxs-lookup"><span data-stu-id="d860c-108">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="d860c-109">Al desinstalar un paquete (pestaña instalados)</span><span class="sxs-lookup"><span data-stu-id="d860c-109">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="d860c-110">[Actualizar un paquete (pestañas instaladas y actualizaciones)](#updating-a-package) (incluye el ["Implícitamente que se hace referencia mediante un SDK" o "Compatibilidad con AutoReferenced" mensaje](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="d860c-110">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="d860c-111">[Administración de paquetes para la solución](#managing-packages-for-the-solution) (trabajar con varios proyectos al mismo tiempo).</span><span class="sxs-lookup"><span data-stu-id="d860c-111">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="d860c-112">Orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="d860c-112">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="d860c-113">Controlan las opciones del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="d860c-113">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="d860c-114">Compruebe si faltan el Administrador de paquetes de NuGet en Visual Studio 2015, **Herramientas > extensiones y actualizaciones...**  y busque el *Administrador de paquetes de NuGet* extensión.</span><span class="sxs-lookup"><span data-stu-id="d860c-114">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="d860c-115">Si no puede usar el instalador de extensiones de Visual Studio, descargue la extensión directamente desde [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="d860c-115">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="d860c-116">En Visual Studio 2017, NuGet y el Administrador de paquetes de NuGet se instalan automáticamente con cualquiera. Cargas de trabajo relacionados con la red.</span><span class="sxs-lookup"><span data-stu-id="d860c-116">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="d860c-117">Instálelo individualmente seleccionando el **componentes individuales > herramientas de código > Administrador de paquetes de NuGet** opción en el instalador de Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d860c-117">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="d860c-118">Búsqueda e instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="d860c-118">Finding and installing a package</span></span>

1. <span data-ttu-id="d860c-119">En **el Explorador de soluciones**, haga clic en cualquiera **referencias** o un proyecto y seleccione **administrar paquetes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="d860c-119">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Administrar la opción de menú de paquetes de NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="d860c-121">El **examinar** pestaña muestra los paquetes por popularidad del origen seleccionado actualmente (vea [orígenes de paquetes](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="d860c-121">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="d860c-122">Busque un paquete específico mediante el cuadro de búsqueda en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="d860c-122">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="d860c-123">Seleccione un paquete de la lista para mostrar su información, lo cual habilita también el **instalar** botón junto con una lista desplegable de selección de versión.</span><span class="sxs-lookup"><span data-stu-id="d860c-123">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Administrar la ficha cuadro de diálogo Examinar de paquetes de NuGet](media/Search.png)

1. <span data-ttu-id="d860c-125">Seleccione la versión deseada de la lista desplegable y seleccione **instalar**.</span><span class="sxs-lookup"><span data-stu-id="d860c-125">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="d860c-126">Visual Studio instala el paquete y sus dependencias en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d860c-126">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="d860c-127">Se le pedirá que acepte los términos de licencia.</span><span class="sxs-lookup"><span data-stu-id="d860c-127">You may be asked to accept license terms.</span></span> <span data-ttu-id="d860c-128">Cuando se complete la instalación, los paquetes agregados aparecen en la **instalado** ficha. Los paquetes también se enumeran en la **referencias** nodo del explorador de soluciones, que indica que puede hacer referencia a ellas en el proyecto con `using` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="d860c-128">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Referencias en el Explorador de soluciones](media/References.png)

> [!Tip]
> <span data-ttu-id="d860c-130">Para incluir versiones preliminares en la búsqueda y para que las versiones preliminares disponibles en la versión lista desplegable, seleccione el **incluir versión preliminar** opción.</span><span class="sxs-lookup"><span data-stu-id="d860c-130">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="d860c-131">Al desinstalar un paquete</span><span class="sxs-lookup"><span data-stu-id="d860c-131">Uninstalling a package</span></span>

1. <span data-ttu-id="d860c-132">En **el Explorador de soluciones**, haga clic en cualquiera **referencias** o el proyecto que desee y seleccione **administrar paquetes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="d860c-132">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="d860c-133">Seleccione el **instalado** ficha.</span><span class="sxs-lookup"><span data-stu-id="d860c-133">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="d860c-134">Seleccione el paquete para desinstalar (mediante la búsqueda para filtrar la lista si es necesario) y seleccione **desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="d860c-134">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Al desinstalar un paquete](media/UninstallPackage.png)

1. <span data-ttu-id="d860c-136">Tenga en cuenta que el **incluir versión preliminar** y **origen del paquete** controles no tienen ningún efecto cuando se desinstala los paquetes.</span><span class="sxs-lookup"><span data-stu-id="d860c-136">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="d860c-137">Actualizar un paquete</span><span class="sxs-lookup"><span data-stu-id="d860c-137">Updating a package</span></span>

1. <span data-ttu-id="d860c-138">En **el Explorador de soluciones**, haga clic en cualquiera **referencias** o el proyecto que desee y seleccione **administrar paquetes NuGet...** . (En proyectos de sitios web, haga clic en el **Bin** carpeta.)</span><span class="sxs-lookup"><span data-stu-id="d860c-138">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="d860c-139">Seleccione el **actualizaciones** pestaña para ver los paquetes que tienen actualizaciones disponibles desde los orígenes del paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d860c-139">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="d860c-140">Seleccione **incluir versión preliminar** para incluir paquetes de versión preliminar en la lista de actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="d860c-140">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="d860c-141">Seleccione el paquete para actualizar, seleccione la versión deseada de la lista desplegable de la derecha y seleccione **actualizar**.</span><span class="sxs-lookup"><span data-stu-id="d860c-141">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Actualizar un paquete](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="d860c-143">Para algunos paquetes, el **actualización** botón está deshabilitado y aparece un mensaje que indica que se "hace referencia implícitamente mediante un SDK" (o "Compatibilidad con AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="d860c-143">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="d860c-144">Este mensaje indica que el paquete forma parte de un marco de trabajo o SDK más grande y no se debe actualizar de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="d860c-144">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="d860c-145">(Estos paquetes internamente se marcan con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Por ejemplo, `Microsoft.NETCore.App` es parte del SDK de .NET Core y la versión del paquete no es igual que la versión de framework en tiempo de ejecución utilizado por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d860c-145">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="d860c-146">Deberá [actualizar su instalación de .NET Core](https://aka.ms/dotnet-download) para obtener nuevas versiones del tiempo de ejecución de ASP.NET Core y .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d860c-146">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="d860c-147">[Consulte este documento para obtener más detalles sobre los metapaquetes de .NET Core y control de versiones](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="d860c-147">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="d860c-148">Esto se aplica a los siguientes paquetes usados:</span><span class="sxs-lookup"><span data-stu-id="d860c-148">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="d860c-149">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="d860c-149">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="d860c-150">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="d860c-150">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="d860c-151">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="d860c-151">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="d860c-152">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="d860c-152">NETStandard.Library</span></span>

    ![Paquete de ejemplo marcada como implícitamente las referencias o compatibilidad con AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="d860c-154">Para actualizar varios paquetes a sus versiones más recientes, selecciónelos en la lista y seleccione el **actualizar** botón encima de la lista.</span><span class="sxs-lookup"><span data-stu-id="d860c-154">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="d860c-155">También puede actualizar un paquete individual desde la **instalado** ficha. En este caso, los detalles para el paquete incluyen un selector de versión (sujeto a la **incluir versión preliminar** opción) y un **actualización** botón.</span><span class="sxs-lookup"><span data-stu-id="d860c-155">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="d860c-156">Administración de paquetes para la solución</span><span class="sxs-lookup"><span data-stu-id="d860c-156">Managing packages for the solution</span></span>

<span data-ttu-id="d860c-157">Administración de paquetes para una solución es un medio cómodo para trabajar con varios proyectos simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="d860c-157">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="d860c-158">Seleccione el **Herramientas > Administrador de paquetes NuGet > Administrar paquetes de NuGet para la solución...**  menú de comandos, o haga clic en la solución y seleccione **administrar paquetes NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="d860c-158">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Administrar paquetes de NuGet para la solución](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="d860c-160">Al administrar los paquetes para la solución, la interfaz de usuario le permite seleccionar los proyectos que se ven afectados por las operaciones:</span><span class="sxs-lookup"><span data-stu-id="d860c-160">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selector de proyecto al administrar los paquetes para la solución](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="d860c-162">Consolidar pestaña</span><span class="sxs-lookup"><span data-stu-id="d860c-162">Consolidate tab</span></span>

<span data-ttu-id="d860c-163">Normalmente los desarrolladores consideran mala práctica usar diferentes versiones del mismo paquete de NuGet en los distintos proyectos en la misma solución.</span><span class="sxs-lookup"><span data-stu-id="d860c-163">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="d860c-164">Si decide administrar los paquetes para una solución, el Administrador de paquetes de UI proporciona una **consolidar** ficha en el que puede ver fácilmente donde diferentes proyectos de la solución usa los paquetes con números de versión distintos:</span><span class="sxs-lookup"><span data-stu-id="d860c-164">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Pestaña consolidar de interfaz de usuario de administrador de paquetes](media/ConsolidateTab.png)

<span data-ttu-id="d860c-166">En este ejemplo, el proyecto ClassLibrary1 usa Entity Framework de la 6.2.0, mientras que usa EntityFramework 6.1.0 ConsoleApp1.</span><span class="sxs-lookup"><span data-stu-id="d860c-166">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="d860c-167">Para consolidar las versiones del paquete, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d860c-167">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="d860c-168">Seleccione los proyectos que se actualizará en la lista de proyectos.</span><span class="sxs-lookup"><span data-stu-id="d860c-168">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="d860c-169">Seleccione la versión que se usará en todos los proyectos de la **versión** control, como la 6.2.0 EntityFramework.</span><span class="sxs-lookup"><span data-stu-id="d860c-169">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="d860c-170">Seleccione el **instalar** botón.</span><span class="sxs-lookup"><span data-stu-id="d860c-170">Select the **Install** button.</span></span>

<span data-ttu-id="d860c-171">El Administrador de paquetes se instala la versión del paquete seleccionado en todos los proyectos seleccionados, después de que el paquete ya no aparece en el **consolidar** ficha.</span><span class="sxs-lookup"><span data-stu-id="d860c-171">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="d860c-172">Orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="d860c-172">Package sources</span></span>

<span data-ttu-id="d860c-173">Para cambiar el origen de los que Visual Studio obtiene los paquetes, seleccione uno en el selector de origen:</span><span class="sxs-lookup"><span data-stu-id="d860c-173">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selector de origen de paquete en el Administrador de paquetes de interfaz de usuario](media/PackageSourceDropDown.png)

<span data-ttu-id="d860c-175">Para administrar orígenes de paquetes:</span><span class="sxs-lookup"><span data-stu-id="d860c-175">To manage package sources:</span></span>

1. <span data-ttu-id="d860c-176">Seleccione el **configuración** icono en la UI del Administrador de paquetes que se describen a continuación o usar el **Herramientas > opciones** de comandos y desplácese hasta **Administrador de paquetes de NuGet**:</span><span class="sxs-lookup"><span data-stu-id="d860c-176">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Icono de configuración de la interfaz de usuario Administrador de paquetes](media/PackageSourceSettings.png)

1. <span data-ttu-id="d860c-178">Seleccione el **orígenes de paquetes** nodo:</span><span class="sxs-lookup"><span data-stu-id="d860c-178">Select the **Package Sources** node:</span></span>

    ![Opciones de orígenes de paquetes](media/options.png)

1. <span data-ttu-id="d860c-180">Para agregar un origen, seleccione **+**, edite el nombre, escriba la dirección URL o ruta de acceso en el **origen** control y seleccione **actualización**.</span><span class="sxs-lookup"><span data-stu-id="d860c-180">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="d860c-181">El origen aparece ahora en el selector de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="d860c-181">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="d860c-182">Para cambiar un origen del paquete, selecciónelo, realice modificaciones en el **nombre** y **origen** cuadros y seleccione **actualización**.</span><span class="sxs-lookup"><span data-stu-id="d860c-182">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="d860c-183">Para deshabilitar un origen del paquete, desactive la casilla a la izquierda del nombre de la lista.</span><span class="sxs-lookup"><span data-stu-id="d860c-183">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="d860c-184">Para quitar un origen del paquete, selecciónelo y, a continuación, seleccione el **X** botón.</span><span class="sxs-lookup"><span data-stu-id="d860c-184">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="d860c-185">Arriba y abajo botones de flecha para cambiar el orden de prioridad de los orígenes del paquete.</span><span class="sxs-lookup"><span data-stu-id="d860c-185">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="d860c-186">Visual Studio busca estos orígenes en el orden de prioridad al restaurar los paquetes de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="d860c-186">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="d860c-187">Para obtener más información, consulte [restauración del paquete](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="d860c-187">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="d860c-188">Si se vuelve a aparecer en un origen de paquete después de eliminarlo, pueden mostrarse en un nivel de equipo o el nivel de usuario `NuGet.Config` archivos.</span><span class="sxs-lookup"><span data-stu-id="d860c-188">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="d860c-189">Consulte [del comportamiento de configuración de NuGet](../consume-packages/configuring-nuget-behavior.md) para la ubicación de estos archivos, a continuación, quitar el origen de editar manualmente los archivos o usando el [nuget orígenes comando](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d860c-189">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="d860c-190">Controlan las opciones del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="d860c-190">Package manager Options control</span></span>

<span data-ttu-id="d860c-191">Cuando se selecciona un paquete, el Administrador de paquetes de UI muestra un pequeño expandible **opciones** control debajo el selector de versión (se muestra aquí tanto contraen y expanden).</span><span class="sxs-lookup"><span data-stu-id="d860c-191">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="d860c-192">Tenga en cuenta que para algunos proyectos, tipos, solo el **Mostrar ventana de vista previa** opción se proporciona.</span><span class="sxs-lookup"><span data-stu-id="d860c-192">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opciones del Administrador de paquetes](media/PackageManagerUIOptions.png)

<span data-ttu-id="d860c-194">Las siguientes secciones explican estas opciones.</span><span class="sxs-lookup"><span data-stu-id="d860c-194">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="d860c-195">Mostrar ventana de vista previa</span><span class="sxs-lookup"><span data-stu-id="d860c-195">Show preview window</span></span>

<span data-ttu-id="d860c-196">Cuando se selecciona, una ventana modal muestra que las dependencias de un paquete elegido antes de instalar el paquete:</span><span class="sxs-lookup"><span data-stu-id="d860c-196">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Cuadro de diálogo de vista previa de ejemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="d860c-198">Instalar y actualizar las opciones</span><span class="sxs-lookup"><span data-stu-id="d860c-198">Install and Update Options</span></span>

<span data-ttu-id="d860c-199">(No disponible para todos los tipos de proyecto).</span><span class="sxs-lookup"><span data-stu-id="d860c-199">(Not available for all project types.)</span></span>

<span data-ttu-id="d860c-200">**Comportamiento de dependencia** configura cómo NuGet decide qué versiones de los paquetes dependientes para instalar:</span><span class="sxs-lookup"><span data-stu-id="d860c-200">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="d860c-201">*Pasar por alto las dependencias* omite instalar las dependencias, lo que interrumpe normalmente está instalado el paquete.</span><span class="sxs-lookup"><span data-stu-id="d860c-201">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="d860c-202">*Menor* [predeterminado] la dependencia instala con el número de versión mínima que cumple los requisitos del paquete principal elegido.</span><span class="sxs-lookup"><span data-stu-id="d860c-202">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="d860c-203">*Revisión mayor* instala la versión con los mismos números de versión principal y secundaria, pero el mayor número de revisión.</span><span class="sxs-lookup"><span data-stu-id="d860c-203">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="d860c-204">Por ejemplo, si se especifica la versión 1.2.2 se instalará la versión más reciente que se inicia con 1.2</span><span class="sxs-lookup"><span data-stu-id="d860c-204">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="d860c-205">*Minor mayor* instala la versión con el mismo número de versión principal, pero el número secundario más alto y el número de revisión.</span><span class="sxs-lookup"><span data-stu-id="d860c-205">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="d860c-206">Si se especifica la versión 1.2.2, se instalará la versión más alta que empieza por 1</span><span class="sxs-lookup"><span data-stu-id="d860c-206">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="d860c-207">*Mayor* instala la versión más alta disponible del paquete.</span><span class="sxs-lookup"><span data-stu-id="d860c-207">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="d860c-208">**Acción de conflictos de archivos** especifica cómo NuGet debe controlar los paquetes que ya existen en el proyecto o equipo local:</span><span class="sxs-lookup"><span data-stu-id="d860c-208">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="d860c-209">*Símbolo del sistema* indica a NuGet que pregunta si desea conservar o sobrescribir los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="d860c-209">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="d860c-210">*Omitir todo* indica a NuGet que omitir sobrescribir todos los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="d860c-210">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="d860c-211">*Sobrescribir todos* indica a NuGet para sobrescribir todos los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="d860c-211">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="d860c-212">Opciones de desinstalación</span><span class="sxs-lookup"><span data-stu-id="d860c-212">Uninstall Options</span></span>

<span data-ttu-id="d860c-213">(No disponible para todos los tipos de proyecto).</span><span class="sxs-lookup"><span data-stu-id="d860c-213">(Not available for all project types.)</span></span>

<span data-ttu-id="d860c-214">**Quitar las dependencias**: cuando se selecciona, quita los paquetes dependientes si no hay referencias en otro lugar en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d860c-214">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="d860c-215">**Forzar la desinstalación incluso si existen dependencias en él**: cuando se selecciona, se desinstala un paquete incluso si se todavía se hace referencia en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d860c-215">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="d860c-216">Esto normalmente se usa en combinación con **quitar las dependencias** para quitar un paquete y lo instala las dependencias.</span><span class="sxs-lookup"><span data-stu-id="d860c-216">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="d860c-217">Con esta opción sin embargo, podría dar lugar a referencias erróneas en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d860c-217">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="d860c-218">En tales casos, es posible que deba [reinstalar esos otros paquetes](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d860c-218">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
