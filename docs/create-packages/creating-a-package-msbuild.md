---
title: Creación de un paquete NuGet con MSBuild
description: Un guía detallada sobre el proceso de diseño y creación de un paquete NuGet, incluidos puntos de decisión clave como archivos y control de versiones.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: a0db6dc95ffa5ad73741ae53a6be9d6f937c1dbf
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833229"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="4e680-103">Creación de un paquete NuGet con MSBuild</span><span class="sxs-lookup"><span data-stu-id="4e680-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="4e680-104">Cuando crea un paquete NuGet a partir del código, empaqueta la funcionalidad en un componente que se pueda compartir con otros desarrolladores, así como que estos puedan usarlo.</span><span class="sxs-lookup"><span data-stu-id="4e680-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="4e680-105">En este artículo se describe cómo crear un paquete con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4e680-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="4e680-106">MSBuild viene preinstalado con cada carga de trabajo de Visual Studio que incluya NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e680-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="4e680-107">Además, también puede usar MSBuild mediante la CLI de dotnet con [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild).</span><span class="sxs-lookup"><span data-stu-id="4e680-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)</span></span>

<span data-ttu-id="4e680-108">Con los proyectos .NET Core y .NET Standard que usan el [formato de estilo SDK](../resources/check-project-format.md) y cualquier otro proyecto de estilo SDK, NuGet usa la información del archivo de proyecto directamente para crear un paquete.</span><span class="sxs-lookup"><span data-stu-id="4e680-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="4e680-109">En el caso de un proyecto sin SDK que use `<PackageReference>`, NuGet también usará el archivo del proyecto para crear un paquete.</span><span class="sxs-lookup"><span data-stu-id="4e680-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="4e680-110">Los proyectos con SDK tienen la funcionalidad de paquetes disponible de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4e680-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="4e680-111">En el caso de los proyectos PackageReference sin SDK, deberá agregar el paquete NuGet.Build.Tasks.Pack a las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="4e680-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="4e680-112">Para obtener información detallada sobre los destinos de paquete de MSBuild, vea [pack y restore de NuGet como destinos de MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="4e680-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="4e680-113">El comando que crea un paquete, `msbuild -t:pack`, es equivalente funcionalmente a `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="4e680-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e680-114">Este tema se aplica a los proyectos [con SDK](../resources/check-project-format.md), que suelen ser proyectos de .NET Core y .NET Standard, así como a los paquetes sin SDK que usan PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4e680-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="4e680-115">Establecimiento de las propiedades</span><span class="sxs-lookup"><span data-stu-id="4e680-115">Set properties</span></span>

<span data-ttu-id="4e680-116">Las propiedades siguientes se requieren para crear un paquete.</span><span class="sxs-lookup"><span data-stu-id="4e680-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="4e680-117">`PackageId`, el identificador de paquete, que debe ser único en la galería que hospeda el paquete.</span><span class="sxs-lookup"><span data-stu-id="4e680-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="4e680-118">Si no se especifica, el valor predeterminado es `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="4e680-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="4e680-119">`Version`, un número de versión específico con el formato *Principal.Secundaria.Revisión[-Sufijo]* donde *-Sufijo* identifica las [versiones preliminares](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="4e680-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="4e680-120">Si no se especifica, el valor predeterminado es 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="4e680-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="4e680-121">El título del paquete como debe aparecer en el host (por ejemplo, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="4e680-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="4e680-122">`Authors`, información del autor y el propietario.</span><span class="sxs-lookup"><span data-stu-id="4e680-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="4e680-123">Si no se especifica, el valor predeterminado es `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="4e680-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="4e680-124">`Company`, el nombre de la empresa.</span><span class="sxs-lookup"><span data-stu-id="4e680-124">`Company`, your company name.</span></span> <span data-ttu-id="4e680-125">Si no se especifica, el valor predeterminado es `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="4e680-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="4e680-126">En Visual Studio, puede establecer estos valores en las propiedades del proyecto (haga clic con el botón derecho en el proyecto en el Explorador de soluciones, elija **Propiedades** y seleccione la pestaña **Paquete**).</span><span class="sxs-lookup"><span data-stu-id="4e680-126">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="4e680-127">También puede establecer estas propiedades directamente en los archivos del proyecto ( *.csproj*).</span><span class="sxs-lookup"><span data-stu-id="4e680-127">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="4e680-128">Asigne al paquete un identificador que sea único en nuget.org o en el origen de paquete que esté usando.</span><span class="sxs-lookup"><span data-stu-id="4e680-128">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="4e680-129">En el ejemplo siguiente se muestra un archivo del proyecto sencillo y completo que incluye estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="4e680-129">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="4e680-130">También puede establecer las propiedades opcionales, como `Title`, `PackageDescription` y `PackageTags`, tal como se describe en los [destinos de paquetes de MSBuild](../reference/msbuild-targets.md#pack-target), la sección [Controlar los recursos de dependencias](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) y [Propiedades de los metadatos de NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="4e680-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="4e680-131">En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **PackageTags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="4e680-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="4e680-132">Para obtener más información sobre cómo declarar dependencias y especificar números de versión, vea [Referencias del paquete (PackageReference) en archivos del proyecto](../consume-packages/package-references-in-project-files.md) y [Control de versiones de paquetes](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4e680-132">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="4e680-133">También es posible exponer recursos directamente desde las dependencias en el paquete mediante los atributos `<IncludeAssets>` y `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="4e680-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="4e680-134">Para más información, consulte [Controlar los recursos de dependencias](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="4e680-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="4e680-135">Elección de un identificador de paquete único y establecimiento del número de versión</span><span class="sxs-lookup"><span data-stu-id="4e680-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="4e680-136">Adición del paquete NuGet.Build.Tasks.Pack</span><span class="sxs-lookup"><span data-stu-id="4e680-136">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="4e680-137">Si usa MSBuild con un proyecto sin SDK y PackageReference, agregue el paquete NuGet.Build.Tasks.Pack al proyecto.</span><span class="sxs-lookup"><span data-stu-id="4e680-137">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="4e680-138">Abra el archivo del proyecto y agregue lo siguiente tras el elemento `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="4e680-138">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="4e680-139">Abra un símbolo del sistema para desarrolladores (en el cuadro **Búsqueda**, escriba **Símbolo del sistema para desarrolladores**).</span><span class="sxs-lookup"><span data-stu-id="4e680-139">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="4e680-140">Normalmente, es preferible iniciar el símbolo del sistema para desarrolladores de Visual Studio en el menú **Inicio**, ya que se configurará con todas las rutas de acceso necesarias para MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4e680-140">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="4e680-141">Cambie a la carpeta que contiene el archivo del proyecto y escriba el siguiente comando para instalar el paquete NuGet.Build.Tasks.Pack.</span><span class="sxs-lookup"><span data-stu-id="4e680-141">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="4e680-142">Asegúrese de que la salida de MSBuild indica que la compilación se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4e680-142">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="4e680-143">Ejecución del comando msbuild -t:pack</span><span class="sxs-lookup"><span data-stu-id="4e680-143">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="4e680-144">Para compilar un paquete NuGet (un archivo `.nupkg`) desde el proyecto, ejecute el comando `msbuild -t:pack`, que también genera el proyecto automáticamente:</span><span class="sxs-lookup"><span data-stu-id="4e680-144">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="4e680-145">En el símbolo del sistema para desarrolladores, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4e680-145">In the Developer command prompt, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="4e680-146">El resultado mostrará la ruta de acceso al archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="4e680-146">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="4e680-147">Generación automática del paquete en la compilación</span><span class="sxs-lookup"><span data-stu-id="4e680-147">Automatically generate package on build</span></span>

<span data-ttu-id="4e680-148">Para ejecutar automáticamente `msbuild -t:pack` al compilar o restaurar el proyecto, agregue la siguiente línea al archivo del proyecto en `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="4e680-148">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="4e680-149">Cuando ejecuta `msbuild -t:pack` en una solución, se empaquetan todos los proyectos de la solución que se pueden empaquetar (la propiedad [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) se establece en `true`).</span><span class="sxs-lookup"><span data-stu-id="4e680-149">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="4e680-150">Cuando genera automáticamente el paquete, el tiempo de empaquetado aumenta el tiempo de compilación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="4e680-150">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="4e680-151">Prueba de instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="4e680-151">Test package installation</span></span>

<span data-ttu-id="4e680-152">Antes de publicar un paquete, normalmente querrá probar el proceso de instalación de un paquete en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="4e680-152">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="4e680-153">Las pruebas aseguran que los archivos necesarios acaban en los lugares correctos en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4e680-153">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="4e680-154">Puede probar las instalaciones de forma manual en Visual Studio o en la línea de comandos mediante los [pasos de instalación de paquetes](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normales.</span><span class="sxs-lookup"><span data-stu-id="4e680-154">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e680-155">Los paquetes son inmutables.</span><span class="sxs-lookup"><span data-stu-id="4e680-155">Packages are immutable.</span></span> <span data-ttu-id="4e680-156">Si corrige un problema, cambie el contenido del paquete y vuelva a empaquetar. Cuando vuelva a realizar la prueba, seguirá usando la versión anterior del paquete hasta que [bote la carpeta global de paquetes](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="4e680-156">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="4e680-157">Esto resulta especialmente relevante cuando se prueban paquetes que no usan una etiqueta preliminar única en cada compilación.</span><span class="sxs-lookup"><span data-stu-id="4e680-157">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e680-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e680-158">Next Steps</span></span>

<span data-ttu-id="4e680-159">Una vez haya creado un paquete, que es un archivo `.nupkg`, puede publicarlo en la galería de su elección como se describe en [Publicación de un paquete](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4e680-159">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="4e680-160">Es posible que también quiera ampliar las funcionalidades del paquete o admitir otros escenarios, como se describe en los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="4e680-160">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="4e680-161">Empaquetado y restauración de NuGet como destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="4e680-161">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="4e680-162">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="4e680-162">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4e680-163">Admitir varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="4e680-163">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="4e680-164">Transformaciones de archivos de origen y configuración</span><span class="sxs-lookup"><span data-stu-id="4e680-164">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="4e680-165">Localización</span><span class="sxs-lookup"><span data-stu-id="4e680-165">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="4e680-166">Versiones preliminares</span><span class="sxs-lookup"><span data-stu-id="4e680-166">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="4e680-167">Definición del tipo de paquete</span><span class="sxs-lookup"><span data-stu-id="4e680-167">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="4e680-168">Creación de paquetes con ensamblados de interoperabilidad COM</span><span class="sxs-lookup"><span data-stu-id="4e680-168">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="4e680-169">Por último, hay tipos de paquete adicionales que tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="4e680-169">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="4e680-170">Paquetes nativos</span><span class="sxs-lookup"><span data-stu-id="4e680-170">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="4e680-171">Paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="4e680-171">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
