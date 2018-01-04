---
title: pack y restore de NuGet como destinos de MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
keywords: "NuGet y MSBuild, destino del comando pack de NuGet, destino de restauración de NuGet"
ms.reviewer: karann-msft
ms.openlocfilehash: def01380e5bc3bf878e72dd437f52cd033641ca5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="3efda-104">pack y restore de NuGet como destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="3efda-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="3efda-105">*NuGet 4.0 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="3efda-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="3efda-106">NuGet 4.0 y versiones posteriores puede trabajar directamente con la información de un archivo `.csproj` sin necesidad de un archivo `.nuspec` o `project.json` independientes.</span><span class="sxs-lookup"><span data-stu-id="3efda-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="3efda-107">Todos los metadatos que se almacenaron previamente en esos archivos de configuración se pueden almacenar directamente en el archivo `.csproj`, como se describe aquí.</span><span class="sxs-lookup"><span data-stu-id="3efda-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="3efda-108">Con MSBuild 15.1 y versiones posteriores, NuGet es también un ciudadano de MSBuild de primera clase con los destinos `pack` y `restore` como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="3efda-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="3efda-109">Estos destinos permiten trabajar con NuGet como lo haría con cualquier otra tarea o destino de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3efda-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="3efda-110">(Para NuGet 3.x y versiones anteriores, los comandos [pack](../tools/cli-ref-pack.md) y [restore](../tools/cli-ref-restore.md) se usan a través de la CLI de NuGet en su lugar).</span><span class="sxs-lookup"><span data-stu-id="3efda-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="3efda-111">En este tema:</span><span class="sxs-lookup"><span data-stu-id="3efda-111">In this topic:</span></span>

- [<span data-ttu-id="3efda-112">Orden de compilación de destinos</span><span class="sxs-lookup"><span data-stu-id="3efda-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="3efda-113">Destino de pack</span><span class="sxs-lookup"><span data-stu-id="3efda-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="3efda-114">Escenarios de pack</span><span class="sxs-lookup"><span data-stu-id="3efda-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="3efda-115">Destino de restore</span><span class="sxs-lookup"><span data-stu-id="3efda-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="3efda-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="3efda-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="3efda-117">Orden de compilación de destinos</span><span class="sxs-lookup"><span data-stu-id="3efda-117">Target build order</span></span>

<span data-ttu-id="3efda-118">Dado que `pack` y `restore` son destinos de MSBuild, puede tener acceso a ellos para mejorar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3efda-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="3efda-119">Por ejemplo, supongamos que quiere copiar el paquete en un recurso compartido de red después de empaquetarlo.</span><span class="sxs-lookup"><span data-stu-id="3efda-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="3efda-120">Puede hacer esto si agrega lo siguiente al archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="3efda-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="3efda-121">De forma similar, puede escribir una tarea de MSBuild, su propio destino y usar propiedades de NuGet en la tarea de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3efda-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="3efda-122">Destino de pack</span><span class="sxs-lookup"><span data-stu-id="3efda-122">pack target</span></span>

<span data-ttu-id="3efda-123">Cuando se usa el destino de pack, es decir `msbuild /t:pack`, MSBuild obtiene sus entradas del archivo `.csproj` en lugar de los archivos `project.json` o `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="3efda-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="3efda-124">En la tabla siguiente se describen las propiedades de MSBuild que se pueden agregar a un archivo `.csproj` dentro del primer nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="3efda-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="3efda-125">Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="3efda-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="3efda-126">Para mayor comodidad, la tabla se organiza por la propiedad equivalente en un [archivo `.nuspec`](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="3efda-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="3efda-127">Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3efda-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="3efda-128">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="3efda-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="3efda-129">Propiedad de MSBuild</span><span class="sxs-lookup"><span data-stu-id="3efda-129">MSBuild Property</span></span> | <span data-ttu-id="3efda-130">Default</span><span class="sxs-lookup"><span data-stu-id="3efda-130">Default</span></span> | <span data-ttu-id="3efda-131">Notas</span><span class="sxs-lookup"><span data-stu-id="3efda-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="3efda-132">Id.</span><span class="sxs-lookup"><span data-stu-id="3efda-132">Id</span></span> | <span data-ttu-id="3efda-133">PackageId</span><span class="sxs-lookup"><span data-stu-id="3efda-133">PackageId</span></span> | <span data-ttu-id="3efda-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="3efda-134">AssemblyName</span></span> | <span data-ttu-id="3efda-135">$(NombreDeEnsamblado) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="3efda-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="3efda-136">Versión</span><span class="sxs-lookup"><span data-stu-id="3efda-136">Version</span></span> | <span data-ttu-id="3efda-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3efda-137">PackageVersion</span></span> | <span data-ttu-id="3efda-138">Versión</span><span class="sxs-lookup"><span data-stu-id="3efda-138">Version</span></span> | <span data-ttu-id="3efda-139">Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="3efda-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="3efda-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3efda-140">VersionPrefix</span></span> | <span data-ttu-id="3efda-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3efda-141">PackageVersionPrefix</span></span> | <span data-ttu-id="3efda-142">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-142">empty</span></span> | <span data-ttu-id="3efda-143">Establecer PackageVersion sobrescribirá PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3efda-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="3efda-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3efda-144">VersionSuffix</span></span> | <span data-ttu-id="3efda-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3efda-145">PackageVersionSuffix</span></span> | <span data-ttu-id="3efda-146">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-146">empty</span></span> | <span data-ttu-id="3efda-147">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3efda-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="3efda-148">Establecer PackageVersion sobrescribirá PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3efda-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="3efda-149">Authors</span><span class="sxs-lookup"><span data-stu-id="3efda-149">Authors</span></span> | <span data-ttu-id="3efda-150">Authors</span><span class="sxs-lookup"><span data-stu-id="3efda-150">Authors</span></span> | <span data-ttu-id="3efda-151">Nombre del usuario actual</span><span class="sxs-lookup"><span data-stu-id="3efda-151">Username of the current user</span></span> | |
| <span data-ttu-id="3efda-152">Owners</span><span class="sxs-lookup"><span data-stu-id="3efda-152">Owners</span></span> | <span data-ttu-id="3efda-153">N/D</span><span class="sxs-lookup"><span data-stu-id="3efda-153">N/A</span></span> | <span data-ttu-id="3efda-154">No está presente en el archivo NuSpec</span><span class="sxs-lookup"><span data-stu-id="3efda-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="3efda-155">Título</span><span class="sxs-lookup"><span data-stu-id="3efda-155">Title</span></span> | <span data-ttu-id="3efda-156">Título</span><span class="sxs-lookup"><span data-stu-id="3efda-156">Title</span></span> | <span data-ttu-id="3efda-157">El identificador de paquete</span><span class="sxs-lookup"><span data-stu-id="3efda-157">The PackageId</span></span>| |
| <span data-ttu-id="3efda-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="3efda-158">Description</span></span> | <span data-ttu-id="3efda-159">Descripción</span><span class="sxs-lookup"><span data-stu-id="3efda-159">Description</span></span> | <span data-ttu-id="3efda-160">"Descripción del paquete"</span><span class="sxs-lookup"><span data-stu-id="3efda-160">"Package Description"</span></span> | |
| <span data-ttu-id="3efda-161">Copyright</span><span class="sxs-lookup"><span data-stu-id="3efda-161">Copyright</span></span> | <span data-ttu-id="3efda-162">Copyright</span><span class="sxs-lookup"><span data-stu-id="3efda-162">Copyright</span></span> | <span data-ttu-id="3efda-163">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-163">empty</span></span> | |
| <span data-ttu-id="3efda-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3efda-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="3efda-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3efda-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="3efda-166">False</span><span class="sxs-lookup"><span data-stu-id="3efda-166">false</span></span> | |
| <span data-ttu-id="3efda-167">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-167">LicenseUrl</span></span> | <span data-ttu-id="3efda-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-168">PackageLicenseUrl</span></span> | <span data-ttu-id="3efda-169">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-169">empty</span></span> | |
| <span data-ttu-id="3efda-170">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-170">ProjectUrl</span></span> | <span data-ttu-id="3efda-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-171">PackageProjectUrl</span></span> | <span data-ttu-id="3efda-172">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-172">empty</span></span> | |
| <span data-ttu-id="3efda-173">IconUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-173">IconUrl</span></span> | <span data-ttu-id="3efda-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-174">PackageIconUrl</span></span> | <span data-ttu-id="3efda-175">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-175">empty</span></span> | |
| <span data-ttu-id="3efda-176">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="3efda-176">Tags</span></span> | <span data-ttu-id="3efda-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3efda-177">PackageTags</span></span> | <span data-ttu-id="3efda-178">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-178">empty</span></span> | <span data-ttu-id="3efda-179">Las etiquetas están delimitadas mediante punto y coma.</span><span class="sxs-lookup"><span data-stu-id="3efda-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="3efda-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3efda-180">ReleaseNotes</span></span> | <span data-ttu-id="3efda-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3efda-181">PackageReleaseNotes</span></span> | <span data-ttu-id="3efda-182">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-182">empty</span></span> | |
| <span data-ttu-id="3efda-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-183">RepositoryUrl</span></span> | <span data-ttu-id="3efda-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-184">RepositoryUrl</span></span> | <span data-ttu-id="3efda-185">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-185">empty</span></span> | |
| <span data-ttu-id="3efda-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3efda-186">RepositoryType</span></span> | <span data-ttu-id="3efda-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3efda-187">RepositoryType</span></span> | <span data-ttu-id="3efda-188">vacío</span><span class="sxs-lookup"><span data-stu-id="3efda-188">empty</span></span> | |
| <span data-ttu-id="3efda-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="3efda-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="3efda-190">Resumen</span><span class="sxs-lookup"><span data-stu-id="3efda-190">Summary</span></span> | <span data-ttu-id="3efda-191">No compatibles</span><span class="sxs-lookup"><span data-stu-id="3efda-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="3efda-192">Entradas de destino de pack</span><span class="sxs-lookup"><span data-stu-id="3efda-192">pack target inputs</span></span>

- <span data-ttu-id="3efda-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="3efda-193">IsPackable</span></span>
- <span data-ttu-id="3efda-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3efda-194">PackageVersion</span></span>
- <span data-ttu-id="3efda-195">PackageId</span><span class="sxs-lookup"><span data-stu-id="3efda-195">PackageId</span></span>
- <span data-ttu-id="3efda-196">Authors</span><span class="sxs-lookup"><span data-stu-id="3efda-196">Authors</span></span>
- <span data-ttu-id="3efda-197">Descripción</span><span class="sxs-lookup"><span data-stu-id="3efda-197">Description</span></span>
- <span data-ttu-id="3efda-198">Copyright</span><span class="sxs-lookup"><span data-stu-id="3efda-198">Copyright</span></span>
- <span data-ttu-id="3efda-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3efda-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="3efda-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="3efda-200">DevelopmentDependency</span></span>
- <span data-ttu-id="3efda-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="3efda-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-202">PackageProjectUrl</span></span>
- <span data-ttu-id="3efda-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-203">PackageIconUrl</span></span>
- <span data-ttu-id="3efda-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3efda-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="3efda-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3efda-205">PackageTags</span></span>
- <span data-ttu-id="3efda-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="3efda-206">PackageOutputPath</span></span>
- <span data-ttu-id="3efda-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3efda-207">IncludeSymbols</span></span>
- <span data-ttu-id="3efda-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3efda-208">IncludeSource</span></span>
- <span data-ttu-id="3efda-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="3efda-209">PackageTypes</span></span>
- <span data-ttu-id="3efda-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="3efda-210">IsTool</span></span>
- <span data-ttu-id="3efda-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-211">RepositoryUrl</span></span>
- <span data-ttu-id="3efda-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3efda-212">RepositoryType</span></span>
- <span data-ttu-id="3efda-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="3efda-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="3efda-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="3efda-214">MinClientVersion</span></span>
- <span data-ttu-id="3efda-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3efda-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="3efda-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="3efda-216">IncludeContentInPack</span></span>
- <span data-ttu-id="3efda-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="3efda-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="3efda-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="3efda-218">ContentTargetFolders</span></span>
- <span data-ttu-id="3efda-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="3efda-219">NuspecFile</span></span>
- <span data-ttu-id="3efda-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="3efda-220">NuspecBasePath</span></span>
- <span data-ttu-id="3efda-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="3efda-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="3efda-222">Escenarios de pack</span><span class="sxs-lookup"><span data-stu-id="3efda-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="3efda-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3efda-223">PackageIconUrl</span></span>

<span data-ttu-id="3efda-224">Como parte del cambio para el [Problema 2582 de NuGet](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` se cambiará en última instancia por `PackageIconUri` y puede ser una ruta de acceso relativa a un archivo de icono que se incluirá en la raíz del paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="3efda-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="3efda-225">Ensamblados de salida</span><span class="sxs-lookup"><span data-stu-id="3efda-225">Output assemblies</span></span>

<span data-ttu-id="3efda-226">`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`.</span><span class="sxs-lookup"><span data-stu-id="3efda-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="3efda-227">Los archivos de salida que se copian dependen de lo que proporciona MSBuild desde el destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="3efda-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="3efda-228">Hay dos propiedades de MSBuild que se pueden usar en el archivo de proyecto o la línea de comandos para controlar dónde van los ensamblados de salida:</span><span class="sxs-lookup"><span data-stu-id="3efda-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="3efda-229">`IncludeBuildOutput`: un valor booleano que determina si los ensamblados de salida de compilación deben incluirse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="3efda-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="3efda-230">`BuildOutputTargetFolder`: especifica la carpeta en la que se deben colocar los ensamblados de salida.</span><span class="sxs-lookup"><span data-stu-id="3efda-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="3efda-231">Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.</span><span class="sxs-lookup"><span data-stu-id="3efda-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="3efda-232">Referencias de paquete</span><span class="sxs-lookup"><span data-stu-id="3efda-232">Package references</span></span>

<span data-ttu-id="3efda-233">Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="3efda-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="3efda-234">Referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="3efda-234">Project to project references</span></span>

<span data-ttu-id="3efda-235">Las referencias entre proyectos se consideran de forma predeterminada como referencias de paquetes NuGet, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3efda-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="3efda-236">También puede agregar los metadatos siguientes a la referencia de proyecto:</span><span class="sxs-lookup"><span data-stu-id="3efda-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="3efda-237">Inclusión de contenido en un paquete</span><span class="sxs-lookup"><span data-stu-id="3efda-237">Including content in a package</span></span>

<span data-ttu-id="3efda-238">Para incluir contenido, agregue metadatos adicionales al elemento `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="3efda-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="3efda-239">De forma predeterminada todos los elementos de tipo "Content" se incluyen en el paquete a menos que los reemplace con entradas como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3efda-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="3efda-240">De forma predeterminada, todo el contenido se agrega a la raíz de la carpeta `content` y `contentFiles\any\<target_framework>` dentro de un paquete y se conserva la estructura de carpetas relativa, a menos que se especifique una ruta de acceso de paquete:</span><span class="sxs-lookup"><span data-stu-id="3efda-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="3efda-241">Si quiere copiar todo el contenido a una carpeta raíz determinada (en lugar de `content` y `contentFiles`), puede usar la propiedad `ContentTargetFolders` de MSBuild, cuyo valor predeterminado es "content;contentFiles", pero que se puede establecer en cualquier otro nombre de carpeta.</span><span class="sxs-lookup"><span data-stu-id="3efda-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="3efda-242">Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="3efda-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="3efda-243">`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="3efda-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="3efda-244">Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="3efda-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="3efda-245">Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:</span><span class="sxs-lookup"><span data-stu-id="3efda-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="3efda-246">También hay una propiedad `$(IncludeContentInPack)` de MSBuild, cuyo valor predeterminado es `true`.</span><span class="sxs-lookup"><span data-stu-id="3efda-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="3efda-247">Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="3efda-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="3efda-248">Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen ```<PackageCopyToOutput>``` y ```<PackageFlatten>```, que establece los valores ```CopyToOutput``` y ```Flatten``` en la entrada ```contentFiles``` del archivo nuspec de salida.</span><span class="sxs-lookup"><span data-stu-id="3efda-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="3efda-249">Además de los elementos Content, los metadatos `<Pack>` y `<PackagePath>` también se pueden establecer en archivos con una acción de compilación Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="3efda-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="3efda-250">Para que el comando pack anexe el nombre de archivo a la ruta de acceso del paquete cuando se usan patrones globales, la ruta de acceso del paquete debe terminar con el carácter separador de carpeta; en caso contrario, la ruta de acceso del paquete se trata como la ruta de acceso completa, incluido el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="3efda-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="3efda-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3efda-251">IncludeSymbols</span></span>

<span data-ttu-id="3efda-252">Cuando se usa `MSBuild /t:pack /p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="3efda-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="3efda-253">Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="3efda-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="3efda-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3efda-254">IncludeSource</span></span>

<span data-ttu-id="3efda-255">Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="3efda-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="3efda-256">Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="3efda-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="3efda-257">Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.</span><span class="sxs-lookup"><span data-stu-id="3efda-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="3efda-258">Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="3efda-258">If a file of type Compile, is outside the project folder, then it is just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="3efda-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="3efda-259">IsTool</span></span>

<span data-ttu-id="3efda-260">Cuando se usa `MSBuild /t:pack /p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="3efda-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="3efda-261">Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="3efda-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="3efda-262">Empaquetado mediante un archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="3efda-262">Packing using a .nuspec</span></span>

<span data-ttu-id="3efda-263">Puede usar un archivo `.nuspec` para empaquetar el proyecto siempre que tenga un archivo de proyecto para importar `NuGet.Build.Tasks.Pack.targets` para que la tarea de empaquetado se pueda ejecutar.</span><span class="sxs-lookup"><span data-stu-id="3efda-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="3efda-264">Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="3efda-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="3efda-265">`NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.</span><span class="sxs-lookup"><span data-stu-id="3efda-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="3efda-266">`NuspecProperties`: lista de pares clave=valor separados por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="3efda-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="3efda-267">Debido al funcionamiento del análisis de línea de comandos de MSBuild, se deben especificar varias propiedades como se indica a continuación: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="3efda-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="3efda-268">`NuspecBasePath`: ruta de acceso base para el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="3efda-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="3efda-269">Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="3efda-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3efda-270">Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="3efda-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="3efda-271">Destino de restore</span><span class="sxs-lookup"><span data-stu-id="3efda-271">restore target</span></span>

<span data-ttu-id="3efda-272">`MSBuild /t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3efda-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="3efda-273">Leer todas las referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="3efda-273">Read all project to project references</span></span>
1. <span data-ttu-id="3efda-274">Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias</span><span class="sxs-lookup"><span data-stu-id="3efda-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="3efda-275">Pasar datos de MSBuild a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="3efda-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="3efda-276">Ejecutar la restauración</span><span class="sxs-lookup"><span data-stu-id="3efda-276">Run restore</span></span>
1. <span data-ttu-id="3efda-277">Descargar los paquetes</span><span class="sxs-lookup"><span data-stu-id="3efda-277">Download packages</span></span>
1. <span data-ttu-id="3efda-278">Escribir el archivo de activos, destinos y propiedades</span><span class="sxs-lookup"><span data-stu-id="3efda-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="3efda-279">Restaurar las propiedades</span><span class="sxs-lookup"><span data-stu-id="3efda-279">Restore properties</span></span>

<span data-ttu-id="3efda-280">Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="3efda-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="3efda-281">También se pueden establecer valores desde la línea de comandos mediante el modificador `/p:` (vea los ejemplos siguientes).</span><span class="sxs-lookup"><span data-stu-id="3efda-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="3efda-282">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3efda-282">Property</span></span> | <span data-ttu-id="3efda-283">Descripción</span><span class="sxs-lookup"><span data-stu-id="3efda-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="3efda-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="3efda-284">RestoreSources</span></span> | <span data-ttu-id="3efda-285">Lista delimitada por punto y coma de orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="3efda-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="3efda-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="3efda-286">RestorePackagesPath</span></span> | <span data-ttu-id="3efda-287">Ruta de acceso de la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="3efda-287">User packages folder path.</span></span> |
| <span data-ttu-id="3efda-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="3efda-288">RestoreDisableParallel</span></span> | <span data-ttu-id="3efda-289">Limitar las descargas a una cada vez.</span><span class="sxs-lookup"><span data-stu-id="3efda-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="3efda-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="3efda-290">RestoreConfigFile</span></span> | <span data-ttu-id="3efda-291">Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="3efda-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="3efda-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="3efda-292">RestoreNoCache</span></span> | <span data-ttu-id="3efda-293">Si es true, evita el uso de la caché web.</span><span class="sxs-lookup"><span data-stu-id="3efda-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="3efda-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="3efda-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="3efda-295">Si es true, ignora los orígenes de paquetes que producen errores o faltan.</span><span class="sxs-lookup"><span data-stu-id="3efda-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="3efda-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="3efda-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="3efda-297">Ruta de acceso a `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="3efda-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="3efda-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="3efda-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="3efda-299">Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="3efda-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="3efda-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="3efda-300">RestoreOutputPath</span></span> | <span data-ttu-id="3efda-301">Carpeta de salida, que de forma predeterminada es `obj`.</span><span class="sxs-lookup"><span data-stu-id="3efda-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="3efda-302">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="3efda-302">**Examples**</span></span>

<span data-ttu-id="3efda-303">Línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="3efda-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="3efda-304">Archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="3efda-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="3efda-305">Restaurar salidas</span><span class="sxs-lookup"><span data-stu-id="3efda-305">Restore outputs</span></span>

<span data-ttu-id="3efda-306">La restauración crea los archivos siguientes en la carpeta `obj` de compilación:</span><span class="sxs-lookup"><span data-stu-id="3efda-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="3efda-307">Archivo</span><span class="sxs-lookup"><span data-stu-id="3efda-307">File</span></span> | <span data-ttu-id="3efda-308">Descripción</span><span class="sxs-lookup"><span data-stu-id="3efda-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="3efda-309">Anteriormente `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="3efda-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="3efda-310">Referencias a propiedades de MSBuild incluidas en paquetes</span><span class="sxs-lookup"><span data-stu-id="3efda-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="3efda-311">Referencias a destinos de MSBuild incluidos en paquetes</span><span class="sxs-lookup"><span data-stu-id="3efda-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="3efda-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="3efda-312">PackageTargetFallback</span></span> 

<span data-ttu-id="3efda-313">El elemento `PackageTargetFallback` permite especificar un conjunto de destinos compatibles que se usarán al restaurar los paquetes (el equivalente de [`imports` en `project.json`](../schema/project-json.md#imports)).</span><span class="sxs-lookup"><span data-stu-id="3efda-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="3efda-314">Está diseñado para permitir que los paquetes que usan un [TxM](../schema/target-frameworks.md) de dotnet funcionen con paquetes compatibles que no declaran un TxM de dotnet.</span><span class="sxs-lookup"><span data-stu-id="3efda-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="3efda-315">Es decir, si el proyecto usa el TxM de dotnet, todos los paquetes de los que depende también deben tener un TxM de dotnet, a menos que agregue `<PackageTargetFallback>` al proyecto para permitir que las plataformas que no sean de dotnet sean compatibles con dotnet.</span><span class="sxs-lookup"><span data-stu-id="3efda-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="3efda-316">Por ejemplo, si el proyecto usa el TxM `netstandard1.6` y un paquete dependiente solo contiene `lib/net45/a.dll` y `lib/portable-net45+win81/a.dll`, se producirá un error al compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3efda-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="3efda-317">Si lo que quiere incluir es el último archivo DLL, puede agregar `PackageTargetFallback` como se indica a continuación para indicar que el archivo DLL `portable-net45+win81` es compatible:</span><span class="sxs-lookup"><span data-stu-id="3efda-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="3efda-318">Para declarar una reserva para todos los destinos del proyecto, excluya el atributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="3efda-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="3efda-319">También puede extender cualquier `PackageTargetFallback` existente mediante la inclusión de `$(PackageTargetFallback)` como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="3efda-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="3efda-320">Reemplazo de una biblioteca desde un gráfico de restauración</span><span class="sxs-lookup"><span data-stu-id="3efda-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="3efda-321">Si una restauración agrega el ensamblado equivocado, se puede excluir la opción predeterminada de ese paquete y reemplazarla por una de su propia elección.</span><span class="sxs-lookup"><span data-stu-id="3efda-321">If a restore is bringing the wrong assembly, it is possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="3efda-322">En primer lugar, con una `PackageReference` de nivel superior, excluya todos los activos:</span><span class="sxs-lookup"><span data-stu-id="3efda-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="3efda-323">Después, agregue su propia referencia a la copia local correspondiente del archivo DLL:</span><span class="sxs-lookup"><span data-stu-id="3efda-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
