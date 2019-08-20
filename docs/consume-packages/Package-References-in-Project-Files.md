---
title: Formato PackageReference de NuGet (referencias de paquete en archivos de proyecto)
description: Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0 y versiones posteriores, VS2017 y .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 05ece5f36ff7ae5920960c42cfde8b271dc3e712
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020008"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="315ae-103">Referencias del paquete (PackageReference) en archivos de proyecto</span><span class="sxs-lookup"><span data-stu-id="315ae-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="315ae-104">Las referencias de paquetes, con el nodo `PackageReference`, administran las dependencias de NuGet directamente en los archivos de proyecto (a diferencia de un archivo `packages.config` independiente).</span><span class="sxs-lookup"><span data-stu-id="315ae-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="315ae-105">El uso de PackageReference, como así se llama, no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en las [configuraciones comunes de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="315ae-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="315ae-106">Con PackageReference, también puede usar las condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras agrupaciones.</span><span class="sxs-lookup"><span data-stu-id="315ae-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="315ae-107">También le proporciona un control específico sobre las dependencias y el flujo de contenido.</span><span class="sxs-lookup"><span data-stu-id="315ae-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="315ae-108">(Para saber más, vea [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) (Empaquetado y restauración de NuGet como destinos de MSBuild).</span><span class="sxs-lookup"><span data-stu-id="315ae-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="315ae-109">Compatibilidad con tipo de proyecto</span><span class="sxs-lookup"><span data-stu-id="315ae-109">Project type support</span></span>

<span data-ttu-id="315ae-110">De forma predeterminada, PackageReference se usa para proyectos de .NET Core, proyectos de .NET Standard y proyectos de UWP que tengan como destino Windows 10 Build 15063 (Creators Update) y versiones posteriores, con la excepción de los proyectos de UWP en C++.</span><span class="sxs-lookup"><span data-stu-id="315ae-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="315ae-111">Los proyectos de .NET Framework admiten PackageReference, pero actualmente tienen como valor predeterminado `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="315ae-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="315ae-112">Para usar PackageReference, [migre](../reference/migrate-packages-config-to-package-reference.md) las dependencias de `packages.config` al archivo de proyecto y luego quite packages.config.</span><span class="sxs-lookup"><span data-stu-id="315ae-112">To use PackageReference, [migrate](../reference/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="315ae-113">Las aplicaciones ASP.NET destinadas a .NET Framework por completo solo incluyen [compatibilidad limitada](https://github.com/NuGet/Home/issues/5877) para PackageReference.</span><span class="sxs-lookup"><span data-stu-id="315ae-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="315ae-114">Los tipos de proyecto de C++y JavaScript no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="315ae-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="315ae-115">Agregar una PackageReference</span><span class="sxs-lookup"><span data-stu-id="315ae-115">Adding a PackageReference</span></span>

<span data-ttu-id="315ae-116">Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="315ae-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="315ae-117">Controlar la versión de una dependencia</span><span class="sxs-lookup"><span data-stu-id="315ae-117">Controlling dependency version</span></span>

<span data-ttu-id="315ae-118">La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="315ae-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="315ae-119">En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).</span><span class="sxs-lookup"><span data-stu-id="315ae-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="315ae-120">Uso de una PackageReference para un proyecto sin PackageReferences</span><span class="sxs-lookup"><span data-stu-id="315ae-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="315ae-121">Avanzado: Si no tiene paquetes instalados en un proyecto (ninguna PackageReference en el archivo de proyecto y ningún archivo packages.config), pero quiere que el proyecto se restaure como de estilo PackageReference, puede establecer una propiedad de proyecto RestoreProjectStyle en PackageReference en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="315ae-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="315ae-122">Esto puede resultar útil si hace referencia a proyectos de estilo PackageReference (csproj existente o proyectos de estilo SDK).</span><span class="sxs-lookup"><span data-stu-id="315ae-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="315ae-123">Esto permitirá que el proyecto haga referencia "de manera transitiva" a los paquetes a los que hacen referencia dichos proyectos.</span><span class="sxs-lookup"><span data-stu-id="315ae-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="315ae-124">Versiones flotantes</span><span class="sxs-lookup"><span data-stu-id="315ae-124">Floating Versions</span></span>

<span data-ttu-id="315ae-125">Las [versiones flotantes](../consume-packages/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="315ae-125">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="315ae-126">Controlar los recursos de dependencias</span><span class="sxs-lookup"><span data-stu-id="315ae-126">Controlling dependency assets</span></span>

<span data-ttu-id="315ae-127">Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete.</span><span class="sxs-lookup"><span data-stu-id="315ae-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="315ae-128">En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="315ae-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="315ae-129">Las siguientes etiquetas de metadatos controlan los recursos de dependencia:</span><span class="sxs-lookup"><span data-stu-id="315ae-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="315ae-130">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="315ae-130">Tag</span></span> | <span data-ttu-id="315ae-131">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="315ae-131">Description</span></span> | <span data-ttu-id="315ae-132">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="315ae-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="315ae-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="315ae-133">IncludeAssets</span></span> | <span data-ttu-id="315ae-134">Se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="315ae-134">These assets will be consumed</span></span> | <span data-ttu-id="315ae-135">todo</span><span class="sxs-lookup"><span data-stu-id="315ae-135">all</span></span> |
| <span data-ttu-id="315ae-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="315ae-136">ExcludeAssets</span></span> | <span data-ttu-id="315ae-137">No se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="315ae-137">These assets will not be consumed</span></span> | <span data-ttu-id="315ae-138">ninguna</span><span class="sxs-lookup"><span data-stu-id="315ae-138">none</span></span> |
| <span data-ttu-id="315ae-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="315ae-139">PrivateAssets</span></span> | <span data-ttu-id="315ae-140">Estos recursos se consumirán, pero no irán al proyecto principal</span><span class="sxs-lookup"><span data-stu-id="315ae-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="315ae-141">archivos de contenido; analizadores; compilación</span><span class="sxs-lookup"><span data-stu-id="315ae-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="315ae-142">A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:</span><span class="sxs-lookup"><span data-stu-id="315ae-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="315ae-143">Valor</span><span class="sxs-lookup"><span data-stu-id="315ae-143">Value</span></span> | <span data-ttu-id="315ae-144">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="315ae-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="315ae-145">compile</span><span class="sxs-lookup"><span data-stu-id="315ae-145">compile</span></span> | <span data-ttu-id="315ae-146">Contenido de la carpeta `lib` y controla si el proyecto se puede compilar con los ensamblados dentro de la carpeta</span><span class="sxs-lookup"><span data-stu-id="315ae-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="315ae-147">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="315ae-147">runtime</span></span> | <span data-ttu-id="315ae-148">Contenido de las carpetas `lib` y `runtimes` y controla si estos ensamblados se copiarán en el directorio de salida de compilación</span><span class="sxs-lookup"><span data-stu-id="315ae-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="315ae-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="315ae-149">contentFiles</span></span> | <span data-ttu-id="315ae-150">Contenido de la carpeta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="315ae-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="315ae-151">compilación</span><span class="sxs-lookup"><span data-stu-id="315ae-151">build</span></span> | <span data-ttu-id="315ae-152">`.props` y `.targets` en la carpeta `build`</span><span class="sxs-lookup"><span data-stu-id="315ae-152">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="315ae-153">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="315ae-153">buildMultitargeting</span></span> | <span data-ttu-id="315ae-154">`.props` y `.targets` en la carpeta `buildMultitargeting`, de los destinos multiplataforma</span><span class="sxs-lookup"><span data-stu-id="315ae-154">`.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="315ae-155">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="315ae-155">buildTransitive</span></span> | <span data-ttu-id="315ae-156">*(5.0+)* `.props` y `.targets` en la carpeta `buildTransitive`, para los recursos que fluyen de manera transitiva a cualquier proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="315ae-156">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="315ae-157">Vea la página de la [característica](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="315ae-157">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="315ae-158">analyzers</span><span class="sxs-lookup"><span data-stu-id="315ae-158">analyzers</span></span> | <span data-ttu-id="315ae-159">Analizadores de .NET</span><span class="sxs-lookup"><span data-stu-id="315ae-159">.NET analyzers</span></span> |
| <span data-ttu-id="315ae-160">nativas</span><span class="sxs-lookup"><span data-stu-id="315ae-160">native</span></span> | <span data-ttu-id="315ae-161">Contenido de la carpeta `native`</span><span class="sxs-lookup"><span data-stu-id="315ae-161">Contents of the `native` folder</span></span> |
| <span data-ttu-id="315ae-162">ninguna</span><span class="sxs-lookup"><span data-stu-id="315ae-162">none</span></span> | <span data-ttu-id="315ae-163">No se usa ninguno de los anteriores.</span><span class="sxs-lookup"><span data-stu-id="315ae-163">None of the above are used.</span></span> |
| <span data-ttu-id="315ae-164">todo</span><span class="sxs-lookup"><span data-stu-id="315ae-164">all</span></span> | <span data-ttu-id="315ae-165">Todo lo anterior (excepto `none`)</span><span class="sxs-lookup"><span data-stu-id="315ae-165">All of the above (except `none`)</span></span> |

<span data-ttu-id="315ae-166">En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="315ae-166">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="315ae-167">Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="315ae-167">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="315ae-168">Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="315ae-168">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="315ae-169">AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.</span><span class="sxs-lookup"><span data-stu-id="315ae-169">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="315ae-170">Agregar una condición PackageReference</span><span class="sxs-lookup"><span data-stu-id="315ae-170">Adding a PackageReference condition</span></span>

<span data-ttu-id="315ae-171">Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="315ae-171">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="315ae-172">Pero actualmente solo se admite la variable `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="315ae-172">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="315ae-173">Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`.</span><span class="sxs-lookup"><span data-stu-id="315ae-173">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="315ae-174">En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria.</span><span class="sxs-lookup"><span data-stu-id="315ae-174">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="315ae-175">Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="315ae-175">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="315ae-176">Un paquete creado con este proyecto mostrará que Newtonsoft.Json se incluye como dependencia únicamente para un destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="315ae-176">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="315ae-178">Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:</span><span class="sxs-lookup"><span data-stu-id="315ae-178">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="315ae-179">Cargando las dependencias</span><span class="sxs-lookup"><span data-stu-id="315ae-179">Locking dependencies</span></span>
<span data-ttu-id="315ae-180">*Esta característica está disponible con NuGet **4.9** o superior y con Visual Studio 2017 **15.9** o superior.*</span><span class="sxs-lookup"><span data-stu-id="315ae-180">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="315ae-181">La entrada a la restauración de NuGet es un conjunto de referencias de paquete del archivo del proyecto (dependencias de nivel superior o directas) y la salida es un cierre completo de todas las dependencias de paquetes, incluidas las dependencias transitivas.</span><span class="sxs-lookup"><span data-stu-id="315ae-181">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="315ae-182">NuGet siempre intenta producir el mismo cierre completo de dependencias de paquetes si no ha cambiado la lista PackageReference de entrada.</span><span class="sxs-lookup"><span data-stu-id="315ae-182">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="315ae-183">Sin embargo, hay algunos escenarios en los que no se puede hacer.</span><span class="sxs-lookup"><span data-stu-id="315ae-183">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="315ae-184">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="315ae-184">For example:</span></span>

* <span data-ttu-id="315ae-185">Al usar versiones flotantes como `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="315ae-185">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="315ae-186">Aunque la intención aquí es hacer flotante la última versión de todas las restauraciones de paquetes, hay escenarios en los que los usuarios necesitan que el gráfico se bloquee hacia una versión más reciente determinada y hacen flotante una versión posterior, en caso de estar disponible, en un gesto explícito.</span><span class="sxs-lookup"><span data-stu-id="315ae-186">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="315ae-187">Se publica una versión más reciente del paquete que coincide con los requisitos de la versión PackageReference.</span><span class="sxs-lookup"><span data-stu-id="315ae-187">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="315ae-188">P. ej.,</span><span class="sxs-lookup"><span data-stu-id="315ae-188">E.g.</span></span> 

  * <span data-ttu-id="315ae-189">Día 1: si especificó `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, pero las versiones disponibles en los repositorios NuGet eran 4.1.0, 4.2.0 y 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="315ae-189">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="315ae-190">En este caso, NuGet habría llevado a cabo la resolución de la versión 4.1.0 (la versión mínima más cercana)</span><span class="sxs-lookup"><span data-stu-id="315ae-190">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="315ae-191">Día 2: Se publica la versión 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="315ae-191">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="315ae-192">Ahora, NuGet encontrará la coincidencia exacta e iniciará la resolución de la versión 4.0.0</span><span class="sxs-lookup"><span data-stu-id="315ae-192">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="315ae-193">Se quita una versión del paquete especificada del repositorio.</span><span class="sxs-lookup"><span data-stu-id="315ae-193">A given package version is removed from the repository.</span></span> <span data-ttu-id="315ae-194">Aunque nuget.org no permite la eliminación de paquetes, no todos los repositorios de paquetes tienen estas restricciones.</span><span class="sxs-lookup"><span data-stu-id="315ae-194">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="315ae-195">Esto da lugar a la búsqueda por parte de NuGet de la mejor coincidencia cuando no puede llevar a cabo la resolución de la versión eliminada.</span><span class="sxs-lookup"><span data-stu-id="315ae-195">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="315ae-196">Habilitación del archivo de bloqueo</span><span class="sxs-lookup"><span data-stu-id="315ae-196">Enabling lock file</span></span>
<span data-ttu-id="315ae-197">A fin de mantener el cierre completo de dependencias de paquetes, puede participar en la característica del archivo de bloqueo estableciendo la propiedad MSBuild `RestorePackagesWithLockFile` para su proyecto:</span><span class="sxs-lookup"><span data-stu-id="315ae-197">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="315ae-198">Si se establece esta propiedad, la restauración de NuGet generará un archivo de bloqueo: archivo `packages.lock.json` del directorio raíz del proyecto que incluye todas las dependencias de paquetes.</span><span class="sxs-lookup"><span data-stu-id="315ae-198">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="315ae-199">Una vez que un proyecto tiene el archivo `packages.lock.json` en su directorio raíz, el archivo de bloqueo siempre se usa con la restauración incluso si no se establece la propiedad `RestorePackagesWithLockFile`.</span><span class="sxs-lookup"><span data-stu-id="315ae-199">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="315ae-200">Así pues, otra forma de participar en esta característica consiste en crear un archivo `packages.lock.json` en blanco ficticio en el directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="315ae-200">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="315ae-201">Comportamiento `restore` con el archivo de bloqueo</span><span class="sxs-lookup"><span data-stu-id="315ae-201">`restore` behavior with lock file</span></span>
<span data-ttu-id="315ae-202">Si un archivo de bloqueo está presente para el proyecto, NuGet usa este archivo de bloqueo para ejecutar `restore`.</span><span class="sxs-lookup"><span data-stu-id="315ae-202">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="315ae-203">NuGet realiza una rápida comprobación para ver si hubo algún cambio en las dependencias de paquetes tal como se mencionó en el archivo del proyecto (o archivos de los proyectos dependientes) y, en caso de no haber ningún cambio, simplemente restaura los paquetes mencionados en el archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="315ae-203">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="315ae-204">No hay ninguna reevaluación de dependencias de paquetes.</span><span class="sxs-lookup"><span data-stu-id="315ae-204">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="315ae-205">Si NuGet detecta un cambio en las dependencias definidas tal como se menciona en los archivos del proyecto, volverá a evaluar el gráfico del paquete y actualizará el archivo de bloqueo para reflejar el nuevo cierre del paquete para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="315ae-205">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="315ae-206">En CI/CD y otros escenarios, en los que no desearía cambiar las dependencias de paquetes en el camino, puede hacerlo estableciendo `lockedmode` en `true`:</span><span class="sxs-lookup"><span data-stu-id="315ae-206">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="315ae-207">En dotnet.exe,ejecute:</span><span class="sxs-lookup"><span data-stu-id="315ae-207">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="315ae-208">En msbuild.exe, ejecute:</span><span class="sxs-lookup"><span data-stu-id="315ae-208">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="315ae-209">También puede establecer esta propiedad MSBuild condicional en su archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="315ae-209">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="315ae-210">Si el modo de bloqueo es `true`, la restauración restaurará los paquetes exactos tal como se incluyen en el archivo de bloqueo o producirá un error si actualizó las dependencias de paquetes definidas para el proyecto tras crearse el archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="315ae-210">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="315ae-211">Haga que el archivo de bloqueo forme parte de su repositorio de origen</span><span class="sxs-lookup"><span data-stu-id="315ae-211">Make lock file part of your source repository</span></span>
<span data-ttu-id="315ae-212">Si crea una aplicación, un archivo ejecutable y el proyecto en cuestión se encuentra al principio de la cadena de dependencia, inserte el archivo de bloqueo en el repositorio de código fuente para que NuGet pueda hacer uso de este durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="315ae-212">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="315ae-213">Sin embargo, si su proyecto es un proyecto de biblioteca que no envía o un proyecto de código común del que dependen otros proyectos, **no debe** insertar en el repositorio el archivo de bloqueo como parte de su código fuente.</span><span class="sxs-lookup"><span data-stu-id="315ae-213">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="315ae-214">No hay nada malo en el hecho de conservar el archivo de bloqueo, pero es posible que no se usen las dependencias de paquetes bloqueadas para el proyecto de código común, como se muestra en el archivo de bloqueo, durante la restauración/creación de un proyecto que depende de este proyecto de código común.</span><span class="sxs-lookup"><span data-stu-id="315ae-214">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="315ae-215">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="315ae-215">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="315ae-216">Si `ProjectA` tiene una dependencia de la versión `2.0.0` de `PackageX` y también hace referencia a `ProjectB`, que depende de la versión `1.0.0` de `PackageX`, el archivo de bloqueo para `ProjectB` mostrará una dependencia de la versión `1.0.0` de `PackageX`.</span><span class="sxs-lookup"><span data-stu-id="315ae-216">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="315ae-217">Sin embargo, al crearse `ProjectA`, su archivo de bloqueo contendrá una dependencia de la versión **`2.0.0`** de `PackageX` y **no** `1.0.0` como se muestra en el archivo de bloqueo para `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="315ae-217">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="315ae-218">Por tanto, el archivo de bloqueo de un proyecto de código común tiene poco que decir sobre los paquetes resueltos para los proyectos que dependen de él.</span><span class="sxs-lookup"><span data-stu-id="315ae-218">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="315ae-219">Extensibilidad del archivo de bloqueo</span><span class="sxs-lookup"><span data-stu-id="315ae-219">Lock file extensibility</span></span>
<span data-ttu-id="315ae-220">Puede controlar diversos comportamientos de la restauración con el archivo de bloqueo como se describe a continuación:</span><span class="sxs-lookup"><span data-stu-id="315ae-220">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="315ae-221">Opción</span><span class="sxs-lookup"><span data-stu-id="315ae-221">Option</span></span> | <span data-ttu-id="315ae-222">Opción equivalente de MSBuild</span><span class="sxs-lookup"><span data-stu-id="315ae-222">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="315ae-223">Uso de arranques del archivo de bloqueo para un proyecto.</span><span class="sxs-lookup"><span data-stu-id="315ae-223">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="315ae-224">De forma alternativa, puede establecer la propiedad `RestorePackagesWithLockFile` en el archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="315ae-224">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="315ae-225">Habilita el modo de bloqueo para la restauración.</span><span class="sxs-lookup"><span data-stu-id="315ae-225">Enables locked mode for restore.</span></span> <span data-ttu-id="315ae-226">Esto resulta útil en los escenarios de CI/CD en los que desea obtener las compilaciones repetibles.</span><span class="sxs-lookup"><span data-stu-id="315ae-226">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="315ae-227">También puede ser estableciendo la propiedad MSBuild `RestoreLockedMode` en `true`</span><span class="sxs-lookup"><span data-stu-id="315ae-227">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="315ae-228">Esta opción es útil con los paquetes con la versión flotante definida en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="315ae-228">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="315ae-229">De forma predeterminada, la restauración de NuGet no actualizará la versión del paquete automáticamente tras cada restauración a menos que ejecute esta con la opción `--force-evaluate`.</span><span class="sxs-lookup"><span data-stu-id="315ae-229">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="315ae-230">Define una ubicación del archivo de bloqueo personalizada para un proyecto.</span><span class="sxs-lookup"><span data-stu-id="315ae-230">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="315ae-231">Esto también puede lograrse estableciendo la propiedad MSBuild `NuGetLockFilePath`.</span><span class="sxs-lookup"><span data-stu-id="315ae-231">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="315ae-232">De forma predeterminada, NuGet admite `packages.lock.json` en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="315ae-232">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="315ae-233">Si tiene varios proyectos en el mismo directorio, NuGet admite el archivo de bloqueo específico del proyecto `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="315ae-233">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
