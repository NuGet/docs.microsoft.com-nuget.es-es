---
title: Formato PackageReference de NuGet (referencias de paquete en archivos de proyecto)
description: Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0 y versiones posteriores, VS2017 y .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: d4f0177183ee3edf595c4ce10d1f26cbaca5755d
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453577"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="46cb4-103">Referencias del paquete (PackageReference) en archivos de proyecto</span><span class="sxs-lookup"><span data-stu-id="46cb4-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="46cb4-104">Las referencias de paquetes, con el nodo `PackageReference`, administran las dependencias de NuGet directamente en los archivos de proyecto (a diferencia de un archivo `packages.config` independiente).</span><span class="sxs-lookup"><span data-stu-id="46cb4-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="46cb4-105">El uso de PackageReference, como así se llama, no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en [Configuración del comportamiento de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="46cb4-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="46cb4-106">Con PackageReference, también puede usar las condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras agrupaciones.</span><span class="sxs-lookup"><span data-stu-id="46cb4-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="46cb4-107">También le proporciona un control específico sobre las dependencias y el flujo de contenido.</span><span class="sxs-lookup"><span data-stu-id="46cb4-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="46cb4-108">(Para saber más, vea [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) (Empaquetado y restauración de NuGet como destinos de MSBuild).</span><span class="sxs-lookup"><span data-stu-id="46cb4-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="46cb4-109">De forma predeterminada, PackageReference se usa para proyectos de .NET Core, proyectos de .NET Standard y proyectos de UWP que tengan como destino Windows 10 Build 15063 (Creators Update) y versiones posteriores, con la excepción de los proyectos de UWP en C++.</span><span class="sxs-lookup"><span data-stu-id="46cb4-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="46cb4-110">Los proyectos de .NET Framework admiten PackageReference, pero actualmente tienen como valor predeterminado `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-110">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="46cb4-111">Para usar PackageReference, migre las dependencias de `packages.config` al archivo de proyecto y luego quite packages.config.</span><span class="sxs-lookup"><span data-stu-id="46cb4-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="46cb4-112">Agregar una PackageReference</span><span class="sxs-lookup"><span data-stu-id="46cb4-112">Adding a PackageReference</span></span>

<span data-ttu-id="46cb4-113">Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="46cb4-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="46cb4-114">Controlar la versión de una dependencia</span><span class="sxs-lookup"><span data-stu-id="46cb4-114">Controlling dependency version</span></span>

<span data-ttu-id="46cb4-115">La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="46cb4-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="46cb4-116">En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).</span><span class="sxs-lookup"><span data-stu-id="46cb4-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="46cb4-117">Uso de una PackageReference para un proyecto sin PackageReferences</span><span class="sxs-lookup"><span data-stu-id="46cb4-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="46cb4-118">Avanzado: Si no tiene paquetes instalados en un proyecto (ninguna PackageReference en el archivo de proyecto y ningún archivo packages.config), pero quiere que el proyecto se restaure como de estilo PackageReference, puede establecer una propiedad de proyecto RestoreProjectStyle en PackageReference en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="46cb4-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="46cb4-119">Esto puede resultar útil si hace referencia a proyectos de estilo PackageReference (csproj existente o proyectos de estilo SDK).</span><span class="sxs-lookup"><span data-stu-id="46cb4-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="46cb4-120">Esto permitirá que el proyecto haga referencia "de manera transitiva" a los paquetes a los que hacen referencia dichos proyectos.</span><span class="sxs-lookup"><span data-stu-id="46cb4-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="46cb4-121">Versiones flotantes</span><span class="sxs-lookup"><span data-stu-id="46cb4-121">Floating Versions</span></span>

<span data-ttu-id="46cb4-122">Las [versiones flotantes](../consume-packages/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="46cb4-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="46cb4-123">Controlar los recursos de dependencias</span><span class="sxs-lookup"><span data-stu-id="46cb4-123">Controlling dependency assets</span></span>

<span data-ttu-id="46cb4-124">Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete.</span><span class="sxs-lookup"><span data-stu-id="46cb4-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="46cb4-125">En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="46cb4-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="46cb4-126">Las siguientes etiquetas de metadatos controlan los recursos de dependencia:</span><span class="sxs-lookup"><span data-stu-id="46cb4-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="46cb4-127">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="46cb4-127">Tag</span></span> | <span data-ttu-id="46cb4-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="46cb4-128">Description</span></span> | <span data-ttu-id="46cb4-129">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="46cb4-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="46cb4-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="46cb4-130">IncludeAssets</span></span> | <span data-ttu-id="46cb4-131">Se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="46cb4-131">These assets will be consumed</span></span> | <span data-ttu-id="46cb4-132">todo</span><span class="sxs-lookup"><span data-stu-id="46cb4-132">all</span></span> |
| <span data-ttu-id="46cb4-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="46cb4-133">ExcludeAssets</span></span> | <span data-ttu-id="46cb4-134">No se consumirán estos recursos</span><span class="sxs-lookup"><span data-stu-id="46cb4-134">These assets will not be consumed</span></span> | <span data-ttu-id="46cb4-135">ninguna</span><span class="sxs-lookup"><span data-stu-id="46cb4-135">none</span></span> |
| <span data-ttu-id="46cb4-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="46cb4-136">PrivateAssets</span></span> | <span data-ttu-id="46cb4-137">Estos recursos se consumirán, pero no irán al proyecto principal</span><span class="sxs-lookup"><span data-stu-id="46cb4-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="46cb4-138">archivos de contenido; analizadores; compilación</span><span class="sxs-lookup"><span data-stu-id="46cb4-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="46cb4-139">A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:</span><span class="sxs-lookup"><span data-stu-id="46cb4-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="46cb4-140">Valor</span><span class="sxs-lookup"><span data-stu-id="46cb4-140">Value</span></span> | <span data-ttu-id="46cb4-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="46cb4-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="46cb4-142">compile</span><span class="sxs-lookup"><span data-stu-id="46cb4-142">compile</span></span> | <span data-ttu-id="46cb4-143">Contenido de la carpeta `lib` y controla si el proyecto se puede compilar con los ensamblados dentro de la carpeta</span><span class="sxs-lookup"><span data-stu-id="46cb4-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="46cb4-144">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="46cb4-144">runtime</span></span> | <span data-ttu-id="46cb4-145">Contenido de las carpetas `lib` y `runtimes` y controla si estos ensamblados se copiarán en el directorio de salida de compilación</span><span class="sxs-lookup"><span data-stu-id="46cb4-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="46cb4-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="46cb4-146">contentFiles</span></span> | <span data-ttu-id="46cb4-147">Contenido de la carpeta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="46cb4-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="46cb4-148">compilación</span><span class="sxs-lookup"><span data-stu-id="46cb4-148">build</span></span> | <span data-ttu-id="46cb4-149">Propiedades y destinos de la carpeta `build`</span><span class="sxs-lookup"><span data-stu-id="46cb4-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="46cb4-150">analyzers</span><span class="sxs-lookup"><span data-stu-id="46cb4-150">analyzers</span></span> | <span data-ttu-id="46cb4-151">Analizadores de .NET</span><span class="sxs-lookup"><span data-stu-id="46cb4-151">.NET analyzers</span></span> |
| <span data-ttu-id="46cb4-152">nativas</span><span class="sxs-lookup"><span data-stu-id="46cb4-152">native</span></span> | <span data-ttu-id="46cb4-153">Contenido de la carpeta `native`</span><span class="sxs-lookup"><span data-stu-id="46cb4-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="46cb4-154">ninguna</span><span class="sxs-lookup"><span data-stu-id="46cb4-154">none</span></span> | <span data-ttu-id="46cb4-155">No se usa ninguno de los anteriores.</span><span class="sxs-lookup"><span data-stu-id="46cb4-155">None of the above are used.</span></span> |
| <span data-ttu-id="46cb4-156">todo</span><span class="sxs-lookup"><span data-stu-id="46cb4-156">all</span></span> | <span data-ttu-id="46cb4-157">Todo lo anterior (excepto `none`)</span><span class="sxs-lookup"><span data-stu-id="46cb4-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="46cb4-158">En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="46cb4-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="46cb4-159">Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal.</span><span class="sxs-lookup"><span data-stu-id="46cb4-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="46cb4-160">Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="46cb4-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="46cb4-161">AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.</span><span class="sxs-lookup"><span data-stu-id="46cb4-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="46cb4-162">Agregar una condición PackageReference</span><span class="sxs-lookup"><span data-stu-id="46cb4-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="46cb4-163">Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="46cb4-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="46cb4-164">Pero actualmente solo se admite la variable `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="46cb4-165">Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="46cb4-166">En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria.</span><span class="sxs-lookup"><span data-stu-id="46cb4-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="46cb4-167">Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="46cb4-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="46cb4-168">Un paquete creado con este proyecto mostrará que Newtonsoft.Json se incluye como dependencia únicamente para un destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="46cb4-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="46cb4-170">Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:</span><span class="sxs-lookup"><span data-stu-id="46cb4-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="46cb4-171">Cargando las dependencias</span><span class="sxs-lookup"><span data-stu-id="46cb4-171">Locking dependencies</span></span>
<span data-ttu-id="46cb4-172">*Esta característica está disponible con NuGet **4.9** o superior y con Visual Studio 2017 **15.9 Preview 5** o superior.*</span><span class="sxs-lookup"><span data-stu-id="46cb4-172">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9 Preview 5** or above.*</span></span>

<span data-ttu-id="46cb4-173">La entrada a la restauración de NuGet es un conjunto de referencias de paquete del archivo del proyecto (dependencias de nivel superior o directas) y la salida es un cierre completo de todas las dependencias de paquetes, incluidas las dependencias transitivas.</span><span class="sxs-lookup"><span data-stu-id="46cb4-173">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="46cb4-174">NuGet siempre intenta producir el mismo cierre completo de dependencias de paquetes si no ha cambiado la lista PackageReference de entrada.</span><span class="sxs-lookup"><span data-stu-id="46cb4-174">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="46cb4-175">Sin embargo, hay algunos escenarios en los que no se puede hacer.</span><span class="sxs-lookup"><span data-stu-id="46cb4-175">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="46cb4-176">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="46cb4-176">For example:</span></span>

* <span data-ttu-id="46cb4-177">Al usar versiones flotantes como `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-177">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="46cb4-178">Aunque la intención aquí es hacer flotante la última versión de todas las restauraciones de paquetes, hay escenarios en los que los usuarios necesitan que el gráfico se bloquee hacia una versión más reciente determinada y hacen flotante una versión posterior, en caso de estar disponible, en un gesto explícito.</span><span class="sxs-lookup"><span data-stu-id="46cb4-178">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="46cb4-179">Se publica una versión más reciente del paquete que coincide con los requisitos de la versión PackageReference.</span><span class="sxs-lookup"><span data-stu-id="46cb4-179">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="46cb4-180">P. ej.,</span><span class="sxs-lookup"><span data-stu-id="46cb4-180">E.g.</span></span> 

  * <span data-ttu-id="46cb4-181">Día 1: si especificó `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, pero las versiones disponibles en los repositorios NuGet eran 4.1.0, 4.2.0 y 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="46cb4-181">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="46cb4-182">En este caso, NuGet habría llevado a cabo la resolución de la versión 4.1.0 (la versión mínima más cercana)</span><span class="sxs-lookup"><span data-stu-id="46cb4-182">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="46cb4-183">Día 2: se publica la versión 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="46cb4-183">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="46cb4-184">Ahora, NuGet encontrará la coincidencia exacta e iniciará la resolución de la versión 4.0.0</span><span class="sxs-lookup"><span data-stu-id="46cb4-184">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="46cb4-185">Se quita una versión del paquete especificada del repositorio.</span><span class="sxs-lookup"><span data-stu-id="46cb4-185">A given package version is removed from the repository.</span></span> <span data-ttu-id="46cb4-186">Aunque nuget.org no permite la eliminación de paquetes, no todos los repositorios de paquetes tienen estas restricciones.</span><span class="sxs-lookup"><span data-stu-id="46cb4-186">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="46cb4-187">Esto da lugar a la búsqueda por parte de NuGet de la mejor coincidencia cuando no puede llevar a cabo la resolución de la versión eliminada.</span><span class="sxs-lookup"><span data-stu-id="46cb4-187">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="46cb4-188">Habilitación del archivo de bloqueo</span><span class="sxs-lookup"><span data-stu-id="46cb4-188">Enabling lock file</span></span>
<span data-ttu-id="46cb4-189">A fin de mantener el cierre completo de dependencias de paquetes, puede participar en la característica del archivo de bloqueo estableciendo la propiedad MSBuild `RestorePackagesWithLockFile` para su proyecto:</span><span class="sxs-lookup"><span data-stu-id="46cb4-189">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="46cb4-190">Si se establece esta propiedad, la restauración de NuGet generará un archivo de bloqueo: archivo `packages.lock.json` del directorio raíz del proyecto que incluye todas las dependencias de paquetes.</span><span class="sxs-lookup"><span data-stu-id="46cb4-190">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="46cb4-191">Una vez que un proyecto tiene el archivo `packages.lock.json` en su directorio raíz, el archivo de bloqueo siempre se usa con la restauración incluso si no se establece la propiedad `RestorePackagesWithLockFile`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-191">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="46cb4-192">Así pues, otra forma de participar en esta característica consiste en crear un archivo `packages.lock.json` en blanco ficticio en el directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="46cb4-192">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="46cb4-193">Comportamiento `restore` con el archivo de bloqueo</span><span class="sxs-lookup"><span data-stu-id="46cb4-193">`restore` behavior with lock file</span></span>
<span data-ttu-id="46cb4-194">Si un archivo de bloqueo está presente para el proyecto, NuGet usa este archivo de bloqueo para ejecutar `restore`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-194">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="46cb4-195">NuGet realiza una rápida comprobación para ver si hubo algún cambio en las dependencias de paquetes tal como se mencionó en el archivo del proyecto (o archivos de los proyectos dependientes) y, en caso de no haber ningún cambio, simplemente restaura los paquetes mencionados en el archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="46cb4-195">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="46cb4-196">No hay ninguna reevaluación de dependencias de paquetes.</span><span class="sxs-lookup"><span data-stu-id="46cb4-196">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="46cb4-197">Si NuGet detecta un cambio en las dependencias definidas tal como se menciona en los archivos del proyecto, volverá a evaluar el gráfico del paquete y actualizará el archivo de bloqueo para reflejar el nuevo cierre del paquete para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="46cb4-197">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="46cb4-198">En CI/CD y otros escenarios, en los que no desearía cambiar las dependencias de paquetes en el camino, puede hacerlo estableciendo `lockedmode` en `true`:</span><span class="sxs-lookup"><span data-stu-id="46cb4-198">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="46cb4-199">En dotnet.exe,ejecute:</span><span class="sxs-lookup"><span data-stu-id="46cb4-199">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="46cb4-200">En msbuild.exe, ejecute:</span><span class="sxs-lookup"><span data-stu-id="46cb4-200">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="46cb4-201">También puede establecer esta propiedad MSBuild condicional en su archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="46cb4-201">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="46cb4-202">Si el modo de bloqueo es `true`, la restauración restaurará los paquetes exactos tal como se incluyen en el archivo de bloqueo o producirá un error si actualizó las dependencias de paquetes definidas para el proyecto tras crearse el archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="46cb4-202">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="46cb4-203">Haga que el archivo de bloqueo forme parte de su repositorio de origen</span><span class="sxs-lookup"><span data-stu-id="46cb4-203">Make lock file part of your source repository</span></span>
<span data-ttu-id="46cb4-204">Si crea una aplicación, un archivo ejecutable y el proyecto en cuestión se encuentra al final de la cadena de dependencia, inserte el archivo de bloqueo en el repositorio de código fuente para que NuGet pueda hacer uso de este durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="46cb4-204">If you are building an application, an executable and the project in question is at the end of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="46cb4-205">Sin embargo, si su proyecto es un proyecto de biblioteca que no envía o un proyecto de código común del que dependen otros proyectos, **no debe** insertar en el repositorio el archivo de bloqueo como parte de su código fuente.</span><span class="sxs-lookup"><span data-stu-id="46cb4-205">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="46cb4-206">No hay nada malo en el hecho de conservar el archivo de bloqueo, pero es posible que no se usen las dependencias de paquetes bloqueadas para el proyecto de código común, como se muestra en el archivo de bloqueo, durante la restauración/creación de un proyecto que depende de este proyecto de código común.</span><span class="sxs-lookup"><span data-stu-id="46cb4-206">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="46cb4-207">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="46cb4-207">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="46cb4-208">Si `ProjectA` tiene una dependencia de la versión `2.0.0` de `PackageX` y también hace referencia a `ProjectB`, que depende de la versión `1.0.0` de `PackageX`, el archivo de bloqueo para `ProjectB` mostrará una dependencia de la versión `1.0.0` de `PackageX`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-208">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="46cb4-209">Sin embargo, al crearse `ProjectA`, su archivo de bloqueo contendrá una dependencia de la versión **`2.0.0`** de `PackageX` y **no** `1.0.0` como se muestra en el archivo de bloqueo para `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-209">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="46cb4-210">Por tanto, el archivo de bloqueo de un proyecto de código común tiene poco que decir sobre los paquetes resueltos para los proyectos que dependen de él.</span><span class="sxs-lookup"><span data-stu-id="46cb4-210">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="46cb4-211">Extensibilidad del archivo de bloqueo</span><span class="sxs-lookup"><span data-stu-id="46cb4-211">Lock file extensibility</span></span>
<span data-ttu-id="46cb4-212">Puede controlar diversos comportamientos de la restauración con el archivo de bloqueo como se describe a continuación:</span><span class="sxs-lookup"><span data-stu-id="46cb4-212">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="46cb4-213">Opción</span><span class="sxs-lookup"><span data-stu-id="46cb4-213">Option</span></span> | <span data-ttu-id="46cb4-214">Opción equivalente de MSBuild</span><span class="sxs-lookup"><span data-stu-id="46cb4-214">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="46cb4-215">Uso de arranques del archivo de bloqueo para un proyecto.</span><span class="sxs-lookup"><span data-stu-id="46cb4-215">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="46cb4-216">De forma alternativa, puede establecer la propiedad `RestorePackagesWithLockFile` en el archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="46cb4-216">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="46cb4-217">Habilita el modo de bloqueo para la restauración.</span><span class="sxs-lookup"><span data-stu-id="46cb4-217">Enables locked mode for restore.</span></span> <span data-ttu-id="46cb4-218">Esto resulta útil en los escenarios de CI/CD en los que desea obtener las compilaciones repetibles.</span><span class="sxs-lookup"><span data-stu-id="46cb4-218">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="46cb4-219">También puede ser estableciendo la propiedad MSBuild `RestoreLockedMode` en `true`</span><span class="sxs-lookup"><span data-stu-id="46cb4-219">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="46cb4-220">Esta opción es útil con los paquetes con la versión flotante definida en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="46cb4-220">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="46cb4-221">De forma predeterminada, la restauración de NuGet no actualizará la versión del paquete automáticamente tras cada restauración a menos que ejecute esta con la opción `--force-evaluate`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-221">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="46cb4-222">Define una ubicación del archivo de bloqueo personalizada para un proyecto.</span><span class="sxs-lookup"><span data-stu-id="46cb4-222">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="46cb4-223">Esto también puede lograrse estableciendo la propiedad MSBuild `NuGetLockFilePath`.</span><span class="sxs-lookup"><span data-stu-id="46cb4-223">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="46cb4-224">De forma predeterminada, NuGet admite `packages.lock.json` en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="46cb4-224">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="46cb4-225">Si tiene varios proyectos en el mismo directorio, NuGet admite el archivo de bloqueo específico del proyecto `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="46cb4-225">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
