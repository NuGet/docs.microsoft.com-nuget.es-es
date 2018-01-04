---
title: Crear paquetes de NuGet de .NET Standard con Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: Tutorial completo para crear paquetes de NuGet de .NET Standard mediante NuGet 3.x y Visual Studio 2015.
keywords: "crear un paquete, paquetes de .NET Standard, tabla de asignación de .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="55658-104">Crear paquetes de .NET Standard con Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="55658-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="55658-105">*Se aplica a NuGet 3.x. Vea [Crear paquetes de .NET Standard con Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) para trabajar con NuGet 4.x+.*</span><span class="sxs-lookup"><span data-stu-id="55658-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="55658-106">La [biblioteca .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) es una especificación formal de las API de .NET diseñada para estar disponible en todos los runtimes de .NET, lo que establece mayor uniformidad en el ecosistema de .NET.</span><span class="sxs-lookup"><span data-stu-id="55658-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="55658-107">La biblioteca de .NET Standard define un conjunto uniforme de API de BCL (biblioteca de clases base) para que todas las plataformas de .NET lo implementen, independientemente de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="55658-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="55658-108">Permite a los desarrolladores generar PCL que se puedan usar en todos los runtimes de .NET y reduce, si no elimina, las directivas de compilación condicional específicas de la plataforma en código compartido.</span><span class="sxs-lookup"><span data-stu-id="55658-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="55658-109">En esta guía se describe la creación de un paquete de NuGet que tenga como destino la biblioteca de .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="55658-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="55658-110">Funcionará en .NET Framework 4.6.1, Plataforma universal de Windows 10, .NET Core y Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="55658-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="55658-111">Para más información, vea la [tabla de asignación de .NET Standard](#net-standard-mapping-table), que aparece más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="55658-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="55658-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="55658-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="55658-113">Crear el proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="55658-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="55658-114">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="55658-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="55658-115">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="55658-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="55658-116">Opciones adicionales</span><span class="sxs-lookup"><span data-stu-id="55658-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="55658-117">Tabla de asignación de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="55658-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="55658-118">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="55658-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="55658-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="55658-119">Pre-requisites</span></span>

1. <span data-ttu-id="55658-120">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="55658-120">Visual Studio 2015.</span></span> <span data-ttu-id="55658-121">Instale la edición Community gratuita desde [visualstudio.com](https://www.visualstudio.com/); también puede usar las ediciones Professional y Enterprise, por supuesto.</span><span class="sxs-lookup"><span data-stu-id="55658-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="55658-122">.NET Core: instale .NET Core junto con las plantillas y otras herramientas para Visual Studio 2015 en [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span><span class="sxs-lookup"><span data-stu-id="55658-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="55658-123">CLI de NuGet.</span><span class="sxs-lookup"><span data-stu-id="55658-123">NuGet CLI.</span></span> <span data-ttu-id="55658-124">Descargue la versión más reciente de nuget.exe desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en una ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="55658-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="55658-125">Después, agregue esa ubicación a la variable de entorno PATH si aún no está.</span><span class="sxs-lookup"><span data-stu-id="55658-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="55658-126">nuget.exe es la propia herramienta de la CLI, no un instalador, por lo que debe asegurarse de guardar el archivo descargado desde el explorador en lugar de ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="55658-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="55658-127">Crear el proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="55658-127">Create the class library project</span></span>

1. <span data-ttu-id="55658-128">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > Windows**, seleccione **Biblioteca de clases (portable)**, cambie el nombre a AppLogger y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="55658-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Crear otro proyecto de biblioteca de clases](media/NetStandard-NewProject.png)

1. <span data-ttu-id="55658-130">En el cuadro de diálogo **Agregar Biblioteca de clases portable** que aparece, seleccione las opciones `.NET Framework 4.6` y `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="55658-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="55658-131">Haga clic con el botón derecho en `AppLogger (Portable)` en el Explorador de soluciones, seleccione **Propiedades**, seleccione la pestaña **Biblioteca** y, luego, haga clic en **Usar como destino la plataforma del estándar .NET** en la sección **Destino**.</span><span class="sxs-lookup"><span data-stu-id="55658-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="55658-132">Se le pedirá que lo confirme. Después, podrá seleccionar `.NET Standard 1.4` en la lista desplegable:</span><span class="sxs-lookup"><span data-stu-id="55658-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Establecer el destino en .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="55658-134">Haga clic en la pestaña **Compilar**, cambie la **configuración** a `Release` y active la casilla de **Archivo de documentación XML**.</span><span class="sxs-lookup"><span data-stu-id="55658-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="55658-135">Agregue el código al componente, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="55658-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="55658-136">Compile el proyecto (con la configuración Versión) y compruebe que los archivos DLL y XML se crean dentro de la carpeta bin\Release.</span><span class="sxs-lookup"><span data-stu-id="55658-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="55658-137">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="55658-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="55658-138">Abra un símbolo del sistema, vaya a la carpeta que contiene la carpeta `AppLogg.csproj` (que está un nivel por debajo de la ubicación del archivo `.sln`) y ejecute el comando `spec` de NuGet para crear el archivo `AppLogger.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="55658-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="55658-139">Abra `AppLogger.nuspec` en un editor y actualícelo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado.</span><span class="sxs-lookup"><span data-stu-id="55658-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="55658-140">El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="55658-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="55658-141">Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="55658-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="55658-142">Agregue ensamblados de referencia al archivo `.nuspec`, es decir, el archivo DLL de la biblioteca y el archivo XML de IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="55658-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="55658-143">Haga clic con el botón derecho en la solución y seleccione **Compilar solución** para generar todos los archivos del paquete.</span><span class="sxs-lookup"><span data-stu-id="55658-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="55658-144">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="55658-144">Package the component</span></span>

<span data-ttu-id="55658-145">Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="55658-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="55658-146">Esto generará `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="55658-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="55658-147">Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, verá el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="55658-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Explorador de paquetes NuGet en el que se muestra el paquete AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="55658-149">Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta.</span><span class="sxs-lookup"><span data-stu-id="55658-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="55658-150">También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="55658-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="55658-151">Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="55658-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="55658-152">Tenga en cuenta que `pack` requiere Mono 4.4.2 en Mac OS X y no funciona en los sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="55658-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="55658-153">En los equipos Mac, también debe convertir los nombres de las rutas de acceso de Windows del archivo `.nuspec` a las rutas de acceso de estilo Unix.</span><span class="sxs-lookup"><span data-stu-id="55658-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="55658-154">Opciones adicionales</span><span class="sxs-lookup"><span data-stu-id="55658-154">Additional options</span></span>

<span data-ttu-id="55658-155">En las siguientes secciones se examinan a fondo opciones adicionales para crear paquetes de NuGet:</span><span class="sxs-lookup"><span data-stu-id="55658-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="55658-156">Declarar dependencias</span><span class="sxs-lookup"><span data-stu-id="55658-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="55658-157">Compatibilidad con varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="55658-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="55658-158">Agregar propiedades y destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="55658-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="55658-159">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="55658-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="55658-160">Agregar un archivo Léame</span><span class="sxs-lookup"><span data-stu-id="55658-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="55658-161">Declarar dependencias</span><span class="sxs-lookup"><span data-stu-id="55658-161">Declaring dependencies</span></span>

<span data-ttu-id="55658-162">Si tiene dependencias en otros paquetes de NuGet, muéstrelos en una lista en el elemento `<dependencies>` con elementos `<group>`.</span><span class="sxs-lookup"><span data-stu-id="55658-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="55658-163">Por ejemplo, para declarar una dependencia en NewtonSoft.Json 8.0.3 o en una versión posterior, agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="55658-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="55658-164">La sintaxis del atributo *version* aquí indica que la versión 8.0.3 o una versión posterior es aceptable.</span><span class="sxs-lookup"><span data-stu-id="55658-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="55658-165">Para especificar distintos intervalos de versiones, vea [Control de versiones de paquetes](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="55658-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="55658-166">Compatibilidad con varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="55658-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="55658-167">Imagínese que quiere aprovechar las ventajas de una API en .NET Framework 4.6.2 que no está disponible en .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="55658-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="55658-168">Para ello, primero tendrá que asegurarse de que la biblioteca se compila para .NET 4.6.2 mediante proyectos compartidos o de compilación condicional</span><span class="sxs-lookup"><span data-stu-id="55658-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="55658-169">(en Visual Studio puede crear un proyecto de NetCore, agregar la plataforma que quiera a la sección de varias plataformas y, luego, efectuar la compilación). Luego, deberá crear el paquete con la sencilla técnica del directorio de trabajo basado en convenciones, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="55658-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="55658-170">En la carpeta raíz del proyecto que contiene el archivo `.nuspec`, cree una carpeta denominada `lib`.</span><span class="sxs-lookup"><span data-stu-id="55658-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="55658-171">Dentro de `lib`, cree carpetas para cada plataforma que quiera admitir:</span><span class="sxs-lookup"><span data-stu-id="55658-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="55658-172">En el archivo `.nuspec`, agregue un nodo `files` debajo del nodo `package` y haga referencia a los archivos de `lib` usando caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="55658-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="55658-173">**Nota:** los reemplazos de tokens no se admiten en el método de directorio de trabajo basado en convenciones, por lo que deberá reemplazarlos por valores literales:</span><span class="sxs-lookup"><span data-stu-id="55658-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="55658-174">Vuelva a crear el paquete mediante `nuget pack AppLogger.spec`.</span><span class="sxs-lookup"><span data-stu-id="55658-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="55658-175">Para más información sobre cómo aplicar esta técnica, vea [Compatibilidad con varias versiones de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="55658-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="55658-176">Agregar propiedades y destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="55658-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="55658-177">En algunos casos es posible que quiera agregar destinos de compilación personalizados o propiedades en proyectos en los que se consume el paquete, como la ejecución de una herramienta o un proceso personalizado durante la compilación.</span><span class="sxs-lookup"><span data-stu-id="55658-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="55658-178">Para ello, debe agregar archivos a una carpeta `\build`, tal como se describe en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="55658-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="55658-179">Cuando NuGet instala un paquete con archivos \build, agrega un elemento de MSBuild en el archivo de proyecto que apunta a los archivos .targets y .props.</span><span class="sxs-lookup"><span data-stu-id="55658-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="55658-180">Cuando se usa `project.json`, los destinos no se agregan al proyecto, pero se ponen a disposición de este a través de `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="55658-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="55658-181">En la carpeta del proyecto que contiene el archivo `.nuspec`, cree una carpeta denominada `build`.</span><span class="sxs-lookup"><span data-stu-id="55658-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="55658-182">Dentro de `build`, cree carpetas para cada propiedad y destino admitidos y, dentro de estos, coloque los archivos `.targets` y `.props`:</span><span class="sxs-lookup"><span data-stu-id="55658-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="55658-183">En el archivo `.nuspec`, agregue un nodo `files` debajo del nodo `package` y haga referencia a los archivos de `build` usando caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="55658-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="55658-184">Vuelva a crear el paquete mediante `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="55658-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="55658-185">Para más información, vea [Incluir propiedades y destinos de MSBuild en un paquete](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="55658-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="55658-186">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="55658-186">Creating localized packages</span></span>

<span data-ttu-id="55658-187">Para crear versiones localizadas de la biblioteca, puede crear paquetes independientes para distintas configuraciones regionales o puede incluir ensamblados de recursos localizados en un único paquete.</span><span class="sxs-lookup"><span data-stu-id="55658-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="55658-188">Aquí se muestra cómo aplicar el último enfoque para los idiomas alemán e italiano:</span><span class="sxs-lookup"><span data-stu-id="55658-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="55658-189">Dentro de cada carpeta de plataforma de destino de `lib`, cree carpetas para cada idioma admitido que no sea el inglés, que es el predeterminado.</span><span class="sxs-lookup"><span data-stu-id="55658-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="55658-190">En estas carpetas puede colocar ensamblados de recursos y archivos XML de IntelliSense localizados.</span><span class="sxs-lookup"><span data-stu-id="55658-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="55658-191">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="55658-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="55658-192">En el archivo `.nuspec`, haga referencia a estos archivos en el nodo `<files>`:</span><span class="sxs-lookup"><span data-stu-id="55658-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="55658-193">Vuelva a crear el paquete mediante `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="55658-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="55658-194">Agregar un archivo Léame</span><span class="sxs-lookup"><span data-stu-id="55658-194">Adding a readme</span></span>

<span data-ttu-id="55658-195">Al incluir un archivo `readme.txt` en la raíz del paquete, Visual Studio lo mostrará cuando el paquete se instale directamente.</span><span class="sxs-lookup"><span data-stu-id="55658-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="55658-196">No se muestran los archivos Léame de los paquetes que se instalan como dependencia, así como tampoco de los proyectos de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="55658-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="55658-197">Para ello, cree el archivo `readme.txt`, colóquelo en la carpeta raíz del proyecto y haga referencia a él en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="55658-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="55658-198">Tabla de asignación de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="55658-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="55658-199">Nombre de la plataforma</span><span class="sxs-lookup"><span data-stu-id="55658-199">Platform Name</span></span> |<span data-ttu-id="55658-200">Alias</span><span class="sxs-lookup"><span data-stu-id="55658-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="55658-201">Estándar .NET</span><span class="sxs-lookup"><span data-stu-id="55658-201">.NET Standard</span></span> | <span data-ttu-id="55658-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="55658-202">netstandard</span></span>| <span data-ttu-id="55658-203">1.0</span><span class="sxs-lookup"><span data-stu-id="55658-203">1.0</span></span>| <span data-ttu-id="55658-204">1.1</span><span class="sxs-lookup"><span data-stu-id="55658-204">1.1</span></span>| <span data-ttu-id="55658-205">1.2</span><span class="sxs-lookup"><span data-stu-id="55658-205">1.2</span></span>| <span data-ttu-id="55658-206">1.3</span><span class="sxs-lookup"><span data-stu-id="55658-206">1.3</span></span>| <span data-ttu-id="55658-207">1.4</span><span class="sxs-lookup"><span data-stu-id="55658-207">1.4</span></span>| <span data-ttu-id="55658-208">1.5</span><span class="sxs-lookup"><span data-stu-id="55658-208">1.5</span></span>| <span data-ttu-id="55658-209">1.6</span><span class="sxs-lookup"><span data-stu-id="55658-209">1.6</span></span>|
|<span data-ttu-id="55658-210">Núcleo de .NET</span><span class="sxs-lookup"><span data-stu-id="55658-210">.NET Core</span></span> | <span data-ttu-id="55658-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="55658-211">netcoreapp</span></span>| <span data-ttu-id="55658-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-212">&#x2192;</span></span>| <span data-ttu-id="55658-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-213">&#x2192;</span></span>| <span data-ttu-id="55658-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-214">&#x2192;</span></span>| <span data-ttu-id="55658-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-215">&#x2192;</span></span>| <span data-ttu-id="55658-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-216">&#x2192;</span></span>| <span data-ttu-id="55658-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-217">&#x2192;</span></span>| <span data-ttu-id="55658-218">1.0</span><span class="sxs-lookup"><span data-stu-id="55658-218">1.0</span></span>|
|<span data-ttu-id="55658-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="55658-219">.NET Framework</span></span>| <span data-ttu-id="55658-220">net</span><span class="sxs-lookup"><span data-stu-id="55658-220">net</span></span>| <span data-ttu-id="55658-221">4.5</span><span class="sxs-lookup"><span data-stu-id="55658-221">4.5</span></span>| <span data-ttu-id="55658-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="55658-222">4.5.1</span></span>| <span data-ttu-id="55658-223">4.6</span><span class="sxs-lookup"><span data-stu-id="55658-223">4.6</span></span>| <span data-ttu-id="55658-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="55658-224">4.6.1</span></span>| <span data-ttu-id="55658-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="55658-225">4.6.2</span></span>| <span data-ttu-id="55658-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="55658-226">4.6.3</span></span>|
|<span data-ttu-id="55658-227">Plataformas Mono/Xamarin</span><span class="sxs-lookup"><span data-stu-id="55658-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="55658-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-228">&#x2192;</span></span>| <span data-ttu-id="55658-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-229">&#x2192;</span></span>| <span data-ttu-id="55658-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-230">&#x2192;</span></span>| <span data-ttu-id="55658-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-231">&#x2192;</span></span>| <span data-ttu-id="55658-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-232">&#x2192;</span></span>| <span data-ttu-id="55658-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-233">&#x2192;</span></span>|
|<span data-ttu-id="55658-234">Plataforma universal de Windows</span><span class="sxs-lookup"><span data-stu-id="55658-234">Universal Windows Platform</span></span>| <span data-ttu-id="55658-235">uap</span><span class="sxs-lookup"><span data-stu-id="55658-235">uap</span></span>| <span data-ttu-id="55658-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-236">&#x2192;</span></span>| <span data-ttu-id="55658-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-237">&#x2192;</span></span>| <span data-ttu-id="55658-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-238">&#x2192;</span></span>| <span data-ttu-id="55658-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-239">&#x2192;</span></span>|<span data-ttu-id="55658-240">10.0</span><span class="sxs-lookup"><span data-stu-id="55658-240">10.0</span></span>|
|<span data-ttu-id="55658-241">Windows</span><span class="sxs-lookup"><span data-stu-id="55658-241">Windows</span></span>| <span data-ttu-id="55658-242">win</span><span class="sxs-lookup"><span data-stu-id="55658-242">win</span></span>| <span data-ttu-id="55658-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-243">&#x2192;</span></span>| <span data-ttu-id="55658-244">8.0</span><span class="sxs-lookup"><span data-stu-id="55658-244">8.0</span></span>| <span data-ttu-id="55658-245">8.1</span><span class="sxs-lookup"><span data-stu-id="55658-245">8.1</span></span>|
|<span data-ttu-id="55658-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="55658-246">Windows Phone</span></span>| <span data-ttu-id="55658-247">wpa</span><span class="sxs-lookup"><span data-stu-id="55658-247">wpa</span></span>| <span data-ttu-id="55658-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-248">&#x2192;</span></span>| <span data-ttu-id="55658-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="55658-249">&#x2192;</span></span>|<span data-ttu-id="55658-250">8.1</span><span class="sxs-lookup"><span data-stu-id="55658-250">8.1</span></span>|
|<span data-ttu-id="55658-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="55658-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="55658-252">wp</span><span class="sxs-lookup"><span data-stu-id="55658-252">wp</span></span>| <span data-ttu-id="55658-253">8.0</span><span class="sxs-lookup"><span data-stu-id="55658-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="55658-254">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="55658-254">Related topics</span></span>

- [<span data-ttu-id="55658-255">Referencia de NuSpec</span><span class="sxs-lookup"><span data-stu-id="55658-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="55658-256">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="55658-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="55658-257">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="55658-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="55658-258">Compatibilidad con varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="55658-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="55658-259">Incluir propiedades y destinos de MSBuild en un paquete</span><span class="sxs-lookup"><span data-stu-id="55658-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="55658-260">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="55658-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="55658-261">Documentación de la biblioteca de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="55658-261">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="55658-262">Portabilidad a .NET Core desde .NET Framework</span><span class="sxs-lookup"><span data-stu-id="55658-262">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
