---
title: Formato PackageReference de NuGet (referencias de paquete en archivos de proyecto)
description: Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0 y versiones posteriores, VS2017 y .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428508"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="2b011-103">Referencias del paquete (PackageReference) en archivos de proyecto</span><span class="sxs-lookup"><span data-stu-id="2b011-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="2b011-104">Las referencias de paquetes, con el nodo `PackageReference`, administran las dependencias de NuGet directamente en los archivos de proyecto (a diferencia de un archivo `packages.config` independiente).</span><span class="sxs-lookup"><span data-stu-id="2b011-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="2b011-105">El uso de PackageReference, como así se llama, no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en las [configuraciones comunes de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="2b011-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="2b011-106">Con PackageReference, también puede usar las condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino u otras agrupaciones.</span><span class="sxs-lookup"><span data-stu-id="2b011-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="2b011-107">También le proporciona un control específico sobre las dependencias y el flujo de contenido.</span><span class="sxs-lookup"><span data-stu-id="2b011-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="2b011-108">(Para saber más, vea [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) (Empaquetado y restauración de NuGet como destinos de MSBuild).</span><span class="sxs-lookup"><span data-stu-id="2b011-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="2b011-109">Compatibilidad con tipo de proyecto</span><span class="sxs-lookup"><span data-stu-id="2b011-109">Project type support</span></span>

<span data-ttu-id="2b011-110">De forma predeterminada, PackageReference se usa para proyectos de .NET Core, proyectos de .NET Standard y proyectos de UWP que tengan como destino Windows 10 Build 15063 (Creators Update) y versiones posteriores, con la excepción de los proyectos de UWP en C++.</span><span class="sxs-lookup"><span data-stu-id="2b011-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="2b011-111">Los proyectos de .NET Framework admiten PackageReference, pero actualmente tienen como valor predeterminado `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="2b011-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="2b011-112">Para usar PackageReference, [migre](../consume-packages/migrate-packages-config-to-package-reference.md) las dependencias de `packages.config` al archivo de proyecto y luego quite packages.config.</span><span class="sxs-lookup"><span data-stu-id="2b011-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="2b011-113">Las aplicaciones ASP.NET destinadas a .NET Framework por completo solo incluyen [compatibilidad limitada](https://github.com/NuGet/Home/issues/5877) para PackageReference.</span><span class="sxs-lookup"><span data-stu-id="2b011-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="2b011-114">Los tipos de proyecto de C++y JavaScript no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="2b011-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="2b011-115">Agregar una PackageReference</span><span class="sxs-lookup"><span data-stu-id="2b011-115">Adding a PackageReference</span></span>

<span data-ttu-id="2b011-116">Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="2b011-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="2b011-117">Controlar la versión de una dependencia</span><span class="sxs-lookup"><span data-stu-id="2b011-117">Controlling dependency version</span></span>

<span data-ttu-id="2b011-118">La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="2b011-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="2b011-119">En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../concepts/package-versioning.md#version-ranges) (Control de versiones de paquetes).</span><span class="sxs-lookup"><span data-stu-id="2b011-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="2b011-120">Uso de una PackageReference para un proyecto sin PackageReferences</span><span class="sxs-lookup"><span data-stu-id="2b011-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="2b011-121">Avanzado: Si no tiene paquetes instalados en un proyecto (ninguna PackageReference en el archivo de proyecto y ningún archivo packages.config), pero quiere que el proyecto se restaure como de estilo PackageReference, puede establecer una propiedad de proyecto RestoreProjectStyle en PackageReference en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b011-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="2b011-122">Esto puede resultar útil si hace referencia a proyectos de estilo PackageReference (csproj existente o proyectos de estilo SDK).</span><span class="sxs-lookup"><span data-stu-id="2b011-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="2b011-123">Esto permitirá que el proyecto haga referencia "de manera transitiva" a los paquetes a los que hacen referencia dichos proyectos.</span><span class="sxs-lookup"><span data-stu-id="2b011-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="2b011-124">PackageReference y los orígenes</span><span class="sxs-lookup"><span data-stu-id="2b011-124">PackageReference and sources</span></span>

<span data-ttu-id="2b011-125">En los proyectos de PackageReference, las versiones de dependencia transitiva se resuelven en el momento de la restauración.</span><span class="sxs-lookup"><span data-stu-id="2b011-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="2b011-126">Como tal, en los proyectos de PackageReference todos los orígenes deben estar disponibles para todas las restauraciones.</span><span class="sxs-lookup"><span data-stu-id="2b011-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="2b011-127">Versiones flotantes</span><span class="sxs-lookup"><span data-stu-id="2b011-127">Floating Versions</span></span>

<span data-ttu-id="2b011-128">Las [versiones flotantes](../concepts/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="2b011-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="2b011-129">Controlar los recursos de dependencias</span><span class="sxs-lookup"><span data-stu-id="2b011-129">Controlling dependency assets</span></span>

<span data-ttu-id="2b011-130">Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete.</span><span class="sxs-lookup"><span data-stu-id="2b011-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="2b011-131">En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="2b011-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="2b011-132">Las siguientes etiquetas de metadatos controlan los recursos de dependencia:</span><span class="sxs-lookup"><span data-stu-id="2b011-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="2b011-133">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="2b011-133">Tag</span></span> | <span data-ttu-id="2b011-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="2b011-134">Description</span></span> | <span data-ttu-id="2b011-135">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2b011-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b011-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="2b011-136">IncludeAssets</span></span> | <span data-ttu-id="2b011-137">Se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="2b011-137">These assets will be consumed</span></span> | <span data-ttu-id="2b011-138">todo</span><span class="sxs-lookup"><span data-stu-id="2b011-138">all</span></span> |
| <span data-ttu-id="2b011-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="2b011-139">ExcludeAssets</span></span> | <span data-ttu-id="2b011-140">No se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="2b011-140">These assets will not be consumed</span></span> | <span data-ttu-id="2b011-141">ninguna</span><span class="sxs-lookup"><span data-stu-id="2b011-141">none</span></span> |
| <span data-ttu-id="2b011-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="2b011-142">PrivateAssets</span></span> | <span data-ttu-id="2b011-143">Estos recursos se consumirán, pero no irán al proyecto principal</span><span class="sxs-lookup"><span data-stu-id="2b011-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="2b011-144">archivos de contenido; analizadores; compilación</span><span class="sxs-lookup"><span data-stu-id="2b011-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="2b011-145">A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:</span><span class="sxs-lookup"><span data-stu-id="2b011-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="2b011-146">Valor</span><span class="sxs-lookup"><span data-stu-id="2b011-146">Value</span></span> | <span data-ttu-id="2b011-147">Descripción</span><span class="sxs-lookup"><span data-stu-id="2b011-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="2b011-148">compile</span><span class="sxs-lookup"><span data-stu-id="2b011-148">compile</span></span> | <span data-ttu-id="2b011-149">Contenido de la carpeta `lib` y controla si el proyecto se puede compilar con los ensamblados dentro de la carpeta</span><span class="sxs-lookup"><span data-stu-id="2b011-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="2b011-150">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="2b011-150">runtime</span></span> | <span data-ttu-id="2b011-151">Contenido de las carpetas `lib` y `runtimes` y controla si estos ensamblados se copiarán en el directorio de salida de compilación</span><span class="sxs-lookup"><span data-stu-id="2b011-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="2b011-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="2b011-152">contentFiles</span></span> | <span data-ttu-id="2b011-153">Contenido de la carpeta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="2b011-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="2b011-154">compilación</span><span class="sxs-lookup"><span data-stu-id="2b011-154">build</span></span> | <span data-ttu-id="2b011-155">`.props` y `.targets` en la carpeta `build`</span><span class="sxs-lookup"><span data-stu-id="2b011-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="2b011-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="2b011-156">buildMultitargeting</span></span> | <span data-ttu-id="2b011-157">*(4.0)* `.props` y `.targets` en la carpeta `buildMultitargeting`, para los destinos multiplataforma</span><span class="sxs-lookup"><span data-stu-id="2b011-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="2b011-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="2b011-158">buildTransitive</span></span> | <span data-ttu-id="2b011-159">*(5.0+)* `.props` y `.targets` en la carpeta `buildTransitive`, para los recursos que fluyen de manera transitiva a cualquier proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="2b011-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="2b011-160">Vea la página de la [característica](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="2b011-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="2b011-161">analyzers</span><span class="sxs-lookup"><span data-stu-id="2b011-161">analyzers</span></span> | <span data-ttu-id="2b011-162">Analizadores de .NET</span><span class="sxs-lookup"><span data-stu-id="2b011-162">.NET analyzers</span></span> |
| <span data-ttu-id="2b011-163">nativas</span><span class="sxs-lookup"><span data-stu-id="2b011-163">native</span></span> | <span data-ttu-id="2b011-164">Contenido de la carpeta `native`</span><span class="sxs-lookup"><span data-stu-id="2b011-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="2b011-165">ninguna</span><span class="sxs-lookup"><span data-stu-id="2b011-165">none</span></span> | <span data-ttu-id="2b011-166">No se usa ninguno de los anteriores.</span><span class="sxs-lookup"><span data-stu-id="2b011-166">None of the above are used.</span></span> |
| <span data-ttu-id="2b011-167">todo</span><span class="sxs-lookup"><span data-stu-id="2b011-167">all</span></span> | <span data-ttu-id="2b011-168">Todo lo anterior (excepto `none`)</span><span class="sxs-lookup"><span data-stu-id="2b011-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="2b011-169">En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="2b011-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="2b011-170">Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="2b011-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="2b011-171">Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="2b011-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="2b011-172">AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.</span><span class="sxs-lookup"><span data-stu-id="2b011-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="2b011-173">Cuando `developmentDependency` se establece en `true` en un archivo `.nuspec`, esto marca un paquete como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="2b011-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="2b011-174">Con PackageReference *(NuGet 4.8 +)* , esta marca también significa que excluirá los recursos en tiempo de compilación de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2b011-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="2b011-175">Para más información, consulte [Compatibilidad de DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="2b011-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="2b011-176">Agregar una condición PackageReference</span><span class="sxs-lookup"><span data-stu-id="2b011-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="2b011-177">Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="2b011-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="2b011-178">Pero actualmente solo se admite la variable `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="2b011-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="2b011-179">Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`.</span><span class="sxs-lookup"><span data-stu-id="2b011-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="2b011-180">En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria.</span><span class="sxs-lookup"><span data-stu-id="2b011-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="2b011-181">Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2b011-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="2b011-182">Un paquete creado con este proyecto mostrará que Newtonsoft.Json se incluye como dependencia únicamente para un destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="2b011-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="2b011-184">Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:</span><span class="sxs-lookup"><span data-stu-id="2b011-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="2b011-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="2b011-185">GeneratePathProperty</span></span>

<span data-ttu-id="2b011-186">Esta característica está disponible con NuGet **5.0** o una versión superior y con Visual Studio 2019 **16.0** o una versión superior.</span><span class="sxs-lookup"><span data-stu-id="2b011-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="2b011-187">A veces es conveniente hacer referencia a los archivos de un paquete desde un destino de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="2b011-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="2b011-188">En los proyectos basados en `packages.config`, los paquetes se instalan en una carpeta relativa al archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b011-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="2b011-189">Sin embargo, en PackageReference, los paquetes se [consumen](../concepts/package-installation-process.md) de la carpeta *global-packages*, que puede variar de una máquina a otra.</span><span class="sxs-lookup"><span data-stu-id="2b011-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="2b011-190">Para salvar esa diferencia, NuGet ha presentado una propiedad que apunta a la ubicación desde la que se va a consumir el paquete.</span><span class="sxs-lookup"><span data-stu-id="2b011-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="2b011-191">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2b011-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="2b011-192">Además, NuGet generará automáticamente las propiedades de los paquetes que contengan una carpeta herramientas.</span><span class="sxs-lookup"><span data-stu-id="2b011-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="2b011-193">Las propiedades de MSBuild y las identidades de paquete no tienen las mismas restricciones, por lo que la identidad de paquete debe cambiarse por un nombre descriptivo de MSBuild, precedido por la palabra `Pkg`.</span><span class="sxs-lookup"><span data-stu-id="2b011-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="2b011-194">Para comprobar el nombre exacto de la propiedad generada, examine el archivo [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) generado.</span><span class="sxs-lookup"><span data-stu-id="2b011-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="2b011-195">Advertencias y errores de NuGet</span><span class="sxs-lookup"><span data-stu-id="2b011-195">NuGet warnings and errors</span></span>

<span data-ttu-id="2b011-196">*Esta característica está disponible con NuGet \*\*4.3*\* o una versión superior y con Visual Studio 2017 **15.3** o una versión superior.\*</span><span class="sxs-lookup"><span data-stu-id="2b011-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="2b011-197">En muchos escenarios de paquetes y restauración, todas las advertencias y errores de NuGet se codifican y comienzan con `NU****`.</span><span class="sxs-lookup"><span data-stu-id="2b011-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="2b011-198">Todas las advertencias y errores de NuGet se enumeran en la documentación de [referencia](../reference/errors-and-warnings.md).</span><span class="sxs-lookup"><span data-stu-id="2b011-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="2b011-199">NuGet observa las propiedades de advertencia siguientes:</span><span class="sxs-lookup"><span data-stu-id="2b011-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="2b011-200">`TreatWarningsAsErrors`, se tratan todas las advertencias como errores.</span><span class="sxs-lookup"><span data-stu-id="2b011-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="2b011-201">`WarningsAsErrors`, se tratan las advertencias específicas como errores.</span><span class="sxs-lookup"><span data-stu-id="2b011-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="2b011-202">`NoWarn`, se ocultan las advertencias concretas, en todo el proyecto o en todo el paquete.</span><span class="sxs-lookup"><span data-stu-id="2b011-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="2b011-203">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="2b011-203">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="2b011-204">Supresión de advertencias de NuGet</span><span class="sxs-lookup"><span data-stu-id="2b011-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="2b011-205">Aunque se recomienda resolver todas las advertencias de NuGet durante las operaciones de paquete y restauración, en determinadas situaciones está garantizada la supresión.</span><span class="sxs-lookup"><span data-stu-id="2b011-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="2b011-206">Para suprimir una advertencia en todo el proyecto, le recomendamos que haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2b011-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="2b011-207">A veces, las advertencias solo se aplican a un determinado paquete del grafo.</span><span class="sxs-lookup"><span data-stu-id="2b011-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="2b011-208">Podemos optar por suprimir esa advertencia de manera más selectiva al agregar `NoWarn` en el elemento PackageReference.</span><span class="sxs-lookup"><span data-stu-id="2b011-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="2b011-209">Supresión de advertencias de paquete NuGet en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2b011-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="2b011-210">En Visual Studio, también puede [suprimir las advertencias](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) a través del IDE.</span><span class="sxs-lookup"><span data-stu-id="2b011-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="2b011-211">Cargando las dependencias</span><span class="sxs-lookup"><span data-stu-id="2b011-211">Locking dependencies</span></span>

<span data-ttu-id="2b011-212">*Esta característica está disponible con NuGet **4.9** o superior y con Visual Studio 2017 **15.9** o superior.*</span><span class="sxs-lookup"><span data-stu-id="2b011-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="2b011-213">La entrada a la restauración de NuGet es un conjunto de referencias de paquete del archivo del proyecto (dependencias de nivel superior o directas) y la salida es un cierre completo de todas las dependencias de paquetes, incluidas las dependencias transitivas.</span><span class="sxs-lookup"><span data-stu-id="2b011-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="2b011-214">NuGet siempre intenta producir el mismo cierre completo de dependencias de paquetes si no ha cambiado la lista PackageReference de entrada.</span><span class="sxs-lookup"><span data-stu-id="2b011-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="2b011-215">Sin embargo, hay algunos escenarios en los que no se puede hacer.</span><span class="sxs-lookup"><span data-stu-id="2b011-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="2b011-216">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2b011-216">For example:</span></span>

* <span data-ttu-id="2b011-217">Al usar versiones flotantes como `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="2b011-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="2b011-218">Aunque la intención aquí es hacer flotante la última versión de todas las restauraciones de paquetes, hay escenarios en los que los usuarios necesitan que el gráfico se bloquee hacia una versión más reciente determinada y hacen flotante una versión posterior, en caso de estar disponible, en un gesto explícito.</span><span class="sxs-lookup"><span data-stu-id="2b011-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="2b011-219">Se publica una versión más reciente del paquete que coincide con los requisitos de la versión PackageReference.</span><span class="sxs-lookup"><span data-stu-id="2b011-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="2b011-220">P. ej.,</span><span class="sxs-lookup"><span data-stu-id="2b011-220">E.g.</span></span> 

  * <span data-ttu-id="2b011-221">Día 1: si especificó `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, pero las versiones disponibles en los repositorios NuGet eran 4.1.0, 4.2.0 y 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="2b011-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="2b011-222">En este caso, NuGet habría llevado a cabo la resolución de la versión 4.1.0 (la versión mínima más cercana)</span><span class="sxs-lookup"><span data-stu-id="2b011-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="2b011-223">Día 2: Se publica la versión 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="2b011-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="2b011-224">Ahora, NuGet encontrará la coincidencia exacta e iniciará la resolución de la versión 4.0.0</span><span class="sxs-lookup"><span data-stu-id="2b011-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="2b011-225">Se quita una versión del paquete especificada del repositorio.</span><span class="sxs-lookup"><span data-stu-id="2b011-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="2b011-226">Aunque nuget.org no permite la eliminación de paquetes, no todos los repositorios de paquetes tienen estas restricciones.</span><span class="sxs-lookup"><span data-stu-id="2b011-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="2b011-227">Esto da lugar a la búsqueda por parte de NuGet de la mejor coincidencia cuando no puede llevar a cabo la resolución de la versión eliminada.</span><span class="sxs-lookup"><span data-stu-id="2b011-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="2b011-228">Habilitación del archivo de bloqueo</span><span class="sxs-lookup"><span data-stu-id="2b011-228">Enabling lock file</span></span>

<span data-ttu-id="2b011-229">A fin de mantener el cierre completo de dependencias de paquetes, puede participar en la característica del archivo de bloqueo estableciendo la propiedad MSBuild `RestorePackagesWithLockFile` para su proyecto:</span><span class="sxs-lookup"><span data-stu-id="2b011-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="2b011-230">Si se establece esta propiedad, la restauración de NuGet generará un archivo de bloqueo: archivo `packages.lock.json` del directorio raíz del proyecto que incluye todas las dependencias de paquetes.</span><span class="sxs-lookup"><span data-stu-id="2b011-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="2b011-231">Una vez que un proyecto tiene el archivo `packages.lock.json` en su directorio raíz, el archivo de bloqueo siempre se usa con la restauración incluso si no se establece la propiedad `RestorePackagesWithLockFile`.</span><span class="sxs-lookup"><span data-stu-id="2b011-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="2b011-232">Así pues, otra forma de participar en esta característica consiste en crear un archivo `packages.lock.json` en blanco ficticio en el directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b011-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="2b011-233">Comportamiento `restore` con el archivo de bloqueo</span><span class="sxs-lookup"><span data-stu-id="2b011-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="2b011-234">Si un archivo de bloqueo está presente para el proyecto, NuGet usa este archivo de bloqueo para ejecutar `restore`.</span><span class="sxs-lookup"><span data-stu-id="2b011-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="2b011-235">NuGet realiza una rápida comprobación para ver si hubo algún cambio en las dependencias de paquetes tal como se mencionó en el archivo del proyecto (o archivos de los proyectos dependientes) y, en caso de no haber ningún cambio, simplemente restaura los paquetes mencionados en el archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="2b011-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="2b011-236">No hay ninguna reevaluación de dependencias de paquetes.</span><span class="sxs-lookup"><span data-stu-id="2b011-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="2b011-237">Si NuGet detecta un cambio en las dependencias definidas tal como se menciona en los archivos del proyecto, volverá a evaluar el gráfico del paquete y actualizará el archivo de bloqueo para reflejar el nuevo cierre del paquete para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b011-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="2b011-238">En CI/CD y otros escenarios, en los que no desearía cambiar las dependencias de paquetes en el camino, puede hacerlo estableciendo `lockedmode` en `true`:</span><span class="sxs-lookup"><span data-stu-id="2b011-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="2b011-239">En dotnet.exe,ejecute:</span><span class="sxs-lookup"><span data-stu-id="2b011-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="2b011-240">En msbuild.exe, ejecute:</span><span class="sxs-lookup"><span data-stu-id="2b011-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="2b011-241">También puede establecer esta propiedad MSBuild condicional en su archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="2b011-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="2b011-242">Si el modo de bloqueo es `true`, la restauración restaurará los paquetes exactos tal como se incluyen en el archivo de bloqueo o producirá un error si actualizó las dependencias de paquetes definidas para el proyecto tras crearse el archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="2b011-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="2b011-243">Haga que el archivo de bloqueo forme parte de su repositorio de origen</span><span class="sxs-lookup"><span data-stu-id="2b011-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="2b011-244">Si crea una aplicación, un archivo ejecutable y el proyecto en cuestión se encuentra al principio de la cadena de dependencia, inserte el archivo de bloqueo en el repositorio de código fuente para que NuGet pueda hacer uso de este durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="2b011-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="2b011-245">Sin embargo, si su proyecto es un proyecto de biblioteca que no envía o un proyecto de código común del que dependen otros proyectos, **no debe** insertar en el repositorio el archivo de bloqueo como parte de su código fuente.</span><span class="sxs-lookup"><span data-stu-id="2b011-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="2b011-246">No hay nada malo en el hecho de conservar el archivo de bloqueo, pero es posible que no se usen las dependencias de paquetes bloqueadas para el proyecto de código común, como se muestra en el archivo de bloqueo, durante la restauración/creación de un proyecto que depende de este proyecto de código común.</span><span class="sxs-lookup"><span data-stu-id="2b011-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="2b011-247">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2b011-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="2b011-248">Si `ProjectA` tiene una dependencia de la versión `2.0.0` de `PackageX` y también hace referencia a `ProjectB`, que depende de la versión `1.0.0` de `PackageX`, el archivo de bloqueo para `ProjectB` mostrará una dependencia de la versión `1.0.0` de `PackageX`.</span><span class="sxs-lookup"><span data-stu-id="2b011-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="2b011-249">Sin embargo, al compilarse `ProjectA`, su archivo de bloqueo contendrá una dependencia de la versión **`2.0.0`** de `PackageX` y **no** en la `1.0.0`, como se muestra en el archivo de bloqueo para `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="2b011-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="2b011-250">Por tanto, el archivo de bloqueo de un proyecto de código común tiene poco que decir sobre los paquetes resueltos para los proyectos que dependen de él.</span><span class="sxs-lookup"><span data-stu-id="2b011-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="2b011-251">Extensibilidad del archivo de bloqueo</span><span class="sxs-lookup"><span data-stu-id="2b011-251">Lock file extensibility</span></span>

<span data-ttu-id="2b011-252">Puede controlar diversos comportamientos de la restauración con el archivo de bloqueo como se describe a continuación:</span><span class="sxs-lookup"><span data-stu-id="2b011-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="2b011-253">Opción NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="2b011-253">NuGet.exe option</span></span> | <span data-ttu-id="2b011-254">Opción dotnet</span><span class="sxs-lookup"><span data-stu-id="2b011-254">dotnet option</span></span> | <span data-ttu-id="2b011-255">Opción equivalente de MSBuild</span><span class="sxs-lookup"><span data-stu-id="2b011-255">MSBuild equivalent option</span></span> | <span data-ttu-id="2b011-256">Descripción</span><span class="sxs-lookup"><span data-stu-id="2b011-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="2b011-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="2b011-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="2b011-258">Opta por el uso de un archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="2b011-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="2b011-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="2b011-259">RestoreLockedMode</span></span> | <span data-ttu-id="2b011-260">Habilita el modo de bloqueo para la restauración.</span><span class="sxs-lookup"><span data-stu-id="2b011-260">Enables locked mode for restore.</span></span> <span data-ttu-id="2b011-261">Esto resulta útil en escenarios de CI/CD donde se necesitan compilaciones repetibles.</span><span class="sxs-lookup"><span data-stu-id="2b011-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="2b011-262">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="2b011-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="2b011-263">Esta opción es útil con los paquetes con la versión flotante definida en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b011-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="2b011-264">De forma predeterminada, la restauración de NuGet no actualizará la versión del paquete automáticamente tras cada restauración a menos que la ejecute con esta opción.</span><span class="sxs-lookup"><span data-stu-id="2b011-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="2b011-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="2b011-265">NuGetLockFilePath</span></span> | <span data-ttu-id="2b011-266">Define una ubicación del archivo de bloqueo personalizada para un proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b011-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="2b011-267">De forma predeterminada, NuGet admite `packages.lock.json` en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="2b011-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="2b011-268">Si tiene varios proyectos en el mismo directorio, NuGet admite el archivo de bloqueo específico del proyecto `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="2b011-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
