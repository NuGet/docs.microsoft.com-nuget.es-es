---
title: Cómo crear un paquete NuGet
description: Un guía detallada sobre el proceso de diseño y creación de un paquete NuGet, incluidos puntos de decisión clave como archivos y control de versiones.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: db02089bec3d2b8c001518fa0542375dc5418eb8
ms.sourcegitcommit: c825eb7e222d4a551431643f5b5617ae868ebe0a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/19/2018
ms.locfileid: "51944072"
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="df90f-103">Creación de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="df90f-103">Creating NuGet packages</span></span>

<span data-ttu-id="df90f-104">Con independencia de lo que haga el paquete o lo que contenga el código, use `nuget.exe` para empaquetar esa funcionalidad en un componente que se pueda compartir y usar por parte de otros desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="df90f-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="df90f-105">Para instalar `nuget.exe`, vea [Instalar la CLI de NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="df90f-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="df90f-106">Tenga en cuenta que Visual Studio no incluye `nuget.exe` de manera automática.</span><span class="sxs-lookup"><span data-stu-id="df90f-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="df90f-107">Desde un punto de vista técnico, un paquete NuGet es simplemente un archivo ZIP en el que se ha cambiado el nombre con la extensión `.nupkg` y cuyo contenido coincide con determinadas convenciones.</span><span class="sxs-lookup"><span data-stu-id="df90f-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="df90f-108">En este tema se describe el proceso detallado de creación de un paquete que cumple estas convenciones.</span><span class="sxs-lookup"><span data-stu-id="df90f-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="df90f-109">Para obtener un tutorial específico, consulte [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md) (Guía de inicio rápido: Crear y publicar un paquete).</span><span class="sxs-lookup"><span data-stu-id="df90f-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="df90f-110">El empaquetado comienza con el código compilado (ensamblados), símbolos y otros archivos que quiera entregar como un paquete (vea [Información general y flujo de trabajo](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="df90f-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="df90f-111">Este proceso es independiente de la compilación o, en otros casos, de la generación de los archivos que se incluyen en el paquete, aunque se puede extraer la información de un archivo de proyecto para mantener sincronizados los ensamblados y paquetes compilados.</span><span class="sxs-lookup"><span data-stu-id="df90f-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="df90f-112">Este tema se aplica a los tipos de proyecto que no son de .NET Core en los que se usa Visual Studio 2017 y NuGet 4.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="df90f-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="df90f-113">En los proyectos de .NET Core, NuGet usa directamente la información del archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="df90f-114">Para obtener más información, vea [Crear paquetes de .NET Standard con Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) y [pack y restore de NuGet como destinos de MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="df90f-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="df90f-115">Decidir qué ensamblados empaquetar</span><span class="sxs-lookup"><span data-stu-id="df90f-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="df90f-116">La mayoría de paquetes de propósito generales contiene uno o más ensamblados que otros desarrolladores pueden usar en sus propios proyectos.</span><span class="sxs-lookup"><span data-stu-id="df90f-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="df90f-117">En general, es preferible disponer de un ensamblado por cada paquete NuGet, siempre que cada ensamblado sea útil por separado.</span><span class="sxs-lookup"><span data-stu-id="df90f-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="df90f-118">Por ejemplo, si tiene un archivo `Utilities.dll` que depende de `Parser.dll` y `Parser.dll` es útil por sí solo, entonces cree un paquete para cada uno.</span><span class="sxs-lookup"><span data-stu-id="df90f-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="df90f-119">Esto permite a los desarrolladores usar `Parser.dll` independientemente de `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="df90f-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="df90f-120">Si la biblioteca está compuesta de varios ensamblados que no son útiles de forma independiente, es correcto combinarlos en un paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="df90f-121">Con el ejemplo anterior, si `Parser.dll` contiene código que se usa únicamente por `Utilities.dll`, es correcto mantener `Parser.dll` en el mismo paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="df90f-122">De forma similar, si `Utilities.dll` depende de `Utilities.resources.dll`, cuando este último no sea útil por sí solo, colóquelos en el mismo paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="df90f-123">De hecho, los recursos son un caso especial.</span><span class="sxs-lookup"><span data-stu-id="df90f-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="df90f-124">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados (vea [Creación de paquetes localizados](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="df90f-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="df90f-125">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="df90f-126">Si la biblioteca contiene ensamblados de interoperabilidad COM, siga las directrices adicionales descritas en [Creación de paquetes con ensamblados de interoperabilidad COM](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="df90f-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="df90f-127">Rol y estructura del archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="df90f-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="df90f-128">Una vez que sepa qué archivos quiere empaquetar, el paso siguiente consiste en crear un manifiesto de paquete en un archivo `.nuspec` XML.</span><span class="sxs-lookup"><span data-stu-id="df90f-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="df90f-129">El manifiesto:</span><span class="sxs-lookup"><span data-stu-id="df90f-129">The manifest:</span></span>

1. <span data-ttu-id="df90f-130">Describe el contenido del paquete y se incluye en el paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="df90f-131">Controla la creación del paquete e indica a NuGet cómo instalar el paquete en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="df90f-132">Por ejemplo, el manifiesto identifica otras dependencias de paquete de forma que NuGet también pueda instalarlas cuando se instala el paquete principal.</span><span class="sxs-lookup"><span data-stu-id="df90f-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="df90f-133">Contiene propiedades obligatorias y opcionales como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="df90f-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="df90f-134">Para obtener los detalles exactos, incluidas otras propiedades que no se mencionan aquí, vea [Referencia de .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="df90f-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="df90f-135">Propiedades necesarias:</span><span class="sxs-lookup"><span data-stu-id="df90f-135">Required properties:</span></span>

- <span data-ttu-id="df90f-136">El identificador de paquete, que debe ser único en la galería que hospeda el paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="df90f-137">Un número de versión específico con el formato *Principal.Secundaria.Revisión[-Sufijo]* donde *-Sufijo* identifica las [versiones preliminares](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="df90f-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="df90f-138">El título del paquete como debe aparecer en el host (por ejemplo, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="df90f-138">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="df90f-139">Información del autor y el propietario.</span><span class="sxs-lookup"><span data-stu-id="df90f-139">Author and owner information.</span></span>
- <span data-ttu-id="df90f-140">Una descripción extensa del paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-140">A long description of the package.</span></span>

<span data-ttu-id="df90f-141">Propiedades opcionales comunes:</span><span class="sxs-lookup"><span data-stu-id="df90f-141">Common optional properties:</span></span>

- <span data-ttu-id="df90f-142">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="df90f-142">Release notes</span></span>
- <span data-ttu-id="df90f-143">Información sobre copyright</span><span class="sxs-lookup"><span data-stu-id="df90f-143">Copyright information</span></span>
- <span data-ttu-id="df90f-144">Una descripción breve de la [interfaz de usuario del Administrador de paquetes en Visual Studio](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="df90f-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="df90f-145">Un Id. de configuración regional</span><span class="sxs-lookup"><span data-stu-id="df90f-145">A locale ID</span></span>
- <span data-ttu-id="df90f-146">URL de proyecto</span><span class="sxs-lookup"><span data-stu-id="df90f-146">Project URL</span></span>
- <span data-ttu-id="df90f-147">Licencia como expresión o archivo (`licenseUrl` está en desuso; [emplee el elemento de metadatos nuspec `license`](../reference/nuspec.md#license))</span><span class="sxs-lookup"><span data-stu-id="df90f-147">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="df90f-148">Dirección URL del icono</span><span class="sxs-lookup"><span data-stu-id="df90f-148">An icon URL</span></span>
- <span data-ttu-id="df90f-149">Listas de dependencias y referencias</span><span class="sxs-lookup"><span data-stu-id="df90f-149">Lists of dependencies and references</span></span>
- <span data-ttu-id="df90f-150">Etiquetas que ayudan en las búsquedas de galería</span><span class="sxs-lookup"><span data-stu-id="df90f-150">Tags that assist in gallery searches</span></span>

<span data-ttu-id="df90f-151">El siguiente archivo `.nuspec` es común (pero ficticio), con comentarios que describen las propiedades:</span><span class="sxs-lookup"><span data-stu-id="df90f-151">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

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
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

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
    </files>
</package>
```

<span data-ttu-id="df90f-152">Para obtener más información sobre cómo declarar dependencias y especificar números de versión, vea [Control de versiones de paquetes](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="df90f-152">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="df90f-153">También es posible exponer activos directamente desde las dependencias en el paquete mediante los atributos `include` y `exclude` del elemento `dependency`.</span><span class="sxs-lookup"><span data-stu-id="df90f-153">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="df90f-154">Vea [Referencia de .nuspec: dependencias](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="df90f-154">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="df90f-155">Dado que el manifiesto se incluye en el paquete creado a partir de él, puede buscar cualquier número de ejemplos adicionales mediante el examen de los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="df90f-155">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="df90f-156">Una buena fuente es la carpeta *global-packages* en el equipo, cuya ubicación se devuelve mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="df90f-156">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="df90f-157">Vaya a cualquier carpeta *paquete\versión*, copie el archivo `.nupkg` a un archivo `.zip`, después abra ese archivo `.zip` y examine `.nuspec` en su interior.</span><span class="sxs-lookup"><span data-stu-id="df90f-157">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="df90f-158">Al crear un archivo `.nuspec` desde un proyecto de Visual Studio, el manifiesto contiene tokens que se reemplazan con información del proyecto cuando se compila el paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-158">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="df90f-159">Vea [Creación del archivo .nuspec desde un proyecto de Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="df90f-159">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="df90f-160">Creación del archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="df90f-160">Creating the .nuspec file</span></span>

<span data-ttu-id="df90f-161">La creación de un manifiesto completo normalmente comienza con un archivo `.nuspec` básico generado a través de uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="df90f-161">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="df90f-162">Un directorio de trabajo basado en convenciones</span><span class="sxs-lookup"><span data-stu-id="df90f-162">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="df90f-163">Un archivo DLL de ensamblado</span><span class="sxs-lookup"><span data-stu-id="df90f-163">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="df90f-164">Un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="df90f-164">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="df90f-165">Archivo nuevo con valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="df90f-165">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="df90f-166">Después, se edita el archivo manualmente para que describa el contenido exacto que quiere en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="df90f-166">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="df90f-167">Los archivos `.nuspec` generados contienen marcadores de posición que se deben modificar antes de crear el paquete con el comando `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="df90f-167">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="df90f-168">Si `.nuspec` contiene marcadores de posición, se produce un error en el comando.</span><span class="sxs-lookup"><span data-stu-id="df90f-168">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="df90f-169">Desde un directorio de trabajo basado en convenciones</span><span class="sxs-lookup"><span data-stu-id="df90f-169">From a convention-based working directory</span></span>

<span data-ttu-id="df90f-170">Dado que un paquete NuGet es simplemente un archivo ZIP que se ha cambiado de nombre con la extensión `.nupkg`, a menudo es más fácil crear la estructura de carpetas que quiere en el sistema de archivos local y, después, crear el archivo `.nuspec` directamente desde esa estructura.</span><span class="sxs-lookup"><span data-stu-id="df90f-170">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="df90f-171">Después, el comando `nuget pack` agrega automáticamente todos los archivos de esa estructura de carpetas (sin incluir las carpetas que comienzan por `.`, lo que permite mantener archivos privados en la misma estructura).</span><span class="sxs-lookup"><span data-stu-id="df90f-171">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="df90f-172">La ventaja de este enfoque es que no es necesario especificar en el manifiesto qué archivos se van a incluir en el paquete (como se explica más adelante en este tema).</span><span class="sxs-lookup"><span data-stu-id="df90f-172">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="df90f-173">Puede hacer que el proceso de compilación genere simplemente la estructura de carpetas exacta que se agrega al paquete e incluir otros archivos que en otros casos es posible que no formen parte de un proyecto:</span><span class="sxs-lookup"><span data-stu-id="df90f-173">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="df90f-174">Contenido y código fuente que debe insertarse en el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="df90f-174">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="df90f-175">Scripts de PowerShell (los paquetes que se usan en NuGet 2.x también puede incluir scripts de instalación, que no se admiten en NuGet 3.x y versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="df90f-175">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="df90f-176">Transformaciones de archivos de código existentes de configuración y código fuente en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-176">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="df90f-177">Las convenciones de carpeta son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="df90f-177">The folder conventions are as follows:</span></span>

| <span data-ttu-id="df90f-178">Carpeta</span><span class="sxs-lookup"><span data-stu-id="df90f-178">Folder</span></span> | <span data-ttu-id="df90f-179">Descripción</span><span class="sxs-lookup"><span data-stu-id="df90f-179">Description</span></span> | <span data-ttu-id="df90f-180">Acción tras la instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="df90f-180">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df90f-181">(raíz)</span><span class="sxs-lookup"><span data-stu-id="df90f-181">(root)</span></span> | <span data-ttu-id="df90f-182">Ubicación de Léame.txt</span><span class="sxs-lookup"><span data-stu-id="df90f-182">Location for readme.txt</span></span> | <span data-ttu-id="df90f-183">Visual Studio muestra un archivo Léame.txt en la raíz del paquete cuando se instala el paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-183">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="df90f-184">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="df90f-184">lib/{tfm}</span></span> | <span data-ttu-id="df90f-185">Archivos de ensamblado (`.dll`), documentación (`.xml`) y símbolos (`.pdb`) para el Moniker de plataforma de destino (TFM) indicado</span><span class="sxs-lookup"><span data-stu-id="df90f-185">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="df90f-186">Los ensamblados se agregan como referencias para la compilación, así como el tiempo de ejecución; `.xml` y `.pdb` se copian en carpetas de proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-186">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="df90f-187">Vea [Compatibilidad con varias plataformas de destino](supporting-multiple-target-frameworks.md) para obtener información sobre cómo crear subcarpetas específicas de la plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="df90f-187">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="df90f-188">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="df90f-188">ref/{tfm}</span></span> | <span data-ttu-id="df90f-189">Archivos de ensamblado (`.dll`) y símbolos (`.pdb`) para el Moniker de la plataforma de destino (TFM) indicado</span><span class="sxs-lookup"><span data-stu-id="df90f-189">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="df90f-190">Los ensamblados se agregan como referencias solo durante el tiempo de compilación; así pues, nada se copiará en la carpeta bin del proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-190">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="df90f-191">runtimes</span><span class="sxs-lookup"><span data-stu-id="df90f-191">runtimes</span></span> | <span data-ttu-id="df90f-192">Archivo de ensamblado (`.dll`), símbolos (`.pdb`) y recursos nativos (`.pri`) específicos de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="df90f-192">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="df90f-193">Los ensamblados se agregan como referencias solo durante el tiempo de ejecución; los demás archivos se copian en carpetas de proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-193">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="df90f-194">Siempre debe haber un ensamblado específico de `AnyCPU` (TFM) correspondiente en la carpeta `/ref/{tfm}` para proporcionar el ensamblado de tiempo de compilación correspondiente.</span><span class="sxs-lookup"><span data-stu-id="df90f-194">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="df90f-195">Vea [Compatibilidad con varias plataformas de destino](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="df90f-195">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="df90f-196">contenido</span><span class="sxs-lookup"><span data-stu-id="df90f-196">content</span></span> | <span data-ttu-id="df90f-197">Archivos arbitrarios</span><span class="sxs-lookup"><span data-stu-id="df90f-197">Arbitrary files</span></span> | <span data-ttu-id="df90f-198">El contenido se copia en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-198">Contents are copied to the project root.</span></span> <span data-ttu-id="df90f-199">Piense en la carpeta **content** como la raíz de la aplicación de destino que consume el paquete en última instancia.</span><span class="sxs-lookup"><span data-stu-id="df90f-199">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="df90f-200">Para que el paquete agregue una imagen en la carpeta */images* de la aplicación, colóquelo en la carpeta *content/images* del paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-200">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="df90f-201">compilación</span><span class="sxs-lookup"><span data-stu-id="df90f-201">build</span></span> | <span data-ttu-id="df90f-202">Archivos `.targets` y `.props` de MSBuild</span><span class="sxs-lookup"><span data-stu-id="df90f-202">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="df90f-203">Se insertan automáticamente en el archivo de proyecto o en `project.lock.json` (NuGet 3.x y versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="df90f-203">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="df90f-204">tools</span><span class="sxs-lookup"><span data-stu-id="df90f-204">tools</span></span> | <span data-ttu-id="df90f-205">Scripts de PowerShell y programas accesibles desde la consola del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="df90f-205">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="df90f-206">La carpeta `tools` se agrega a la variable de entorno `PATH` solo para la consola del Administrador de paquetes (en concreto, *no* a `PATH` como se establece para MSBuild al compilar el proyecto).</span><span class="sxs-lookup"><span data-stu-id="df90f-206">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="df90f-207">Dado que la estructura de carpetas puede contener cualquier número de ensamblados para cualquier número de plataformas de destino, este método es necesario al crear paquetes que admiten varias plataformas.</span><span class="sxs-lookup"><span data-stu-id="df90f-207">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="df90f-208">En cualquier caso, una vez que tenga la estructura de carpetas deseada, ejecute el comando siguiente en esa carpeta para crear el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="df90f-208">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="df90f-209">Una vez más, el archivo `.nuspec` generado no contiene ninguna referencia explícita a los archivos de la estructura de carpetas.</span><span class="sxs-lookup"><span data-stu-id="df90f-209">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="df90f-210">NuGet incluye de manera automática todos los archivos cuando se crea el paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-210">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="df90f-211">Pero necesitará modificar los valores de marcador de posición en otras partes del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="df90f-211">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="df90f-212">Desde un archivo DLL de ensamblado</span><span class="sxs-lookup"><span data-stu-id="df90f-212">From an assembly DLL</span></span>

<span data-ttu-id="df90f-213">En el simple caso de creación de un paquete desde un ensamblado, puede generar un archivo `.nuspec` a partir de los metadatos del ensamblado con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="df90f-213">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="df90f-214">El uso de este formato reemplaza algunos marcadores de posición en el manifiesto con valores específicos del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="df90f-214">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="df90f-215">Por ejemplo, la propiedad `<id>` se establece en el nombre del ensamblado y `<version>` se establece en la versión del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="df90f-215">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="df90f-216">Pero otras propiedades del manifiesto no tienen valores coincidentes en el ensamblado y, por tanto, aún contienen marcadores de posición.</span><span class="sxs-lookup"><span data-stu-id="df90f-216">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="df90f-217">Desde un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="df90f-217">From a Visual Studio project</span></span>

<span data-ttu-id="df90f-218">La creación de un archivo `.nuspec` desde un archivo `.csproj` o `.vbproj` resulta práctica porque, de manera automática, se hace referencia como dependencias a otros paquetes que se han instalado en los proyectos.</span><span class="sxs-lookup"><span data-stu-id="df90f-218">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="df90f-219">Simplemente use el comando siguiente en la misma carpeta que el archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="df90f-219">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="df90f-220">El archivo `<project-name>.nuspec` resultante contiene *tokens* que se reemplazan durante el empaquetado con valores del proyecto, incluidas las referencias a todos los demás paquetes que ya se han instalado.</span><span class="sxs-lookup"><span data-stu-id="df90f-220">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="df90f-221">Un token está delimitado por símbolos `$` en ambos lados de la propiedad del proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-221">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="df90f-222">Por ejemplo, el valor `<id>` en un manifiesto generado de este modo normalmente tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="df90f-222">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="df90f-223">Este token se reemplaza por el valor `AssemblyName` del archivo de proyecto en tiempo de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="df90f-223">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="df90f-224">Para obtener la asignación exacta de valores de proyecto a tokens `.nuspec`, vea la [Referencia de tokens de reemplazo](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="df90f-224">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="df90f-225">Los tokens le liberan de la necesidad de actualizar valores esenciales como el número de versión en el archivo `.nuspec` cuando se actualiza el proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-225">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="df90f-226">(Siempre puede reemplazar los tokens con valores literales, si quiere).</span><span class="sxs-lookup"><span data-stu-id="df90f-226">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="df90f-227">Tenga en cuenta que hay varias opciones de empaquetado adicionales disponibles cuando se trabaja desde un proyecto de Visual Studio, como se describe en [Ejecución del paquete nuget para generar el archivo .nupkg](#running-nuget-pack-to-generate-the-nupkg-file) más adelante.</span><span class="sxs-lookup"><span data-stu-id="df90f-227">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="df90f-228">Paquetes de nivel de solución</span><span class="sxs-lookup"><span data-stu-id="df90f-228">Solution-level packages</span></span>

<span data-ttu-id="df90f-229">*Solo para NuGet 2.x. No disponible en NuGet 3.0 y versiones posteriores.*</span><span class="sxs-lookup"><span data-stu-id="df90f-229">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="df90f-230">En NuGet 2.x se admite la noción de paquete de nivel de solución que instala herramientas o comandos adicionales para la consola del Administrador de paquetes (el contenido de la carpeta `tools`), pero no agrega referencias, contenido o personalizaciones de compilación a ninguno de los proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="df90f-230">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="df90f-231">Estos paquetes no contienen ningún archivo en su carpetas `lib`, `content` o `build` directas, y ninguna de sus dependencias tienen archivos en sus respectivas carpetas `lib`, `content` o `build`.</span><span class="sxs-lookup"><span data-stu-id="df90f-231">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="df90f-232">NuGet realiza el seguimiento de los paquetes de nivel de la solución instalados en un archivo `packages.config` en la carpeta `.nuget`, en lugar del archivo `packages.config` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-232">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="df90f-233">Archivo nuevo con valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="df90f-233">New file with default values</span></span>

<span data-ttu-id="df90f-234">El comando siguiente crea un manifiesto predeterminado con marcadores de posición, lo que garantiza que comience con la estructura de archivos adecuada:</span><span class="sxs-lookup"><span data-stu-id="df90f-234">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="df90f-235">Si se omite \<nombre_del_paquete\>, el archivo resultante es `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="df90f-235">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="df90f-236">Si proporciona un nombre como `Contoso.Utility.UsefulStuff`, el archivo es `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="df90f-236">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="df90f-237">El archivo `.nuspec` resultante contiene marcadores de posición para valores como `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="df90f-237">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="df90f-238">Asegúrese de modificar el archivo antes de usarlo para crear el archivo `.nupkg` definitivo.</span><span class="sxs-lookup"><span data-stu-id="df90f-238">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="df90f-239">Elección de un identificador de paquete único y establecimiento del número de versión</span><span class="sxs-lookup"><span data-stu-id="df90f-239">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="df90f-240">El identificador del paquete (el elemento `<id>`) y el número de versión (el elemento `<version>`) son los dos valores más importantes del manifiesto ya que identifican de forma única el código exacto que se incluye en el paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-240">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="df90f-241">**Procedimientos recomendados para el identificador del paquete:**</span><span class="sxs-lookup"><span data-stu-id="df90f-241">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="df90f-242">**Unicidad**: el identificador debe ser único en nuget.org o en la galería que hospede el paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-242">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="df90f-243">Antes de decidirse por un identificador, busque en la galería aplicable para comprobar si el nombre ya está en uso.</span><span class="sxs-lookup"><span data-stu-id="df90f-243">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="df90f-244">Para evitar conflictos, un buen patrón consiste en usar el nombre de la empresa como la primera parte del identificador, por ejemplo `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="df90f-244">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="df90f-245">**Nombres de tipo espacio de nombres**: siguen un patrón similar a los espacios de nombres de .NET, con notación de puntos en lugar de guiones.</span><span class="sxs-lookup"><span data-stu-id="df90f-245">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="df90f-246">Por ejemplo, use `Contoso.Utility.UsefulStuff` en lugar de `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="df90f-246">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="df90f-247">También es útil para los consumidores cuando el identificador del paquete coincide con los espacios de nombres que se usan en el código.</span><span class="sxs-lookup"><span data-stu-id="df90f-247">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="df90f-248">**Paquetes de ejemplo**: si genera un paquete de código de ejemplo que muestra cómo usar otro paquete, adjunte `.Sample` como sufijo al identificador, como en `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="df90f-248">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="df90f-249">(El paquete de ejemplo tendría evidentemente una dependencia en el otro paquete). Al crear un paquete de ejemplo, use el método de directorio de trabajo basado en convenciones descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="df90f-249">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="df90f-250">En la carpeta `content`, organice el código de ejemplo en una carpeta denominada `\Samples\<identifier>` como en `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="df90f-250">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="df90f-251">**Procedimientos recomendados para la versión del paquete:**</span><span class="sxs-lookup"><span data-stu-id="df90f-251">**Best practices for the package version:**</span></span>

- <span data-ttu-id="df90f-252">En general, establezca la versión del paquete para que coincida con la biblioteca, aunque esto no es estrictamente necesario.</span><span class="sxs-lookup"><span data-stu-id="df90f-252">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="df90f-253">Esto es sencillo cuando se limita un paquete a un único ensamblado, como se describió anteriormente en [Decidir qué ensamblados empaquetar](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="df90f-253">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="df90f-254">En general, recuerde que el propio NuGet trabaja con versiones del paquete al resolver las dependencias, no con versiones de ensamblado.</span><span class="sxs-lookup"><span data-stu-id="df90f-254">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="df90f-255">Cuando se usa un esquema de la versión no estándar, asegúrese de tener en cuenta las reglas de control de versiones de NuGet, como se explica en [Control de versiones de paquetes](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="df90f-255">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="df90f-256">La siguiente serie de entradas de blog breves también es útil para entender el control de versiones:</span><span class="sxs-lookup"><span data-stu-id="df90f-256">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - <span data-ttu-id="df90f-257">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Enfrentarse al infierno de los archivos DLL)</span><span class="sxs-lookup"><span data-stu-id="df90f-257">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="df90f-258">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: El algoritmo básico)</span><span class="sxs-lookup"><span data-stu-id="df90f-258">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="df90f-259">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificación mediante redirecciones de enlaces)</span><span class="sxs-lookup"><span data-stu-id="df90f-259">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>

## <a name="setting-a-package-type"></a><span data-ttu-id="df90f-260">Establecimiento de un tipo de paquete</span><span class="sxs-lookup"><span data-stu-id="df90f-260">Setting a package type</span></span>

<span data-ttu-id="df90f-261">Con NuGet 3.5 y versiones posteriores, los paquetes se pueden marcar con un *tipo de paquete* concreto para indicar su uso previsto.</span><span class="sxs-lookup"><span data-stu-id="df90f-261">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="df90f-262">Los paquetes que no se marcan con un tipo, incluidos todos los creados con versiones anteriores de NuGet, tienen el tipo `Dependency` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="df90f-262">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="df90f-263">Los paquetes de tipo `Dependency` agregan activos de tiempo de compilación o ejecución a las aplicaciones y bibliotecas, y se pueden instalar en cualquier tipo de proyecto (suponiendo que sean compatibles).</span><span class="sxs-lookup"><span data-stu-id="df90f-263">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="df90f-264">Los paquetes de tipo `DotnetCliTool` son extensiones de la [CLI de .NET](/dotnet/articles/core/tools/index) y se invocan desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="df90f-264">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="df90f-265">Estos paquetes solo se pueden instalar en proyectos de .NET Core y no tienen ningún efecto en las operaciones de restauración.</span><span class="sxs-lookup"><span data-stu-id="df90f-265">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="df90f-266">Para obtener más información sobre estas extensiones por proyecto, vea la documentación de [extensibilidad de .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="df90f-266">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="df90f-267">Los paquetes de tipo personalizado usan un identificador de tipo arbitrario que se ajusta a las mismas reglas de formato que los identificadores de paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-267">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="df90f-268">Pero el Administrador de paquetes NuGet en Visual Studio no reconoce otros tipos que no sean `Dependency` y `DotnetCliTool`.</span><span class="sxs-lookup"><span data-stu-id="df90f-268">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="df90f-269">Los tipos de paquetes se establecen en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="df90f-269">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="df90f-270">Para la compatibilidad con versiones anteriores se recomienda *no* establecer explícitamente el tipo `Dependency` y, en su lugar, confiar en que NuGet asuma este tipo cuando no se especifique ninguno.</span><span class="sxs-lookup"><span data-stu-id="df90f-270">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="df90f-271">`.nuspec`: indicar el tipo de paquete dentro de un nodo `packageTypes\packageType` bajo el elemento `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="df90f-271">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="df90f-272">Adición de un archivo Léame y otros archivos</span><span class="sxs-lookup"><span data-stu-id="df90f-272">Adding a readme and other files</span></span>

<span data-ttu-id="df90f-273">Para especificar directamente los archivos que se van a incluir en el paquete, use el nodo `<files>` en el archivo `.nuspec`, que *sigue* a la etiqueta `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="df90f-273">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
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
> <span data-ttu-id="df90f-274">Cuando se usa el enfoque de directorio de trabajo basado en convenciones, puede colocar el archivo Léame.txt en la raíz del paquete y otro contenido en la carpeta `content`.</span><span class="sxs-lookup"><span data-stu-id="df90f-274">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="df90f-275">En el manifiesto no se necesitan elementos `<file>`.</span><span class="sxs-lookup"><span data-stu-id="df90f-275">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="df90f-276">Al incluir un archivo denominado `readme.txt` en la raíz del paquete, Visual Studio muestra el contenido de ese archivo como texto sin formato inmediatamente después de instalar el paquete directamente.</span><span class="sxs-lookup"><span data-stu-id="df90f-276">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="df90f-277">(Los archivos Léame no se muestran para paquetes instalados como dependencias).</span><span class="sxs-lookup"><span data-stu-id="df90f-277">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="df90f-278">Por ejemplo, este es el aspecto del archivo Léame para el paquete HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="df90f-278">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![La presentación de un archivo Léame para un paquete NuGet tras la instalación](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="df90f-280">Si incluye un nodo `<files>` vacío en el archivo `.nuspec`, NuGet no incluye ningún otro contenido en el paquete que no sea el que aparece en la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="df90f-280">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="df90f-281">Inclusión de propiedades y destinos de MSBuild en un paquete</span><span class="sxs-lookup"><span data-stu-id="df90f-281">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="df90f-282">En algunos casos, es posible que quiera agregar destinos de compilación personalizados o propiedades en proyectos en los que se consume el paquete, como la ejecución de una herramienta o un proceso personalizado durante la compilación.</span><span class="sxs-lookup"><span data-stu-id="df90f-282">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="df90f-283">Para ello, coloque los archivos en el formato `<package_id>.targets` o `<package_id>.props` (por ejemplo `Contoso.Utility.UsefulStuff.targets`) dentro de la carpeta `\build` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-283">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="df90f-284">Los archivos en la carpeta `\build` raíz se consideran adecuados para todas las plataformas de destino.</span><span class="sxs-lookup"><span data-stu-id="df90f-284">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="df90f-285">Para proporcionar archivos específicos de la plataforma, colóquelos primero en las subcarpetas adecuadas, como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="df90f-285">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="df90f-286">Después, en el archivo `.nuspec`, asegúrese de hacer referencia a estos archivos en el nodo `<files>`:</span><span class="sxs-lookup"><span data-stu-id="df90f-286">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="df90f-287">Con [NuGet 2.5 se introdujo](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files) la inclusión de propiedades y destinos de MSBuild en un paquete. Por tanto, se recomienda agregar el atributo `minClientVersion="2.5"` al elemento `metadata` para indicar la versión de cliente de NuGet mínima necesaria para usar el paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-287">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="df90f-288">Cuando NuGet instala un paquete con archivos `\build`, agrega elementos `<Import>` de MSBuild al archivo de proyecto que apunta a los archivos `.targets` y `.props`.</span><span class="sxs-lookup"><span data-stu-id="df90f-288">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="df90f-289">(`.props` se agrega en la parte superior del archivo del proyecto; `.targets` se agrega al final). Se agrega un elemento condicional `<Import>` de MSBuild independiente para cada plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="df90f-289">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="df90f-290">Los archivos `.props` y `.targets` de MSBuild de los destinos multiplataforma pueden colocarse en la carpeta `\buildCrossTargeting`.</span><span class="sxs-lookup"><span data-stu-id="df90f-290">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildCrossTargeting` folder.</span></span> <span data-ttu-id="df90f-291">Durante la instalación de paquetes, NuGet agrega los elementos `<Import>` correspondientes al archivo de proyecto, con la condición de que no se establezca la plataforma de destino (la propiedad `$(TargetFramework)` de MSBuild debe estar vacía).</span><span class="sxs-lookup"><span data-stu-id="df90f-291">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="df90f-292">Con NuGet 3.x, los destinos no se agregan al proyecto pero en su lugar se ponen a disposición a través de `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="df90f-292">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="df90f-293">Creación de paquetes con ensamblados de interoperabilidad COM</span><span class="sxs-lookup"><span data-stu-id="df90f-293">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="df90f-294">Los paquetes que contienen ensamblados de interoperabilidad COM deben incluir un [archivo de destinos](#including-msbuild-props-and-targets-in-a-package) adecuado para que los metadatos `EmbedInteropTypes` correctos se agreguen a los proyectos con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="df90f-294">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="df90f-295">De forma predeterminada, los metadatos `EmbedInteropTypes` siempre son false para todos los ensamblados cuando se usa PackageReference, por lo que el archivo de destinos agrega estos metadatos de manera explícita.</span><span class="sxs-lookup"><span data-stu-id="df90f-295">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="df90f-296">Para evitar conflictos, el nombre del destino debe ser único; lo ideal es usar una combinación del nombre del paquete y del ensamblado que se va a insertar, reemplazando el `{InteropAssemblyName}` en el ejemplo siguiente con ese valor.</span><span class="sxs-lookup"><span data-stu-id="df90f-296">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="df90f-297">(Vea también [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) para obtener un ejemplo).</span><span class="sxs-lookup"><span data-stu-id="df90f-297">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="df90f-298">Tenga en cuenta que, cuando se usa el formato de administración `packages.config`, agregar referencias a los ensamblados desde los paquetes hace que NuGet y Visual Studio comprueben los ensamblados de interoperabilidad COM y establezcan `EmbedInteropTypes` en true en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-298">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="df90f-299">En este caso, los destinos se reemplazan.</span><span class="sxs-lookup"><span data-stu-id="df90f-299">In this case the targets are overriden.</span></span>

<span data-ttu-id="df90f-300">Además, de forma predeterminada los [activos de compilación no fluyen de manera transitiva](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="df90f-300">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="df90f-301">Los paquetes creados como se describe aquí funcionan de manera diferente cuando se extraen como una dependencia transitiva de un proyecto a una referencia de proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-301">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="df90f-302">El consumidor del paquete puede permitir que fluyan si modifica el valor predeterminado de PrivateAssets para que no se incluya la compilación.</span><span class="sxs-lookup"><span data-stu-id="df90f-302">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="df90f-303">Ejecución del paquete nuget para generar el archivo .nupkg</span><span class="sxs-lookup"><span data-stu-id="df90f-303">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="df90f-304">Cuando se usa un ensamblado o el directorio de trabajo basado en convenciones, cree un paquete mediante la ejecución de `nuget pack` con el archivo `.nuspec`, reemplazando `<project-name>` con el nombre de archivo específico:</span><span class="sxs-lookup"><span data-stu-id="df90f-304">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="df90f-305">Cuando se usa un proyecto de Visual Studio, ejecute `nuget pack` con el archivo de proyecto, que carga automáticamente el archivo `.nuspec` del proyecto y reemplaza los tokens que contiene mediante valores del archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="df90f-305">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="df90f-306">Es necesario usar el archivo de proyecto directamente para el reemplazo de tokens porque el proyecto es el origen de los valores de token.</span><span class="sxs-lookup"><span data-stu-id="df90f-306">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="df90f-307">El reemplazo de tokens no se realiza si se usa `nuget pack` con un archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="df90f-307">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="df90f-308">En todos los casos, `nuget pack` excluye las carpetas que comienzan con un punto, como `.git` o `.hg`.</span><span class="sxs-lookup"><span data-stu-id="df90f-308">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="df90f-309">NuGet indica si hay errores en el archivo `.nuspec` que se deben corregir, como olvidar cambiar valores de marcador de posición en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="df90f-309">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="df90f-310">Una vez que `nuget pack` es correcto, tendrá un archivo `.nupkg` que se puede publicar en una galería adecuada como se describe en [Publicación de un paquete](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="df90f-310">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="df90f-311">Una manera útil de examinar un paquete después de crearlo consiste en abrirlo en la herramienta [Explorador de paquetes](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="df90f-311">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="df90f-312">Esto ofrece una vista gráfica del contenido del paquete y el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="df90f-312">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="df90f-313">También puede cambiar el nombre del archivo `.nupkg` resultante a un archivo `.zip` y explorar directamente su contenido.</span><span class="sxs-lookup"><span data-stu-id="df90f-313">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="df90f-314">Opciones adicionales</span><span class="sxs-lookup"><span data-stu-id="df90f-314">Additional options</span></span>

<span data-ttu-id="df90f-315">Puede usar diversos modificadores de línea de comandos con `nuget pack` para excluir archivos, reemplazar el número de versión en el manifiesto y cambiar la carpeta de salida, entre otras características.</span><span class="sxs-lookup"><span data-stu-id="df90f-315">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="df90f-316">Para obtener una lista completa, consulte la [referencia del comando pack](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="df90f-316">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="df90f-317">Las opciones siguientes son algunas comunes en proyectos de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="df90f-317">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="df90f-318">**Proyectos a los que se hace referencia**: si el proyecto hace referencia a otros proyectos, puede agregar los proyectos a los que se hace referencia como parte del paquete, o bien como dependencias, mediante la opción `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="df90f-318">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="df90f-319">Este proceso de inclusión es recursivo, por lo que si `MyProject.csproj` hace referencia a los proyectos B y C, y esos proyectos hacen referencia a D, E y F, los archivos de B, C, D, E y F se incluyen en el paquete.</span><span class="sxs-lookup"><span data-stu-id="df90f-319">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="df90f-320">Si un proyecto al que se hace referencia incluye un archivo `.nuspec` propio, en su lugar NuGet agrega ese proyecto al que se hace referencia como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="df90f-320">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="df90f-321">Debe empaquetar y publicar ese proyecto por separado.</span><span class="sxs-lookup"><span data-stu-id="df90f-321">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="df90f-322">**Configuración de compilación**: de forma predeterminada, NuGet usa la configuración de compilación predeterminada establecida en el archivo de proyecto, normalmente *Debug*.</span><span class="sxs-lookup"><span data-stu-id="df90f-322">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="df90f-323">Para empaquetar archivos de una configuración de compilación diferente, como *Release*, use la opción `-properties` con la configuración:</span><span class="sxs-lookup"><span data-stu-id="df90f-323">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="df90f-324">**Símbolos**: para incluir símbolos que permitan a los consumidores recorrer el código del paquete en el depurador, use la opción `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="df90f-324">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="df90f-325">Prueba de la instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="df90f-325">Testing package installation</span></span>

<span data-ttu-id="df90f-326">Antes de publicar un paquete, normalmente querrá probar el proceso de instalación de un paquete en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-326">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="df90f-327">Las pruebas aseguran que los archivos necesarios acaban en los lugares correctos en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="df90f-327">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="df90f-328">Puede probar las instalaciones de forma manual en Visual Studio o en la línea de comandos mediante los [pasos de instalación de paquetes](../consume-packages/ways-to-install-a-package.md) normales.</span><span class="sxs-lookup"><span data-stu-id="df90f-328">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="df90f-329">Para las pruebas automatizadas, el proceso básico es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="df90f-329">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="df90f-330">Copie el archivo `.nupkg` en una carpeta local.</span><span class="sxs-lookup"><span data-stu-id="df90f-330">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="df90f-331">Agregue la carpeta a los orígenes de paquete mediante el comando `nuget sources add -name <name> -source <path>` (vea [Orígenes de nuget](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="df90f-331">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="df90f-332">Tenga en cuenta que solo es necesario establecer este origen local una vez en un equipo determinado.</span><span class="sxs-lookup"><span data-stu-id="df90f-332">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="df90f-333">Instale el paquete desde ese origen mediante `nuget install <packageID> -source <name>`, donde `<name>` coincide con el nombre del origen tal como se indicó a `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="df90f-333">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="df90f-334">Especificar el origen asegura que el paquete se instala únicamente desde ese origen.</span><span class="sxs-lookup"><span data-stu-id="df90f-334">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="df90f-335">Examine el sistema de archivos para comprobar que los archivos se instalan correctamente.</span><span class="sxs-lookup"><span data-stu-id="df90f-335">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df90f-336">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df90f-336">Next Steps</span></span>

<span data-ttu-id="df90f-337">Una vez haya creado un paquete, que es un archivo `.nupkg`, puede publicarlo en la galería de su elección como se describe en [Publicación de un paquete](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="df90f-337">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="df90f-338">Es posible que también quiera ampliar las funcionalidades del paquete o admitir otros escenarios, como se describe en los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="df90f-338">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="df90f-339">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="df90f-339">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="df90f-340">Compatibilidad con varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="df90f-340">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="df90f-341">Transformaciones de archivos de origen y configuración</span><span class="sxs-lookup"><span data-stu-id="df90f-341">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="df90f-342">Localización</span><span class="sxs-lookup"><span data-stu-id="df90f-342">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="df90f-343">Versiones preliminares</span><span class="sxs-lookup"><span data-stu-id="df90f-343">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="df90f-344">Por último, hay tipos de paquete adicionales que tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="df90f-344">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="df90f-345">Paquetes nativos</span><span class="sxs-lookup"><span data-stu-id="df90f-345">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="df90f-346">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="df90f-346">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
