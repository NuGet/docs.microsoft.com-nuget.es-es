---
title: pack y restore de NuGet como destinos de MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
keywords: "NuGet y MSBuild, destino del comando pack de NuGet, destino de restauración de NuGet"
ms.reviewer:
- karann-msft
ms.openlocfilehash: 6c488f49e12b014e7bd197d57041745387a4d7b4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="bc3bb-104">pack y restore de NuGet como destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="bc3bb-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="bc3bb-105">*NuGet 4.0 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="bc3bb-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="bc3bb-106">Con el formato PackageReference, NuGet 4.0 + puede almacenar metadatos de todos los manifiestos directamente dentro de un archivo de proyecto, en lugar de usar una `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="bc3bb-107">Con MSBuild 15.1 y versiones posteriores, NuGet es también un ciudadano de MSBuild de primera clase con los destinos `pack` y `restore` como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="bc3bb-108">Estos destinos permiten trabajar con NuGet como lo haría con cualquier otra tarea o destino de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="bc3bb-109">(Para NuGet 3.x y versiones anteriores, los comandos [pack](../tools/cli-ref-pack.md) y [restore](../tools/cli-ref-restore.md) se usan a través de la CLI de NuGet en su lugar).</span><span class="sxs-lookup"><span data-stu-id="bc3bb-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="bc3bb-110">Orden de compilación de destinos</span><span class="sxs-lookup"><span data-stu-id="bc3bb-110">Target build order</span></span>

<span data-ttu-id="bc3bb-111">Dado que `pack` y `restore` son destinos de MSBuild, puede tener acceso a ellos para mejorar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="bc3bb-112">Por ejemplo, supongamos que quiere copiar el paquete en un recurso compartido de red después de empaquetarlo.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="bc3bb-113">Puede hacer esto si agrega lo siguiente al archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="bc3bb-114">De forma similar, puede escribir una tarea de MSBuild, su propio destino y usar propiedades de NuGet en la tarea de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="bc3bb-115">Destino de pack</span><span class="sxs-lookup"><span data-stu-id="bc3bb-115">pack target</span></span>

<span data-ttu-id="bc3bb-116">Cuando se usa el módulo de destino, es decir, `msbuild /t:pack`, MSBuild dibuja sus entradas del archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="bc3bb-117">En la tabla siguiente se describe las propiedades de MSBuild que se pueden agregar a un archivo de proyecto dentro de la primera `<PropertyGroup>` nodo.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="bc3bb-118">Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="bc3bb-119">Para mayor comodidad, la tabla se organiza por la propiedad equivalente en un [archivo `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="bc3bb-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="bc3bb-120">Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="bc3bb-121">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="bc3bb-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="bc3bb-122">Propiedad de MSBuild</span><span class="sxs-lookup"><span data-stu-id="bc3bb-122">MSBuild Property</span></span> | <span data-ttu-id="bc3bb-123">Default</span><span class="sxs-lookup"><span data-stu-id="bc3bb-123">Default</span></span> | <span data-ttu-id="bc3bb-124">Notas</span><span class="sxs-lookup"><span data-stu-id="bc3bb-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="bc3bb-125">Id.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-125">Id</span></span> | <span data-ttu-id="bc3bb-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="bc3bb-126">PackageId</span></span> | <span data-ttu-id="bc3bb-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="bc3bb-127">AssemblyName</span></span> | <span data-ttu-id="bc3bb-128">$(NombreDeEnsamblado) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="bc3bb-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="bc3bb-129">Versión</span><span class="sxs-lookup"><span data-stu-id="bc3bb-129">Version</span></span> | <span data-ttu-id="bc3bb-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="bc3bb-130">PackageVersion</span></span> | <span data-ttu-id="bc3bb-131">Versión</span><span class="sxs-lookup"><span data-stu-id="bc3bb-131">Version</span></span> | <span data-ttu-id="bc3bb-132">Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="bc3bb-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="bc3bb-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="bc3bb-133">VersionPrefix</span></span> | <span data-ttu-id="bc3bb-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="bc3bb-134">PackageVersionPrefix</span></span> | <span data-ttu-id="bc3bb-135">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-135">empty</span></span> | <span data-ttu-id="bc3bb-136">Establecer PackageVersion sobrescribe PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="bc3bb-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="bc3bb-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="bc3bb-137">VersionSuffix</span></span> | <span data-ttu-id="bc3bb-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="bc3bb-138">PackageVersionSuffix</span></span> | <span data-ttu-id="bc3bb-139">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-139">empty</span></span> | <span data-ttu-id="bc3bb-140">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="bc3bb-141">Establecer PackageVersion sobrescribe PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="bc3bb-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="bc3bb-142">Authors</span><span class="sxs-lookup"><span data-stu-id="bc3bb-142">Authors</span></span> | <span data-ttu-id="bc3bb-143">Authors</span><span class="sxs-lookup"><span data-stu-id="bc3bb-143">Authors</span></span> | <span data-ttu-id="bc3bb-144">Nombre del usuario actual</span><span class="sxs-lookup"><span data-stu-id="bc3bb-144">Username of the current user</span></span> | |
| <span data-ttu-id="bc3bb-145">Owners</span><span class="sxs-lookup"><span data-stu-id="bc3bb-145">Owners</span></span> | <span data-ttu-id="bc3bb-146">N/D</span><span class="sxs-lookup"><span data-stu-id="bc3bb-146">N/A</span></span> | <span data-ttu-id="bc3bb-147">No está presente en el archivo NuSpec</span><span class="sxs-lookup"><span data-stu-id="bc3bb-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="bc3bb-148">Title</span><span class="sxs-lookup"><span data-stu-id="bc3bb-148">Title</span></span> | <span data-ttu-id="bc3bb-149">Title</span><span class="sxs-lookup"><span data-stu-id="bc3bb-149">Title</span></span> | <span data-ttu-id="bc3bb-150">El identificador de paquete</span><span class="sxs-lookup"><span data-stu-id="bc3bb-150">The PackageId</span></span>| |
| <span data-ttu-id="bc3bb-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="bc3bb-151">Description</span></span> | <span data-ttu-id="bc3bb-152">Descripción</span><span class="sxs-lookup"><span data-stu-id="bc3bb-152">Description</span></span> | <span data-ttu-id="bc3bb-153">"Descripción del paquete"</span><span class="sxs-lookup"><span data-stu-id="bc3bb-153">"Package Description"</span></span> | |
| <span data-ttu-id="bc3bb-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="bc3bb-154">Copyright</span></span> | <span data-ttu-id="bc3bb-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="bc3bb-155">Copyright</span></span> | <span data-ttu-id="bc3bb-156">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-156">empty</span></span> | |
| <span data-ttu-id="bc3bb-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="bc3bb-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="bc3bb-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="bc3bb-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="bc3bb-159">False</span><span class="sxs-lookup"><span data-stu-id="bc3bb-159">false</span></span> | |
| <span data-ttu-id="bc3bb-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-160">LicenseUrl</span></span> | <span data-ttu-id="bc3bb-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-161">PackageLicenseUrl</span></span> | <span data-ttu-id="bc3bb-162">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-162">empty</span></span> | |
| <span data-ttu-id="bc3bb-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-163">ProjectUrl</span></span> | <span data-ttu-id="bc3bb-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-164">PackageProjectUrl</span></span> | <span data-ttu-id="bc3bb-165">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-165">empty</span></span> | |
| <span data-ttu-id="bc3bb-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-166">IconUrl</span></span> | <span data-ttu-id="bc3bb-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-167">PackageIconUrl</span></span> | <span data-ttu-id="bc3bb-168">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-168">empty</span></span> | |
| <span data-ttu-id="bc3bb-169">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="bc3bb-169">Tags</span></span> | <span data-ttu-id="bc3bb-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="bc3bb-170">PackageTags</span></span> | <span data-ttu-id="bc3bb-171">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-171">empty</span></span> | <span data-ttu-id="bc3bb-172">Las etiquetas están delimitadas mediante punto y coma.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="bc3bb-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="bc3bb-173">ReleaseNotes</span></span> | <span data-ttu-id="bc3bb-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="bc3bb-174">PackageReleaseNotes</span></span> | <span data-ttu-id="bc3bb-175">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-175">empty</span></span> | |
| <span data-ttu-id="bc3bb-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-176">RepositoryUrl</span></span> | <span data-ttu-id="bc3bb-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-177">RepositoryUrl</span></span> | <span data-ttu-id="bc3bb-178">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-178">empty</span></span> | |
| <span data-ttu-id="bc3bb-179">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="bc3bb-179">RepositoryType</span></span> | <span data-ttu-id="bc3bb-180">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="bc3bb-180">RepositoryType</span></span> | <span data-ttu-id="bc3bb-181">vacío</span><span class="sxs-lookup"><span data-stu-id="bc3bb-181">empty</span></span> | |
| <span data-ttu-id="bc3bb-182">PackageType</span><span class="sxs-lookup"><span data-stu-id="bc3bb-182">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="bc3bb-183">Resumen</span><span class="sxs-lookup"><span data-stu-id="bc3bb-183">Summary</span></span> | <span data-ttu-id="bc3bb-184">No compatibles</span><span class="sxs-lookup"><span data-stu-id="bc3bb-184">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="bc3bb-185">Entradas de destino de pack</span><span class="sxs-lookup"><span data-stu-id="bc3bb-185">pack target inputs</span></span>

- <span data-ttu-id="bc3bb-186">IsPackable</span><span class="sxs-lookup"><span data-stu-id="bc3bb-186">IsPackable</span></span>
- <span data-ttu-id="bc3bb-187">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="bc3bb-187">PackageVersion</span></span>
- <span data-ttu-id="bc3bb-188">PackageId</span><span class="sxs-lookup"><span data-stu-id="bc3bb-188">PackageId</span></span>
- <span data-ttu-id="bc3bb-189">Authors</span><span class="sxs-lookup"><span data-stu-id="bc3bb-189">Authors</span></span>
- <span data-ttu-id="bc3bb-190">Descripción</span><span class="sxs-lookup"><span data-stu-id="bc3bb-190">Description</span></span>
- <span data-ttu-id="bc3bb-191">Copyright</span><span class="sxs-lookup"><span data-stu-id="bc3bb-191">Copyright</span></span>
- <span data-ttu-id="bc3bb-192">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="bc3bb-192">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="bc3bb-193">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="bc3bb-193">DevelopmentDependency</span></span>
- <span data-ttu-id="bc3bb-194">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-194">PackageLicenseUrl</span></span>
- <span data-ttu-id="bc3bb-195">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-195">PackageProjectUrl</span></span>
- <span data-ttu-id="bc3bb-196">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-196">PackageIconUrl</span></span>
- <span data-ttu-id="bc3bb-197">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="bc3bb-197">PackageReleaseNotes</span></span>
- <span data-ttu-id="bc3bb-198">PackageTags</span><span class="sxs-lookup"><span data-stu-id="bc3bb-198">PackageTags</span></span>
- <span data-ttu-id="bc3bb-199">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="bc3bb-199">PackageOutputPath</span></span>
- <span data-ttu-id="bc3bb-200">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="bc3bb-200">IncludeSymbols</span></span>
- <span data-ttu-id="bc3bb-201">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="bc3bb-201">IncludeSource</span></span>
- <span data-ttu-id="bc3bb-202">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="bc3bb-202">PackageTypes</span></span>
- <span data-ttu-id="bc3bb-203">IsTool</span><span class="sxs-lookup"><span data-stu-id="bc3bb-203">IsTool</span></span>
- <span data-ttu-id="bc3bb-204">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-204">RepositoryUrl</span></span>
- <span data-ttu-id="bc3bb-205">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="bc3bb-205">RepositoryType</span></span>
- <span data-ttu-id="bc3bb-206">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="bc3bb-206">NoPackageAnalysis</span></span>
- <span data-ttu-id="bc3bb-207">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="bc3bb-207">MinClientVersion</span></span>
- <span data-ttu-id="bc3bb-208">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="bc3bb-208">IncludeBuildOutput</span></span>
- <span data-ttu-id="bc3bb-209">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="bc3bb-209">IncludeContentInPack</span></span>
- <span data-ttu-id="bc3bb-210">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="bc3bb-210">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="bc3bb-211">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="bc3bb-211">ContentTargetFolders</span></span>
- <span data-ttu-id="bc3bb-212">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="bc3bb-212">NuspecFile</span></span>
- <span data-ttu-id="bc3bb-213">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="bc3bb-213">NuspecBasePath</span></span>
- <span data-ttu-id="bc3bb-214">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="bc3bb-214">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="bc3bb-215">Escenarios de pack</span><span class="sxs-lookup"><span data-stu-id="bc3bb-215">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="bc3bb-216">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="bc3bb-216">PackageIconUrl</span></span>

<span data-ttu-id="bc3bb-217">Como parte del cambio para el [Problema 2582 de NuGet](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` se cambiará en última instancia por `PackageIconUri` y puede ser una ruta de acceso relativa a un archivo de icono que se incluirá en la raíz del paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-217">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="bc3bb-218">Ensamblados de salida</span><span class="sxs-lookup"><span data-stu-id="bc3bb-218">Output assemblies</span></span>

<span data-ttu-id="bc3bb-219">`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-219">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="bc3bb-220">Los archivos de salida que se copian dependen de lo que proporciona MSBuild desde el destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-220">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="bc3bb-221">Hay dos propiedades de MSBuild que se pueden usar en el archivo de proyecto o la línea de comandos para controlar dónde van los ensamblados de salida:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-221">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="bc3bb-222">`IncludeBuildOutput`: un valor booleano que determina si los ensamblados de salida de compilación deben incluirse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-222">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="bc3bb-223">`BuildOutputTargetFolder`: especifica la carpeta en la que se deben colocar los ensamblados de salida.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-223">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="bc3bb-224">Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-224">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="bc3bb-225">Referencias de paquete</span><span class="sxs-lookup"><span data-stu-id="bc3bb-225">Package references</span></span>

<span data-ttu-id="bc3bb-226">Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="bc3bb-226">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="bc3bb-227">Referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="bc3bb-227">Project to project references</span></span>

<span data-ttu-id="bc3bb-228">Las referencias entre proyectos se consideran de forma predeterminada como referencias de paquetes NuGet, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-228">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="bc3bb-229">También puede agregar los metadatos siguientes a la referencia de proyecto:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-229">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="bc3bb-230">Inclusión de contenido en un paquete</span><span class="sxs-lookup"><span data-stu-id="bc3bb-230">Including content in a package</span></span>

<span data-ttu-id="bc3bb-231">Para incluir contenido, agregue metadatos adicionales al elemento `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-231">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="bc3bb-232">De forma predeterminada todos los elementos de tipo "Content" se incluyen en el paquete a menos que los reemplace con entradas como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-232">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="bc3bb-233">De forma predeterminada, todo el contenido se agrega a la raíz de la carpeta `content` y `contentFiles\any\<target_framework>` dentro de un paquete y se conserva la estructura de carpetas relativa, a menos que se especifique una ruta de acceso de paquete:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-233">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="bc3bb-234">Si quiere copiar todo el contenido a una carpeta raíz determinada (en lugar de `content` y `contentFiles`), puede usar la propiedad `ContentTargetFolders` de MSBuild, cuyo valor predeterminado es "content;contentFiles", pero que se puede establecer en cualquier otro nombre de carpeta.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-234">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="bc3bb-235">Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-235">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="bc3bb-236">`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-236">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="bc3bb-237">Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-237">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="bc3bb-238">Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-238">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="bc3bb-239">También hay una propiedad `$(IncludeContentInPack)` de MSBuild, cuyo valor predeterminado es `true`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-239">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="bc3bb-240">Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-240">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="bc3bb-241">Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen ```<PackageCopyToOutput>``` y ```<PackageFlatten>```, que establece los valores ```CopyToOutput``` y ```Flatten``` en la entrada ```contentFiles``` del archivo nuspec de salida.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-241">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="bc3bb-242">Además de elementos de contenido, el `<Pack>` y `<PackagePath>` metadatos también pueden establecerse en los archivos con una acción de compilación de compilación, EmbeddedResource, ApplicationDefinition, página, recursos, pantalla de presentación, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o ninguno.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-242">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="bc3bb-243">Para que el comando pack anexe el nombre de archivo a la ruta de acceso del paquete cuando se usan patrones globales, la ruta de acceso del paquete debe terminar con el carácter separador de carpeta; en caso contrario, la ruta de acceso del paquete se trata como la ruta de acceso completa, incluido el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-243">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="bc3bb-244">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="bc3bb-244">IncludeSymbols</span></span>

<span data-ttu-id="bc3bb-245">Cuando se usa `MSBuild /t:pack /p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="bc3bb-245">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="bc3bb-246">Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-246">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="bc3bb-247">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="bc3bb-247">IncludeSource</span></span>

<span data-ttu-id="bc3bb-248">Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-248">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="bc3bb-249">Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-249">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="bc3bb-250">Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-250">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="bc3bb-251">Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-251">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="bc3bb-252">IsTool</span><span class="sxs-lookup"><span data-stu-id="bc3bb-252">IsTool</span></span>

<span data-ttu-id="bc3bb-253">Cuando se usa `MSBuild /t:pack /p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-253">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="bc3bb-254">Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-254">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="bc3bb-255">Empaquetado mediante un archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="bc3bb-255">Packing using a .nuspec</span></span>

<span data-ttu-id="bc3bb-256">Puede usar un archivo `.nuspec` para empaquetar el proyecto siempre que tenga un archivo de proyecto para importar `NuGet.Build.Tasks.Pack.targets` para que la tarea de empaquetado se pueda ejecutar.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-256">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="bc3bb-257">Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-257">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="bc3bb-258">`NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-258">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="bc3bb-259">`NuspecProperties`: lista de pares clave=valor separados por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-259">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="bc3bb-260">Debido al funcionamiento del análisis de línea de comandos de MSBuild, se deben especificar varias propiedades como se indica a continuación: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-260">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="bc3bb-261">`NuspecBasePath`: ruta de acceso base para el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-261">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="bc3bb-262">Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-262">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="bc3bb-263">Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-263">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="bc3bb-264">Destino de restore</span><span class="sxs-lookup"><span data-stu-id="bc3bb-264">restore target</span></span>

<span data-ttu-id="bc3bb-265">`MSBuild /t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-265">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="bc3bb-266">Leer todas las referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="bc3bb-266">Read all project to project references</span></span>
1. <span data-ttu-id="bc3bb-267">Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias</span><span class="sxs-lookup"><span data-stu-id="bc3bb-267">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="bc3bb-268">Pasar datos de MSBuild a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="bc3bb-268">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="bc3bb-269">Ejecutar la restauración</span><span class="sxs-lookup"><span data-stu-id="bc3bb-269">Run restore</span></span>
1. <span data-ttu-id="bc3bb-270">Descargar los paquetes</span><span class="sxs-lookup"><span data-stu-id="bc3bb-270">Download packages</span></span>
1. <span data-ttu-id="bc3bb-271">Escribir el archivo de activos, destinos y propiedades</span><span class="sxs-lookup"><span data-stu-id="bc3bb-271">Write assets file, targets, and props</span></span>

### <a name="restore-properties"></a><span data-ttu-id="bc3bb-272">Restaurar las propiedades</span><span class="sxs-lookup"><span data-stu-id="bc3bb-272">Restore properties</span></span>

<span data-ttu-id="bc3bb-273">Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-273">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="bc3bb-274">También se pueden establecer valores desde la línea de comandos mediante el modificador `/p:` (vea los ejemplos siguientes).</span><span class="sxs-lookup"><span data-stu-id="bc3bb-274">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="bc3bb-275">Property</span><span class="sxs-lookup"><span data-stu-id="bc3bb-275">Property</span></span> | <span data-ttu-id="bc3bb-276">Descripción</span><span class="sxs-lookup"><span data-stu-id="bc3bb-276">Description</span></span> |
|--------|--------|
| <span data-ttu-id="bc3bb-277">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="bc3bb-277">RestoreSources</span></span> | <span data-ttu-id="bc3bb-278">Lista delimitada por punto y coma de orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-278">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="bc3bb-279">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="bc3bb-279">RestorePackagesPath</span></span> | <span data-ttu-id="bc3bb-280">Ruta de acceso de la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-280">User packages folder path.</span></span> |
| <span data-ttu-id="bc3bb-281">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="bc3bb-281">RestoreDisableParallel</span></span> | <span data-ttu-id="bc3bb-282">Limitar las descargas a una cada vez.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-282">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="bc3bb-283">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="bc3bb-283">RestoreConfigFile</span></span> | <span data-ttu-id="bc3bb-284">Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-284">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="bc3bb-285">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="bc3bb-285">RestoreNoCache</span></span> | <span data-ttu-id="bc3bb-286">Si es true, evita el uso de la caché web.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-286">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="bc3bb-287">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="bc3bb-287">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="bc3bb-288">Si es true, ignora los orígenes de paquetes que producen errores o faltan.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-288">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="bc3bb-289">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="bc3bb-289">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="bc3bb-290">Ruta de acceso a `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-290">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="bc3bb-291">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="bc3bb-291">RestoreGraphProjectInput</span></span> | <span data-ttu-id="bc3bb-292">Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-292">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="bc3bb-293">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="bc3bb-293">RestoreOutputPath</span></span> | <span data-ttu-id="bc3bb-294">Carpeta de salida, que de forma predeterminada es `obj`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-294">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="bc3bb-295">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="bc3bb-295">Examples</span></span>

<span data-ttu-id="bc3bb-296">Línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-296">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="bc3bb-297">Archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-297">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="bc3bb-298">Restaurar salidas</span><span class="sxs-lookup"><span data-stu-id="bc3bb-298">Restore outputs</span></span>

<span data-ttu-id="bc3bb-299">La restauración crea los archivos siguientes en la carpeta `obj` de compilación:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-299">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="bc3bb-300">Archivo</span><span class="sxs-lookup"><span data-stu-id="bc3bb-300">File</span></span> | <span data-ttu-id="bc3bb-301">Descripción</span><span class="sxs-lookup"><span data-stu-id="bc3bb-301">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="bc3bb-302">Anteriormente `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="bc3bb-302">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="bc3bb-303">Referencias a propiedades de MSBuild incluidas en paquetes</span><span class="sxs-lookup"><span data-stu-id="bc3bb-303">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="bc3bb-304">Referencias a destinos de MSBuild incluidos en paquetes</span><span class="sxs-lookup"><span data-stu-id="bc3bb-304">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="bc3bb-305">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="bc3bb-305">PackageTargetFallback</span></span>

<span data-ttu-id="bc3bb-306">El elemento `PackageTargetFallback` permite especificar un conjunto de destinos compatibles que se usarán al restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-306">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="bc3bb-307">Está diseñado para permitir que los paquetes que usan un [TxM](../reference/target-frameworks.md) de dotnet funcionen con paquetes compatibles que no declaran un TxM de dotnet.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-307">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="bc3bb-308">Es decir, si el proyecto usa el TxM de dotnet, todos los paquetes de los que depende también deben tener un TxM de dotnet, a menos que agregue `<PackageTargetFallback>` al proyecto para permitir que las plataformas que no sean de dotnet sean compatibles con dotnet.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-308">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="bc3bb-309">Por ejemplo, si el proyecto usa el TxM `netstandard1.6` y un paquete dependiente solo contiene `lib/net45/a.dll` y `lib/portable-net45+win81/a.dll`, se producirá un error al compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-309">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="bc3bb-310">Si lo que quiere incluir es el último archivo DLL, puede agregar `PackageTargetFallback` como se indica a continuación para indicar que el archivo DLL `portable-net45+win81` es compatible:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-310">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="bc3bb-311">Para declarar una reserva para todos los destinos del proyecto, excluya el atributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-311">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="bc3bb-312">También puede extender cualquier `PackageTargetFallback` existente mediante la inclusión de `$(PackageTargetFallback)` como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-312">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="bc3bb-313">Reemplazo de una biblioteca desde un gráfico de restauración</span><span class="sxs-lookup"><span data-stu-id="bc3bb-313">Replacing one library from a restore graph</span></span>

<span data-ttu-id="bc3bb-314">Si una restauración agrega el ensamblado equivocado, se puede excluir la opción predeterminada de ese paquete y reemplazarla por una de su propia elección.</span><span class="sxs-lookup"><span data-stu-id="bc3bb-314">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="bc3bb-315">En primer lugar, con una `PackageReference` de nivel superior, excluya todos los activos:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-315">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="bc3bb-316">Después, agregue su propia referencia a la copia local correspondiente del archivo DLL:</span><span class="sxs-lookup"><span data-stu-id="bc3bb-316">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
