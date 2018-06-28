---
title: Formato PackageReference de NuGet (referencias de paquete en archivos de proyecto)
description: Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0 y versiones posteriores, VS2017 y .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 61f447877459764906cf9a2b88b32a8bc0553689
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817676"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="3cefe-103">Referencias del paquete (PackageReference) en archivos de proyecto</span><span class="sxs-lookup"><span data-stu-id="3cefe-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="3cefe-104">Las referencias de paquetes, con el nodo `PackageReference`, administran las dependencias de NuGet directamente en los archivos de proyecto (a diferencia de un archivo `packages.config` independiente).</span><span class="sxs-lookup"><span data-stu-id="3cefe-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="3cefe-105">El uso de PackageReference, como así se llama, no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.Config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en [Configuración del comportamiento de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3cefe-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="3cefe-106">Con PackageReference, también puede usar las condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras agrupaciones.</span><span class="sxs-lookup"><span data-stu-id="3cefe-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="3cefe-107">También le proporciona un control específico sobre las dependencias y el flujo de contenido.</span><span class="sxs-lookup"><span data-stu-id="3cefe-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="3cefe-108">(Para saber más, vea [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) (Empaquetado y restauración de NuGet como destinos de MSBuild).</span><span class="sxs-lookup"><span data-stu-id="3cefe-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="3cefe-109">De forma predeterminada, PackageReference se usa para proyectos de .NET Core, proyectos de .NET Standard y proyectos de UWP que tengan como destino Windows 10 Build 15063 (Creators Update) y versiones posteriores, con la excepción de los proyectos de UWP en C++.</span><span class="sxs-lookup"><span data-stu-id="3cefe-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="3cefe-110">Los proyectos completos de .NET Framework admiten PackageReference, pero actualmente tienen como valor predeterminado `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="3cefe-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="3cefe-111">Para usar PackageReference, migre las dependencias de `packages.config` al archivo de proyecto y luego quite packages.config.</span><span class="sxs-lookup"><span data-stu-id="3cefe-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="3cefe-112">Agregar una PackageReference</span><span class="sxs-lookup"><span data-stu-id="3cefe-112">Adding a PackageReference</span></span>

<span data-ttu-id="3cefe-113">Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="3cefe-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="3cefe-114">Controlar la versión de una dependencia</span><span class="sxs-lookup"><span data-stu-id="3cefe-114">Controlling dependency version</span></span>

<span data-ttu-id="3cefe-115">La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="3cefe-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="3cefe-116">En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).</span><span class="sxs-lookup"><span data-stu-id="3cefe-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="3cefe-117">Uso de una PackageReference para un proyecto sin PackageReferences</span><span class="sxs-lookup"><span data-stu-id="3cefe-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="3cefe-118">Avanzado: Si no tiene paquetes instalados en un proyecto (ninguna PackageReference en el archivo de proyecto y ningún archivo packages.config), pero quiere que el proyecto se restaure como de estilo PackageReference, puede establecer una propiedad de proyecto RestoreProjectStyle en PackageReference en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="3cefe-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="3cefe-119">Esto puede resultar útil si hace referencia a proyectos de estilo PackageReference (csproj existente o proyectos de estilo SDK).</span><span class="sxs-lookup"><span data-stu-id="3cefe-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="3cefe-120">Esto permitirá que el proyecto haga referencia "de manera transitiva" a los paquetes a los que hacen referencia dichos proyectos.</span><span class="sxs-lookup"><span data-stu-id="3cefe-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="3cefe-121">Versiones flotantes</span><span class="sxs-lookup"><span data-stu-id="3cefe-121">Floating Versions</span></span>

<span data-ttu-id="3cefe-122">Las [versiones flotantes](../consume-packages/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="3cefe-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="3cefe-123">Controlar los recursos de dependencias</span><span class="sxs-lookup"><span data-stu-id="3cefe-123">Controlling dependency assets</span></span>

<span data-ttu-id="3cefe-124">Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete.</span><span class="sxs-lookup"><span data-stu-id="3cefe-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="3cefe-125">En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="3cefe-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="3cefe-126">Las siguientes etiquetas de metadatos controlan los recursos de dependencia:</span><span class="sxs-lookup"><span data-stu-id="3cefe-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="3cefe-127">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="3cefe-127">Tag</span></span> | <span data-ttu-id="3cefe-128">Description</span><span class="sxs-lookup"><span data-stu-id="3cefe-128">Description</span></span> | <span data-ttu-id="3cefe-129">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cefe-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3cefe-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="3cefe-130">IncludeAssets</span></span> | <span data-ttu-id="3cefe-131">Se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="3cefe-131">These assets will be consumed</span></span> | <span data-ttu-id="3cefe-132">todo</span><span class="sxs-lookup"><span data-stu-id="3cefe-132">all</span></span> |
| <span data-ttu-id="3cefe-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="3cefe-133">ExcludeAssets</span></span> | <span data-ttu-id="3cefe-134">No se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="3cefe-134">These assets will not be consumed</span></span> | <span data-ttu-id="3cefe-135">ninguna</span><span class="sxs-lookup"><span data-stu-id="3cefe-135">none</span></span> |
| <span data-ttu-id="3cefe-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="3cefe-136">PrivateAssets</span></span> | <span data-ttu-id="3cefe-137">Estos recursos se consumirán, pero no irán al proyecto principal</span><span class="sxs-lookup"><span data-stu-id="3cefe-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="3cefe-138">archivos de contenido; analizadores; compilación</span><span class="sxs-lookup"><span data-stu-id="3cefe-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="3cefe-139">A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:</span><span class="sxs-lookup"><span data-stu-id="3cefe-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="3cefe-140">Valor</span><span class="sxs-lookup"><span data-stu-id="3cefe-140">Value</span></span> | <span data-ttu-id="3cefe-141">Description</span><span class="sxs-lookup"><span data-stu-id="3cefe-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="3cefe-142">compile</span><span class="sxs-lookup"><span data-stu-id="3cefe-142">compile</span></span> | <span data-ttu-id="3cefe-143">Contenido de la carpeta `lib` y controla si el proyecto se puede compilar con los ensamblados dentro de la carpeta</span><span class="sxs-lookup"><span data-stu-id="3cefe-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="3cefe-144">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="3cefe-144">runtime</span></span> | <span data-ttu-id="3cefe-145">Contenido de las carpetas `lib` y `runtimes` y controla si estos ensamblados se copiarán en el directorio de salida de compilación</span><span class="sxs-lookup"><span data-stu-id="3cefe-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="3cefe-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="3cefe-146">contentFiles</span></span> | <span data-ttu-id="3cefe-147">Contenido de la carpeta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="3cefe-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="3cefe-148">compilación</span><span class="sxs-lookup"><span data-stu-id="3cefe-148">build</span></span> | <span data-ttu-id="3cefe-149">Propiedades y destinos de la carpeta `build`</span><span class="sxs-lookup"><span data-stu-id="3cefe-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="3cefe-150">analyzers</span><span class="sxs-lookup"><span data-stu-id="3cefe-150">analyzers</span></span> | <span data-ttu-id="3cefe-151">Analizadores de .NET</span><span class="sxs-lookup"><span data-stu-id="3cefe-151">.NET analyzers</span></span> |
| <span data-ttu-id="3cefe-152">nativas</span><span class="sxs-lookup"><span data-stu-id="3cefe-152">native</span></span> | <span data-ttu-id="3cefe-153">Contenido de la carpeta `native`</span><span class="sxs-lookup"><span data-stu-id="3cefe-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="3cefe-154">ninguna</span><span class="sxs-lookup"><span data-stu-id="3cefe-154">none</span></span> | <span data-ttu-id="3cefe-155">No se usa ninguno de los anteriores.</span><span class="sxs-lookup"><span data-stu-id="3cefe-155">None of the above are used.</span></span> |
| <span data-ttu-id="3cefe-156">todo</span><span class="sxs-lookup"><span data-stu-id="3cefe-156">all</span></span> | <span data-ttu-id="3cefe-157">Todo lo anterior (excepto `none`)</span><span class="sxs-lookup"><span data-stu-id="3cefe-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="3cefe-158">En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="3cefe-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="3cefe-159">Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="3cefe-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="3cefe-160">Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="3cefe-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="3cefe-161">AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.</span><span class="sxs-lookup"><span data-stu-id="3cefe-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="3cefe-162">Agregar una condición PackageReference</span><span class="sxs-lookup"><span data-stu-id="3cefe-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="3cefe-163">Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="3cefe-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="3cefe-164">Pero actualmente solo se admite la variable `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="3cefe-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="3cefe-165">Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`.</span><span class="sxs-lookup"><span data-stu-id="3cefe-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="3cefe-166">En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria.</span><span class="sxs-lookup"><span data-stu-id="3cefe-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="3cefe-167">Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3cefe-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="3cefe-168">Un paquete creado con este proyecto mostrará que Newtonsoft.json se incluye como dependencia únicamente para un destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="3cefe-168">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="3cefe-170">Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:</span><span class="sxs-lookup"><span data-stu-id="3cefe-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
