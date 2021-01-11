---
title: Creación de un paquete NuGet con la CLI de nuget.exe
description: Guía detallada sobre el diseño y la creación de un paquete NuGet, incluidos los archivos y el control de versiones.
author: karann-msft
ms.author: feaguila
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: ec06a8f721b7b67ddc5d72323305b9b22f292de6
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699792"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="ad930-103">Creación de un paquete con la CLI de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ad930-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="ad930-104">Con independencia de lo que haga el paquete o lo que contenga el código, use una de las herramientas de CLI, ya sea `nuget.exe` o `dotnet.exe`, para empaquetar esa funcionalidad en un componente que se pueda compartir y usar por parte de otros desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="ad930-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="ad930-105">Para instalar las herramientas de CLI de NuGet, consulte [Instalación de las herramientas del cliente NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="ad930-106">Tenga en cuenta que Visual Studio no incluye una herramienta de CLI de manera automática.</span><span class="sxs-lookup"><span data-stu-id="ad930-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="ad930-107">Con los proyectos que no son de estilo SDK, normalmente proyectos de .NET Framework, siga los pasos descritos en este artículo para crear un paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="ad930-108">Para instrucciones paso a paso sobre cómo usar Visual Studio y la CLI de `nuget.exe`, consulte [Creación y publicación de un paquete de .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="ad930-109">En el caso de los proyectos de .NET Core y .NET Standard que usan el [formato de estilo SDK](../resources/check-project-format.md) y cualquier otro proyecto de estilo SDK, consulte [Creación de un paquete NuGet con la CLI de dotnet](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="ad930-110">Para los proyectos migrados desde `packages.config` a [PackageReference](../consume-packages/package-references-in-project-files.md), utilice [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="ad930-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="ad930-111">Desde un punto de vista técnico, un paquete NuGet es simplemente un archivo ZIP en el que se ha cambiado el nombre con la extensión `.nupkg` y cuyo contenido coincide con determinadas convenciones.</span><span class="sxs-lookup"><span data-stu-id="ad930-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="ad930-112">En este tema se describe el proceso detallado de creación de un paquete que cumple estas convenciones.</span><span class="sxs-lookup"><span data-stu-id="ad930-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="ad930-113">El empaquetado comienza con el código compilado (ensamblados), símbolos y otros archivos que quiera entregar como un paquete (vea [Información general y flujo de trabajo](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="ad930-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="ad930-114">Este proceso es independiente de la compilación o, en otros casos, de la generación de los archivos que se incluyen en el paquete, aunque se puede extraer la información de un archivo de proyecto para mantener sincronizados los ensamblados y paquetes compilados.</span><span class="sxs-lookup"><span data-stu-id="ad930-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="ad930-115">Este tema se aplica a proyectos que no son de estilo SDK, generalmente proyectos que no son de .NET Core y .NET Standard que usan Visual Studio 2017 y versiones superiores, así como NuGet 4.0 y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="ad930-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="ad930-116">Decisión sobre qué ensamblados empaquetar</span><span class="sxs-lookup"><span data-stu-id="ad930-116">Decide which assemblies to package</span></span>

<span data-ttu-id="ad930-117">La mayoría de paquetes de propósito generales contiene uno o más ensamblados que otros desarrolladores pueden usar en sus propios proyectos.</span><span class="sxs-lookup"><span data-stu-id="ad930-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="ad930-118">En general, es preferible disponer de un ensamblado por cada paquete NuGet, siempre que cada ensamblado sea útil por separado.</span><span class="sxs-lookup"><span data-stu-id="ad930-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="ad930-119">Por ejemplo, si tiene un archivo `Utilities.dll` que depende de `Parser.dll` y `Parser.dll` es útil por sí solo, entonces cree un paquete para cada uno.</span><span class="sxs-lookup"><span data-stu-id="ad930-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="ad930-120">Esto permite a los desarrolladores usar `Parser.dll` independientemente de `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="ad930-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="ad930-121">Si la biblioteca está compuesta de varios ensamblados que no son útiles de forma independiente, es correcto combinarlos en un paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="ad930-122">Con el ejemplo anterior, si `Parser.dll` contiene código que se usa únicamente por `Utilities.dll`, es correcto mantener `Parser.dll` en el mismo paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="ad930-123">De forma similar, si `Utilities.dll` depende de `Utilities.resources.dll`, cuando este último no sea útil por sí solo, colóquelos en el mismo paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="ad930-124">De hecho, los recursos son un caso especial.</span><span class="sxs-lookup"><span data-stu-id="ad930-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="ad930-125">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados (vea [Creación de paquetes localizados](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="ad930-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="ad930-126">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="ad930-127">Si la biblioteca contiene ensamblados de interoperabilidad COM, siga las directrices adicionales descritas en [Creación de paquetes con ensamblados de interoperabilidad COM](author-packages-with-com-interop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="ad930-128">Rol y estructura del archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="ad930-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="ad930-129">Una vez que sepa qué archivos quiere empaquetar, el paso siguiente consiste en crear un manifiesto de paquete en un archivo `.nuspec` XML.</span><span class="sxs-lookup"><span data-stu-id="ad930-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="ad930-130">El manifiesto:</span><span class="sxs-lookup"><span data-stu-id="ad930-130">The manifest:</span></span>

1. <span data-ttu-id="ad930-131">Describe el contenido del paquete y se incluye en el paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="ad930-132">Controla la creación del paquete e indica a NuGet cómo instalar el paquete en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="ad930-133">Por ejemplo, el manifiesto identifica otras dependencias de paquete de forma que NuGet también pueda instalarlas cuando se instala el paquete principal.</span><span class="sxs-lookup"><span data-stu-id="ad930-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="ad930-134">Contiene propiedades obligatorias y opcionales como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="ad930-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="ad930-135">Para obtener los detalles exactos, incluidas otras propiedades que no se mencionan aquí, vea [Referencia de .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="ad930-136">Propiedades necesarias:</span><span class="sxs-lookup"><span data-stu-id="ad930-136">Required properties:</span></span>

- <span data-ttu-id="ad930-137">El identificador de paquete, que debe ser único en la galería que hospeda el paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="ad930-138">Un número de versión específico con el formato *Principal.Secundaria.Revisión[-Sufijo]* donde *-Sufijo* identifica las [versiones preliminares](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ad930-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="ad930-139">El título del paquete como debe aparecer en el host (por ejemplo, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="ad930-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="ad930-140">Información del autor y el propietario.</span><span class="sxs-lookup"><span data-stu-id="ad930-140">Author and owner information.</span></span>
- <span data-ttu-id="ad930-141">Una descripción extensa del paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-141">A long description of the package.</span></span>

<span data-ttu-id="ad930-142">Propiedades opcionales comunes:</span><span class="sxs-lookup"><span data-stu-id="ad930-142">Common optional properties:</span></span>

- <span data-ttu-id="ad930-143">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="ad930-143">Release notes</span></span>
- <span data-ttu-id="ad930-144">Información sobre copyright</span><span class="sxs-lookup"><span data-stu-id="ad930-144">Copyright information</span></span>
- <span data-ttu-id="ad930-145">Una descripción breve de la [interfaz de usuario del Administrador de paquetes en Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="ad930-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="ad930-146">Un Id. de configuración regional</span><span class="sxs-lookup"><span data-stu-id="ad930-146">A locale ID</span></span>
- <span data-ttu-id="ad930-147">URL de proyecto</span><span class="sxs-lookup"><span data-stu-id="ad930-147">Project URL</span></span>
- <span data-ttu-id="ad930-148">Licencia como expresión o archivo (`licenseUrl` está en desuso; use el [elemento de metadatos nuspec `license`](../reference/nuspec.md#license) en su lugar)</span><span class="sxs-lookup"><span data-stu-id="ad930-148">License as an expression or file (`licenseUrl` is deprecated, use [`license` nuspec metadata element](../reference/nuspec.md#license) instead)</span></span>
- <span data-ttu-id="ad930-149">Archivo de icono (`iconUrl` está en desuso; use el [elemento de metadatos nuspec `icon`](../reference/nuspec.md#icon) en su lugar)</span><span class="sxs-lookup"><span data-stu-id="ad930-149">An icon file (`iconUrl` is deprecated use [`icon` nuspec metadata element](../reference/nuspec.md#icon) instead)</span></span>
- <span data-ttu-id="ad930-150">Listas de dependencias y referencias</span><span class="sxs-lookup"><span data-stu-id="ad930-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="ad930-151">Etiquetas que ayudan en las búsquedas de galería</span><span class="sxs-lookup"><span data-stu-id="ad930-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="ad930-152">El siguiente archivo `.nuspec` es común (pero ficticio), con comentarios que describen las propiedades:</span><span class="sxs-lookup"><span data-stu-id="ad930-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- Package version number that is used when resolving dependencies -->
        <version>1.8.3</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- Icon is used in Visual Studio's package manager UI -->
        <icon>icon.png</icon>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
        <file src="icon.png" target="" />
    </files>
</package>
```

<span data-ttu-id="ad930-153">Para obtener más información sobre cómo declarar dependencias y especificar números de versión, consulte [packages.config](../reference/packages-config.md) y [Control de versiones de paquetes](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="ad930-154">También es posible exponer activos directamente desde las dependencias en el paquete mediante los atributos `include` y `exclude` del elemento `dependency`.</span><span class="sxs-lookup"><span data-stu-id="ad930-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="ad930-155">Vea [Referencia de .nuspec: dependencias](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="ad930-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="ad930-156">Dado que el manifiesto se incluye en el paquete creado a partir de él, puede buscar cualquier número de ejemplos adicionales mediante el examen de los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="ad930-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="ad930-157">Una buena fuente es la carpeta *global-packages* en el equipo, cuya ubicación se devuelve mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="ad930-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="ad930-158">Vaya a cualquier carpeta *paquete\versión*, copie el archivo `.nupkg` a un archivo `.zip`, después abra ese archivo `.zip` y examine `.nuspec` en su interior.</span><span class="sxs-lookup"><span data-stu-id="ad930-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="ad930-159">Al crear un archivo `.nuspec` desde un proyecto de Visual Studio, el manifiesto contiene tokens que se reemplazan con información del proyecto cuando se compila el paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="ad930-160">Vea [Creación del archivo .nuspec desde un proyecto de Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="ad930-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="ad930-161">Creación del archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="ad930-161">Create the .nuspec file</span></span>

<span data-ttu-id="ad930-162">La creación de un manifiesto completo normalmente comienza con un archivo `.nuspec` básico generado a través de uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad930-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="ad930-163">Un directorio de trabajo basado en convenciones</span><span class="sxs-lookup"><span data-stu-id="ad930-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="ad930-164">Un archivo DLL de ensamblado</span><span class="sxs-lookup"><span data-stu-id="ad930-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="ad930-165">Un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ad930-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="ad930-166">Archivo nuevo con valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="ad930-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="ad930-167">Después, se edita el archivo manualmente para que describa el contenido exacto que quiere en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="ad930-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="ad930-168">Los archivos `.nuspec` generados contienen marcadores de posición que se deben modificar antes de crear el paquete con el comando `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="ad930-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="ad930-169">Si `.nuspec` contiene marcadores de posición, se produce un error en el comando.</span><span class="sxs-lookup"><span data-stu-id="ad930-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="ad930-170">Desde un directorio de trabajo basado en convenciones</span><span class="sxs-lookup"><span data-stu-id="ad930-170">From a convention-based working directory</span></span>

<span data-ttu-id="ad930-171">Dado que un paquete NuGet es simplemente un archivo ZIP que se ha cambiado de nombre con la extensión `.nupkg`, a menudo es más fácil crear la estructura de carpetas que quiere en el sistema de archivos local y, después, crear el archivo `.nuspec` directamente desde esa estructura.</span><span class="sxs-lookup"><span data-stu-id="ad930-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="ad930-172">Después, el comando `nuget pack` agrega automáticamente todos los archivos de esa estructura de carpetas (sin incluir las carpetas que comienzan por `.`, lo que permite mantener archivos privados en la misma estructura).</span><span class="sxs-lookup"><span data-stu-id="ad930-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="ad930-173">La ventaja de este enfoque es que no es necesario especificar en el manifiesto qué archivos se van a incluir en el paquete (como se explica más adelante en este tema).</span><span class="sxs-lookup"><span data-stu-id="ad930-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="ad930-174">Puede hacer que el proceso de compilación genere simplemente la estructura de carpetas exacta que se agrega al paquete e incluir otros archivos que en otros casos es posible que no formen parte de un proyecto:</span><span class="sxs-lookup"><span data-stu-id="ad930-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="ad930-175">Contenido y código fuente que debe insertarse en el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="ad930-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="ad930-176">Scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad930-176">PowerShell scripts</span></span>
- <span data-ttu-id="ad930-177">Transformaciones de archivos de código existentes de configuración y código fuente en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="ad930-178">Las convenciones de carpeta son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad930-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="ad930-179">Carpeta</span><span class="sxs-lookup"><span data-stu-id="ad930-179">Folder</span></span> | <span data-ttu-id="ad930-180">Descripción</span><span class="sxs-lookup"><span data-stu-id="ad930-180">Description</span></span> | <span data-ttu-id="ad930-181">Acción tras la instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="ad930-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad930-182">(raíz)</span><span class="sxs-lookup"><span data-stu-id="ad930-182">(root)</span></span> | <span data-ttu-id="ad930-183">Ubicación de Léame.txt</span><span class="sxs-lookup"><span data-stu-id="ad930-183">Location for readme.txt</span></span> | <span data-ttu-id="ad930-184">Visual Studio muestra un archivo Léame.txt en la raíz del paquete cuando se instala el paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="ad930-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="ad930-185">lib/{tfm}</span></span> | <span data-ttu-id="ad930-186">Archivos de ensamblado (`.dll`), documentación (`.xml`) y símbolos (`.pdb`) para el Moniker de plataforma de destino (TFM) indicado</span><span class="sxs-lookup"><span data-stu-id="ad930-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="ad930-187">Los ensamblados se agregan como referencias para la compilación, así como el tiempo de ejecución; `.xml` y `.pdb` se copian en carpetas de proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="ad930-188">Vea [Compatibilidad con varias plataformas de destino](supporting-multiple-target-frameworks.md) para obtener información sobre cómo crear subcarpetas específicas de la plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="ad930-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="ad930-189">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="ad930-189">ref/{tfm}</span></span> | <span data-ttu-id="ad930-190">Archivos de ensamblado (`.dll`) y símbolos (`.pdb`) para el Moniker de la plataforma de destino (TFM) indicado</span><span class="sxs-lookup"><span data-stu-id="ad930-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="ad930-191">Los ensamblados se agregan como referencias solo durante el tiempo de compilación; así pues, nada se copiará en la carpeta bin del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="ad930-192">runtimes</span><span class="sxs-lookup"><span data-stu-id="ad930-192">runtimes</span></span> | <span data-ttu-id="ad930-193">Archivo de ensamblado (`.dll`), símbolos (`.pdb`) y recursos nativos (`.pri`) específicos de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="ad930-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="ad930-194">Los ensamblados se agregan como referencias solo durante el tiempo de ejecución; los demás archivos se copian en carpetas de proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="ad930-195">Siempre debe haber un ensamblado específico de `AnyCPU` (TFM) correspondiente en la carpeta `/ref/{tfm}` para proporcionar el ensamblado de tiempo de compilación correspondiente.</span><span class="sxs-lookup"><span data-stu-id="ad930-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="ad930-196">Vea [Compatibilidad con varias plataformas de destino](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="ad930-197">contenido</span><span class="sxs-lookup"><span data-stu-id="ad930-197">content</span></span> | <span data-ttu-id="ad930-198">Archivos arbitrarios</span><span class="sxs-lookup"><span data-stu-id="ad930-198">Arbitrary files</span></span> | <span data-ttu-id="ad930-199">El contenido se copia en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-199">Contents are copied to the project root.</span></span> <span data-ttu-id="ad930-200">Piense en la carpeta **content** como la raíz de la aplicación de destino que consume el paquete en última instancia.</span><span class="sxs-lookup"><span data-stu-id="ad930-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="ad930-201">Para que el paquete agregue una imagen en la carpeta */images* de la aplicación, colóquelo en la carpeta *content/images* del paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="ad930-202">compilación</span><span class="sxs-lookup"><span data-stu-id="ad930-202">build</span></span> | <span data-ttu-id="ad930-203">*(3.x+)* Archivos `.targets` y `.props` de MSBuild</span><span class="sxs-lookup"><span data-stu-id="ad930-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="ad930-204">Se insertan automáticamente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="ad930-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="ad930-205">buildMultiTargeting</span></span> | <span data-ttu-id="ad930-206">*(4.0+)* Archivos `.targets` y `.props` de MSBuild de los destinos multiplataforma</span><span class="sxs-lookup"><span data-stu-id="ad930-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="ad930-207">Se insertan automáticamente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="ad930-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="ad930-208">buildTransitive</span></span> | <span data-ttu-id="ad930-209">*(5.0 +)*  Los archivos `.targets` y `.props` de MSBuild que fluyen de manera transitiva a cualquier proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="ad930-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="ad930-210">Vea la página de la [característica](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="ad930-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="ad930-211">Se insertan automáticamente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="ad930-212">tools</span><span class="sxs-lookup"><span data-stu-id="ad930-212">tools</span></span> | <span data-ttu-id="ad930-213">Scripts de PowerShell y programas accesibles desde la consola del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="ad930-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="ad930-214">La carpeta `tools` se agrega a la variable de entorno `PATH` solo para la consola del Administrador de paquetes (en concreto, *no* a `PATH` como se establece para MSBuild al compilar el proyecto).</span><span class="sxs-lookup"><span data-stu-id="ad930-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="ad930-215">Dado que la estructura de carpetas puede contener cualquier número de ensamblados para cualquier número de plataformas de destino, este método es necesario al crear paquetes que admiten varias plataformas.</span><span class="sxs-lookup"><span data-stu-id="ad930-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="ad930-216">En cualquier caso, una vez que tenga la estructura de carpetas deseada, ejecute el comando siguiente en esa carpeta para crear el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="ad930-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="ad930-217">Una vez más, el archivo `.nuspec` generado no contiene ninguna referencia explícita a los archivos de la estructura de carpetas.</span><span class="sxs-lookup"><span data-stu-id="ad930-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="ad930-218">NuGet incluye de manera automática todos los archivos cuando se crea el paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="ad930-219">Pero necesitará modificar los valores de marcador de posición en otras partes del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="ad930-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="ad930-220">Desde un archivo DLL de ensamblado</span><span class="sxs-lookup"><span data-stu-id="ad930-220">From an assembly DLL</span></span>

<span data-ttu-id="ad930-221">En el simple caso de creación de un paquete desde un ensamblado, puede generar un archivo `.nuspec` a partir de los metadatos del ensamblado con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="ad930-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="ad930-222">El uso de este formato reemplaza algunos marcadores de posición en el manifiesto con valores específicos del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="ad930-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="ad930-223">Por ejemplo, la propiedad `<id>` se establece en el nombre del ensamblado y `<version>` se establece en la versión del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="ad930-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="ad930-224">Pero otras propiedades del manifiesto no tienen valores coincidentes en el ensamblado y, por tanto, aún contienen marcadores de posición.</span><span class="sxs-lookup"><span data-stu-id="ad930-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="ad930-225">Desde un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ad930-225">From a Visual Studio project</span></span>

<span data-ttu-id="ad930-226">La creación de un archivo `.nuspec` desde un archivo `.csproj` o `.vbproj` resulta práctica porque, de manera automática, se hace referencia como dependencias a otros paquetes que se han instalado en los proyectos.</span><span class="sxs-lookup"><span data-stu-id="ad930-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="ad930-227">Simplemente use el comando siguiente en la misma carpeta que el archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="ad930-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="ad930-228">El archivo `<project-name>.nuspec` resultante contiene *tokens* que se reemplazan durante el empaquetado con valores del proyecto, incluidas las referencias a todos los demás paquetes que ya se han instalado.</span><span class="sxs-lookup"><span data-stu-id="ad930-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="ad930-229">Si tiene dependencias de paquete que se van a incluir en el archivo *.nuspec*, use en su lugar `nuget pack` y obtenga el archivo *.nuspec* en el archivo *.nupkg* generado.</span><span class="sxs-lookup"><span data-stu-id="ad930-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="ad930-230">Por ejemplo, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ad930-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="ad930-231">Un token está delimitado por símbolos `$` en ambos lados de la propiedad del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="ad930-232">Por ejemplo, el valor `<id>` en un manifiesto generado de este modo normalmente tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="ad930-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="ad930-233">Este token se reemplaza por el valor `AssemblyName` del archivo de proyecto en tiempo de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="ad930-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="ad930-234">Para obtener la asignación exacta de valores de proyecto a tokens `.nuspec`, vea la [Referencia de tokens de reemplazo](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="ad930-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="ad930-235">Los tokens le liberan de la necesidad de actualizar valores esenciales como el número de versión en el archivo `.nuspec` cuando se actualiza el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="ad930-236">(Siempre puede reemplazar los tokens con valores literales, si quiere).</span><span class="sxs-lookup"><span data-stu-id="ad930-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="ad930-237">Tenga en cuenta que hay varias opciones de empaquetado adicionales disponibles cuando se trabaja desde un proyecto de Visual Studio, como se describe en [Ejecución del paquete nuget para generar el archivo .nupkg](#run-nuget-pack-to-generate-the-nupkg-file) más adelante.</span><span class="sxs-lookup"><span data-stu-id="ad930-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="ad930-238">Paquetes de nivel de solución</span><span class="sxs-lookup"><span data-stu-id="ad930-238">Solution-level packages</span></span>

<span data-ttu-id="ad930-239">*Solo para NuGet 2.x. No disponible en NuGet 3.0 y versiones posteriores.*</span><span class="sxs-lookup"><span data-stu-id="ad930-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="ad930-240">En NuGet 2.x se admite la noción de paquete de nivel de solución que instala herramientas o comandos adicionales para la consola del Administrador de paquetes (el contenido de la carpeta `tools`), pero no agrega referencias, contenido o personalizaciones de compilación a ninguno de los proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="ad930-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="ad930-241">Estos paquetes no contienen ningún archivo en su carpetas `lib`, `content` o `build` directas, y ninguna de sus dependencias tienen archivos en sus respectivas carpetas `lib`, `content` o `build`.</span><span class="sxs-lookup"><span data-stu-id="ad930-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="ad930-242">NuGet realiza el seguimiento de los paquetes de nivel de la solución instalados en un archivo `packages.config` en la carpeta `.nuget`, en lugar del archivo `packages.config` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="ad930-243">Archivo nuevo con valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="ad930-243">New file with default values</span></span>

<span data-ttu-id="ad930-244">El comando siguiente crea un manifiesto predeterminado con marcadores de posición, lo que garantiza que comience con la estructura de archivos adecuada:</span><span class="sxs-lookup"><span data-stu-id="ad930-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="ad930-245">Si se omite \<package-name\>, el archivo resultante es `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ad930-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="ad930-246">Si proporciona un nombre como `Contoso.Utility.UsefulStuff`, el archivo es `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ad930-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="ad930-247">El archivo `.nuspec` resultante contiene marcadores de posición para valores como `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="ad930-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="ad930-248">Asegúrese de modificar el archivo antes de usarlo para crear el archivo `.nupkg` definitivo.</span><span class="sxs-lookup"><span data-stu-id="ad930-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="ad930-249">Elección de un identificador de paquete único y establecimiento del número de versión</span><span class="sxs-lookup"><span data-stu-id="ad930-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="ad930-250">El identificador del paquete (el elemento `<id>`) y el número de versión (el elemento `<version>`) son los dos valores más importantes del manifiesto ya que identifican de forma única el código exacto que se incluye en el paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="ad930-251">**Procedimientos recomendados para el identificador del paquete:**</span><span class="sxs-lookup"><span data-stu-id="ad930-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="ad930-252">**Unicidad**: el identificador debe ser único en nuget.org o en la galería que hospede el paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="ad930-253">Antes de decidirse por un identificador, busque en la galería aplicable para comprobar si el nombre ya está en uso.</span><span class="sxs-lookup"><span data-stu-id="ad930-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="ad930-254">Para evitar conflictos, un buen patrón consiste en usar el nombre de la empresa como la primera parte del identificador, por ejemplo `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="ad930-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="ad930-255">**Nombres de tipo espacio de nombres**: siguen un patrón similar a los espacios de nombres de .NET, con notación de puntos en lugar de guiones.</span><span class="sxs-lookup"><span data-stu-id="ad930-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="ad930-256">Por ejemplo, use `Contoso.Utility.UsefulStuff` en lugar de `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="ad930-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="ad930-257">También es útil para los consumidores cuando el identificador del paquete coincide con los espacios de nombres que se usan en el código.</span><span class="sxs-lookup"><span data-stu-id="ad930-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="ad930-258">**Paquetes de ejemplo**: si genera un paquete de código de ejemplo que muestra cómo usar otro paquete, adjunte `.Sample` como sufijo al identificador, como en `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="ad930-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="ad930-259">(El paquete de ejemplo tendría evidentemente una dependencia en el otro paquete). Al crear un paquete de ejemplo, use el método de directorio de trabajo basado en convenciones descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ad930-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="ad930-260">En la carpeta `content`, organice el código de ejemplo en una carpeta denominada `\Samples\<identifier>` como en `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="ad930-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="ad930-261">**Procedimientos recomendados para la versión del paquete:**</span><span class="sxs-lookup"><span data-stu-id="ad930-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="ad930-262">En general, establezca la versión del paquete para que coincida con la biblioteca, aunque esto no es estrictamente necesario.</span><span class="sxs-lookup"><span data-stu-id="ad930-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="ad930-263">Esto es sencillo cuando se limita un paquete a un único ensamblado, como se describió anteriormente en [Decidir qué ensamblados empaquetar](#decide-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="ad930-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="ad930-264">En general, recuerde que el propio NuGet trabaja con versiones del paquete al resolver las dependencias, no con versiones de ensamblado.</span><span class="sxs-lookup"><span data-stu-id="ad930-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="ad930-265">Cuando se usa un esquema de la versión no estándar, asegúrese de tener en cuenta las reglas de control de versiones de NuGet, como se explica en [Control de versiones de paquetes](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="ad930-266">La siguiente serie de entradas de blog breves también es útil para entender el control de versiones:</span><span class="sxs-lookup"><span data-stu-id="ad930-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - <span data-ttu-id="ad930-267">[Parte 1: Taking on DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Enfrentarse al infierno de los archivos DLL)</span><span class="sxs-lookup"><span data-stu-id="ad930-267">[Part 1: Taking on DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="ad930-268">[Parte 2: The core algorithm](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: El algoritmo básico)</span><span class="sxs-lookup"><span data-stu-id="ad930-268">[Part 2: The core algorithm](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="ad930-269">[Part 3: Unification via Binding Redirects](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificación mediante redirecciones de enlaces)</span><span class="sxs-lookup"><span data-stu-id="ad930-269">[Part 3: Unification via Binding Redirects](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="ad930-270">Adición de un archivo Léame y otros archivos</span><span class="sxs-lookup"><span data-stu-id="ad930-270">Add a readme and other files</span></span>

<span data-ttu-id="ad930-271">Para especificar directamente los archivos que se van a incluir en el paquete, use el nodo `<files>` en el archivo `.nuspec`, que *sigue* a la etiqueta `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="ad930-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="ad930-272">Cuando se usa el enfoque de directorio de trabajo basado en convenciones, puede colocar el archivo Léame.txt en la raíz del paquete y otro contenido en la carpeta `content`.</span><span class="sxs-lookup"><span data-stu-id="ad930-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="ad930-273">En el manifiesto no se necesitan elementos `<file>`.</span><span class="sxs-lookup"><span data-stu-id="ad930-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="ad930-274">Al incluir un archivo denominado `readme.txt` en la raíz del paquete, Visual Studio muestra el contenido de ese archivo como texto sin formato inmediatamente después de instalar el paquete directamente.</span><span class="sxs-lookup"><span data-stu-id="ad930-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="ad930-275">(Los archivos Léame no se muestran para paquetes instalados como dependencias).</span><span class="sxs-lookup"><span data-stu-id="ad930-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="ad930-276">Por ejemplo, este es el aspecto del archivo Léame para el paquete HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="ad930-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![La presentación de un archivo Léame para un paquete NuGet tras la instalación](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="ad930-278">Si incluye un nodo `<files>` vacío en el archivo `.nuspec`, NuGet no incluye ningún otro contenido en el paquete que no sea el que aparece en la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="ad930-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="ad930-279">Inclusión de propiedades y destinos de MSBuild en un paquete</span><span class="sxs-lookup"><span data-stu-id="ad930-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="ad930-280">En algunos casos, es posible que quiera agregar destinos de compilación personalizados o propiedades en proyectos en los que se consume el paquete, como la ejecución de una herramienta o un proceso personalizado durante la compilación.</span><span class="sxs-lookup"><span data-stu-id="ad930-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="ad930-281">Para ello, coloque los archivos en el formato `<package_id>.targets` o `<package_id>.props` (por ejemplo `Contoso.Utility.UsefulStuff.targets`) dentro de la carpeta `\build` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="ad930-282">Los archivos en la carpeta `\build` raíz se consideran adecuados para todas las plataformas de destino.</span><span class="sxs-lookup"><span data-stu-id="ad930-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="ad930-283">Para proporcionar archivos específicos de la plataforma, colóquelos primero en las subcarpetas adecuadas, como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad930-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

```
    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
```

<span data-ttu-id="ad930-284">Después, en el archivo `.nuspec`, asegúrese de hacer referencia a estos archivos en el nodo `<files>`:</span><span class="sxs-lookup"><span data-stu-id="ad930-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="ad930-285">Con [NuGet 2.5 se introdujo](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files) la inclusión de propiedades y destinos de MSBuild en un paquete. Por tanto, se recomienda agregar el atributo `minClientVersion="2.5"` al elemento `metadata` para indicar la versión de cliente de NuGet mínima necesaria para usar el paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="ad930-286">Cuando NuGet instala un paquete con archivos `\build`, agrega elementos `<Import>` de MSBuild al archivo de proyecto que apunta a los archivos `.targets` y `.props`.</span><span class="sxs-lookup"><span data-stu-id="ad930-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="ad930-287">(`.props` se agrega en la parte superior del archivo del proyecto; `.targets` se agrega al final). Se agrega un elemento condicional `<Import>` de MSBuild independiente para cada plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="ad930-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="ad930-288">Los archivos `.props` y `.targets` de MSBuild de los destinos multiplataforma pueden colocarse en la carpeta `\buildMultiTargeting`.</span><span class="sxs-lookup"><span data-stu-id="ad930-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="ad930-289">Durante la instalación de paquetes, NuGet agrega los elementos `<Import>` correspondientes al archivo de proyecto, con la condición de que no se establezca la plataforma de destino (la propiedad `$(TargetFramework)` de MSBuild debe estar vacía).</span><span class="sxs-lookup"><span data-stu-id="ad930-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="ad930-290">Con NuGet 3.x, los destinos no se agregan al proyecto pero en su lugar se ponen a disposición a través de `{projectName}.nuget.g.targets` y `{projectName}.nuget.g.props`.</span><span class="sxs-lookup"><span data-stu-id="ad930-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="ad930-291">Ejecución del paquete nuget para generar el archivo .nupkg</span><span class="sxs-lookup"><span data-stu-id="ad930-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="ad930-292">Cuando se usa un ensamblado o el directorio de trabajo basado en convenciones, cree un paquete mediante la ejecución de `nuget pack` con el archivo `.nuspec`, reemplazando `<project-name>` con el nombre de archivo específico:</span><span class="sxs-lookup"><span data-stu-id="ad930-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="ad930-293">Cuando se usa un proyecto de Visual Studio, ejecute `nuget pack` con el archivo de proyecto, que carga automáticamente el archivo `.nuspec` del proyecto y reemplaza los tokens que contiene mediante valores del archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="ad930-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="ad930-294">Es necesario usar el archivo de proyecto directamente para el reemplazo de tokens porque el proyecto es el origen de los valores de token.</span><span class="sxs-lookup"><span data-stu-id="ad930-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="ad930-295">El reemplazo de tokens no se realiza si se usa `nuget pack` con un archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ad930-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="ad930-296">En todos los casos, `nuget pack` excluye las carpetas que comienzan con un punto, como `.git` o `.hg`.</span><span class="sxs-lookup"><span data-stu-id="ad930-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="ad930-297">NuGet indica si hay errores en el archivo `.nuspec` que se deben corregir, como olvidar cambiar valores de marcador de posición en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="ad930-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="ad930-298">Una vez que `nuget pack` es correcto, tendrá un archivo `.nupkg` que se puede publicar en una galería adecuada como se describe en [Publicación de un paquete](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="ad930-299">Una manera útil de examinar un paquete después de crearlo consiste en abrirlo en la herramienta [Explorador de paquetes](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="ad930-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="ad930-300">Esto ofrece una vista gráfica del contenido del paquete y el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="ad930-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="ad930-301">También puede cambiar el nombre del archivo `.nupkg` resultante a un archivo `.zip` y explorar directamente su contenido.</span><span class="sxs-lookup"><span data-stu-id="ad930-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="ad930-302">Opciones adicionales</span><span class="sxs-lookup"><span data-stu-id="ad930-302">Additional options</span></span>

<span data-ttu-id="ad930-303">Puede usar diversos modificadores de línea de comandos con `nuget pack` para excluir archivos, reemplazar el número de versión en el manifiesto y cambiar la carpeta de salida, entre otras características.</span><span class="sxs-lookup"><span data-stu-id="ad930-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="ad930-304">Para obtener una lista completa, consulte la [referencia del comando pack](../reference/cli-reference/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="ad930-305">Las opciones siguientes son algunas comunes en proyectos de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ad930-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="ad930-306">**Proyectos a los que se hace referencia**: si el proyecto hace referencia a otros proyectos, puede agregar los proyectos a los que se hace referencia como parte del paquete, o bien como dependencias, mediante la opción `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="ad930-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="ad930-307">Este proceso de inclusión es recursivo, por lo que si `MyProject.csproj` hace referencia a los proyectos B y C, y esos proyectos hacen referencia a D, E y F, los archivos de B, C, D, E y F se incluyen en el paquete.</span><span class="sxs-lookup"><span data-stu-id="ad930-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="ad930-308">Si un proyecto al que se hace referencia incluye un archivo `.nuspec` propio, en su lugar NuGet agrega ese proyecto al que se hace referencia como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="ad930-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="ad930-309">Debe empaquetar y publicar ese proyecto por separado.</span><span class="sxs-lookup"><span data-stu-id="ad930-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="ad930-310">**Configuración de compilación**: de forma predeterminada, NuGet usa la configuración de compilación predeterminada establecida en el archivo de proyecto, normalmente *Debug*.</span><span class="sxs-lookup"><span data-stu-id="ad930-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="ad930-311">Para empaquetar archivos de una configuración de compilación diferente, como *Release*, use la opción `-properties` con la configuración:</span><span class="sxs-lookup"><span data-stu-id="ad930-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="ad930-312">**Símbolos**: para incluir símbolos que permitan a los consumidores recorrer el código del paquete en el depurador, use la opción `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="ad930-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="ad930-313">Prueba de instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="ad930-313">Test package installation</span></span>

<span data-ttu-id="ad930-314">Antes de publicar un paquete, normalmente querrá probar el proceso de instalación de un paquete en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="ad930-315">Las pruebas aseguran que los archivos necesarios acaban en los lugares correctos en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad930-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="ad930-316">Puede probar las instalaciones de forma manual en Visual Studio o en la línea de comandos mediante los [pasos de instalación de paquetes](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normales.</span><span class="sxs-lookup"><span data-stu-id="ad930-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="ad930-317">Para las pruebas automatizadas, el proceso básico es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="ad930-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="ad930-318">Copie el archivo `.nupkg` en una carpeta local.</span><span class="sxs-lookup"><span data-stu-id="ad930-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="ad930-319">Agregue la carpeta a los orígenes de paquete mediante el comando `nuget sources add -name <name> -source <path>` (vea [Orígenes de nuget](../reference/cli-reference/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="ad930-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="ad930-320">Tenga en cuenta que solo es necesario establecer este origen local una vez en un equipo determinado.</span><span class="sxs-lookup"><span data-stu-id="ad930-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="ad930-321">Instale el paquete desde ese origen mediante `nuget install <packageID> -source <name>`, donde `<name>` coincide con el nombre del origen tal como se indicó a `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="ad930-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="ad930-322">Especificar el origen asegura que el paquete se instala únicamente desde ese origen.</span><span class="sxs-lookup"><span data-stu-id="ad930-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="ad930-323">Examine el sistema de archivos para comprobar que los archivos se instalan correctamente.</span><span class="sxs-lookup"><span data-stu-id="ad930-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad930-324">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad930-324">Next Steps</span></span>

<span data-ttu-id="ad930-325">Una vez haya creado un paquete, que es un archivo `.nupkg`, puede publicarlo en la galería de su elección como se describe en [Publicación de un paquete](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ad930-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="ad930-326">Es posible que también quiera ampliar las funcionalidades del paquete o admitir otros escenarios, como se describe en los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad930-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="ad930-327">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="ad930-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="ad930-328">Compatibilidad con varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="ad930-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ad930-329">Transformaciones de archivos de origen y configuración</span><span class="sxs-lookup"><span data-stu-id="ad930-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="ad930-330">Localización</span><span class="sxs-lookup"><span data-stu-id="ad930-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ad930-331">Versiones preliminares</span><span class="sxs-lookup"><span data-stu-id="ad930-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="ad930-332">Definición del tipo de paquete</span><span class="sxs-lookup"><span data-stu-id="ad930-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="ad930-333">Creación de paquetes con ensamblados de interoperabilidad COM</span><span class="sxs-lookup"><span data-stu-id="ad930-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="ad930-334">Por último, hay tipos de paquete adicionales que tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="ad930-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="ad930-335">Paquetes nativos</span><span class="sxs-lookup"><span data-stu-id="ad930-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="ad930-336">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="ad930-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
