---
title: "Guía de consola de administrador de paquetes de NuGet | Documentos de Microsoft"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
description: Instrucciones para usar la consola de administrador de paquetes de NuGet en Visual Studio para trabajar con paquetes.
keywords: Consola de administrador de paquetes de NuGet, powershell de NuGet, administrar paquetes de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc11963a9b9bfe9aa456d8cd4c8397e1084f660b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="f96d0-104">Consola de administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="f96d0-104">Package Manager Console</span></span>

<span data-ttu-id="f96d0-105">La consola de administrador de paquetes de NuGet se compila en Visual Studio en Windows 2012 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="f96d0-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="f96d0-106">(No se incluye con Visual Studio para Mac o código de Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="f96d0-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="f96d0-107">La consola le permite usar [comandos de NuGet PowerShell](../tools/powershell-reference.md) para buscar, instalar, desinstalar y actualizar paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f96d0-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="f96d0-108">Es necesario en casos donde la UI del Administrador de paquetes no proporciona una manera de realizar una operación mediante la consola.</span><span class="sxs-lookup"><span data-stu-id="f96d0-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span>

<span data-ttu-id="f96d0-109">Por ejemplo, la búsqueda e instalación de un paquete se realiza con tres sencillos pasos:</span><span class="sxs-lookup"><span data-stu-id="f96d0-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="f96d0-110">Abra el proyecto o la solución en Visual Studio y abra la consola utilizando la **Herramientas > Administrador de paquetes de NuGet > Package Manager Console** comando.</span><span class="sxs-lookup"><span data-stu-id="f96d0-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="f96d0-111">Busque el paquete que desea instalar.</span><span class="sxs-lookup"><span data-stu-id="f96d0-111">Find the package you want to install.</span></span> <span data-ttu-id="f96d0-112">Si ya sabe esto, vaya al paso 3.</span><span class="sxs-lookup"><span data-stu-id="f96d0-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="f96d0-113">Ejecute el comando de instalación:</span><span class="sxs-lookup"><span data-stu-id="f96d0-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

<span data-ttu-id="f96d0-114">En este tema:</span><span class="sxs-lookup"><span data-stu-id="f96d0-114">In this topic:</span></span>

- [<span data-ttu-id="f96d0-115">Abra la consola de</span><span class="sxs-lookup"><span data-stu-id="f96d0-115">Opening the console</span></span>](#opening-the-console-and-console-controls)
- [<span data-ttu-id="f96d0-116">Instalar un paquete</span><span class="sxs-lookup"><span data-stu-id="f96d0-116">Installing a package</span></span>](#installing-a-package)
- [<span data-ttu-id="f96d0-117">Desinstalar un paquete</span><span class="sxs-lookup"><span data-stu-id="f96d0-117">Uninstalling a package</span></span>](#uninstalling-a-package)
- [<span data-ttu-id="f96d0-118">Buscar un paquete</span><span class="sxs-lookup"><span data-stu-id="f96d0-118">Finding a package</span></span>](#finding-a-package)
- [<span data-ttu-id="f96d0-119">Actualizar un paquete</span><span class="sxs-lookup"><span data-stu-id="f96d0-119">Updating a package</span></span>](#updating-a-package)
- [<span data-ttu-id="f96d0-120">Disponibilidad de la consola</span><span class="sxs-lookup"><span data-stu-id="f96d0-120">Availability of the console</span></span>](#availability-of-the-console)
- [<span data-ttu-id="f96d0-121">Extender la consola de administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="f96d0-121">Extending the Package Manager Console</span></span>](#extending-the-package-manager-console)
- [<span data-ttu-id="f96d0-122">Cómo configurar un perfil de NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="f96d0-122">Setting up a NuGet PowerShell profile</span></span>](#setting-up-a-nuget-powershell-profile)

> [!Important]
> <span data-ttu-id="f96d0-123">Todas las operaciones que están disponibles en la consola también pueden realizarse con el [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f96d0-123">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="f96d0-124">Sin embargo, comandos de la consola operan dentro del contexto de Visual Studio y una proyecto o solución guardada y a menudo llevar más de sus comandos CLI equivalente.</span><span class="sxs-lookup"><span data-stu-id="f96d0-124">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="f96d0-125">Por ejemplo, instalando un paquete mediante la consola de, agrega una referencia al proyecto, mientras que el comando CLI no.</span><span class="sxs-lookup"><span data-stu-id="f96d0-125">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="f96d0-126">Por este motivo, los desarrolladores que trabajan en Visual Studio normalmente prefieren mediante la consola de la CLI.</span><span class="sxs-lookup"><span data-stu-id="f96d0-126">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="f96d0-127">Muchas operaciones de consola dependen de tener una solución abierta en Visual Studio con un nombre de ruta de acceso conocida.</span><span class="sxs-lookup"><span data-stu-id="f96d0-127">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="f96d0-128">Si tiene una solución que no haya guardado o no hay ninguna solución, puede ver el error, "solución no está abierta o no guardada.</span><span class="sxs-lookup"><span data-stu-id="f96d0-128">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="f96d0-129">Asegúrese de que dispone de una solución abierta y guardada."</span><span class="sxs-lookup"><span data-stu-id="f96d0-129">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="f96d0-130">Esto indica que la consola no puede determinar la carpeta de soluciones.</span><span class="sxs-lookup"><span data-stu-id="f96d0-130">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="f96d0-131">Guardar una solución que no haya guardado, o crear y guardar una solución si no dispone de uno abierto, debe corregir el error.</span><span class="sxs-lookup"><span data-stu-id="f96d0-131">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="f96d0-132">Abra la consola y los controles de la consola</span><span class="sxs-lookup"><span data-stu-id="f96d0-132">Opening the console and console controls</span></span>

1. <span data-ttu-id="f96d0-133">Abra la consola en Visual Studio mediante el **Herramientas > Administrador de paquetes de NuGet > Package Manager Console** comando.</span><span class="sxs-lookup"><span data-stu-id="f96d0-133">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="f96d0-134">La consola es una ventana de Visual Studio que se pueden organizan y coloca sin embargo igual (vea [personalizar diseños de ventana de Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="f96d0-134">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="f96d0-135">De forma predeterminada, los comandos de consola operan en un origen de paquete específico y un proyecto como se establece en el control en la parte superior de la ventana:</span><span class="sxs-lookup"><span data-stu-id="f96d0-135">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Controles de la consola de administrador de paquetes de origen del paquete y proyecto](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="f96d0-137">Al seleccionar un origen de otro paquete o proyecto cambia los valores predeterminados para los comandos siguientes.</span><span class="sxs-lookup"><span data-stu-id="f96d0-137">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="f96d0-138">Admite la mayoría de los comandos anular estos valores sin cambiar los valores predeterminados, `-Source` y `-ProjectName` opciones.</span><span class="sxs-lookup"><span data-stu-id="f96d0-138">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="f96d0-139">Para administrar orígenes de paquetes, seleccione el icono de engranaje.</span><span class="sxs-lookup"><span data-stu-id="f96d0-139">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="f96d0-140">Se trata de un acceso directo a la **Herramientas > Opciones > Administrador de paquetes de NuGet > orígenes de paquetes** cuadro de diálogo tal como se describe en el [UI del Administrador de paquetes](Package-Manager-UI.md#package-sources) página.</span><span class="sxs-lookup"><span data-stu-id="f96d0-140">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span></span> <span data-ttu-id="f96d0-141">Además, el control a la derecha del selector de proyecto borra el contenido de la consola:</span><span class="sxs-lookup"><span data-stu-id="f96d0-141">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Configuración de la consola de administrador de paquetes y desactive los controles](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="f96d0-143">El botón situado interrumpe un comando de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="f96d0-143">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="f96d0-144">Por ejemplo, ejecutar `Get-Package -ListAvailable -PageSize 500` enumera los paquetes de 500 principales en el origen predeterminado (por ejemplo, nuget.org), que puede tardar varios minutos en ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="f96d0-144">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Control de detención de la consola de administrador de paquetes](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="f96d0-146">Instalar un paquete</span><span class="sxs-lookup"><span data-stu-id="f96d0-146">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="f96d0-147">Vea [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="f96d0-147">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="f96d0-148">Instalar un paquete realiza las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="f96d0-148">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="f96d0-149">Muestra los términos de licencia aplicables en la ventana de consola con acuerdo implícito.</span><span class="sxs-lookup"><span data-stu-id="f96d0-149">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="f96d0-150">Si no acepta los términos, debe desinstalar el paquete inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="f96d0-150">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="f96d0-151">Agrega una referencia al proyecto en el formato de referencia está en uso.</span><span class="sxs-lookup"><span data-stu-id="f96d0-151">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="f96d0-152">Las referencias posteriormente aparecen en el Explorador de soluciones y el archivo de formato de referencia aplicable.</span><span class="sxs-lookup"><span data-stu-id="f96d0-152">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="f96d0-153">Sin embargo, tenga en cuenta que con PackageReference, debe guardar el proyecto para ver los cambios en el archivo de proyecto directamente.</span><span class="sxs-lookup"><span data-stu-id="f96d0-153">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="f96d0-154">Almacena en caché el paquete:</span><span class="sxs-lookup"><span data-stu-id="f96d0-154">Caches the package:</span></span>
    - <span data-ttu-id="f96d0-155">PackageReference: el paquete está almacenado en caché en `%USERPROFILE%\.nuget\packages` y el bloqueo de archivos, es decir, `project.assets.json` se actualiza.</span><span class="sxs-lookup"><span data-stu-id="f96d0-155">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
    - <span data-ttu-id="f96d0-156">`packages.config`: crea un `packages` carpeta en la raíz de la solución y copia los archivos de paquete en una subcarpeta dentro de él.</span><span class="sxs-lookup"><span data-stu-id="f96d0-156">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="f96d0-157">El `package.config` archivo se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="f96d0-157">The `package.config` file is updated.</span></span>
- <span data-ttu-id="f96d0-158">Las actualizaciones de `app.config` o `web.config` si el paquete utiliza [transformaciones de archivos de origen y configuración](../create-packages/source-and-config-file-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="f96d0-158">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="f96d0-159">Instala todas las dependencias si no están ya presentes en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f96d0-159">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="f96d0-160">Esto podría actualizar versiones del paquete en el proceso, como se describe en [resolución de dependencia](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="f96d0-160">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="f96d0-161">Muestra al archivo Léame del paquete, si está disponible, en una ventana de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f96d0-161">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="f96d0-162">Una de las ventajas principales de la instalación de paquetes con el `Install-Package` comando en la consola es que agrega una referencia al proyecto como si ha usado la UI del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="f96d0-162">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="f96d0-163">En cambio, la `nuget install` comando de CLI de solo descarga el paquete y no se agrega automáticamente una referencia.</span><span class="sxs-lookup"><span data-stu-id="f96d0-163">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="f96d0-164">Desinstalar un paquete</span><span class="sxs-lookup"><span data-stu-id="f96d0-164">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="f96d0-165">Vea [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="f96d0-165">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="f96d0-166">Use [Get-Package](../tools/ps-ref-get-package.md) para ver todos los paquetes instalados actualmente en el proyecto predeterminado si fuese necesario encontrar un identificador.</span><span class="sxs-lookup"><span data-stu-id="f96d0-166">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="f96d0-167">Desinstalar un paquete realiza las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="f96d0-167">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="f96d0-168">Quita las referencias a los paquetes del proyecto (y cualquier formato de referencia está en uso).</span><span class="sxs-lookup"><span data-stu-id="f96d0-168">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="f96d0-169">Las referencias ya no aparecen en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="f96d0-169">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="f96d0-170">(Es posible que deba volver a generar el proyecto para verlo quita de la **Bin** carpeta.)</span><span class="sxs-lookup"><span data-stu-id="f96d0-170">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="f96d0-171">Invierte los cambios realizados en `app.config` o `web.config` cuando se instaló el paquete.</span><span class="sxs-lookup"><span data-stu-id="f96d0-171">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="f96d0-172">Quita instaladas con anterioridad dependencias si no hay paquetes restantes usan esas dependencias.</span><span class="sxs-lookup"><span data-stu-id="f96d0-172">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="f96d0-173">Al igual que `Install-Package`, el `Uninstall-Package` comando tiene la ventaja de administrar referencias en el proyecto, a diferencia de las `nuget uninstall` comando de CLI.</span><span class="sxs-lookup"><span data-stu-id="f96d0-173">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="f96d0-174">Actualizar un paquete</span><span class="sxs-lookup"><span data-stu-id="f96d0-174">Updating a package</span></span>

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

<span data-ttu-id="f96d0-175">Vea [Get-Package](../tools/ps-ref-get-package.md) y [paquete de actualización](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="f96d0-175">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="f96d0-176">Buscar un paquete</span><span class="sxs-lookup"><span data-stu-id="f96d0-176">Finding a package</span></span>

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

<span data-ttu-id="f96d0-177">Vea [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="f96d0-177">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="f96d0-178">En Visual Studio 2013 y versiones anteriores, utilice [Get-Package](../tools/ps-ref-get-package.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f96d0-178">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="f96d0-179">Disponibilidad de la consola</span><span class="sxs-lookup"><span data-stu-id="f96d0-179">Availability of the console</span></span>

<span data-ttu-id="f96d0-180">En Visual Studio 2017 NuGet y el Administrador de paquetes de NuGet se instalan automáticamente cuando se selecciona cualquiera. Cargas de trabajo relacionados con NET; También puede instalarlo por separado mediante la comprobación de la **componentes individuales > herramientas de código > Administrador de paquetes de NuGet** opción en el programa de instalación de Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="f96d0-180">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="f96d0-181">Además, compruebe si faltan el Administrador de paquetes de NuGet en Visual Studio 2015 y versiones anteriores, **Herramientas > extensiones y actualizaciones...**  y busque la extensión del Administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f96d0-181">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="f96d0-182">Si no puede usar el instalador de extensiones de Visual Studio, puede descargar la extensión directamente desde [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="f96d0-182">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="f96d0-183">La consola de administrador de paquetes no está actualmente disponible con Visual Studio para Mac.</span><span class="sxs-lookup"><span data-stu-id="f96d0-183">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="f96d0-184">Los comandos equivalentes, sin embargo, están disponibles a través de la [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f96d0-184">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="f96d0-185">Visual Studio para Mac tiene una interfaz de usuario para administrar paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f96d0-185">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="f96d0-186">Vea [paquete NuGet unos incluidos en el proyecto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="f96d0-186">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="f96d0-187">La consola de administrador de paquetes no se incluye con Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f96d0-187">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="f96d0-188">Extender la consola de administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="f96d0-188">Extending the Package Manager Console</span></span>

<span data-ttu-id="f96d0-189">Algunos paquetes instalarán nuevos comandos para la consola.</span><span class="sxs-lookup"><span data-stu-id="f96d0-189">Some packages install new commands for the console.</span></span> <span data-ttu-id="f96d0-190">Por ejemplo, `MvcScaffolding` crea comandos como `Scaffold` se muestra a continuación, lo cual genera ASP.NET MVC controladores y vistas:</span><span class="sxs-lookup"><span data-stu-id="f96d0-190">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalar y usar MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="f96d0-192">Cómo configurar un perfil de PowerShell de NuGet</span><span class="sxs-lookup"><span data-stu-id="f96d0-192">Setting up a NuGet PowerShell Profile</span></span>

<span data-ttu-id="f96d0-193">Un perfil de PowerShell le permite disponer de los comandos usados con frecuencia siempre que utilice PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f96d0-193">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="f96d0-194">NuGet es compatible con un perfil específico de NuGet que normalmente se encuentran en la siguiente ubicación:</span><span class="sxs-lookup"><span data-stu-id="f96d0-194">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="f96d0-195">Para encontrar el perfil, escriba `$profile` en la consola:</span><span class="sxs-lookup"><span data-stu-id="f96d0-195">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="f96d0-196">Para obtener más información, consulte [perfiles de Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="f96d0-196">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>
