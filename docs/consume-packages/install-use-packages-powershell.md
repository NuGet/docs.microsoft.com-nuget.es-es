---
title: Instalación y administración de paquetes NuGet mediante la consola en Visual Studio
description: Instrucciones para usar la consola del Administrador de paquetes NuGet en Visual Studio para trabajar con paquetes.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611102"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="cd1a8-103">Instalación y administración de paquetes con la consola del Administrador de paquetes en Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="cd1a8-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="cd1a8-104">La consola del Administrador de paquetes NuGet le permite usar [comandos de PowerShell de NuGet](../reference/powershell-reference.md) para buscar, instalar, desinstalar y actualizar paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="cd1a8-105">Usar la consola es necesarios cuando la interfaz de usuario del Administrador de paquetes no ofrece una manera de realizar una operación.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="cd1a8-106">Para usar los comandos de la CLI `nuget.exe` en la consola, consulte la sección sobre el [uso de la CLI nuget.exe en la consola](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="cd1a8-107">La consola está integrada en Visual Studio en Windows.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="cd1a8-108">No se incluye con Visual Studio para Mac ni con Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="cd1a8-109">Búsqueda e instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="cd1a8-109">Find and install a package</span></span>

<span data-ttu-id="cd1a8-110">Por ejemplo, buscar e instalar un paquete se hace con tres pasos sencillos:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="cd1a8-111">Abra el proyecto o la solución en Visual Studio y abra la consola con el comando **Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="cd1a8-112">Busque el paquete que quiere instalar.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-112">Find the package you want to install.</span></span> <span data-ttu-id="cd1a8-113">Si ya sabe cuál es, vaya al paso 3.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="cd1a8-114">Ejecute el comando de instalación:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="cd1a8-115">Todas las operaciones disponibles en la consola también se puede realizar con la [CLI de NuGet](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="cd1a8-116">Sin embargo, los comandos de la consola funcionan dentro del contexto de Visual Studio y una solución o proyecto guardado y, a menudo, logran más que sus comandos de la CLI equivalentes.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="cd1a8-117">Por ejemplo, instalar un paquete a través de la consola agrega una referencia al proyecto, mientras que el comando de la CLI no lo hace.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="cd1a8-118">Por esta razón, los desarrolladores que trabajan en Visual Studio por lo general prefieren usar la consola en lugar de la CLI.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="cd1a8-119">Muchas operaciones de la consola dependen de tener una solución abierta en Visual Studio con un nombre de ruta de acceso conocido.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="cd1a8-120">Si tiene una solución no guardada, o no tiene ninguna solución, es posible que vea el error "La solución no está abierta ni guardada.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="cd1a8-121">Asegúrese de tener una solución abierta y guardada".</span><span class="sxs-lookup"><span data-stu-id="cd1a8-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="cd1a8-122">Esto indica que la consola no puede determinar la carpeta de la solución.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="cd1a8-123">Al guardar una solución no guardada o al crear y guardar una solución si no hay ninguna abierta se debería corregir el error.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="cd1a8-124">Apertura de la consola y sus controles</span><span class="sxs-lookup"><span data-stu-id="cd1a8-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="cd1a8-125">Para abrir la consola en Visual Studio, use el comando **Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="cd1a8-126">La consola es una ventana de Visual Studio que se puede organizar y posicionar como quiera (consulte [Personalizar los diseños de ventana de Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="cd1a8-127">De manera predeterminada, los comandos de la consola operan en un proyecto y origen de paquete específico, tal como se establece en el control en la parte superior de la ventana:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Controles de la consola del Administrador de paquetes para un proyecto y origen de paquete](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="cd1a8-129">Si selecciona un origen de paquete o un proyecto distinto, estos valores predeterminados se cambian por los comandos subsiguientes.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="cd1a8-130">Para invalidar esta configuración sin cambiar los valores predeterminados, la mayoría de los comandos admiten las opciones `-Source` y `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="cd1a8-131">Para administrar los orígenes de paquete, seleccione el icono de engranaje.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="cd1a8-132">Se trata de un acceso directo al cuadro de diálogo **Herramientas > Opciones > Administrador de paquetes NuGet > Orígenes de paquetes** tal como se describe en la página sobre la [interfaz de usuario del Administrador de paquetes](install-use-packages-visual-studio.md#package-sources).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="cd1a8-133">Además, el control ubicado a la derecha del selector de proyectos borra el contenido de la consola:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Configuración de la consola del Administrador de paquetes y controles de borrado](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="cd1a8-135">El botón que está más a la derecha interrumpe un comando de ejecución de larga duración.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="cd1a8-136">Por ejemplo, si ejecuta `Get-Package -ListAvailable -PageSize 500` se muestran los primeros 500 paquetes en el origen predeterminado (como nuget.org), lo que podría tardar varios minutos en ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Control de detención de la consola del Administrador de paquetes](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="cd1a8-138">Instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="cd1a8-139">Consulte [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="cd1a8-140">Al instalar un paquete en la consola se llevan a cabo los mismos pasos que se describen en [¿Qué ocurre cuando se instala un paquete?](../concepts/package-installation-process.md) con las siguientes incorporaciones:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="cd1a8-141">En esta ventana, la consola muestra los términos de licencia con un contrato implícito.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="cd1a8-142">Si no está de acuerdo con los términos, debe desinstalar inmediatamente el paquete.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="cd1a8-143">También se agrega una referencia al paquete en el archivo del proyecto y aparece en el **Explorador de soluciones** en el nodo **Referencias**. Para ver directamente los cambios en el archivo del proyecto, debe guardar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="cd1a8-144">Desinstala un paquete.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="cd1a8-145">Consulte [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="cd1a8-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) para ver todos los paquetes que están instalados actualmente en el proyecto predeterminado si necesita buscar un identificador.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="cd1a8-147">Al desinstalar un paquete se llevan a cabo las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="cd1a8-148">Se quitan las referencias al paquete del proyecto (y todos los formatos de administración que estén en uso).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="cd1a8-149">Las referencias ya no aparecen en el **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="cd1a8-150">(Es posible que tenga que recompilar el proyecto para ver que se quitó de la carpeta **Bin**).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="cd1a8-151">Invierte los cambios realizados en `app.config` o en `web.config` cuando se instaló el paquete.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="cd1a8-152">Quita las dependencias instaladas previamente si no queda ningún paquete que las use.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="cd1a8-153">Actualización de un paquete</span><span class="sxs-lookup"><span data-stu-id="cd1a8-153">Update a package</span></span>

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

<span data-ttu-id="cd1a8-154">Consulte [Get-Package](../reference/ps-reference/ps-ref-get-package.md) y [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="cd1a8-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="cd1a8-155">Búsqueda de un paquete</span><span class="sxs-lookup"><span data-stu-id="cd1a8-155">Find a package</span></span>

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

<span data-ttu-id="cd1a8-156">Consulte [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="cd1a8-157">En Visual Studio 2013 y versiones anteriores, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="cd1a8-158">Disponibilidad de la consola</span><span class="sxs-lookup"><span data-stu-id="cd1a8-158">Availability of the console</span></span>

<span data-ttu-id="cd1a8-159">A partir de Visual Studio 2017, NuGet y el Administrador de paquetes NuGet se instalan automáticamente cuando se selecciona cualquier carga de trabajo relacionada con .NET, también puede instalarla de manera individual si activa la opción **Componentes individuales > Herramientas de código > Administrador de paquetes NuGet** en el instalador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="cd1a8-160">Además, si falta el Administrador de paquetes NuGet en Visual Studio 2015 y versiones anteriores, revise **Herramientas > Extensiones y actualizaciones…** y busque la extensión Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="cd1a8-161">Si no puede usar el instalador de extensiones en Visual Studio, puede descargar la extensión directamente de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="cd1a8-162">Actualmente, la consola del Administrador de paquetes no está disponible con Visual Studio para Mac.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="cd1a8-163">Sin embargo, hay comandos equivalentes disponibles a través de la [CLI de NuGet](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="cd1a8-164">Visual Studio para Mac sí tiene una interfaz de usuario para administrar paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="cd1a8-165">Consulte [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="cd1a8-166">La consola del Administrador de paquetes no está incluida en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="cd1a8-167">Extensión de la consola del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="cd1a8-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="cd1a8-168">Algunos paquetes instalan comandos nuevos para la consola.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="cd1a8-169">Por ejemplo, `MvcScaffolding` crea comandos como `Scaffold` que se muestra a continuación, el que genera vistas y controladores de MVC de ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalación y uso de MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="cd1a8-171">Configuración de un perfil de PowerShell de NuGet</span><span class="sxs-lookup"><span data-stu-id="cd1a8-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="cd1a8-172">Un perfil de PowerShell le permite usar los comandos de uso común disponibles cada vez que use PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd1a8-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="cd1a8-173">NuGet admite un perfil específico de NuGet que habitualmente se encuentra en esta ubicación:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="cd1a8-174">Para buscar el perfil, escriba `$profile` en la consola:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="cd1a8-175">Para más detalles, consulte [Perfiles de Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd1a8-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="cd1a8-176">Uso de la CLI nuget.exe en la consola</span><span class="sxs-lookup"><span data-stu-id="cd1a8-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="cd1a8-177">Para que la [CLI `nuget.exe`](../reference/nuget-exe-cli-reference.md) esté disponible en la consola del Administrador de paquetes, instale el paquete [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) desde la consola:</span><span class="sxs-lookup"><span data-stu-id="cd1a8-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
