---
title: "Notas de la versión de NuGet 1.4 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 1.4, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 1.4 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a69f4f5c7172817d711fa5e995cf6db3875c4810
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="81156-104">Notas de la versión 1.4 de NuGet</span><span class="sxs-lookup"><span data-stu-id="81156-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="81156-105">[Notas de la versión de NuGet 1.3](../release-notes/nuget-1.3.md) | [notas de la versión 1.5 de NuGet](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="81156-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="81156-106">NuGet 1.4 se publicó en 17 de junio de 2011.</span><span class="sxs-lookup"><span data-stu-id="81156-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="81156-107">Características</span><span class="sxs-lookup"><span data-stu-id="81156-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="81156-108">Mejoras de paquete de actualización</span><span class="sxs-lookup"><span data-stu-id="81156-108">Update-Package improvements</span></span>
<span data-ttu-id="81156-109">NuGet 1.4 presenta una gran cantidad de mejoras en el comando de paquete de actualización, lo que facilita mantener paquetes en la misma versión en varios proyectos en una solución.</span><span class="sxs-lookup"><span data-stu-id="81156-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="81156-110">Por ejemplo, cuando se actualiza un paquete a la versión más reciente, es muy común que se desee todos los proyectos con ese paquete instalado para su actualización en el mismo verision.</span><span class="sxs-lookup"><span data-stu-id="81156-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="81156-111">El `Update-Package` comando ahora resulta más fácil:</span><span class="sxs-lookup"><span data-stu-id="81156-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="81156-112">Actualizar todos los paquetes en un solo proyecto</span><span class="sxs-lookup"><span data-stu-id="81156-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="81156-113">Actualizar un paquete en todos los proyectos</span><span class="sxs-lookup"><span data-stu-id="81156-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="81156-114">Actualizar todos los paquetes en todos los proyectos</span><span class="sxs-lookup"><span data-stu-id="81156-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="81156-115">Realizar una actualización "segura" en todos los paquetes</span><span class="sxs-lookup"><span data-stu-id="81156-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="81156-116">El `-Safe` marca restringe las actualizaciones a solo las versiones con el mismo componente de versión principal y secundaria.</span><span class="sxs-lookup"><span data-stu-id="81156-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="81156-117">Por ejemplo, si está instalada la versión 1.0.0 de un paquete y las versiones 1.0.1, 1.0.2 y 1.1 están disponibles en la fuente, la `-Safe` marca actualiza el paquete a la versión 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="81156-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="81156-118">Actualizar sin el `-Safe` marca actualice el paquete a la versión más reciente, 1.1.</span><span class="sxs-lookup"><span data-stu-id="81156-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="81156-119">Administrar paquetes en el nivel de solución</span><span class="sxs-lookup"><span data-stu-id="81156-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="81156-120">Antes de NuGet 1.4, instalar un paquete en varios proyectos era complejo mediante el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81156-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="81156-121">Es necesario iniciar el cuadro de diálogo una vez por proyecto.</span><span class="sxs-lookup"><span data-stu-id="81156-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="81156-122">NuGet 1.4 agrega compatibilidad para instalar, desinstalar o actualizar los paquetes en varios proyectos al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="81156-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="81156-123">Simplemente inicie el, haga clic en la solución y seleccione la **administrar paquetes de NuGet** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="81156-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Cuadro de diálogo de solución Nivel administrar paquetes de NuGet](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="81156-125">Observe que en la barra de título del cuadro de diálogo, se muestra el nombre de la solución, no el nombre de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="81156-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="81156-126">Operaciones de paquetes proporcionan ahora una lista de casillas de verificación con la lista de proyectos que se debe aplicar la operación a.</span><span class="sxs-lookup"><span data-stu-id="81156-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Administrar la selección de proyecto de paquetes de NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="81156-128">Para obtener más información, vea el tema en [administrar paquetes de la solución](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="81156-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="81156-129">Si se restringen los actualiza a permitido versiones</span><span class="sxs-lookup"><span data-stu-id="81156-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="81156-130">De forma predeterminada, cuando se ejecuta el `Update-Package` comando en un paquete (o actualizar el paquete mediante el cuadro de diálogo), se actualizarán a la versión más reciente de la fuente.</span><span class="sxs-lookup"><span data-stu-id="81156-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="81156-131">Con la nueva compatibilidad para actualizar todos los paquetes, puede haber casos en los que desea bloquear un paquete a un intervalo de la versión específica.</span><span class="sxs-lookup"><span data-stu-id="81156-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="81156-132">Por ejemplo, puede saber de antemano que la aplicación solo funcionará con 2.\* de versión de un paquete, pero no 3.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="81156-132">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="81156-133">Para evitar que accidentalmente la actualización del paquete a 3, NuGet 1.4 agrega compatibilidad para restringir el intervalo de versiones que se pueden actualizar los paquetes a editando manualmente el `packages.config` archivos con el nuevo `allowedVersions` atributo.</span><span class="sxs-lookup"><span data-stu-id="81156-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="81156-134">Por ejemplo, en el ejemplo siguiente se muestra cómo bloquear la `SomePackage` intervalo de paquete de la versión 2.0 y 3.0 (exclusivo).</span><span class="sxs-lookup"><span data-stu-id="81156-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="81156-135">El `allowedVersions` atributo acepta valores mediante la [formato de intervalo de versión](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="81156-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="81156-136">Tenga en cuenta que en 1.4, bloqueo de un paquete a un intervalo de versión específica debe editar manualmente.</span><span class="sxs-lookup"><span data-stu-id="81156-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="81156-137">En 1.5 de NuGet planeamos agregar compatibilidad para colocar este intervalo a través de la `Install-Package` comando.</span><span class="sxs-lookup"><span data-stu-id="81156-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="81156-138">Visualizador de paquete</span><span class="sxs-lookup"><span data-stu-id="81156-138">Package Visualizer</span></span>
<span data-ttu-id="81156-139">El visualizador de paquete nuevo, iniciado mediante la **herramientas** -> **Administrador de paquetes de biblioteca** -> **paquete visualizador** le permite la opción de menú visualizar fácilmente todos los proyectos y sus dependencias de paquete en una solución.</span><span class="sxs-lookup"><span data-stu-id="81156-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="81156-140">_**Nota importante:** esta característica aprovecha las ventajas de la compatibilidad DGML en Visual Studio. Crear la visualización solo se admite en Visual Studio Ultimate. Ver un diagrama DGML solo se admite en Visual Studio Premium o superior._</span><span class="sxs-lookup"><span data-stu-id="81156-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Visualizador de paquete](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="81156-142">Comprobación de actualización automática para el cuadro de diálogo de NuGet</span><span class="sxs-lookup"><span data-stu-id="81156-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="81156-143">Algunas versiones de NuGet incorporar nuevas características que se expresan a través de la `.nuspec` archivo que no se entiende por versiones anteriores del cuadro de diálogo de NuGet.</span><span class="sxs-lookup"><span data-stu-id="81156-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="81156-144">Un ejemplo es la introducción de NuGet 1.4 para [especificar los ensamblados de framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="81156-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="81156-145">Por este motivo, es importante que use la versión más reciente de NuGet para asegurarse de que se pueden utilizar los paquetes sacar partido de las características más recientes.</span><span class="sxs-lookup"><span data-stu-id="81156-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="81156-146">Para realizar actualizaciones en NuGet más visible, el cuadro de diálogo de NuGet contiene la lógica para resaltar cuando hay disponible una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="81156-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="81156-147">_**Tenga en cuenta**: solo se realiza la comprobación de si el **Online** ficha se ha seleccionado en la sesión actual._</span><span class="sxs-lookup"><span data-stu-id="81156-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Administrar el cuadro de diálogo de paquetes de NuGet con la nueva versión disponible](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="81156-149">Para desactivar la comprobación automática de actualizaciones, vaya al cuadro de diálogo de configuración de NuGet y desactive la opción **buscar automáticamente actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="81156-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Configuración de NuGet](./media/nuget-settings.png)

<span data-ttu-id="81156-151">Esta característica se agregó realmente en NuGet 1.3, pero no estará visible, por supuesto, hasta que una actualización de 1.3, por ejemplo, NuGet 1.4, se puso a disposición.</span><span class="sxs-lookup"><span data-stu-id="81156-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="81156-152">Mejoras de cuadro de diálogo Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="81156-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="81156-153">**Los nombres de menús mejorado**: opciones de menú para abrir el cuadro de diálogo se cambió para mayor claridad.</span><span class="sxs-lookup"><span data-stu-id="81156-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="81156-154">La opción de menú es ahora **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="81156-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="81156-155">**Panel de detalles muestra la fecha última actualización**: NuGet el cuadro de diálogo muestra la fecha de la actualización más reciente en el panel de detalles para un paquete cuando el **en línea** o **actualiza** ficha está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="81156-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="81156-156">**Lista de etiquetas que se muestran**: Nuget el cuadro de diálogo muestra las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="81156-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="81156-157">Mejoras de PowerShell</span><span class="sxs-lookup"><span data-stu-id="81156-157">Powershell Improvements</span></span>
* <span data-ttu-id="81156-158">**Secuencias de comandos de PowerShell firmadas**: NuGet incluye scripts de Powershell firmados Habilitar uso en entornos más restrictivos.</span><span class="sxs-lookup"><span data-stu-id="81156-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="81156-159">**Solicitar soporte técnico**: la consola de administrador de paquetes ahora es compatible con preguntar a través de la `$host.ui.Prompt` y `$host.ui.PromptForChoice` comandos.</span><span class="sxs-lookup"><span data-stu-id="81156-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="81156-160">**Nombres de origen del paquete**: proporcionando el nombre de un origen de paquete se admite cuando se especifica un origen de paquete mediante la `-Source` marca.</span><span class="sxs-lookup"><span data-stu-id="81156-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="81156-161">mejoras de la línea de comandos de NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="81156-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="81156-162">**Comandos de NuGet personalizados**: nuget.exe es extensible a través de los comandos personalizados utilizando MEF.</span><span class="sxs-lookup"><span data-stu-id="81156-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="81156-163">**Más sencillo el flujo de trabajo para crear paquetes de símbolos**: el `-Symbols` marca se puede aplicar a una estructura de carpeta basada en normal convenciones crear un paquete de símbolos solo incluyendo el origen y `.pdb` archivos dentro de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="81156-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="81156-164">**Selección de varios orígenes**: el `NuGet install` comando admite la especificación de varios orígenes con punto y coma como delimitador o mediante la especificación de `-Source` varias veces.</span><span class="sxs-lookup"><span data-stu-id="81156-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="81156-165">**Admite la autenticación de proxy**: NuGet 1.4 agrega compatibilidad para solicitar las credenciales de usuario al usar NuGet detrás de un proxy que requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="81156-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="81156-166">**NuGet.exe actualizar cambio problemático**: el `-Self` marca ahora es necesario para que nuget.exe se actualice automáticamente.</span><span class="sxs-lookup"><span data-stu-id="81156-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="81156-167">`nuget.exe Update`Ahora tiene una ruta de acceso a la `packages.config` archivo e intentará a los paquetes de actualización.</span><span class="sxs-lookup"><span data-stu-id="81156-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="81156-168">Tenga en cuenta que esta actualización se limita en que no puede: ** actualizar, agregar, quitar el contenido del archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="81156-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="81156-169">** Ejecutar scripts de Powershell dentro del paquete.</span><span class="sxs-lookup"><span data-stu-id="81156-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="81156-170">Compatibilidad de servidor de NuGet para insertar los paquetes con nuget.exe</span><span class="sxs-lookup"><span data-stu-id="81156-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="81156-171">NuGet incluye una manera sencilla de host un [web ligero basado repositorio de NuGet](../hosting-packages/NuGet-Server.md) a través de la `NuGet.Server` paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="81156-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/NuGet-Server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="81156-172">Con NuGet 1.4, el servidor ligero admite la inserción y eliminación de paquetes con nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="81156-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="81156-173">La versión más reciente de `NuGet.Server` agrega un nuevo `appSetting`, que se denomina `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="81156-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="81156-174">Cuando la clave se omite o se deja en blanco, e inserta los paquetes a la fuente está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="81156-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="81156-175">Establecer el apiKey en un valor (lo ideal es que una contraseña segura) permite la inserción de paquetes con nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="81156-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="81156-176">Compatibilidad con herramientas Mango Edition de Windows Phone</span><span class="sxs-lookup"><span data-stu-id="81156-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="81156-177">NuGet ahora es compatible con la versión release candidate de herramientas de Windows Phone para Mango.</span><span class="sxs-lookup"><span data-stu-id="81156-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="81156-178">Actualmente, herramientas de Windows Phone no tiene compatibilidad con el Administrador de extensión de Visual Studio, por lo que instalar las herramientas de NuGet para Windows Phone, puede que tenga que descargar y ejecutar manualmente la extensión VSIX.</span><span class="sxs-lookup"><span data-stu-id="81156-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="81156-179">Para desinstalar herramientas de NuGet para Windows Phone, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="81156-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="81156-180">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="81156-180">Bug Fixes</span></span>
<span data-ttu-id="81156-181">NuGet 1.4 tenía un total de 88 fijo de elementos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="81156-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="81156-182">71 de los que se han marcado como errores.</span><span class="sxs-lookup"><span data-stu-id="81156-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="81156-183">Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.4, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="81156-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="81156-184">Correcciones de errores cabe destacar:</span><span class="sxs-lookup"><span data-stu-id="81156-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="81156-185">[Problema 603](http://nuget.codeplex.com/workitem/603): dependencias de paquetes en repositorios diferentes resuelve correctamente al especificar un origen de paquete específico.</span><span class="sxs-lookup"><span data-stu-id="81156-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="81156-186">[Problema 1036](http://nuget.codeplex.com/workitem/1036): agregar `NuGet Pack SomeProject.csproj` a posteriores al evento de compilación ya no provoca un bucle infinito.</span><span class="sxs-lookup"><span data-stu-id="81156-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="81156-187">[Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` marca es compatible con rutas de acceso relativas.</span><span class="sxs-lookup"><span data-stu-id="81156-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="81156-188">Actualización de NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="81156-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="81156-189">Poco después de la versión de NuGet 1.4, nos encontramos con un par de problemas que eran importantes para solucionar.</span><span class="sxs-lookup"><span data-stu-id="81156-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="81156-190">El número de versión específica de esta actualización a 1.4 es 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="81156-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="81156-191">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="81156-191">Bug Fixes</span></span>
* <span data-ttu-id="81156-192">[Problema 1220](http://nuget.codeplex.com/workitem/1220): paquete de actualización no ejecuta `install.ps1` / `uninstall.ps1` en todos los proyectos cuando hay más de un proyecto</span><span class="sxs-lookup"><span data-stu-id="81156-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="81156-193">[Problema 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Console atascados en W2K3/XP (si no está instalado el 2 de Powershell)</span><span class="sxs-lookup"><span data-stu-id="81156-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
