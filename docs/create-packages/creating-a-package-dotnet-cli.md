---
title: Creación de un paquete NuGet con la CLI de dotnet
description: Un guía detallada sobre el proceso de diseño y creación de un paquete NuGet, incluidos puntos de decisión clave como archivos y control de versiones.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 40a42be91d3848db3e721a674e3fec4096fccd08
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69489022"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="ffa96-103">Creación de un paquete NuGet con la CLI de dotnet</span><span class="sxs-lookup"><span data-stu-id="ffa96-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="ffa96-104">Con independencia de lo que haga el paquete o lo que contenga el código, use una de las herramientas de CLI, ya sea `nuget.exe` o `dotnet.exe`, para empaquetar esa funcionalidad en un componente que se pueda compartir y usar por parte de otros desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="ffa96-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="ffa96-105">En este artículo se describe cómo crear un paquete con la CLI de dotnet.</span><span class="sxs-lookup"><span data-stu-id="ffa96-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="ffa96-106">Para instalar la CLI de `dotnet`, consulte [Instalación de las herramientas del cliente NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="ffa96-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="ffa96-107">A partir de Visual Studio 2017, la CLI de dotnet se incluye con las cargas de trabajo de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ffa96-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="ffa96-108">Con los proyectos .NET Core y .NET Standard que usan el [formato de estilo SDK](../resources/check-project-format.md) y cualquier otro proyecto de estilo SDK, NuGet usa la información del archivo de proyecto directamente para crear un paquete.</span><span class="sxs-lookup"><span data-stu-id="ffa96-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="ffa96-109">Para consultar tutoriales paso a paso, vea [Creación de paquetes de .NET Standard con la CLI de dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) o [Creación de paquetes de .NET Standard con Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ffa96-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="ffa96-110">`msbuild -t:pack` es funcionalmente equivalente a `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="ffa96-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="ffa96-111">Para compilar con MSBuild, vea [Creación de un paquete de NuGet con MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="ffa96-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffa96-112">Este tema se aplica a los proyectos de [estilo SDK](../resources/check-project-format.md), por lo general proyectos de .NET Core y .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="ffa96-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="ffa96-113">Establecimiento de las propiedades</span><span class="sxs-lookup"><span data-stu-id="ffa96-113">Set properties</span></span>

<span data-ttu-id="ffa96-114">Las propiedades siguientes se requieren para crear un paquete.</span><span class="sxs-lookup"><span data-stu-id="ffa96-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="ffa96-115">`PackageId`, el identificador de paquete, que debe ser único en la galería que hospeda el paquete.</span><span class="sxs-lookup"><span data-stu-id="ffa96-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="ffa96-116">Si no se especifica, el valor predeterminado es `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="ffa96-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="ffa96-117">`Version`, un número de versión específico con el formato *Principal.Secundaria.Revisión[-Sufijo]* donde *-Sufijo* identifica las [versiones preliminares](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ffa96-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="ffa96-118">Si no se especifica, el valor predeterminado es 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="ffa96-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="ffa96-119">El título del paquete como debe aparecer en el host (por ejemplo, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="ffa96-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="ffa96-120">`Authors`, información del autor y el propietario.</span><span class="sxs-lookup"><span data-stu-id="ffa96-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="ffa96-121">Si no se especifica, el valor predeterminado es `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="ffa96-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="ffa96-122">`Company`, el nombre de la empresa.</span><span class="sxs-lookup"><span data-stu-id="ffa96-122">`Company`, your company name.</span></span> <span data-ttu-id="ffa96-123">Si no se especifica, el valor predeterminado es `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="ffa96-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="ffa96-124">En Visual Studio, puede establecer estos valores en las propiedades del proyecto (haga clic con el botón derecho en el proyecto en el Explorador de soluciones, elija **Propiedades** y seleccione la pestaña **Paquete**).</span><span class="sxs-lookup"><span data-stu-id="ffa96-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="ffa96-125">También puede establecer estas propiedades directamente en los archivos del proyecto (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="ffa96-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="ffa96-126">Asigne al paquete un identificador que sea único en nuget.org o en el origen de paquete que esté usando.</span><span class="sxs-lookup"><span data-stu-id="ffa96-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="ffa96-127">En el ejemplo siguiente se muestra un archivo del proyecto sencillo y completo que incluye estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="ffa96-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="ffa96-128">(Puede crear un nuevo proyecto predeterminado mediante el comando `dotnet new classlib`).</span><span class="sxs-lookup"><span data-stu-id="ffa96-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="ffa96-129">También puede establecer las propiedades opcionales, como `Title`, `PackageDescription` y `PackageTags`, tal como se describe en los [destinos de paquetes de MSBuild](../reference/msbuild-targets.md#pack-target), la sección [Controlar los recursos de dependencias](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) y [Propiedades de los metadatos de NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="ffa96-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="ffa96-130">En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **PackageTags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="ffa96-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="ffa96-131">Para obtener más información sobre cómo declarar dependencias y especificar números de versión, vea [Referencias del paquete en archivos del proyecto](../consume-packages/package-references-in-project-files.md) y [Control de versiones de paquetes](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ffa96-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="ffa96-132">También es posible exponer recursos directamente desde las dependencias en el paquete mediante los atributos `<IncludeAssets>` y `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="ffa96-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="ffa96-133">Para más información, consulte [Controlar los recursos de dependencias](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="ffa96-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="ffa96-134">Elección de un identificador de paquete único y establecimiento del número de versión</span><span class="sxs-lookup"><span data-stu-id="ffa96-134">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="ffa96-135">Ejecutar el comando pack</span><span class="sxs-lookup"><span data-stu-id="ffa96-135">Run the pack command</span></span>

<span data-ttu-id="ffa96-136">Para compilar un paquete NuGet (un archivo `.nupkg`) desde el proyecto, ejecute el comando `dotnet pack`, que también genera el proyecto automáticamente:</span><span class="sxs-lookup"><span data-stu-id="ffa96-136">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="ffa96-137">El resultado mostrará la ruta de acceso al archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ffa96-137">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="ffa96-138">Generación automática del paquete en la compilación</span><span class="sxs-lookup"><span data-stu-id="ffa96-138">Automatically generate package on build</span></span>

<span data-ttu-id="ffa96-139">Para ejecutar automáticamente `dotnet pack` al ejecutar `dotnet build`, agregue la siguiente línea al archivo de proyecto en `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="ffa96-139">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="ffa96-140">Cuando ejecute `dotnet pack` en una solución, se empaquetarán todos los proyectos de la solución que lo permitan (la propiedad [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) se establece en `true`).</span><span class="sxs-lookup"><span data-stu-id="ffa96-140">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="ffa96-141">Cuando genera automáticamente el paquete, el tiempo de empaquetado aumenta el tiempo de compilación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ffa96-141">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="ffa96-142">Prueba de instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="ffa96-142">Test package installation</span></span>

<span data-ttu-id="ffa96-143">Antes de publicar un paquete, normalmente querrá probar el proceso de instalación de un paquete en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="ffa96-143">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="ffa96-144">Las pruebas aseguran que los archivos necesarios acaban en los lugares correctos en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ffa96-144">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="ffa96-145">Puede probar las instalaciones de forma manual en Visual Studio o en la línea de comandos mediante los [pasos de instalación de paquetes](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normales.</span><span class="sxs-lookup"><span data-stu-id="ffa96-145">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffa96-146">Los paquetes son inmutables.</span><span class="sxs-lookup"><span data-stu-id="ffa96-146">Packages are immutable.</span></span> <span data-ttu-id="ffa96-147">Si corrige un problema, cambie el contenido del paquete y vuelva a empaquetar. Cuando vuelva a realizar la prueba, seguirá usando la versión anterior del paquete hasta que [bote la carpeta global de paquetes](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="ffa96-147">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="ffa96-148">Esto resulta especialmente relevante cuando se prueban paquetes que no usan una etiqueta preliminar única en cada compilación.</span><span class="sxs-lookup"><span data-stu-id="ffa96-148">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffa96-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ffa96-149">Next Steps</span></span>

<span data-ttu-id="ffa96-150">Una vez haya creado un paquete, que es un archivo `.nupkg`, puede publicarlo en la galería de su elección como se describe en [Publicación de un paquete](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ffa96-150">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="ffa96-151">Es posible que también quiera ampliar las funcionalidades del paquete o admitir otros escenarios, como se describe en los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="ffa96-151">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="ffa96-152">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="ffa96-152">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="ffa96-153">Admitir varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="ffa96-153">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="ffa96-154">Transformaciones de archivos de origen y configuración</span><span class="sxs-lookup"><span data-stu-id="ffa96-154">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="ffa96-155">Localización</span><span class="sxs-lookup"><span data-stu-id="ffa96-155">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ffa96-156">Versiones preliminares</span><span class="sxs-lookup"><span data-stu-id="ffa96-156">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="ffa96-157">Definición del tipo de paquete</span><span class="sxs-lookup"><span data-stu-id="ffa96-157">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="ffa96-158">Creación de paquetes con ensamblados de interoperabilidad COM</span><span class="sxs-lookup"><span data-stu-id="ffa96-158">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="ffa96-159">Por último, hay tipos de paquete adicionales que tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="ffa96-159">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="ffa96-160">Paquetes nativos</span><span class="sxs-lookup"><span data-stu-id="ffa96-160">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="ffa96-161">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="ffa96-161">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
