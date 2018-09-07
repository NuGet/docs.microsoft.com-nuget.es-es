---
title: Creación de paquetes NuGet de .NET Standard y .NET Framework con Visual Studio 2015
description: Tutorial completo para crear paquetes NuGet de .NET Standard y .NET Framework mediante NuGet 3.x y Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 7b1ccfbede4cec53cee3ec7d1c023e4c5be60bf0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545918"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="15993-103">Creación de paquetes de .NET Standard y .NET Framework con Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="15993-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="15993-104">**Nota**: Se recomienda usar Visual Studio 2017 para desarrollar bibliotecas de .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="15993-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="15993-105">Visual Studio 2015 puede funcionar pero las herramientas de .NET Core solo se llevaron al estado de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="15993-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="15993-106">Vea [Creación y publicación de un paquete con Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) para trabajar con NuGet 4.x y versiones posteriores y Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="15993-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="15993-107">La [biblioteca .NET Standard](/dotnet/articles/standard/library) es una especificación formal de las API de .NET diseñada para estar disponible en todos los runtimes de .NET, lo que establece mayor uniformidad en el ecosistema de .NET.</span><span class="sxs-lookup"><span data-stu-id="15993-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="15993-108">La biblioteca de .NET Standard define un conjunto uniforme de API de BCL (biblioteca de clases base) para que todas las plataformas de .NET lo implementen, independientemente de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="15993-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="15993-109">Permite a los desarrolladores generar código que se pueda usar en todos los runtimes de .NET y reduce, si no las elimina, las directivas de compilación condicional específicas de la plataforma en código compartido.</span><span class="sxs-lookup"><span data-stu-id="15993-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="15993-110">En esta guía se describe la creación de un paquete NuGet destinado a la biblioteca de .NET Standard 1.4 o un paquete destinado a .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="15993-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="15993-111">Una biblioteca de .NET Standard 1.4 funcionará en .NET Framework 4.6.1, la Plataforma universal de Windows 10, .NET Core y Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="15993-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="15993-112">Para más información, vea la [tabla de asignación de .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (documentación de .NET).</span><span class="sxs-lookup"><span data-stu-id="15993-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="15993-113">Puede elegir otra versión de la biblioteca de .NET si lo prefiere.</span><span class="sxs-lookup"><span data-stu-id="15993-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15993-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="15993-114">Prerequisites</span></span>

1. <span data-ttu-id="15993-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="15993-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="15993-116">(Solo .NET Standard) [SDK de .NET Core](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="15993-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="15993-117">CLI de NuGet.</span><span class="sxs-lookup"><span data-stu-id="15993-117">NuGet CLI.</span></span> <span data-ttu-id="15993-118">Descargue la versión más reciente de nuget.exe desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en una ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="15993-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="15993-119">Después, agregue esa ubicación a la variable de entorno PATH si aún no está.</span><span class="sxs-lookup"><span data-stu-id="15993-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="15993-120">nuget.exe es la propia herramienta de la CLI, no un instalador, por lo que debe asegurarse de guardar el archivo descargado desde el explorador en lugar de ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="15993-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="15993-121">Crear el proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="15993-121">Create the class library project</span></span>

1. <span data-ttu-id="15993-122">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > Windows**, seleccione **Biblioteca de clases (portable)**, cambie el nombre a AppLogger y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="15993-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Crear otro proyecto de biblioteca de clases](media/NetStandard-NewProject.png)

1. <span data-ttu-id="15993-124">En el cuadro de diálogo **Agregar Biblioteca de clases portable** que aparece, seleccione las opciones `.NET Framework 4.6` y `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="15993-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="15993-125">(Si el destino es .NET Framework, puede seleccionar las opciones que sean adecuadas).</span><span class="sxs-lookup"><span data-stu-id="15993-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="15993-126">Si el destino es .NET Framework, haga clic con el botón derecho en `AppLogger (Portable)` en el Explorador de soluciones, seleccione **Propiedades**, la pestaña **Biblioteca** y luego, **Usar como destino la plataforma del estándar .NET** en la sección **Destino**.</span><span class="sxs-lookup"><span data-stu-id="15993-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="15993-127">Esta acción le pedirá confirmación, tras la cual podrá seleccionar `.NET Standard 1.4` (u otra versión disponible) en la lista desplegable:</span><span class="sxs-lookup"><span data-stu-id="15993-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Establecer el destino en .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="15993-129">Haga clic en la pestaña **Compilar**, cambie la **configuración** a `Release` y active la casilla de **Archivo de documentación XML**.</span><span class="sxs-lookup"><span data-stu-id="15993-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="15993-130">Agregue el código al componente, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="15993-130">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="15993-131">Establezca la configuración en Liberar, compile el proyecto y compruebe que los archivos DLL y XML se crean dentro de la carpeta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="15993-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="15993-132">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="15993-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="15993-133">Abra un símbolo del sistema, vaya a la carpeta que contiene la carpeta `AppLogger.csproj` (que está un nivel por debajo de la ubicación del archivo `.sln`) y ejecute el comando `spec` de NuGet para crear el archivo `AppLogger.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="15993-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="15993-134">Abra `AppLogger.nuspec` en un editor y actualícelo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado.</span><span class="sxs-lookup"><span data-stu-id="15993-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="15993-135">El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="15993-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="15993-136">Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="15993-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="15993-137">Agregue ensamblados de referencia al archivo `.nuspec`, es decir, el archivo DLL de la biblioteca y el archivo XML de IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="15993-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="15993-138">Si el destino es .NET Standard, las entradas tendrán un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="15993-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="15993-139">Si el destino es .NET Framework, las entradas tendrán un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="15993-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="15993-140">Haga clic con el botón derecho en la solución y seleccione **Compilar solución** para generar todos los archivos del paquete.</span><span class="sxs-lookup"><span data-stu-id="15993-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="15993-141">Declarar dependencias</span><span class="sxs-lookup"><span data-stu-id="15993-141">Declaring dependencies</span></span>

<span data-ttu-id="15993-142">Si tiene dependencias en otros paquetes de NuGet, muéstrelos en una lista en el elemento `<dependencies>` del manifiesto con elementos `<group>`.</span><span class="sxs-lookup"><span data-stu-id="15993-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="15993-143">Por ejemplo, para declarar una dependencia en NewtonSoft.Json 8.0.3 o en una versión posterior, agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="15993-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="15993-144">La sintaxis del atributo *version* aquí indica que la versión 8.0.3 o una versión posterior es aceptable.</span><span class="sxs-lookup"><span data-stu-id="15993-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="15993-145">Para especificar distintos intervalos de versiones, vea [Control de versiones de paquetes](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="15993-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="15993-146">Agregar un archivo Léame</span><span class="sxs-lookup"><span data-stu-id="15993-146">Adding a readme</span></span>

<span data-ttu-id="15993-147">Cree el archivo `readme.txt`, colóquelo en la carpeta raíz del proyecto y haga referencia a él en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="15993-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="15993-148">Visual Studio muestra `readme.txt` cuando el paquete se instala en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="15993-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="15993-149">El archivo no se muestra cuando se instala en los proyectos de .NET Core, o para paquetes que se instalan como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="15993-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="15993-150">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="15993-150">Package the component</span></span>

<span data-ttu-id="15993-151">Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="15993-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="15993-152">Así se genera `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="15993-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="15993-153">Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, se ve el contenido siguiente (mostrado para .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="15993-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Explorador de paquetes NuGet en el que se muestra el paquete AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="15993-155">Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta.</span><span class="sxs-lookup"><span data-stu-id="15993-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="15993-156">También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="15993-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="15993-157">Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar paquetes](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="15993-157">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="15993-158">Tenga en cuenta que `pack` requiere Mono 4.4.2 en Mac OS X y no funciona en los sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="15993-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="15993-159">En los equipos Mac, también debe convertir los nombres de las rutas de acceso de Windows del archivo `.nuspec` a las rutas de acceso de estilo Unix.</span><span class="sxs-lookup"><span data-stu-id="15993-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="15993-160">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="15993-160">Related topics</span></span>

- [<span data-ttu-id="15993-161">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="15993-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="15993-162">Compatibilidad con varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="15993-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="15993-163">Incluir propiedades y destinos de MSBuild en un paquete</span><span class="sxs-lookup"><span data-stu-id="15993-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="15993-164">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="15993-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="15993-165">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="15993-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="15993-166">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="15993-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="15993-167">Documentación de la biblioteca de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="15993-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="15993-168">Portabilidad a .NET Core desde .NET Framework</span><span class="sxs-lookup"><span data-stu-id="15993-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
