---
title: Crear paquetes NuGet para la Plataforma universal de Windows
description: Un tutorial integral de creación de paquetes NuGet con un componente de Windows Runtime para la Plataforma universal de Windows.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 86fbeea0b815d40ffae016a5f76b96d5baf3ff1b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="create-uwp-packages"></a><span data-ttu-id="6c0f1-103">Crear paquetes UWP</span><span class="sxs-lookup"><span data-stu-id="6c0f1-103">Create UWP packages</span></span>

<span data-ttu-id="6c0f1-104">La [Plataforma universal de Windows (UWP)](https://developer.microsoft.com/windows) proporciona una plataforma de aplicación común para todos los dispositivos que ejecutan Windows 10.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="6c0f1-105">Dentro de este modelo, las aplicaciones para UWP pueden llamar a las API de WinRT que son comunes a todos los dispositivos y también a las API (incluidas las de Win32 y .NET) que son específicas de la familia de dispositivos en la que se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="6c0f1-106">En este tutorial creará un paquete NuGet con un componente nativo de UWP (incluido un control XAML) que se puede usar en proyectos administrados y nativos.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c0f1-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6c0f1-107">Prerequisites</span></span>

1. <span data-ttu-id="6c0f1-108">Visual Studio 2017 o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="6c0f1-109">Instale la 2017 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/); también puede usar las ediciones Professional y Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="6c0f1-110">CLI de NuGet.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-110">NuGet CLI.</span></span> <span data-ttu-id="6c0f1-111">Descargue la versión más reciente de `nuget.exe` desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en la ubicación que prefiera (se descarga directamente el `.exe`).</span><span class="sxs-lookup"><span data-stu-id="6c0f1-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="6c0f1-112">Después, agregue esa ubicación a la variable de entorno PATH si aún no está.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="6c0f1-113">Crear un componente de Windows Runtime para UWP</span><span class="sxs-lookup"><span data-stu-id="6c0f1-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="6c0f1-114">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C++ > Windows > Universal**, seleccione la plantilla **Componente de Windows Runtime (Windows universal)**, cambie el nombre a ImageEnhancer y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="6c0f1-115">Cuando se le solicite, acepte los valores predeterminados para Versión de destino y Versión mínima.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Creación de un proyecto de componente de Windows Runtime para UWP](media/UWP-NewProject.png)

1. <span data-ttu-id="6c0f1-117">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones, seleccione **Agregar > Nuevo elemento**, haga clic en el nodo **Visual C++ > XAML**, seleccione **Control basado en modelo**, cambie el nombre a AwesomeImageControl.cpp y haga clic en **Agregar**:</span><span class="sxs-lookup"><span data-stu-id="6c0f1-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Adición de un nuevo elemento de control basado en modelo XAML al proyecto](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="6c0f1-119">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones y seleccione **Propiedades.**</span><span class="sxs-lookup"><span data-stu-id="6c0f1-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="6c0f1-120">En la página Propiedades, expanda **Propiedades de configuración > C o C++** y haga clic en **Archivos de salida**.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="6c0f1-121">En el panel de la derecha, cambie el valor de **Generar archivos de documentación XML** a Sí:</span><span class="sxs-lookup"><span data-stu-id="6c0f1-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Establecimiento de Generar archivos de documentación XML en Sí](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="6c0f1-123">Ahora, haga clic con el botón derecho en la *solución*, seleccione **Compilación por lotes** y active las tres casillas Depuración del cuadro de diálogo como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="6c0f1-124">Esto garantiza que, cuando realice una compilación, se generará un conjunto completo de artefactos para cada uno de los sistemas de destino compatibles con Windows.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Generación por lotes](media/UWP-BatchBuild.png)

1. <span data-ttu-id="6c0f1-126">En el cuadro de diálogo Generación por lotes, haga clic en **Compilar** para comprobar el proyecto y crear los archivos de salida que necesita para el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="6c0f1-127">En este tutorial se usan los artefactos de depuración para el paquete.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="6c0f1-128">Para un paquete que no sea de depuración, compruebe las opciones Versión del cuadro de diálogo Generación por lotes en su lugar y haga referencia a las carpetas Versión resultantes en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="6c0f1-129">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="6c0f1-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="6c0f1-130">Para crear el archivo `.nuspec` inicial, siga los tres pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="6c0f1-131">En las secciones siguientes se le guiará a través de otras actualizaciones necesarias.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="6c0f1-132">Abra un símbolo del sistema y desplácese hasta la carpeta que contiene `ImageEnhancer.vcxproj` (será una subcarpeta por debajo de donde se encuentra el archivo de la solución).</span><span class="sxs-lookup"><span data-stu-id="6c0f1-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="6c0f1-133">Ejecute el comando `spec` de NuGet para generar `ImageEnhancer.nuspec` (el nombre del archivo se toma del nombre del archivo `.vcxproj`):</span><span class="sxs-lookup"><span data-stu-id="6c0f1-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="6c0f1-134">Abra `ImageEnhancer.nuspec` en un editor y actualícelo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="6c0f1-135">El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="6c0f1-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="6c0f1-136">Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="6c0f1-137">Para los paquetes creados para consumo público, preste especial atención al elemento `<tags>`, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="6c0f1-138">Agregar metadatos de Windows al paquete</span><span class="sxs-lookup"><span data-stu-id="6c0f1-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="6c0f1-139">Un componente de Windows Runtime requiere metadatos que describan todos sus tipos disponibles públicamente, lo que permite que otras aplicaciones y bibliotecas consuman el componente.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="6c0f1-140">Estos metadatos se incluyen en un archivo .winmd, que se crea al compilar el proyecto y que se debe incluir en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="6c0f1-141">Al mismo tiempo se crea un archivo XML con datos de IntelliSense y también se debe incluir.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="6c0f1-142">Agregue el siguiente nodo `<files>` al archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6c0f1-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="6c0f1-143">Adición de contenido XAML</span><span class="sxs-lookup"><span data-stu-id="6c0f1-143">Adding XAML content</span></span>

<span data-ttu-id="6c0f1-144">Para incluir un control XAML con el componente, debe agregar el archivo XAML que tiene la plantilla predeterminada para el control (generado por la plantilla de proyecto).</span><span class="sxs-lookup"><span data-stu-id="6c0f1-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="6c0f1-145">Esto también se incluye en la sección `<files>`:</span><span class="sxs-lookup"><span data-stu-id="6c0f1-145">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="6c0f1-146">Adición de las bibliotecas de implementación nativas</span><span class="sxs-lookup"><span data-stu-id="6c0f1-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="6c0f1-147">Dentro del componente, la lógica básica del tipo ImageEnhancer está en código nativo, que se incluye en los distintos ensamblados `ImageEnhancer.dll` que se generan para cada runtime de destino (ARM, x86 y x64).</span><span class="sxs-lookup"><span data-stu-id="6c0f1-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="6c0f1-148">Para incluirlos en el paquete, haga referencia a ellos en la sección `<files>` junto con sus archivos de recursos .pri asociados:</span><span class="sxs-lookup"><span data-stu-id="6c0f1-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="6c0f1-149">Adición de .targets</span><span class="sxs-lookup"><span data-stu-id="6c0f1-149">Adding .targets</span></span>

<span data-ttu-id="6c0f1-150">Después, los proyectos de C++ y JavaScript que es posible que consuman el paquete NuGet necesitan un archivo .targets para identificar los archivos de ensamblado y winmd necesarios.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="6c0f1-151">(Los proyectos de C# y Visual Basic lo hacen de forma automática). Cree este archivo copiando el texto siguiente en `ImageEnhancer.targets` y guárdelo en la misma carpeta que el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="6c0f1-152">_Nota_: Este archivo `.targets` debe tener el mismo nombre que el identificador de paquete (por ejemplo, el elemento `<Id>` del archivo `.nupspec`):</span><span class="sxs-lookup"><span data-stu-id="6c0f1-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="6c0f1-153">Después, haga referencia a `ImageEnhancer.targets` en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6c0f1-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="6c0f1-154">Archivo .nuspec final</span><span class="sxs-lookup"><span data-stu-id="6c0f1-154">Final .nuspec</span></span>

<span data-ttu-id="6c0f1-155">Ahora el archivo `.nuspec` final debería ser similar al siguiente, donde debe reemplazar de nuevo SU_NOMBRE con un valor apropiado:</span><span class="sxs-lookup"><span data-stu-id="6c0f1-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="6c0f1-156">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="6c0f1-156">Package the component</span></span>

<span data-ttu-id="6c0f1-157">Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="6c0f1-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="6c0f1-158">Así se genera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="6c0f1-159">Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, se ve el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c0f1-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Explorador de paquetes NuGet en el que se muestra el paquete ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="6c0f1-161">Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="6c0f1-162">También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6c0f1-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="6c0f1-163">Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="6c0f1-163">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="6c0f1-164">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="6c0f1-164">Related topics</span></span>

- [<span data-ttu-id="6c0f1-165">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="6c0f1-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="6c0f1-166">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="6c0f1-166">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="6c0f1-167">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="6c0f1-167">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="6c0f1-168">Compatibilidad con varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6c0f1-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="6c0f1-169">Incluir propiedades y destinos de MSBuild en un paquete</span><span class="sxs-lookup"><span data-stu-id="6c0f1-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="6c0f1-170">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="6c0f1-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
