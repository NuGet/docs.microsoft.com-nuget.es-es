---
title: PackageReference de NuGet en archivos de proyecto de Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0+ y VS2017"
keywords: Dependencias de paquetes de NuGet, referencias de paquetes, archivos de proyecto, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c8fc9e558557af444d9a35ace36d043a5f6382a7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="ba890-104">Referencias del paquete (PackageReference) en archivos de proyecto</span><span class="sxs-lookup"><span data-stu-id="ba890-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="ba890-105">Las referencias de paquetes, mediante el nodo `PackageReference`, le permiten administrar las dependencias de NuGet directamente dentro de los archivos de proyecto, en lugar de necesitar un archivo `packages.config` o `project.json` independiente.</span><span class="sxs-lookup"><span data-stu-id="ba890-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="ba890-106">Este método no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.Config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en [Configuración del comportamiento de NuGet](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ba890-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="ba890-107">Actualmente, las referencias de paquetes solo se admiten en Visual Studio 2017 para los proyectos de .NET Core, .NET Standard y UWP que tengan como destino Windows 10 Build 15063 (Creators Update).</span><span class="sxs-lookup"><span data-stu-id="ba890-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="ba890-108">El enfoque `PackageReference` le permite usar condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras agrupaciones.</span><span class="sxs-lookup"><span data-stu-id="ba890-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="ba890-109">También le proporciona un control específico sobre las dependencias y el flujo de contenido.</span><span class="sxs-lookup"><span data-stu-id="ba890-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="ba890-110">En términos de comportamiento y de [resolución de dependencias](Dependency-Resolution.md), es lo mismo que usar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ba890-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it is the same as using `project.json`.</span></span>

<span data-ttu-id="ba890-111">Para más información sobre la integración de MSBuild con referencias de paquetes en los archivos de proyecto, vea [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="ba890-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="ba890-112">Agregar una PackageReference</span><span class="sxs-lookup"><span data-stu-id="ba890-112">Adding a PackageReference</span></span>

<span data-ttu-id="ba890-113">Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="ba890-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="ba890-114">Controlar la versión de una dependencia</span><span class="sxs-lookup"><span data-stu-id="ba890-114">Controlling dependency version</span></span>

<span data-ttu-id="ba890-115">La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config` o `project.json`:</span><span class="sxs-lookup"><span data-stu-id="ba890-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ba890-116">En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).</span><span class="sxs-lookup"><span data-stu-id="ba890-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="ba890-117">Versiones flotantes</span><span class="sxs-lookup"><span data-stu-id="ba890-117">Floating Versions</span></span>

<span data-ttu-id="ba890-118">Las [versiones flotantes](../consume-packages/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="ba890-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="ba890-119">Controlar los recursos de dependencias</span><span class="sxs-lookup"><span data-stu-id="ba890-119">Controlling dependency assets</span></span>

<span data-ttu-id="ba890-120">Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete.</span><span class="sxs-lookup"><span data-stu-id="ba890-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="ba890-121">En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="ba890-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ba890-122">Las siguientes etiquetas de metadatos controlan los recursos de dependencia:</span><span class="sxs-lookup"><span data-stu-id="ba890-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="ba890-123">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="ba890-123">Tag</span></span> | <span data-ttu-id="ba890-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="ba890-124">Description</span></span> | <span data-ttu-id="ba890-125">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="ba890-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba890-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="ba890-126">IncludeAssets</span></span> | <span data-ttu-id="ba890-127">Se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="ba890-127">These assets will be consumed</span></span> | <span data-ttu-id="ba890-128">todo</span><span class="sxs-lookup"><span data-stu-id="ba890-128">all</span></span> |
| <span data-ttu-id="ba890-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="ba890-129">ExcludeAssets</span></span> | <span data-ttu-id="ba890-130">No se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="ba890-130">These assets will not be consumed</span></span> | <span data-ttu-id="ba890-131">ninguna</span><span class="sxs-lookup"><span data-stu-id="ba890-131">none</span></span> | 
| <span data-ttu-id="ba890-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="ba890-132">PrivateAssets</span></span> | <span data-ttu-id="ba890-133">Estos recursos se consumirán, pero no irán al proyecto principal</span><span class="sxs-lookup"><span data-stu-id="ba890-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="ba890-134">archivos de contenido; analizadores; compilación</span><span class="sxs-lookup"><span data-stu-id="ba890-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="ba890-135">A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:</span><span class="sxs-lookup"><span data-stu-id="ba890-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="ba890-136">Valor</span><span class="sxs-lookup"><span data-stu-id="ba890-136">Value</span></span> | <span data-ttu-id="ba890-137">Descripción</span><span class="sxs-lookup"><span data-stu-id="ba890-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="ba890-138">compile</span><span class="sxs-lookup"><span data-stu-id="ba890-138">compile</span></span> | <span data-ttu-id="ba890-139">Contenido de la carpeta `lib`</span><span class="sxs-lookup"><span data-stu-id="ba890-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="ba890-140">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="ba890-140">runtime</span></span> | <span data-ttu-id="ba890-141">Contenido de la carpeta `runtime`</span><span class="sxs-lookup"><span data-stu-id="ba890-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="ba890-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="ba890-142">contentFiles</span></span> | <span data-ttu-id="ba890-143">Contenido de la carpeta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="ba890-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="ba890-144">compilación</span><span class="sxs-lookup"><span data-stu-id="ba890-144">build</span></span> | <span data-ttu-id="ba890-145">Propiedades y destinos de la carpeta `build`</span><span class="sxs-lookup"><span data-stu-id="ba890-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="ba890-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="ba890-146">analyzers</span></span> | <span data-ttu-id="ba890-147">Analizadores de .NET</span><span class="sxs-lookup"><span data-stu-id="ba890-147">.NET analyzers</span></span> |
| <span data-ttu-id="ba890-148">nativas</span><span class="sxs-lookup"><span data-stu-id="ba890-148">native</span></span> | <span data-ttu-id="ba890-149">Contenido de la carpeta `native`</span><span class="sxs-lookup"><span data-stu-id="ba890-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="ba890-150">ninguna</span><span class="sxs-lookup"><span data-stu-id="ba890-150">none</span></span> | <span data-ttu-id="ba890-151">No se usa ninguno de los anteriores.</span><span class="sxs-lookup"><span data-stu-id="ba890-151">None of the above are used.</span></span> |
| <span data-ttu-id="ba890-152">todo</span><span class="sxs-lookup"><span data-stu-id="ba890-152">all</span></span> | <span data-ttu-id="ba890-153">Todo lo anterior (excepto `none`)</span><span class="sxs-lookup"><span data-stu-id="ba890-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="ba890-154">En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="ba890-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="ba890-155">Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="ba890-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="ba890-156">Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="ba890-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="ba890-157">AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.</span><span class="sxs-lookup"><span data-stu-id="ba890-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="ba890-158">Agregar una condición PackageReference</span><span class="sxs-lookup"><span data-stu-id="ba890-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="ba890-159">Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="ba890-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="ba890-160">Pero actualmente solo se admite la variable `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="ba890-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="ba890-161">Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`.</span><span class="sxs-lookup"><span data-stu-id="ba890-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="ba890-162">En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria.</span><span class="sxs-lookup"><span data-stu-id="ba890-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="ba890-163">Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="ba890-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ba890-164">Un paquete creado con este proyecto mostrará que Newtonsoft.json se incluye como dependencia únicamente para un destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="ba890-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="ba890-166">Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:</span><span class="sxs-lookup"><span data-stu-id="ba890-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
