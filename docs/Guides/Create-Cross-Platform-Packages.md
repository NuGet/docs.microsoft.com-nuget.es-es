---
title: Crear paquetes NuGet multiplataforma (para iOS, Android y Windows) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Un tutorial integral de creación de paquetes NuGet para Xamarin que usan las API nativas en iOS, Android y Windows."
keywords: crear un paquete, paquetes para Xamarin, paquetes multiplataforma
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fbb1c3fccf04202dedc686583b3a2f27f105266a
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2018
---
# <a name="create-cross-platform-packages"></a><span data-ttu-id="8329c-104">Crear paquetes multiplataforma</span><span class="sxs-lookup"><span data-stu-id="8329c-104">Create cross-platform packages</span></span>

<span data-ttu-id="8329c-105">Un paquete multiplataforma contiene código en el que se usan las API nativas en iOS, Android y Windows, según el sistema operativo del tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8329c-105">A cross-platform package contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="8329c-106">Aunque esto es sencillo de hacer, es preferible permitir que los desarrolladores consuman el paquete desde una PCL o bibliotecas de .NET Standard a través del área expuesta de una API común.</span><span class="sxs-lookup"><span data-stu-id="8329c-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="8329c-107">En este tutorial creará un paquete NuGet multiplataforma que se puede usar en proyectos para dispositivos móviles en iOS, Android y Windows.</span><span class="sxs-lookup"><span data-stu-id="8329c-107">In this walkthrough you create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="8329c-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8329c-108">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="8329c-109">Crear la estructura y el código de abstracción del proyecto</span><span class="sxs-lookup"><span data-stu-id="8329c-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="8329c-110">Escribir el código específico de la plataforma</span><span class="sxs-lookup"><span data-stu-id="8329c-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="8329c-111">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="8329c-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="8329c-112">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="8329c-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="8329c-113">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="8329c-113">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="8329c-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8329c-114">Pre-requisites</span></span>

1. <span data-ttu-id="8329c-115">Visual Studio 2015 con la Plataforma universal de Windows (UWP) y Xamarin.</span><span class="sxs-lookup"><span data-stu-id="8329c-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="8329c-116">Instale la edición Community gratuita desde [visualstudio.com](https://www.visualstudio.com/); también puede usar las ediciones Professional y Enterprise, por supuesto.</span><span class="sxs-lookup"><span data-stu-id="8329c-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="8329c-117">Para incluir las herramientas de UWP y Xamarin, seleccione una instalación personalizada y active las opciones adecuadas.</span><span class="sxs-lookup"><span data-stu-id="8329c-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="8329c-118">CLI de NuGet.</span><span class="sxs-lookup"><span data-stu-id="8329c-118">NuGet CLI.</span></span> <span data-ttu-id="8329c-119">Descargue la versión más reciente de nuget.exe desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en una ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="8329c-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="8329c-120">Después, agregue esa ubicación a la variable de entorno PATH si aún no está.</span><span class="sxs-lookup"><span data-stu-id="8329c-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="8329c-121">nuget.exe es la propia herramienta de la CLI, no un instalador, por lo que debe asegurarse de guardar el archivo descargado desde el explorador en lugar de ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="8329c-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="8329c-122">Crear la estructura y el código de abstracción del proyecto</span><span class="sxs-lookup"><span data-stu-id="8329c-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="8329c-123">Descargue y ejecute la [extensión Complemento para plantillas de Xamarin](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8329c-123">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="8329c-124">Estas plantillas facilitan la creación de la estructura del proyecto necesaria para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8329c-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="8329c-125">En Visual Studio, **Archivo > Nuevo > Proyecto**, busque `Plugin`, seleccione la plantilla **Complemento para Xamarin**, cambie el nombre a LoggingLibrary y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="8329c-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nuevo proyecto de aplicación vacía (Xamarin.Forms Portable) en Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="8329c-127">La solución resultante contiene dos proyectos PCL, junto con varios proyectos específicos de la plataforma:</span><span class="sxs-lookup"><span data-stu-id="8329c-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="8329c-128">El PCL denominado `Plugin.LoggingLibrary.Abstractions (Portable)` define la interfaz pública (el área expuesta de la API) del componente, en este caso, la interfaz `ILoggingLibrary` incluida en el archivo ILoggingLibrary.cs.</span><span class="sxs-lookup"><span data-stu-id="8329c-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="8329c-129">Aquí es donde se define la interfaz de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="8329c-129">This is where you'll define the interface to your library.</span></span>
- <span data-ttu-id="8329c-130">El otro PCL, `Plugin.LoggingLibrary (Portable)`, contiene código de CrossLoggingLibrary.cs que buscará una implementación específica de la plataforma de la interfaz abstracta en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8329c-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="8329c-131">Normalmente no es necesario modificar este archivo.</span><span class="sxs-lookup"><span data-stu-id="8329c-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="8329c-132">Los proyectos específicos de la plataforma, como `Plugin.LoggingLibrary.Android`, contienen cada uno una implementación nativa de la interfaz en sus respectivos archivos LoggingLibraryImplementation.cs.</span><span class="sxs-lookup"><span data-stu-id="8329c-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="8329c-133">Aquí es donde se compila el código de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="8329c-133">This is where you'll build out your library's code.</span></span>

<span data-ttu-id="8329c-134">De forma predeterminada, el archivo ILoggingLibrary.cs del proyecto Abstractions contiene una definición de interfaz, pero ningún método.</span><span class="sxs-lookup"><span data-stu-id="8329c-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="8329c-135">Para los fines de este tutorial, agregue un método `Log` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="8329c-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="8329c-136">Escribir el código específico de la plataforma</span><span class="sxs-lookup"><span data-stu-id="8329c-136">Write your platform-specific code</span></span>

<span data-ttu-id="8329c-137">Para implementar una implementación específica de la plataforma de la interfaz `ILoggingLibrary` y sus métodos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="8329c-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="8329c-138">Abra el archivo `LoggingLibraryImplementation.cs` de cada proyecto de plataforma y agregue el código necesario.</span><span class="sxs-lookup"><span data-stu-id="8329c-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="8329c-139">Por ejemplo (con el proyecto `Plugin.LoggingLibrary.Android`):</span><span class="sxs-lookup"><span data-stu-id="8329c-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

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

1. <span data-ttu-id="8329c-140">Repita esta implementación en los proyectos de cada plataforma que quiera admitir.</span><span class="sxs-lookup"><span data-stu-id="8329c-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="8329c-141">Haga clic con el botón derecho en el proyecto de iOS, seleccione **Propiedades**, haga clic en la pestaña **Compilar** y quite "\iPhone" de las opciones **Ruta de acceso de salida** y **Archivo de documentación XML**.</span><span class="sxs-lookup"><span data-stu-id="8329c-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="8329c-142">Esto es solo para su comodidad más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8329c-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="8329c-143">Guarde el archivo cuando termine.</span><span class="sxs-lookup"><span data-stu-id="8329c-143">Save the file when done.</span></span>
1. <span data-ttu-id="8329c-144">Haga clic con el botón derecho en la solución, seleccione **Configuration Manager...** y active las casillas **Compilar** de los PCL y las plataformas que vaya a admitir.</span><span class="sxs-lookup"><span data-stu-id="8329c-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="8329c-145">Haga clic con el botón derecho en la solución y seleccione **Compilar solución** para comprobar el trabajo y generar los artefactos que se van a empaquetar después.</span><span class="sxs-lookup"><span data-stu-id="8329c-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you'll package next.</span></span> <span data-ttu-id="8329c-146">Si recibe errores sobre referencias que faltan, haga clic con el botón derecho en la solución, seleccione **Restaurar paquetes NuGet** para instalar las dependencias y vuelva a compilar.</span><span class="sxs-lookup"><span data-stu-id="8329c-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="8329c-147">Para compilar para iOS necesita un equipo Mac en red conectado a Visual Studio como se describe en [Introducción a Xamarin.iOS para Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="8329c-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="8329c-148">Si no tiene un equipo Mac disponible, desactive el proyecto de iOS en el administrador de configuración (paso 3 anterior).</span><span class="sxs-lookup"><span data-stu-id="8329c-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="8329c-149">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="8329c-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="8329c-150">Abra un símbolo del sistema, vaya a la carpeta `LoggingLibrary` que está un nivel por debajo de la ubicación del archivo `.sln` y ejecute el comando `spec` de NuGet para crear el archivo `Package.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="8329c-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

```cli
nuget spec
```

1. <span data-ttu-id="8329c-151">Cambie el nombre de este archivo por `LoggingLibrary.nuspec` y ábralo en un editor.</span><span class="sxs-lookup"><span data-stu-id="8329c-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="8329c-152">Actualice el archivo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado.</span><span class="sxs-lookup"><span data-stu-id="8329c-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="8329c-153">El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="8329c-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="8329c-154">Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="8329c-154">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

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
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="8329c-155">Puede usar `-alpha`, `-beta` o `-rc` como sufijo de la versión del paquete para marcarlo como versión preliminar, consulte [Versiones preliminares](../create-packages/prerelease-packages.md) para obtener más información sobre las versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="8329c-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="8329c-156">Agregar ensamblados de referencia</span><span class="sxs-lookup"><span data-stu-id="8329c-156">Add reference assemblies</span></span>

<span data-ttu-id="8329c-157">Para incluir ensamblados de referencia específicos de la plataforma, agregue lo siguiente al elemento `<files>` de `LoggingLibrary.nuspec` según corresponda para las plataformas admitidas:</span><span class="sxs-lookup"><span data-stu-id="8329c-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="8329c-158">Para reducir los nombres de los archivos DLL y XML, haga clic con el botón derecho en cualquier proyecto, seleccione la pestaña **Biblioteca** y cambie los nombres de ensamblado.</span><span class="sxs-lookup"><span data-stu-id="8329c-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="8329c-159">Agregar dependencias</span><span class="sxs-lookup"><span data-stu-id="8329c-159">Add dependencies</span></span>

<span data-ttu-id="8329c-160">Si tiene dependencias específicas para implementaciones nativas, use el elemento `<dependencies>` con elementos `<group>` para especificarlas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8329c-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="8329c-161">Por ejemplo, lo siguiente establecería iTextSharp como una dependencia para el destino UAP:</span><span class="sxs-lookup"><span data-stu-id="8329c-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="8329c-162">Archivo .nuspec final</span><span class="sxs-lookup"><span data-stu-id="8329c-162">Final .nuspec</span></span>

<span data-ttu-id="8329c-163">Ahora el archivo `.nuspec` final debería ser similar al siguiente, donde debe reemplazar de nuevo SU_NOMBRE con un valor apropiado:</span><span class="sxs-lookup"><span data-stu-id="8329c-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2016</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="8329c-164">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="8329c-164">Package the component</span></span>

<span data-ttu-id="8329c-165">Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="8329c-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="8329c-166">Esto generará `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="8329c-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="8329c-167">Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, verá el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="8329c-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Explorador de paquetes NuGet que en el que se muestra el paquete LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="8329c-169">Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta.</span><span class="sxs-lookup"><span data-stu-id="8329c-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="8329c-170">También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8329c-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="8329c-171">Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="8329c-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="8329c-172">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="8329c-172">Related topics</span></span>

- [<span data-ttu-id="8329c-173">Referencia de NuSpec</span><span class="sxs-lookup"><span data-stu-id="8329c-173">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="8329c-174">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="8329c-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="8329c-175">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="8329c-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="8329c-176">Compatibilidad con varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8329c-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="8329c-177">Inclusión de propiedades y destinos de MSBuild en un paquete</span><span class="sxs-lookup"><span data-stu-id="8329c-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="8329c-178">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="8329c-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)