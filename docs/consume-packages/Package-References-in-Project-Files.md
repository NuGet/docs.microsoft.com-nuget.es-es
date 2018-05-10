---
title: Formato PackageReference de NuGet (referencias de paquete en archivos de proyecto)
description: Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0 y versiones posteriores, VS2017 y .NET Core 2.0
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="bd2f0-103">Referencias del paquete (PackageReference) en archivos de proyecto</span><span class="sxs-lookup"><span data-stu-id="bd2f0-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="bd2f0-104">Las referencias de paquetes, con el nodo `PackageReference`, administran las dependencias de NuGet directamente en los archivos de proyecto (a diferencia de un archivo `packages.config` independiente).</span><span class="sxs-lookup"><span data-stu-id="bd2f0-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="bd2f0-105">El uso de PackageReference, como así se llama, no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.Config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en [Configuración del comportamiento de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="bd2f0-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="bd2f0-106">Con PackageReference, también puede usar las condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras agrupaciones.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="bd2f0-107">También le proporciona un control específico sobre las dependencias y el flujo de contenido.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="bd2f0-108">(Para saber más, vea [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) (Empaquetado y restauración de NuGet como destinos de MSBuild).</span><span class="sxs-lookup"><span data-stu-id="bd2f0-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="bd2f0-109">De forma predeterminada, PackageReference se usa para proyectos de .NET Core, proyectos de .NET Standard y proyectos de UWP que tengan como destino Windows 10 Build 15063 (Creators Update) y versiones posteriores, con la excepción de los proyectos de UWP en C++.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="bd2f0-110">Los proyectos completos de .NET Framework admiten PackageReference, pero actualmente tienen como valor predeterminado `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="bd2f0-111">Para usar PackageReference, migre las dependencias de `packages.config` al archivo de proyecto y luego quite packages.config.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="bd2f0-112">Agregar una PackageReference</span><span class="sxs-lookup"><span data-stu-id="bd2f0-112">Adding a PackageReference</span></span>

<span data-ttu-id="bd2f0-113">Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="bd2f0-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="bd2f0-114">Controlar la versión de una dependencia</span><span class="sxs-lookup"><span data-stu-id="bd2f0-114">Controlling dependency version</span></span>

<span data-ttu-id="bd2f0-115">La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="bd2f0-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="bd2f0-116">En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).</span><span class="sxs-lookup"><span data-stu-id="bd2f0-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="bd2f0-117">Versiones flotantes</span><span class="sxs-lookup"><span data-stu-id="bd2f0-117">Floating Versions</span></span>

<span data-ttu-id="bd2f0-118">Las [versiones flotantes](../consume-packages/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="bd2f0-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="bd2f0-119">Controlar los recursos de dependencias</span><span class="sxs-lookup"><span data-stu-id="bd2f0-119">Controlling dependency assets</span></span>

<span data-ttu-id="bd2f0-120">Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="bd2f0-121">En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="bd2f0-122">Las siguientes etiquetas de metadatos controlan los recursos de dependencia:</span><span class="sxs-lookup"><span data-stu-id="bd2f0-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="bd2f0-123">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="bd2f0-123">Tag</span></span> | <span data-ttu-id="bd2f0-124">Description</span><span class="sxs-lookup"><span data-stu-id="bd2f0-124">Description</span></span> | <span data-ttu-id="bd2f0-125">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="bd2f0-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd2f0-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="bd2f0-126">IncludeAssets</span></span> | <span data-ttu-id="bd2f0-127">Se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="bd2f0-127">These assets will be consumed</span></span> | <span data-ttu-id="bd2f0-128">todo</span><span class="sxs-lookup"><span data-stu-id="bd2f0-128">all</span></span> |
| <span data-ttu-id="bd2f0-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="bd2f0-129">ExcludeAssets</span></span> | <span data-ttu-id="bd2f0-130">No se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="bd2f0-130">These assets will not be consumed</span></span> | <span data-ttu-id="bd2f0-131">ninguna</span><span class="sxs-lookup"><span data-stu-id="bd2f0-131">none</span></span> |
| <span data-ttu-id="bd2f0-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="bd2f0-132">PrivateAssets</span></span> | <span data-ttu-id="bd2f0-133">Estos recursos se consumirán, pero no irán al proyecto principal</span><span class="sxs-lookup"><span data-stu-id="bd2f0-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="bd2f0-134">archivos de contenido; analizadores; compilación</span><span class="sxs-lookup"><span data-stu-id="bd2f0-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="bd2f0-135">A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:</span><span class="sxs-lookup"><span data-stu-id="bd2f0-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="bd2f0-136">Valor</span><span class="sxs-lookup"><span data-stu-id="bd2f0-136">Value</span></span> | <span data-ttu-id="bd2f0-137">Description</span><span class="sxs-lookup"><span data-stu-id="bd2f0-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="bd2f0-138">compile</span><span class="sxs-lookup"><span data-stu-id="bd2f0-138">compile</span></span> | <span data-ttu-id="bd2f0-139">Contenido de la carpeta `lib` y controla si el proyecto se puede compilar con los ensamblados dentro de la carpeta</span><span class="sxs-lookup"><span data-stu-id="bd2f0-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="bd2f0-140">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="bd2f0-140">runtime</span></span> | <span data-ttu-id="bd2f0-141">Contenido de las carpetas `lib` y `runtimes` y controla si estos ensamblados se copiarán en el directorio de salida de compilación</span><span class="sxs-lookup"><span data-stu-id="bd2f0-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="bd2f0-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="bd2f0-142">contentFiles</span></span> | <span data-ttu-id="bd2f0-143">Contenido de la carpeta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="bd2f0-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="bd2f0-144">compilación</span><span class="sxs-lookup"><span data-stu-id="bd2f0-144">build</span></span> | <span data-ttu-id="bd2f0-145">Propiedades y destinos de la carpeta `build`</span><span class="sxs-lookup"><span data-stu-id="bd2f0-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="bd2f0-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="bd2f0-146">analyzers</span></span> | <span data-ttu-id="bd2f0-147">Analizadores de .NET</span><span class="sxs-lookup"><span data-stu-id="bd2f0-147">.NET analyzers</span></span> |
| <span data-ttu-id="bd2f0-148">nativas</span><span class="sxs-lookup"><span data-stu-id="bd2f0-148">native</span></span> | <span data-ttu-id="bd2f0-149">Contenido de la carpeta `native`</span><span class="sxs-lookup"><span data-stu-id="bd2f0-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="bd2f0-150">ninguna</span><span class="sxs-lookup"><span data-stu-id="bd2f0-150">none</span></span> | <span data-ttu-id="bd2f0-151">No se usa ninguno de los anteriores.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-151">None of the above are used.</span></span> |
| <span data-ttu-id="bd2f0-152">todo</span><span class="sxs-lookup"><span data-stu-id="bd2f0-152">all</span></span> | <span data-ttu-id="bd2f0-153">Todo lo anterior (excepto `none`)</span><span class="sxs-lookup"><span data-stu-id="bd2f0-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="bd2f0-154">En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="bd2f0-155">Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="bd2f0-156">Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="bd2f0-157">AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="bd2f0-158">Agregar una condición PackageReference</span><span class="sxs-lookup"><span data-stu-id="bd2f0-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="bd2f0-159">Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="bd2f0-160">Pero actualmente solo se admite la variable `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="bd2f0-161">Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="bd2f0-162">En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria.</span><span class="sxs-lookup"><span data-stu-id="bd2f0-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="bd2f0-163">Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="bd2f0-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="bd2f0-164">Un paquete creado con este proyecto mostrará que Newtonsoft.json se incluye como dependencia únicamente para un destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="bd2f0-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="bd2f0-166">Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:</span><span class="sxs-lookup"><span data-stu-id="bd2f0-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
