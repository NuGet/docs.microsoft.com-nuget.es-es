---
title: Creación de paquetes NuGet para la plataforma UWP (C#)
description: Un tutorial integral de creación de paquetes NuGet con un componente de Windows Runtime para la Plataforma universal de Windows en C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 22df2cd6dc374ba265c79a019747191e797b774c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774286"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="e9e53-103">Creación de paquetes UWP (C#)</span><span class="sxs-lookup"><span data-stu-id="e9e53-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="e9e53-104">La [Plataforma universal de Windows (UWP)](/windows/uwp) proporciona una plataforma de aplicación común para todos los dispositivos que ejecutan Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e9e53-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="e9e53-105">Dentro de este modelo, las aplicaciones para UWP pueden llamar a las API de WinRT que son comunes a todos los dispositivos y también a las API (incluidas las de Win32 y .NET) que son específicas de la familia de dispositivos en la que se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9e53-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="e9e53-106">En este tutorial se creará un paquete NuGet con un componente de C# de UWP (incluido un control XAML) que se puede usar en proyectos administrados y nativos.</span><span class="sxs-lookup"><span data-stu-id="e9e53-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9e53-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9e53-107">Prerequisites</span></span>

1. <span data-ttu-id="e9e53-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="e9e53-108">Visual Studio 2019.</span></span> <span data-ttu-id="e9e53-109">Instale la versión 2019 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/); también puede usar las ediciones Professional y Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e9e53-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="e9e53-110">CLI de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e9e53-110">NuGet CLI.</span></span> <span data-ttu-id="e9e53-111">Descargue la versión más reciente de `nuget.exe` desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en la ubicación que prefiera (se descarga directamente el `.exe`).</span><span class="sxs-lookup"><span data-stu-id="e9e53-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="e9e53-112">Después, agregue esa ubicación a la variable de entorno PATH si aún no está.</span><span class="sxs-lookup"><span data-stu-id="e9e53-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="e9e53-113">[Más detalles](../reference/nuget-exe-cli-reference.md#windows).</span><span class="sxs-lookup"><span data-stu-id="e9e53-113">[More details](../reference/nuget-exe-cli-reference.md#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="e9e53-114">Crear un componente de Windows Runtime para UWP</span><span class="sxs-lookup"><span data-stu-id="e9e53-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="e9e53-115">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, busque "uwp c#", seleccione la plantilla **Componente de Windows Runtime (Windows universal)** , haga clic en Siguiente, cambie el nombre a ImageEnhancer y haga clic en Crear.</span><span class="sxs-lookup"><span data-stu-id="e9e53-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="e9e53-116">Cuando se le solicite, acepte los valores predeterminados para Versión de destino y Versión mínima.</span><span class="sxs-lookup"><span data-stu-id="e9e53-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Creación de un proyecto de componente de Windows Runtime para UWP](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="e9e53-118">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones, seleccione **Agregar > Nuevo elemento**, seleccione **Control basado en modelo**, cambie el nombre a AwesomeImageControl.cs y haga clic en **Agregar**:</span><span class="sxs-lookup"><span data-stu-id="e9e53-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Adición de un nuevo elemento de control basado en modelo XAML al proyecto](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="e9e53-120">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones y seleccione **Propiedades.**</span><span class="sxs-lookup"><span data-stu-id="e9e53-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="e9e53-121">En la página Propiedades, elija la pestaña **Compilar** y habilite **Archivo de documentación XML**:</span><span class="sxs-lookup"><span data-stu-id="e9e53-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![Establecimiento de Generar archivos de documentación XML en Sí](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="e9e53-123">Ahora, haga clic con el botón derecho en la *solución*, seleccione **Compilación por lotes** y active las cinco casillas de compilación del cuadro de diálogo como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e9e53-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="e9e53-124">Esto garantiza que, cuando realice una compilación, se generará un conjunto completo de artefactos para cada uno de los sistemas de destino compatibles con Windows.</span><span class="sxs-lookup"><span data-stu-id="e9e53-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Generación por lotes](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="e9e53-126">En el cuadro de diálogo Generación por lotes, haga clic en **Compilar** para comprobar el proyecto y crear los archivos de salida que necesita para el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="e9e53-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="e9e53-127">En este tutorial se usan los artefactos de depuración para el paquete.</span><span class="sxs-lookup"><span data-stu-id="e9e53-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="e9e53-128">Para un paquete que no sea de depuración, compruebe las opciones Versión del cuadro de diálogo Generación por lotes en su lugar y haga referencia a las carpetas Versión resultantes en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="e9e53-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="e9e53-129">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="e9e53-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="e9e53-130">Para crear el archivo `.nuspec` inicial, siga los tres pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="e9e53-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="e9e53-131">En las secciones siguientes se le guiará a través de otras actualizaciones necesarias.</span><span class="sxs-lookup"><span data-stu-id="e9e53-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="e9e53-132">Abra un símbolo del sistema y desplácese hasta la carpeta que contiene `ImageEnhancer.csproj` (será una subcarpeta por debajo de donde se encuentra el archivo de la solución).</span><span class="sxs-lookup"><span data-stu-id="e9e53-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="e9e53-133">Ejecute el comando [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md) para generar `ImageEnhancer.nuspec` (el nombre del archivo se toma del nombre del archivo `.csroj`):</span><span class="sxs-lookup"><span data-stu-id="e9e53-133">Run the [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="e9e53-134">Abra `ImageEnhancer.nuspec` en un editor y actualícelo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado.</span><span class="sxs-lookup"><span data-stu-id="e9e53-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="e9e53-135">No deje ninguno de los valores $propertyName$.</span><span class="sxs-lookup"><span data-stu-id="e9e53-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="e9e53-136">El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="e9e53-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="e9e53-137">Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="e9e53-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="e9e53-138">Para los paquetes creados para consumo público, preste especial atención al elemento `<tags>`, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="e9e53-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="e9e53-139">Agregar metadatos de Windows al paquete</span><span class="sxs-lookup"><span data-stu-id="e9e53-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="e9e53-140">Un componente de Windows Runtime requiere metadatos que describan todos sus tipos disponibles públicamente, lo que permite que otras aplicaciones y bibliotecas consuman el componente.</span><span class="sxs-lookup"><span data-stu-id="e9e53-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="e9e53-141">Estos metadatos se incluyen en un archivo .winmd, que se crea al compilar el proyecto y que se debe incluir en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="e9e53-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="e9e53-142">Al mismo tiempo se crea un archivo XML con datos de IntelliSense y también se debe incluir.</span><span class="sxs-lookup"><span data-stu-id="e9e53-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="e9e53-143">Agregue el siguiente nodo `<files>` al archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="e9e53-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="e9e53-144">Adición de contenido XAML</span><span class="sxs-lookup"><span data-stu-id="e9e53-144">Adding XAML content</span></span>

<span data-ttu-id="e9e53-145">Para incluir un control XAML con el componente, debe agregar el archivo XAML que tiene la plantilla predeterminada para el control (generado por la plantilla de proyecto).</span><span class="sxs-lookup"><span data-stu-id="e9e53-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="e9e53-146">Esto también se incluye en la sección `<files>`:</span><span class="sxs-lookup"><span data-stu-id="e9e53-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="e9e53-147">Adición de las bibliotecas de implementación nativas</span><span class="sxs-lookup"><span data-stu-id="e9e53-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="e9e53-148">Dentro del componente, la lógica básica del tipo ImageEnhancer está en código nativo, que se incluye en los distintos ensamblados `ImageEnhancer.winmd` que se generan para cada entorno de ejecución de destino (ARM, ARM64, x86 y x64).</span><span class="sxs-lookup"><span data-stu-id="e9e53-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="e9e53-149">Para incluirlos en el paquete, haga referencia a ellos en la sección `<files>` junto con sus archivos de recursos .pri asociados:</span><span class="sxs-lookup"><span data-stu-id="e9e53-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="e9e53-150">Archivo .nuspec final</span><span class="sxs-lookup"><span data-stu-id="e9e53-150">Final .nuspec</span></span>

<span data-ttu-id="e9e53-151">Ahora el archivo `.nuspec` final debería ser similar al siguiente, donde debe reemplazar de nuevo SU_NOMBRE con un valor apropiado:</span><span class="sxs-lookup"><span data-stu-id="e9e53-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="e9e53-152">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="e9e53-152">Package the component</span></span>

<span data-ttu-id="e9e53-153">Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está a punto para ejecutar el comando [`nuget pack`](../reference/cli-reference/cli-ref-pack.md):</span><span class="sxs-lookup"><span data-stu-id="e9e53-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](../reference/cli-reference/cli-ref-pack.md) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="e9e53-154">Así se genera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="e9e53-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="e9e53-155">Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, verá el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9e53-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Explorador de paquetes NuGet en el que se muestra el paquete ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="e9e53-157">Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta.</span><span class="sxs-lookup"><span data-stu-id="e9e53-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="e9e53-158">También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e9e53-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="e9e53-159">Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e9e53-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="e9e53-160">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="e9e53-160">Related topics</span></span>

- [<span data-ttu-id="e9e53-161">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="e9e53-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="e9e53-162">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="e9e53-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="e9e53-163">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="e9e53-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="e9e53-164">Compatibilidad con varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e9e53-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e9e53-165">Incluir propiedades y destinos de MSBuild en un paquete</span><span class="sxs-lookup"><span data-stu-id="e9e53-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="e9e53-166">Creación de paquetes de localizados</span><span class="sxs-lookup"><span data-stu-id="e9e53-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)