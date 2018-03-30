---
title: Formato PackageReference de NuGet (referencias de paquete en archivos de proyecto) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0 y versiones posteriores, VS2017 y .NET Core 2.0
keywords: Dependencias de paquetes NuGet, referencias de paquetes, archivos de proyecto, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99caf371ca1bd85e6af4e879741e3e2caab6e860
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="50d43-104">Referencias del paquete (PackageReference) en archivos de proyecto</span><span class="sxs-lookup"><span data-stu-id="50d43-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="50d43-105">Las referencias de paquetes, con el nodo `PackageReference`, administran las dependencias de NuGet directamente en los archivos de proyecto (a diferencia de un archivo `packages.config` independiente).</span><span class="sxs-lookup"><span data-stu-id="50d43-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="50d43-106">El uso de PackageReference, como así se llama, no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.Config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en [Configuración del comportamiento de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="50d43-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="50d43-107">Con PackageReference, también puede usar las condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras agrupaciones.</span><span class="sxs-lookup"><span data-stu-id="50d43-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="50d43-108">También le proporciona un control específico sobre las dependencias y el flujo de contenido.</span><span class="sxs-lookup"><span data-stu-id="50d43-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="50d43-109">(Para saber más, vea [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) (Empaquetado y restauración de NuGet como destinos de MSBuild).</span><span class="sxs-lookup"><span data-stu-id="50d43-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="50d43-110">De forma predeterminada, PackageReference se usa para proyectos de .NET Core, proyectos de .NET Standard y proyectos de UWP que tengan como destino Windows 10 Build 15063 (Creators Update) y versiones posteriores, con la excepción de los proyectos de UWP en C++.</span><span class="sxs-lookup"><span data-stu-id="50d43-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="50d43-111">Los proyectos completos de .NET Framework admiten PackageReference, pero actualmente tienen como valor predeterminado `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="50d43-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="50d43-112">Para usar PackageReference, migre las dependencias de `packages.config` al archivo de proyecto y luego quite packages.config.</span><span class="sxs-lookup"><span data-stu-id="50d43-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="50d43-113">Agregar una PackageReference</span><span class="sxs-lookup"><span data-stu-id="50d43-113">Adding a PackageReference</span></span>

<span data-ttu-id="50d43-114">Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="50d43-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="50d43-115">Controlar la versión de una dependencia</span><span class="sxs-lookup"><span data-stu-id="50d43-115">Controlling dependency version</span></span>

<span data-ttu-id="50d43-116">La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="50d43-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="50d43-117">En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).</span><span class="sxs-lookup"><span data-stu-id="50d43-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="50d43-118">Versiones flotantes</span><span class="sxs-lookup"><span data-stu-id="50d43-118">Floating Versions</span></span>

<span data-ttu-id="50d43-119">Las [versiones flotantes](../consume-packages/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="50d43-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="50d43-120">Controlar los recursos de dependencias</span><span class="sxs-lookup"><span data-stu-id="50d43-120">Controlling dependency assets</span></span>

<span data-ttu-id="50d43-121">Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete.</span><span class="sxs-lookup"><span data-stu-id="50d43-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="50d43-122">En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="50d43-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="50d43-123">Las siguientes etiquetas de metadatos controlan los recursos de dependencia:</span><span class="sxs-lookup"><span data-stu-id="50d43-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="50d43-124">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="50d43-124">Tag</span></span> | <span data-ttu-id="50d43-125">Description</span><span class="sxs-lookup"><span data-stu-id="50d43-125">Description</span></span> | <span data-ttu-id="50d43-126">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="50d43-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50d43-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="50d43-127">IncludeAssets</span></span> | <span data-ttu-id="50d43-128">Se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="50d43-128">These assets will be consumed</span></span> | <span data-ttu-id="50d43-129">todo</span><span class="sxs-lookup"><span data-stu-id="50d43-129">all</span></span> |
| <span data-ttu-id="50d43-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="50d43-130">ExcludeAssets</span></span> | <span data-ttu-id="50d43-131">No se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="50d43-131">These assets will not be consumed</span></span> | <span data-ttu-id="50d43-132">ninguna</span><span class="sxs-lookup"><span data-stu-id="50d43-132">none</span></span> |
| <span data-ttu-id="50d43-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="50d43-133">PrivateAssets</span></span> | <span data-ttu-id="50d43-134">Estos recursos se consumirán, pero no irán al proyecto principal</span><span class="sxs-lookup"><span data-stu-id="50d43-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="50d43-135">archivos de contenido; analizadores; compilación</span><span class="sxs-lookup"><span data-stu-id="50d43-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="50d43-136">A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:</span><span class="sxs-lookup"><span data-stu-id="50d43-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="50d43-137">Valor</span><span class="sxs-lookup"><span data-stu-id="50d43-137">Value</span></span> | <span data-ttu-id="50d43-138">Description</span><span class="sxs-lookup"><span data-stu-id="50d43-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="50d43-139">compile</span><span class="sxs-lookup"><span data-stu-id="50d43-139">compile</span></span> | <span data-ttu-id="50d43-140">Contenido de la carpeta `lib`</span><span class="sxs-lookup"><span data-stu-id="50d43-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="50d43-141">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="50d43-141">runtime</span></span> | <span data-ttu-id="50d43-142">Contenido de la carpeta `runtimes`</span><span class="sxs-lookup"><span data-stu-id="50d43-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="50d43-143">contentFiles</span><span class="sxs-lookup"><span data-stu-id="50d43-143">contentFiles</span></span> | <span data-ttu-id="50d43-144">Contenido de la carpeta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="50d43-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="50d43-145">compilación</span><span class="sxs-lookup"><span data-stu-id="50d43-145">build</span></span> | <span data-ttu-id="50d43-146">Propiedades y destinos de la carpeta `build`</span><span class="sxs-lookup"><span data-stu-id="50d43-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="50d43-147">analyzers</span><span class="sxs-lookup"><span data-stu-id="50d43-147">analyzers</span></span> | <span data-ttu-id="50d43-148">Analizadores de .NET</span><span class="sxs-lookup"><span data-stu-id="50d43-148">.NET analyzers</span></span> |
| <span data-ttu-id="50d43-149">nativas</span><span class="sxs-lookup"><span data-stu-id="50d43-149">native</span></span> | <span data-ttu-id="50d43-150">Contenido de la carpeta `native`</span><span class="sxs-lookup"><span data-stu-id="50d43-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="50d43-151">ninguna</span><span class="sxs-lookup"><span data-stu-id="50d43-151">none</span></span> | <span data-ttu-id="50d43-152">No se usa ninguno de los anteriores.</span><span class="sxs-lookup"><span data-stu-id="50d43-152">None of the above are used.</span></span> |
| <span data-ttu-id="50d43-153">todo</span><span class="sxs-lookup"><span data-stu-id="50d43-153">all</span></span> | <span data-ttu-id="50d43-154">Todo lo anterior (excepto `none`)</span><span class="sxs-lookup"><span data-stu-id="50d43-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="50d43-155">En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="50d43-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="50d43-156">Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="50d43-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="50d43-157">Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="50d43-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="50d43-158">AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.</span><span class="sxs-lookup"><span data-stu-id="50d43-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="50d43-159">Agregar una condición PackageReference</span><span class="sxs-lookup"><span data-stu-id="50d43-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="50d43-160">Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="50d43-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="50d43-161">Pero actualmente solo se admite la variable `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="50d43-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="50d43-162">Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`.</span><span class="sxs-lookup"><span data-stu-id="50d43-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="50d43-163">En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria.</span><span class="sxs-lookup"><span data-stu-id="50d43-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="50d43-164">Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="50d43-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="50d43-165">Un paquete creado con este proyecto mostrará que Newtonsoft.json se incluye como dependencia únicamente para un destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="50d43-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="50d43-167">Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:</span><span class="sxs-lookup"><span data-stu-id="50d43-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
