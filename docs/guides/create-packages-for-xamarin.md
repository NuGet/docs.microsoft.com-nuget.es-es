---
title: Creación de paquetes NuGet para Xamarin (en iOS, Android y Windows) con Visual Studio 2017 o 2019
description: Un tutorial integral de creación de paquetes NuGet para Xamarin que usan las API nativas en iOS, Android y Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230907"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="3605d-103">Creación de paquetes para Xamarin con Visual Studio 2017 o 2019</span><span class="sxs-lookup"><span data-stu-id="3605d-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="3605d-104">Un paquete de Xamarin contiene código en el que se usan las API nativas en iOS, Android y Windows, según el sistema operativo del tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3605d-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="3605d-105">Aunque esto es sencillo de hacer, es preferible permitir que los desarrolladores consuman el paquete desde una PCL o bibliotecas de .NET Standard a través del área expuesta de una API común.</span><span class="sxs-lookup"><span data-stu-id="3605d-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="3605d-106">En este tutorial usará Visual Studio 2017 o 2019 para crear un paquete NuGet multiplataforma que se puede usar en proyectos para dispositivos móviles en iOS, Android y Windows.</span><span class="sxs-lookup"><span data-stu-id="3605d-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="3605d-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3605d-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="3605d-108">Crear la estructura y el código de abstracción del proyecto</span><span class="sxs-lookup"><span data-stu-id="3605d-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="3605d-109">Escribir el código específico de la plataforma</span><span class="sxs-lookup"><span data-stu-id="3605d-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="3605d-110">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="3605d-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="3605d-111">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="3605d-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="3605d-112">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="3605d-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="3605d-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3605d-113">Prerequisites</span></span>

1. <span data-ttu-id="3605d-114">Visual Studio 2017 o 2019 con la Plataforma universal de Windows (UWP) y Xamarin.</span><span class="sxs-lookup"><span data-stu-id="3605d-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="3605d-115">Instale la edición Community gratuita desde [visualstudio.com](https://www.visualstudio.com/); también puede usar las ediciones Professional y Enterprise, por supuesto.</span><span class="sxs-lookup"><span data-stu-id="3605d-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="3605d-116">Para incluir las herramientas de UWP y Xamarin, seleccione una instalación personalizada y active las opciones adecuadas.</span><span class="sxs-lookup"><span data-stu-id="3605d-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="3605d-117">CLI de NuGet.</span><span class="sxs-lookup"><span data-stu-id="3605d-117">NuGet CLI.</span></span> <span data-ttu-id="3605d-118">Descargue la versión más reciente de nuget.exe desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en una ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="3605d-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="3605d-119">Después, agregue esa ubicación a la variable de entorno PATH si aún no está.</span><span class="sxs-lookup"><span data-stu-id="3605d-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="3605d-120">nuget.exe es la propia herramienta de la CLI, no un instalador, por lo que debe asegurarse de guardar el archivo descargado desde el explorador en lugar de ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="3605d-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="3605d-121">Crear la estructura y el código de abstracción del proyecto</span><span class="sxs-lookup"><span data-stu-id="3605d-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="3605d-122">Descargue y ejecute la [extensión Plantillas de complemento de .NET Standard multiplataforma](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3605d-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="3605d-123">Estas plantillas facilitan la creación de la estructura del proyecto necesaria para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3605d-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="3605d-124">En Visual Studio 2017, **Archivo > Nuevo > Proyecto**, busque `Plugin`, seleccione la plantilla **Complemento de Biblioteca de .NET Standard multiplataforma**, cambie el nombre a LoggingLibrary y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="3605d-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nuevo proyecto de aplicación en blanco (Xamarin.Forms Portable) en VS 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="3605d-126">En Visual Studio 2019, **Archivo > Nuevo > Proyecto**, busque `Plugin`, seleccione la plantilla **Complemento de Biblioteca de .NET Standard multiplataforma** y haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="3605d-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Nuevo proyecto de aplicación en blanco (Xamarin.Forms Portable) en VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="3605d-128">Cambie el nombre a LoggingLibrary y haga clic en Crear.</span><span class="sxs-lookup"><span data-stu-id="3605d-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Nueva configuración de aplicación en blanco (Xamarin.Forms Portable) en VS 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="3605d-130">La solución resultante contiene dos proyectos compartidos, junto con varios proyectos específicos de la plataforma:</span><span class="sxs-lookup"><span data-stu-id="3605d-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="3605d-131">El proyecto `ILoggingLibrary`, que se encuentra en el archivo `ILoggingLibrary.shared.cs`, define la interfaz pública (el área expuesta de la API) del componente.</span><span class="sxs-lookup"><span data-stu-id="3605d-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="3605d-132">Aquí es donde se define la interfaz de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="3605d-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="3605d-133">El otro proyecto compartido contiene código en `CrossLoggingLibrary.shared.cs` que buscará una implementación específica de la plataforma de la interfaz abstracta en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3605d-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="3605d-134">Normalmente no es necesario modificar este archivo.</span><span class="sxs-lookup"><span data-stu-id="3605d-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="3605d-135">Los proyectos específicos de la plataforma, como `LoggingLibrary.android.cs`, contienen cada uno una implementación nativa de la interfaz en sus respectivos archivos `LoggingLibraryImplementation.cs` (VS 2017) o `LoggingLibrary.<PLATFORM>.cs` (VS 2019).</span><span class="sxs-lookup"><span data-stu-id="3605d-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="3605d-136">Aquí es donde se compila el código de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="3605d-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="3605d-137">De forma predeterminada, el archivo ILoggingLibrary.shared.cs del proyecto `ILoggingLibrary` contiene una definición de interfaz, pero ningún método.</span><span class="sxs-lookup"><span data-stu-id="3605d-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="3605d-138">Para los fines de este tutorial, agregue un método `Log` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3605d-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="3605d-139">Escribir el código específico de la plataforma</span><span class="sxs-lookup"><span data-stu-id="3605d-139">Write your platform-specific code</span></span>

<span data-ttu-id="3605d-140">Para implementar una implementación específica de la plataforma de la interfaz `ILoggingLibrary` y sus métodos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3605d-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="3605d-141">Abra el archivo `LoggingLibraryImplementation.cs` (VS 2017) o `LoggingLibrary.<PLATFORM>.cs` (VS 2019) de cada proyecto de plataforma y agregue el código necesario.</span><span class="sxs-lookup"><span data-stu-id="3605d-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="3605d-142">Por ejemplo (mediante el proyecto de plataforma `Android`):</span><span class="sxs-lookup"><span data-stu-id="3605d-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="3605d-143">Repita esta implementación en los proyectos de cada plataforma que quiera admitir.</span><span class="sxs-lookup"><span data-stu-id="3605d-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="3605d-144">Haga clic con el botón derecho en la solución y seleccione **Compilar solución** para comprobar el trabajo y generar los artefactos que se empaquetan después.</span><span class="sxs-lookup"><span data-stu-id="3605d-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="3605d-145">Si recibe errores sobre referencias que faltan, haga clic con el botón derecho en la solución, seleccione **Restaurar paquetes NuGet** para instalar las dependencias y vuelva a compilar.</span><span class="sxs-lookup"><span data-stu-id="3605d-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="3605d-146">Si usa Visual Studio 2019, antes de seleccionar **Restaurar paquetes NuGet** e intentar la recompilación, debe cambiar la versión de `MSBuild.Sdk.Extras` a `2.0.54` en `LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="3605d-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="3605d-147">Solo se puede acceder a este archivo haciendo clic con el botón derecho en el proyecto (debajo de la solución) y seleccionando `Unload Project`, después de lo cual se hace clic con el botón derecho en el proyecto descargado y se selecciona `Edit LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="3605d-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="3605d-148">Para compilar para iOS necesita un equipo Mac en red conectado a Visual Studio como se describe en [Introducción a Xamarin.iOS para Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="3605d-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="3605d-149">Si no tiene un equipo Mac disponible, desactive el proyecto de iOS en el administrador de configuración (paso 3 anterior).</span><span class="sxs-lookup"><span data-stu-id="3605d-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="3605d-150">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="3605d-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="3605d-151">Abra un símbolo del sistema, vaya a la carpeta `LoggingLibrary` que está un nivel por debajo de la ubicación del archivo `.sln` y ejecute el comando `spec` de NuGet para crear el archivo `Package.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="3605d-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="3605d-152">Cambie el nombre de este archivo por `LoggingLibrary.nuspec` y ábralo en un editor.</span><span class="sxs-lookup"><span data-stu-id="3605d-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="3605d-153">Actualice el archivo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado.</span><span class="sxs-lookup"><span data-stu-id="3605d-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="3605d-154">El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="3605d-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="3605d-155">Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="3605d-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="3605d-156">Puede usar `-alpha`, `-beta` o `-rc` como sufijo de la versión del paquete para marcarlo como versión preliminar, consulte [Versiones preliminares](../create-packages/prerelease-packages.md) para obtener más información sobre las versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="3605d-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="3605d-157">Agregar ensamblados de referencia</span><span class="sxs-lookup"><span data-stu-id="3605d-157">Add reference assemblies</span></span>

<span data-ttu-id="3605d-158">Para incluir ensamblados de referencia específicos de la plataforma, agregue lo siguiente al elemento `<files>` de `LoggingLibrary.nuspec` según corresponda para las plataformas admitidas:</span><span class="sxs-lookup"><span data-stu-id="3605d-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="3605d-159">Para reducir los nombres de los archivos DLL y XML, haga clic con el botón derecho en cualquier proyecto, seleccione la pestaña **Biblioteca** y cambie los nombres de ensamblado.</span><span class="sxs-lookup"><span data-stu-id="3605d-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="3605d-160">Agregar dependencias</span><span class="sxs-lookup"><span data-stu-id="3605d-160">Add dependencies</span></span>

<span data-ttu-id="3605d-161">Si tiene dependencias específicas para implementaciones nativas, use el elemento `<dependencies>` con elementos `<group>` para especificarlas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3605d-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="3605d-162">Por ejemplo, lo siguiente establecería iTextSharp como una dependencia para el destino UAP:</span><span class="sxs-lookup"><span data-stu-id="3605d-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="3605d-163">Archivo .nuspec final</span><span class="sxs-lookup"><span data-stu-id="3605d-163">Final .nuspec</span></span>

<span data-ttu-id="3605d-164">Ahora el archivo `.nuspec` final debería ser similar al siguiente, donde debe reemplazar de nuevo SU_NOMBRE con un valor apropiado:</span><span class="sxs-lookup"><span data-stu-id="3605d-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="3605d-165">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="3605d-165">Package the component</span></span>

<span data-ttu-id="3605d-166">Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="3605d-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="3605d-167">Esto generará `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="3605d-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="3605d-168">Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, se ve el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="3605d-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Explorador de paquetes NuGet que en el que se muestra el paquete LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="3605d-170">Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta.</span><span class="sxs-lookup"><span data-stu-id="3605d-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="3605d-171">También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3605d-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="3605d-172">Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="3605d-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="3605d-173">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="3605d-173">Related topics</span></span>

- [<span data-ttu-id="3605d-174">Referencia de NuSpec</span><span class="sxs-lookup"><span data-stu-id="3605d-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="3605d-175">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="3605d-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="3605d-176">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="3605d-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="3605d-177">Compatibilidad con varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3605d-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="3605d-178">Incluir propiedades y destinos de MSBuild en un paquete</span><span class="sxs-lookup"><span data-stu-id="3605d-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="3605d-179">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="3605d-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
