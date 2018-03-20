---
title: Crear paquetes de NuGet de .NET Standard con Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Tutorial completo para crear paquetes de NuGet de .NET Standard mediante NuGet 3.x y Visual Studio 2015.
keywords: "crear un paquete, paquetes de .NET Standard, tabla de asignación de .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="cd839-104">Crear paquetes de .NET Standard con Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="cd839-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="cd839-105">*Se aplica a NuGet 3.x. Vea [Creación y publicación de un paquete de .NET Standard](../quickstart/create-and-publish-a-package-using-visual-studio.md) para trabajar con NuGet 4.x+.*</span><span class="sxs-lookup"><span data-stu-id="cd839-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="cd839-106">La [biblioteca .NET Standard](/dotnet/articles/standard/library) es una especificación formal de las API de .NET diseñada para estar disponible en todos los runtimes de .NET, lo que establece mayor uniformidad en el ecosistema de .NET.</span><span class="sxs-lookup"><span data-stu-id="cd839-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="cd839-107">La biblioteca de .NET Standard define un conjunto uniforme de API de BCL (biblioteca de clases base) para que todas las plataformas de .NET lo implementen, independientemente de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cd839-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="cd839-108">Permite a los desarrolladores generar código que se pueda usar en todos los runtimes de .NET y reduce, si no las elimina, las directivas de compilación condicional específicas de la plataforma en código compartido.</span><span class="sxs-lookup"><span data-stu-id="cd839-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="cd839-109">En esta guía se describe la creación de un paquete NuGet que tiene como destino la biblioteca de .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="cd839-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="cd839-110">Dicha biblioteca funcionará en .NET Framework 4.6.1, Plataforma universal de Windows 10, .NET Core y Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="cd839-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="cd839-111">Para más información, vea la [tabla de asignación de .NET Standard](#net-standard-mapping-table), que aparece más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="cd839-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd839-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cd839-112">Prerequisites</span></span>

1. <span data-ttu-id="cd839-113">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="cd839-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="cd839-114">SDK de .NET Core</span><span class="sxs-lookup"><span data-stu-id="cd839-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="cd839-115">CLI de NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd839-115">NuGet CLI.</span></span> <span data-ttu-id="cd839-116">Descargue la versión más reciente de nuget.exe desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en una ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="cd839-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="cd839-117">Después, agregue esa ubicación a la variable de entorno PATH si aún no está.</span><span class="sxs-lookup"><span data-stu-id="cd839-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="cd839-118">nuget.exe es la propia herramienta de la CLI, no un instalador, por lo que debe asegurarse de guardar el archivo descargado desde el explorador en lugar de ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="cd839-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="cd839-119">Crear el proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="cd839-119">Create the class library project</span></span>

1. <span data-ttu-id="cd839-120">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > Windows**, seleccione **Biblioteca de clases (portable)**, cambie el nombre a AppLogger y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="cd839-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Crear otro proyecto de biblioteca de clases](media/NetStandard-NewProject.png)

1. <span data-ttu-id="cd839-122">En el cuadro de diálogo **Agregar Biblioteca de clases portable** que aparece, seleccione las opciones `.NET Framework 4.6` y `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="cd839-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="cd839-123">Haga clic con el botón derecho en `AppLogger (Portable)` en el Explorador de soluciones, seleccione **Propiedades**, seleccione la pestaña **Biblioteca** y, luego, haga clic en **Usar como destino la plataforma del estándar .NET** en la sección **Destino**.</span><span class="sxs-lookup"><span data-stu-id="cd839-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="cd839-124">Se le pedirá que lo confirme. Después, podrá seleccionar `.NET Standard 1.4` en la lista desplegable:</span><span class="sxs-lookup"><span data-stu-id="cd839-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Establecer el destino en .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="cd839-126">Haga clic en la pestaña **Compilar**, cambie la **configuración** a `Release` y active la casilla de **Archivo de documentación XML**.</span><span class="sxs-lookup"><span data-stu-id="cd839-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="cd839-127">Agregue el código al componente, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cd839-127">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="cd839-128">Establezca la configuración en Liberar, compile el proyecto y compruebe que los archivos DLL y XML se crean dentro de la carpeta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="cd839-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="cd839-129">Crear y actualizar el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="cd839-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="cd839-130">Abra un símbolo del sistema, vaya a la carpeta que contiene la carpeta `AppLogger.csproj` (que está un nivel por debajo de la ubicación del archivo `.sln`) y ejecute el comando `spec` de NuGet para crear el archivo `AppLogger.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="cd839-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="cd839-131">Abra `AppLogger.nuspec` en un editor y actualícelo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado.</span><span class="sxs-lookup"><span data-stu-id="cd839-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="cd839-132">El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="cd839-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="cd839-133">Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="cd839-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="cd839-134">Agregue ensamblados de referencia al archivo `.nuspec`, es decir, el archivo DLL de la biblioteca y el archivo XML de IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="cd839-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="cd839-135">Haga clic con el botón derecho en la solución y seleccione **Compilar solución** para generar todos los archivos del paquete.</span><span class="sxs-lookup"><span data-stu-id="cd839-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="cd839-136">Declarar dependencias</span><span class="sxs-lookup"><span data-stu-id="cd839-136">Declaring dependencies</span></span>

<span data-ttu-id="cd839-137">Si tiene dependencias en otros paquetes de NuGet, muéstrelos en una lista en el elemento `<dependencies>` del manifiesto con elementos `<group>`.</span><span class="sxs-lookup"><span data-stu-id="cd839-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="cd839-138">Por ejemplo, para declarar una dependencia en NewtonSoft.Json 8.0.3 o en una versión posterior, agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cd839-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="cd839-139">La sintaxis del atributo *version* aquí indica que la versión 8.0.3 o una versión posterior es aceptable.</span><span class="sxs-lookup"><span data-stu-id="cd839-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="cd839-140">Para especificar distintos intervalos de versiones, vea [Control de versiones de paquetes](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="cd839-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="cd839-141">Agregar un archivo Léame</span><span class="sxs-lookup"><span data-stu-id="cd839-141">Adding a readme</span></span>

<span data-ttu-id="cd839-142">Cree el archivo `readme.txt`, colóquelo en la carpeta raíz del proyecto y haga referencia a él en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="cd839-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="cd839-143">Visual Studio muestra `readme.txt` cuando el paquete se instala en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="cd839-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="cd839-144">El archivo no se muestra cuando se instala en los proyectos de .NET Core, o para paquetes que se instalan como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="cd839-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="cd839-145">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="cd839-145">Package the component</span></span>

<span data-ttu-id="cd839-146">Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="cd839-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="cd839-147">Esto generará `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="cd839-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="cd839-148">Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, se ve el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="cd839-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Explorador de paquetes NuGet en el que se muestra el paquete AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="cd839-150">Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta.</span><span class="sxs-lookup"><span data-stu-id="cd839-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="cd839-151">También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cd839-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="cd839-152">Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar paquetes](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="cd839-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="cd839-153">Tenga en cuenta que `pack` requiere Mono 4.4.2 en Mac OS X y no funciona en los sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="cd839-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="cd839-154">En los equipos Mac, también debe convertir los nombres de las rutas de acceso de Windows del archivo `.nuspec` a las rutas de acceso de estilo Unix.</span><span class="sxs-lookup"><span data-stu-id="cd839-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="cd839-155">Tabla de asignación de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="cd839-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="cd839-156">Nombre de la plataforma</span><span class="sxs-lookup"><span data-stu-id="cd839-156">Platform Name</span></span> | <span data-ttu-id="cd839-157">Alias</span><span class="sxs-lookup"><span data-stu-id="cd839-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="cd839-158">Estándar .NET</span><span class="sxs-lookup"><span data-stu-id="cd839-158">.NET Standard</span></span> | <span data-ttu-id="cd839-159">netstandard</span><span class="sxs-lookup"><span data-stu-id="cd839-159">netstandard</span></span> | <span data-ttu-id="cd839-160">1.0</span><span class="sxs-lookup"><span data-stu-id="cd839-160">1.0</span></span> | <span data-ttu-id="cd839-161">1.1</span><span class="sxs-lookup"><span data-stu-id="cd839-161">1.1</span></span> | <span data-ttu-id="cd839-162">1.2</span><span class="sxs-lookup"><span data-stu-id="cd839-162">1.2</span></span> | <span data-ttu-id="cd839-163">1.3</span><span class="sxs-lookup"><span data-stu-id="cd839-163">1.3</span></span> | <span data-ttu-id="cd839-164">1.4</span><span class="sxs-lookup"><span data-stu-id="cd839-164">1.4</span></span> | <span data-ttu-id="cd839-165">1.5</span><span class="sxs-lookup"><span data-stu-id="cd839-165">1.5</span></span> | <span data-ttu-id="cd839-166">1.6</span><span class="sxs-lookup"><span data-stu-id="cd839-166">1.6</span></span> |
| <span data-ttu-id="cd839-167">Núcleo de .NET</span><span class="sxs-lookup"><span data-stu-id="cd839-167">.NET Core</span></span> | <span data-ttu-id="cd839-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="cd839-168">netcoreapp</span></span> | <span data-ttu-id="cd839-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-169">&#x2192;</span></span> | <span data-ttu-id="cd839-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-170">&#x2192;</span></span> | <span data-ttu-id="cd839-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-171">&#x2192;</span></span> | <span data-ttu-id="cd839-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-172">&#x2192;</span></span> | <span data-ttu-id="cd839-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-173">&#x2192;</span></span> | <span data-ttu-id="cd839-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-174">&#x2192;</span></span> | <span data-ttu-id="cd839-175">1.0</span><span class="sxs-lookup"><span data-stu-id="cd839-175">1.0</span></span> |
| <span data-ttu-id="cd839-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="cd839-176">.NET Framework</span></span> | <span data-ttu-id="cd839-177">net</span><span class="sxs-lookup"><span data-stu-id="cd839-177">net</span></span> | <span data-ttu-id="cd839-178">4.5</span><span class="sxs-lookup"><span data-stu-id="cd839-178">4.5</span></span> | <span data-ttu-id="cd839-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="cd839-179">4.5.1</span></span> | <span data-ttu-id="cd839-180">4.6</span><span class="sxs-lookup"><span data-stu-id="cd839-180">4.6</span></span> | <span data-ttu-id="cd839-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="cd839-181">4.6.1</span></span> | <span data-ttu-id="cd839-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="cd839-182">4.6.2</span></span> | <span data-ttu-id="cd839-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="cd839-183">4.6.3</span></span> |
| <span data-ttu-id="cd839-184">Plataformas Mono/Xamarin</span><span class="sxs-lookup"><span data-stu-id="cd839-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="cd839-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-185">&#x2192;</span></span> | <span data-ttu-id="cd839-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-186">&#x2192;</span></span> | <span data-ttu-id="cd839-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-187">&#x2192;</span></span> | <span data-ttu-id="cd839-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-188">&#x2192;</span></span> | <span data-ttu-id="cd839-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-189">&#x2192;</span></span> | <span data-ttu-id="cd839-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-190">&#x2192;</span></span> |
| <span data-ttu-id="cd839-191">Plataforma universal de Windows</span><span class="sxs-lookup"><span data-stu-id="cd839-191">Universal Windows Platform</span></span> | <span data-ttu-id="cd839-192">uap</span><span class="sxs-lookup"><span data-stu-id="cd839-192">uap</span></span> | <span data-ttu-id="cd839-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-193">&#x2192;</span></span> | <span data-ttu-id="cd839-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-194">&#x2192;</span></span> | <span data-ttu-id="cd839-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-195">&#x2192;</span></span> | <span data-ttu-id="cd839-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-196">&#x2192;</span></span> |<span data-ttu-id="cd839-197">10.0</span><span class="sxs-lookup"><span data-stu-id="cd839-197">10.0</span></span> |
| <span data-ttu-id="cd839-198">Windows</span><span class="sxs-lookup"><span data-stu-id="cd839-198">Windows</span></span> | <span data-ttu-id="cd839-199">win</span><span class="sxs-lookup"><span data-stu-id="cd839-199">win</span></span>| <span data-ttu-id="cd839-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-200">&#x2192;</span></span> | <span data-ttu-id="cd839-201">8.0</span><span class="sxs-lookup"><span data-stu-id="cd839-201">8.0</span></span> | <span data-ttu-id="cd839-202">8.1</span><span class="sxs-lookup"><span data-stu-id="cd839-202">8.1</span></span> |
| <span data-ttu-id="cd839-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="cd839-203">Windows Phone</span></span> | <span data-ttu-id="cd839-204">wpa</span><span class="sxs-lookup"><span data-stu-id="cd839-204">wpa</span></span>| <span data-ttu-id="cd839-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-205">&#x2192;</span></span>| <span data-ttu-id="cd839-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cd839-206">&#x2192;</span></span> | <span data-ttu-id="cd839-207">8.1</span><span class="sxs-lookup"><span data-stu-id="cd839-207">8.1</span></span> |
| <span data-ttu-id="cd839-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="cd839-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="cd839-209">wp</span><span class="sxs-lookup"><span data-stu-id="cd839-209">wp</span></span> | <span data-ttu-id="cd839-210">8.0</span><span class="sxs-lookup"><span data-stu-id="cd839-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="cd839-211">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="cd839-211">Related topics</span></span>

- [<span data-ttu-id="cd839-212">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="cd839-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="cd839-213">Compatibilidad con varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="cd839-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="cd839-214">Incluir propiedades y destinos de MSBuild en un paquete</span><span class="sxs-lookup"><span data-stu-id="cd839-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="cd839-215">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="cd839-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="cd839-216">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="cd839-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="cd839-217">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="cd839-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="cd839-218">Documentación de la biblioteca de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="cd839-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="cd839-219">Portabilidad a .NET Core desde .NET Framework</span><span class="sxs-lookup"><span data-stu-id="cd839-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
