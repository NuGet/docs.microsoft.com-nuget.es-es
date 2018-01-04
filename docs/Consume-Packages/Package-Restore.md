---
title: "Restauración de paquetes NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Una descripción de cómo NuGet restaura los paquetes de los que depende un proyecto, incluido cómo deshabilitar la restauración y restringir las versiones."
keywords: "Restauración de paquetes NuGet, instalación de paquetes NuGet, instalación del paquete, restauración de paquetes, versiones de dependencia, deshabilitar la restauración automática, restricción de versiones de paquetes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a><span data-ttu-id="33ade-104">Restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="33ade-104">Package Restore</span></span>

<span data-ttu-id="33ade-105">Para promover un entorno de desarrollo más limpio y reducir el tamaño del repositorio, **Restauración de paquetes** de NuGet instala todos los paquetes a los que se hace referencia antes de compilar un proyecto.</span><span class="sxs-lookup"><span data-stu-id="33ade-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="33ade-106">Esta característica de uso frecuente garantiza que todas las dependencias están disponibles en un proyecto sin necesidad de almacenar esos paquetes en el control de código fuente (vea [Paquetes y control de código fuente](../consume-packages/packages-and-source-control.md) para obtener información sobre cómo configurar el repositorio para excluir archivos binarios de paquete).</span><span class="sxs-lookup"><span data-stu-id="33ade-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="33ade-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="33ade-107">In this topic:</span></span>
- [<span data-ttu-id="33ade-108">Guía rápida de la restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="33ade-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="33ade-109">Información general sobre restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="33ade-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="33ade-110">Habilitar y deshabilitar la restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="33ade-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="33ade-111">Restricción de versiones de paquetes con la restauración</span><span class="sxs-lookup"><span data-stu-id="33ade-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="33ade-112">[Restauración de línea de comandos](#command-line-restore), para todas las versiones de NuGet</span><span class="sxs-lookup"><span data-stu-id="33ade-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="33ade-113">[Restauración automática en Visual Studio](#automatic-restore-in-visual-studio), para NuGet 2.7 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="33ade-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="33ade-114">[Restauración integrada de MSBuild en Visual Studio](#msbuild-integrated-restore), para NuGet 2.6 y versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="33ade-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="33ade-115">Restauración de paquetes con Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="33ade-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="33ade-116">El comportamiento de restauración varía según la versión; para comprobar la versión de NuGet, simplemente ejecute `nuget.exe` en la línea de comandos y mire la primera línea de la salida.</span><span class="sxs-lookup"><span data-stu-id="33ade-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="33ade-117">Para obtener más detalles sobre la restauración de paquetes en servidores de compilación, vea [Restauración de paquetes con TFBuild](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="33ade-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="33ade-118">Los proyectos configurados para la restauración de paquetes también funcionan con xbuild en Mono.</span><span class="sxs-lookup"><span data-stu-id="33ade-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="33ade-119">Guía rápida de la restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="33ade-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="33ade-120">Si ve el error "Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo" o "Uno o varios paquetes de NuGet se deben restaurar, pero no pudieron restaurarse porque no se ha concedido el consentimiento", active la restauración automática mediante las instrucciones descritas en [Habilitar y deshabilitar la restauración de paquetes](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="33ade-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="33ade-121">Información general sobre restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="33ade-121">Package restore overview</span></span>

<span data-ttu-id="33ade-122">En primer lugar, las referencias de paquete se mantienen en uno de los formatos de administración de paquetes siguientes, según el tipo de proyecto y la versión de NuGet.</span><span class="sxs-lookup"><span data-stu-id="33ade-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="33ade-123">(Tenga en cuenta que NuGet 4 y MSBuild 15.1 se instalan con Visual Studio 2017).</span><span class="sxs-lookup"><span data-stu-id="33ade-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="33ade-124">Método</span><span class="sxs-lookup"><span data-stu-id="33ade-124">Method</span></span> | <span data-ttu-id="33ade-125">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="33ade-125">NuGet Version</span></span> | <span data-ttu-id="33ade-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="33ade-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="33ade-127">2.x y posterior</span><span class="sxs-lookup"><span data-stu-id="33ade-127">2.x+</span></span> | <span data-ttu-id="33ade-128">Muestra el conjunto completo de dependencias.</span><span class="sxs-lookup"><span data-stu-id="33ade-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="33ade-129">Los paquetes agregados a `packages.config` también se deben agregar al archivo de proyecto, así como los destinos y propiedades.</span><span class="sxs-lookup"><span data-stu-id="33ade-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="33ade-130">Este es el método de base de referencia para todas las versiones de NuGet, pero tiene un rendimiento más lento en comparación con las otras opciones.</span><span class="sxs-lookup"><span data-stu-id="33ade-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="33ade-131">(Vea [esquema packages.config](../schema/packages-config.md)).</span><span class="sxs-lookup"><span data-stu-id="33ade-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="33ade-132">3.x y posteriores</span><span class="sxs-lookup"><span data-stu-id="33ade-132">3.x+</span></span> | <span data-ttu-id="33ade-133">Solo se usa de forma predeterminada con proyectos de UWP, pero los proyectos se pueden convertir desde `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="33ade-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="33ade-134">`project.json` muestra únicamente las dependencias de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="33ade-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="33ade-135">Las referencias, destinos y propiedades se agregan de forma dinámica al proyecto durante la compilación, lo que da lugar a un mejor rendimiento en comparación con `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="33ade-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="33ade-136">(Vea [esquema project.json](../schema/project-json.md)).</span><span class="sxs-lookup"><span data-stu-id="33ade-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="33ade-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="33ade-137">PackageReference</span></span> | <span data-ttu-id="33ade-138">4.x y posteriores</span><span class="sxs-lookup"><span data-stu-id="33ade-138">4.x+</span></span> | <span data-ttu-id="33ade-139">Enumera las dependencias directamente en el archivo de proyecto en el nodo `<PackageReference>`, junto a `<Reference>` y `<ProjectReference>`.</span><span class="sxs-lookup"><span data-stu-id="33ade-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="33ade-140">Funciona de forma similar a `project.json`; vea [Referencias de paquete en archivos de proyecto](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="33ade-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="33ade-141">En segundo lugar, una restauración se inicia con la lista de referencias de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="33ade-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="33ade-142">Desde la línea de comandos o la [Consola del Administrador de paquetes](../tools/Package-Manager-Console.md):</span><span class="sxs-lookup"><span data-stu-id="33ade-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="33ade-143">Comando</span><span class="sxs-lookup"><span data-stu-id="33ade-143">Command</span></span> | <span data-ttu-id="33ade-144">Escenarios aplicables</span><span class="sxs-lookup"><span data-stu-id="33ade-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="33ade-145">Todas las versiones de NuGet y todos los tipos de referencia.</span><span class="sxs-lookup"><span data-stu-id="33ade-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="33ade-146">Vea [Restauración de línea de comandos](#command-line-restore) a continuación.</span><span class="sxs-lookup"><span data-stu-id="33ade-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="33ade-147">Igual que `nuget restore` para los proyectos de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="33ade-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="33ade-148">Vea [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span><span class="sxs-lookup"><span data-stu-id="33ade-148">See [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="33ade-149">Solo para NuGet 4.x y versiones posteriores, y MSBuild 15.1 y versiones posteriores con [referencias de paquete en archivos de proyecto](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="33ade-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="33ade-150">`nuget restore` y `dotnet restore` usan este comando para los proyectos aplicables.</span><span class="sxs-lookup"><span data-stu-id="33ade-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="33ade-151">Vea [pack y restore de NuGet como destinos de MSBuild: restaurar destino](../schema/msbuild-targets.md#restore-target).</span><span class="sxs-lookup"><span data-stu-id="33ade-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="33ade-152">Visual Studio también restaura paquetes en momentos diferentes:</span><span class="sxs-lookup"><span data-stu-id="33ade-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="33ade-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="33ade-153">Type</span></span> | <span data-ttu-id="33ade-154">Cuando se produce la restauración</span><span class="sxs-lookup"><span data-stu-id="33ade-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="33ade-155">Restauración de plantilla</span><span class="sxs-lookup"><span data-stu-id="33ade-155">Template restore</span></span> | <span data-ttu-id="33ade-156">Durante la creación de un proyecto nuevo, dado que algunas plantillas dependen de paquetes externos.</span><span class="sxs-lookup"><span data-stu-id="33ade-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="33ade-157">Restauración de compilación</span><span class="sxs-lookup"><span data-stu-id="33ade-157">Build restore</span></span> | <span data-ttu-id="33ade-158">Como el primer paso de una compilación.</span><span class="sxs-lookup"><span data-stu-id="33ade-158">As the first step of a build.</span></span> |
| <span data-ttu-id="33ade-159">Restauración de la solución</span><span class="sxs-lookup"><span data-stu-id="33ade-159">Solution restore</span></span> | <span data-ttu-id="33ade-160">Cuando el usuario hace clic con el botón derecho en una solución y selecciona **Restaurar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="33ade-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="33ade-161">Restauración al cambiar el proyecto</span><span class="sxs-lookup"><span data-stu-id="33ade-161">Restore on project change</span></span> | <span data-ttu-id="33ade-162">*(Solo para NuGet 4.x)* Cuando se usa una proyecto basado en el SDK de .NET Core, incluidos los cambios de estado del proyecto.</span><span class="sxs-lookup"><span data-stu-id="33ade-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="33ade-163">Habilitar y deshabilitar la restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="33ade-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="33ade-164">La restauración de paquetes se habilita principalmente a través de **Herramientas > Opciones > Administrador de paquetes NuGet** en Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="33ade-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Control de los comportamientos de restauración de paquetes a través de las opciones del Administrador de paquetes NuGet](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="33ade-166">**Permitir a NuGet descargar los paquetes que falten**: controla todas las formas de restauración de paquetes cambiando la opción `packageRestore/enabled` en el archivo `%AppData%\NuGet\NuGet.Config` como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="33ade-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="33ade-167">La opción `packageRestore/enabled` se puede invalidar de forma global estableciendo una variable de entorno denominada **EnableNuGetPackageRestore** con un valor de TRUE o FALSE antes de iniciar Visual Studio o una compilación.</span><span class="sxs-lookup"><span data-stu-id="33ade-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="33ade-168">**Comprobar automáticamente los paquetes que falten durante la compilación en Visual Studio**: controla la restauración automática para NuGet 2.7 y versiones posteriores cambiando la opción `packageRestore/automatic` en el archivo `%AppData%\NuGet\NuGet.Config` como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="33ade-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="33ade-169">Como referencia, vea el [archivo de configuración de NuGet: sección packageRestore](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="33ade-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="33ade-170">En algunos casos, es posible que un desarrollador o una empresa quiera habilitar o deshabilitar la restauración de paquetes en un equipo de forma predeterminada para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="33ade-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="33ade-171">Esto se puede hacer mediante la adición de la misma configuración anterior al archivo de configuración global de NuGet ubicado en `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="33ade-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="33ade-172">Después, los usuarios individuales pueden habilitar la restauración de forma selectiva cuando sea necesario en un nivel de proyecto.</span><span class="sxs-lookup"><span data-stu-id="33ade-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="33ade-173">Vea [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) para obtener información exacta sobre cómo prioriza NuGet varios archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="33ade-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="33ade-174">Restricción de versiones de paquetes con la restauración</span><span class="sxs-lookup"><span data-stu-id="33ade-174">Constraining package versions with restore</span></span>

<span data-ttu-id="33ade-175">Cuando NuGet restaure paquetes a través de cualquier método, respetará las restricciones especificadas en `packages.config`, `project.json` o el archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="33ade-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="33ade-176">`packages.config`: especifique un intervalo de versiones en la propiedad `allowedVersion` de la dependencia.</span><span class="sxs-lookup"><span data-stu-id="33ade-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="33ade-177">Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="33ade-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="33ade-178">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="33ade-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="33ade-179">`project.json`: especifique un intervalo de versiones directamente con el número de versión de la dependencia.</span><span class="sxs-lookup"><span data-stu-id="33ade-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="33ade-180">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="33ade-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="33ade-181">Referencias de paquetes en archivos de proyecto: especifique un intervalo de versiones directamente con el número de versión de la dependencia.</span><span class="sxs-lookup"><span data-stu-id="33ade-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="33ade-182">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="33ade-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="33ade-183">En todos los casos, use la notación que se describe en [Package versioning](../reference/package-versioning.md) (Control de versiones de paquetes).</span><span class="sxs-lookup"><span data-stu-id="33ade-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="33ade-184">Restauración de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="33ade-184">Command-line restore</span></span>

<span data-ttu-id="33ade-185">Para NuGet 2.7 y versiones posteriores, use el comando [Restore](../tools/cli-ref-restore.md) para restaurar todos los paquetes de una solución (con independencia de que se use `packages.config`, `project.json` o referencias de paquete en archivos de proyecto).</span><span class="sxs-lookup"><span data-stu-id="33ade-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="33ade-186">Para una carpeta de proyecto determinada, como `c:\proj\app`, las variaciones comunes siguientes restauran los paquetes:</span><span class="sxs-lookup"><span data-stu-id="33ade-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="33ade-187">Para NuGet 4.0 y versiones posteriores, y MSBuild 15.1 y versiones posteriores, también se puede usar `MSBuild /t:restore` como se describe en [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="33ade-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="33ade-188">Restauración en tiempo de compilación en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="33ade-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="33ade-189">Visual Studio restaurará automáticamente los paquetes que falten al principio de una compilación de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="33ade-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="33ade-190">Se puede cambiar este comportamiento desactivando **Herramientas > Opciones > Administrador de paquetes NuGet > General > Comprobar automáticamente los paquetes que falten durante la compilación en Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="33ade-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="33ade-191">Cuando se habilita, la restauración automática funciona del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="33ade-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="33ade-192">Cuando se inicia una compilación, Visual Studio indica a NuGet que restaure los paquetes.</span><span class="sxs-lookup"><span data-stu-id="33ade-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="33ade-193">NuGet busca de forma recurrente todos los archivos `packages.config` en la solución, busca `project.json`, o bien busca en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="33ade-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="33ade-194">Para cada paquete enumerado en los archivos de referencia, NuGet comprueba si ya existe en la solución (la carpeta `packages`, `project.lock.json` o `project.assets.json` en función de si el proyecto usa `packages.config`, `project.json` o referencias de paquete en archivos de proyecto).</span><span class="sxs-lookup"><span data-stu-id="33ade-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="33ade-195">Si no se encuentra el paquete, NuGet intenta recuperarlo primero de la memoria caché (vea [Administración de la caché NuGet](../consume-packages/managing-the-nuget-cache.md)).</span><span class="sxs-lookup"><span data-stu-id="33ade-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="33ade-196">Si el paquete no está en la memoria caché, NuGet intenta descargarlo desde los orígenes habilitados indicados en **Herramientas > Opciones > Administrador de paquetes NuGet > Orígenes de paquetes**, en el orden en que aparecen los orígenes.</span><span class="sxs-lookup"><span data-stu-id="33ade-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="33ade-197">En este caso, NuGet no indica un error al buscar el paquete hasta que se han comprobado todos los orígenes, momento en el que informa del error solo para el último origen de la lista.</span><span class="sxs-lookup"><span data-stu-id="33ade-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="33ade-198">Por implicación, este tipo de error también significa que el paquete no estaba presente en ninguno de los otros orígenes, aunque no se mostraran errores para esos orígenes de manera individual.</span><span class="sxs-lookup"><span data-stu-id="33ade-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="33ade-199">Si la descarga se realiza correctamente, NuGet almacena en caché el paquete y lo instala en la solución (de nuevo, en la carpeta `packages`, `project.lock.json` o `project.assets.json`); de lo contrario, se produce un error de NuGet y de compilación.</span><span class="sxs-lookup"><span data-stu-id="33ade-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="33ade-200">Durante este proceso, verá un cuadro de diálogo de progreso con la opción de cancelar la restauración del paquete.</span><span class="sxs-lookup"><span data-stu-id="33ade-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="33ade-201">Restauración de paquetes con Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="33ade-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="33ade-202">La restauración de paquetes se usa habitualmente al compilar proyectos en servidores de compilación, al igual que con Team Foundation Server (TFS) y Visual Studio Team Services (así como otros sistemas de compilación, que no se tratan aquí).</span><span class="sxs-lookup"><span data-stu-id="33ade-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="33ade-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="33ade-203">Visual Studio Team Services</span></span>

<span data-ttu-id="33ade-204">Al crear una definición de compilación en Team Services, basta con incluir la tarea Restaurar paquetes NuGet en la definición antes de cualquier tarea de compilación.</span><span class="sxs-lookup"><span data-stu-id="33ade-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="33ade-205">Esta tarea se incluye de forma predeterminada en una serie de plantillas de compilación.</span><span class="sxs-lookup"><span data-stu-id="33ade-205">This task is included by default in a number of build templates.</span></span>

![Tarea Restaurar paquetes NuGet en una definición de compilación de Visual Studio Team Services](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="33ade-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="33ade-207">Team Foundation Server</span></span>

<span data-ttu-id="33ade-208">Con TFS 2013 y versiones posteriores, los paquetes se restauran automáticamente de forma predeterminada durante la compilación, siempre que se use una plantilla de Team Build para Team Foundation Server 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="33ade-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="33ade-209">Si usa una versión anterior de plantillas de compilación (como en un proyecto que se ha migrado desde versiones anteriores de TFS), también debe migrar esas plantillas de compilación a TFS 2013.</span><span class="sxs-lookup"><span data-stu-id="33ade-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="33ade-210">Esto significa, básicamente, volver a crear los elementos personalizados de las plantillas de compilación mediante la plantilla adecuada para el control de código fuente (TFVC o Git).</span><span class="sxs-lookup"><span data-stu-id="33ade-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="33ade-211">Para la versión anterior de TFS, simplemente puede incluir un paso de compilación para invocar la [restauración de línea de comandos](#command-line-restore) como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="33ade-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="33ade-212">Para obtener más información, vea [Tutorial de restauración de paquetes con Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="33ade-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
