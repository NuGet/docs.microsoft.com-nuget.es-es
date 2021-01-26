---
title: Notas de la versión de NuGet 1,4
description: Notas de la versión de NuGet 1,4, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777141"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="1b54f-103">Notas de la versión de NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="1b54f-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="1b54f-104">Notas de la [versión de NuGet 1,3](../release-notes/nuget-1.3.md)  |  [Notas de la versión de NuGet 1,5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="1b54f-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="1b54f-105">NuGet 1,4 se lanzó el 17 de junio de 2011.</span><span class="sxs-lookup"><span data-stu-id="1b54f-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="1b54f-106">Características</span><span class="sxs-lookup"><span data-stu-id="1b54f-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="1b54f-107">Mejoras en Update-Package</span><span class="sxs-lookup"><span data-stu-id="1b54f-107">Update-Package improvements</span></span>
<span data-ttu-id="1b54f-108">NuGet 1,4 introduce una gran cantidad de mejoras en el comando Update-Package que facilita la tarea de mantener los paquetes con la misma versión en varios proyectos de una solución.</span><span class="sxs-lookup"><span data-stu-id="1b54f-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="1b54f-109">Por ejemplo, al actualizar un paquete a la versión más reciente, es muy habitual que todos los proyectos con ese paquete instalado se actualicen en el mismo Verision.</span><span class="sxs-lookup"><span data-stu-id="1b54f-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="1b54f-110">El `Update-Package` comando ahora facilita:</span><span class="sxs-lookup"><span data-stu-id="1b54f-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="1b54f-111">Actualizar todos los paquetes en un solo proyecto</span><span class="sxs-lookup"><span data-stu-id="1b54f-111">Update all packages in a single project</span></span>

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="1b54f-112">Actualizar un paquete en todos los proyectos</span><span class="sxs-lookup"><span data-stu-id="1b54f-112">Update a package in all projects</span></span>

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="1b54f-113">Actualizar todos los paquetes de todos los proyectos</span><span class="sxs-lookup"><span data-stu-id="1b54f-113">Update all packages in all projects</span></span>

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="1b54f-114">Realizar una actualización "segura" en todos los paquetes</span><span class="sxs-lookup"><span data-stu-id="1b54f-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="1b54f-115">La `-Safe` marca restringe las actualizaciones solo a las versiones con el mismo componente de versión principal y secundaria.</span><span class="sxs-lookup"><span data-stu-id="1b54f-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="1b54f-116">Por ejemplo, si se instala la versión 1.0.0 de un paquete y las versiones 1.0.1, 1.0.2 y 1,1 están disponibles en la fuente, la `-Safe` marca actualiza el paquete a 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="1b54f-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="1b54f-117">La actualización sin la `-Safe` marca actualizaría el paquete a la versión más reciente, 1,1.</span><span class="sxs-lookup"><span data-stu-id="1b54f-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="1b54f-118">Administrar paquetes en el nivel de solución</span><span class="sxs-lookup"><span data-stu-id="1b54f-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="1b54f-119">Antes de NuGet 1,4, la instalación de un paquete en varios proyectos era complicada mediante el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b54f-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="1b54f-120">Requiere que se inicie el cuadro de diálogo una vez por proyecto.</span><span class="sxs-lookup"><span data-stu-id="1b54f-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="1b54f-121">NuGet 1,4 agrega compatibilidad para instalar o desinstalar o actualizar paquetes en varios proyectos al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="1b54f-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="1b54f-122">Simplemente inicie el haciendo clic con el botón derecho en la solución y seleccionando la opción de menú **administrar paquetes NuGet** .</span><span class="sxs-lookup"><span data-stu-id="1b54f-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Cuadro de diálogo administrar paquetes NuGet en el nivel de solución](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="1b54f-124">Observe que en la barra de título del cuadro de diálogo, se muestra el nombre de la solución, no el nombre de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="1b54f-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="1b54f-125">Las operaciones de paquete ahora proporcionan una lista de casillas con la lista de proyectos a los que se debe aplicar la operación.</span><span class="sxs-lookup"><span data-stu-id="1b54f-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Selección de proyectos de administración de paquetes NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="1b54f-127">Para obtener más información, vea el tema sobre la [Administración de paquetes para la solución](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="1b54f-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="1b54f-128">Restringir las actualizaciones a las versiones permitidas</span><span class="sxs-lookup"><span data-stu-id="1b54f-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="1b54f-129">De forma predeterminada, al ejecutar el `Update-Package` comando en un paquete (o actualizar el paquete mediante el cuadro de diálogo), se actualizará a la versión más reciente de la fuente.</span><span class="sxs-lookup"><span data-stu-id="1b54f-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="1b54f-130">Con la nueva compatibilidad para actualizar todos los paquetes, puede haber casos en los que desee bloquear un paquete a un intervalo de versiones específico.</span><span class="sxs-lookup"><span data-stu-id="1b54f-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="1b54f-131">Por ejemplo, puede saber de antemano que la aplicación solo funcionará con la versión 2. \* de un paquete, pero no 3,0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="1b54f-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="1b54f-132">Con el fin de evitar que se actualice el paquete accidentalmente a 3, NuGet 1,4 agrega compatibilidad para restringir el intervalo de versiones que los paquetes pueden actualizarse a mediante la edición manual del `packages.config` archivo mediante el nuevo `allowedVersions` atributo.</span><span class="sxs-lookup"><span data-stu-id="1b54f-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="1b54f-133">Por ejemplo, en el ejemplo siguiente se muestra cómo bloquear el `SomePackage` paquete con el intervalo de versión 2,0-3,0 (exclusivo).</span><span class="sxs-lookup"><span data-stu-id="1b54f-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="1b54f-134">El `allowedVersions` atributo acepta valores mediante el [formato de intervalo de versión](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="1b54f-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="1b54f-135">Tenga en cuenta que, en 1,4, se debe editar manualmente el bloqueo de un paquete en un intervalo de versiones específico.</span><span class="sxs-lookup"><span data-stu-id="1b54f-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="1b54f-136">En NuGet 1,5 tenemos previsto agregar compatibilidad para colocar este intervalo a través del `Install-Package` comando.</span><span class="sxs-lookup"><span data-stu-id="1b54f-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="1b54f-137">Visualizador de paquetes</span><span class="sxs-lookup"><span data-stu-id="1b54f-137">Package Visualizer</span></span>
<span data-ttu-id="1b54f-138">El nuevo visualizador de paquetes, que se inicia mediante la opción de menú visualizador de paquetes del administrador de paquetes de la biblioteca de **herramientas**  ->    ->   , le permite visualizar fácilmente todos los proyectos y sus dependencias de paquete dentro de una solución.</span><span class="sxs-lookup"><span data-stu-id="1b54f-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="1b54f-139">_**Nota importante:** Esta característica aprovecha la compatibilidad con DGML en Visual Studio. Solo se admite la creación de la visualización en Visual Studio Ultimate. La visualización de un diagrama de DGML solo se admite en Visual Studio Premium o superior._</span><span class="sxs-lookup"><span data-stu-id="1b54f-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Visualizador de paquetes](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="1b54f-141">Comprobación automática de actualizaciones para el cuadro de diálogo NuGet</span><span class="sxs-lookup"><span data-stu-id="1b54f-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="1b54f-142">Algunas versiones de NuGet presentan nuevas características que se expresan a través del `.nuspec` archivo que no se entienden en las versiones anteriores del cuadro de diálogo de Nuget.</span><span class="sxs-lookup"><span data-stu-id="1b54f-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="1b54f-143">Un ejemplo es la introducción a NuGet 1,4 para [especificar ensamblados de .NET Framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="1b54f-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="1b54f-144">Por este motivo, es importante usar la versión más reciente de NuGet para asegurarse de que puede usar los paquetes que aprovechan las características más recientes.</span><span class="sxs-lookup"><span data-stu-id="1b54f-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="1b54f-145">Para que las actualizaciones de NuGet sean más visibles, el cuadro de diálogo NuGet contiene lógica que se resalta cuando hay disponible una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="1b54f-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="1b54f-146">_**Nota**: la comprobación solo se realiza si se ha seleccionado la pestaña en **línea** en la sesión actual._</span><span class="sxs-lookup"><span data-stu-id="1b54f-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Cuadro de diálogo administrar paquetes NuGet con la nueva versión disponible](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="1b54f-148">Para desactivar la comprobación automática de actualizaciones, vaya al cuadro de diálogo Configuración de NuGet y desactive la casilla **Buscar actualizaciones automáticamente**.</span><span class="sxs-lookup"><span data-stu-id="1b54f-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Configuración de NuGet](./media/nuget-settings.png)

<span data-ttu-id="1b54f-150">Esta característica se agregó realmente en NuGet 1,3, pero no sería visible, por supuesto, hasta que haya disponible una actualización de 1,3, como NuGet 1,4.</span><span class="sxs-lookup"><span data-stu-id="1b54f-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="1b54f-151">Mejoras en el cuadro de diálogo Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="1b54f-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="1b54f-152">**Nombres de menús mejorados**: se ha cambiado el nombre de las opciones de menú para iniciar el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1b54f-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="1b54f-153">La opción de menú es ahora **administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1b54f-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="1b54f-154">El **Panel de detalles muestra la fecha de actualización más reciente**: el cuadro de diálogo NuGet muestra la fecha de la última actualización en el panel de detalles de un paquete cuando se selecciona la pestaña **en línea** o **actualizaciones** .</span><span class="sxs-lookup"><span data-stu-id="1b54f-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="1b54f-155">**Lista de etiquetas mostradas**: el cuadro de diálogo Nuget muestra etiquetas.</span><span class="sxs-lookup"><span data-stu-id="1b54f-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="1b54f-156">Mejoras de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b54f-156">Powershell Improvements</span></span>
* <span data-ttu-id="1b54f-157">**Scripts de PowerShell firmados**: NuGet incluye scripts de PowerShell firmados que permiten el uso en entornos más restrictivos.</span><span class="sxs-lookup"><span data-stu-id="1b54f-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="1b54f-158">**Solicitar soporte técnico**: la consola del administrador de paquetes admite ahora la solicitud a través de los `$host.ui.Prompt` `$host.ui.PromptForChoice` comandos y.</span><span class="sxs-lookup"><span data-stu-id="1b54f-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="1b54f-159">**Nombres de origen del paquete**: se admite proporcionar el nombre de un origen de paquete al especificar un origen de paquete mediante la `-Source` marca.</span><span class="sxs-lookup"><span data-stu-id="1b54f-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="1b54f-160">Mejoras en la línea de comandos nuget.exe</span><span class="sxs-lookup"><span data-stu-id="1b54f-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="1b54f-161">**Comandos personalizados de NuGet**: nuget.exe es extensible mediante comandos personalizados mediante MEF.</span><span class="sxs-lookup"><span data-stu-id="1b54f-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="1b54f-162">Es **más sencillo el flujo de trabajo para crear paquetes de símbolos**: la `-Symbols` marca se puede aplicar a una estructura de carpetas basada en Convención normal que crea un paquete de símbolos incluyendo únicamente el origen y `.pdb` los archivos dentro de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1b54f-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="1b54f-163">**Especificar varios orígenes**: el `NuGet install` comando admite la especificación de varios orígenes mediante punto y coma como delimitador o especificando `-Source` varias veces.</span><span class="sxs-lookup"><span data-stu-id="1b54f-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="1b54f-164">**Compatibilidad con autenticación de proxy**: NuGet 1,4 agrega compatibilidad para solicitar credenciales de usuario al usar NuGet detrás de un proxy que requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="1b54f-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="1b54f-165">**nuget.exe cambio importante**: la `-Self` marca es ahora necesaria para que nuget.exe se actualice a sí misma.</span><span class="sxs-lookup"><span data-stu-id="1b54f-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="1b54f-166">`nuget.exe Update` Ahora toma una ruta de acceso al `packages.config` archivo e intentará actualizar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="1b54f-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="1b54f-167">Tenga en cuenta que esta actualización está limitada, ya que no se: \* \* actualizar, agregar y quitar contenido en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="1b54f-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="1b54f-168">\* \* Ejecute scripts de PowerShell en el paquete.</span><span class="sxs-lookup"><span data-stu-id="1b54f-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="1b54f-169">Compatibilidad del servidor de NuGet con la inserción de paquetes mediante nuget.exe</span><span class="sxs-lookup"><span data-stu-id="1b54f-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="1b54f-170">NuGet incluye una forma sencilla de hospedar un [repositorio de Nuget basado en web ligero](../hosting-packages/nuget-server.md) mediante el `NuGet.Server` paquete Nuget.</span><span class="sxs-lookup"><span data-stu-id="1b54f-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="1b54f-171">Con NuGet 1,4, el servidor ligero permite insertar y eliminar paquetes mediante nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="1b54f-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="1b54f-172">La versión más reciente de `NuGet.Server` agrega un nuevo `appSetting` denominado `apiKey` .</span><span class="sxs-lookup"><span data-stu-id="1b54f-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="1b54f-173">Cuando se omite la clave o se deja en blanco, se deshabilita la inserción de paquetes en la fuente.</span><span class="sxs-lookup"><span data-stu-id="1b54f-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="1b54f-174">Establecer apiKey en un valor (idealmente una contraseña segura) permite insertar paquetes mediante nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="1b54f-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="1b54f-175">Compatibilidad con Windows Phone Tools mango Edition</span><span class="sxs-lookup"><span data-stu-id="1b54f-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="1b54f-176">Ahora se admite NuGet en la versión Release Candidate de herramientas de Windows Phone para mango.</span><span class="sxs-lookup"><span data-stu-id="1b54f-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="1b54f-177">Actualmente, Windows Phone Tools no es compatible con el administrador de extensiones de Visual Studio para instalar NuGet para herramientas de Windows Phone, puede que tenga que descargar y ejecutar VSIX manualmente.</span><span class="sxs-lookup"><span data-stu-id="1b54f-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="1b54f-178">Para desinstalar NuGet para herramientas de Windows Phone, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="1b54f-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a><span data-ttu-id="1b54f-179">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="1b54f-179">Bug Fixes</span></span>
<span data-ttu-id="1b54f-180">NuGet 1,4 tenía un total de 88 elementos de trabajo fijos.</span><span class="sxs-lookup"><span data-stu-id="1b54f-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="1b54f-181">71 se marcaron como errores.</span><span class="sxs-lookup"><span data-stu-id="1b54f-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="1b54f-182">Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 1,4, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="1b54f-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="1b54f-183">Las correcciones de errores merecen tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="1b54f-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="1b54f-184">[Problema 603](http://nuget.codeplex.com/workitem/603): las dependencias de paquete entre diferentes repositorios se resuelven correctamente al especificar un origen de paquete específico.</span><span class="sxs-lookup"><span data-stu-id="1b54f-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="1b54f-185">[Problema 1036](http://nuget.codeplex.com/workitem/1036): agregar `NuGet Pack SomeProject.csproj` a un evento posterior a la compilación ya no produce un bucle infinito.</span><span class="sxs-lookup"><span data-stu-id="1b54f-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="1b54f-186">[Problema 961](http://nuget.codeplex.com/workitem/961): la `-Source` marca es compatible con rutas de acceso relativas.</span><span class="sxs-lookup"><span data-stu-id="1b54f-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="1b54f-187">Actualización de NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="1b54f-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="1b54f-188">Poco después del lanzamiento de NuGet 1,4, encontramos un par de problemas que era importante corregir.</span><span class="sxs-lookup"><span data-stu-id="1b54f-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="1b54f-189">El número de versión específico de esta actualización a 1,4 es 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="1b54f-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="1b54f-190">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="1b54f-190">Bug Fixes</span></span>
* <span data-ttu-id="1b54f-191">[Problema 1220](http://nuget.codeplex.com/workitem/1220): Update-Package no `install.ps1` / `uninstall.ps1` se ejecuta en todos los proyectos cuando hay más de un proyecto</span><span class="sxs-lookup"><span data-stu-id="1b54f-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="1b54f-192">[Problema 1156](http://nuget.codeplex.com/workitem/1156): la consola del administrador de paquetes se bloqueó en W2K3/XP (cuando PowerShell 2 no está instalado)</span><span class="sxs-lookup"><span data-stu-id="1b54f-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
