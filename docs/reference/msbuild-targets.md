---
title: pack y restore de NuGet como destinos de MSBuild
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: b450a5bfa3dcf70056c99a951f51a78845ef8438
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342448"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="39fd2-103">pack y restore de NuGet como destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="39fd2-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="39fd2-104">*NuGet 4.0 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="39fd2-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="39fd2-105">Con el formato PackageReference, NuGet 4.0 + puede almacenar los metadatos de todos los manifiestos directamente en un archivo de proyecto, en lugar de usar un archivo `.nuspec` aparte.</span><span class="sxs-lookup"><span data-stu-id="39fd2-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="39fd2-106">Con MSBuild 15.1 y versiones posteriores, NuGet es también un ciudadano de MSBuild de primera clase con los destinos `pack` y `restore` como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="39fd2-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="39fd2-107">Estos destinos permiten trabajar con NuGet como lo haría con cualquier otra tarea o destino de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="39fd2-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="39fd2-108">(Para NuGet 3.x y versiones anteriores, los comandos [pack](../reference/cli-reference/cli-ref-pack.md) y [restore](../reference/cli-reference/cli-ref-restore.md) se usan a través de la CLI de NuGet en su lugar).</span><span class="sxs-lookup"><span data-stu-id="39fd2-108">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="39fd2-109">Orden de compilación de destinos</span><span class="sxs-lookup"><span data-stu-id="39fd2-109">Target build order</span></span>

<span data-ttu-id="39fd2-110">Dado que `pack` y `restore` son destinos de MSBuild, puede tener acceso a ellos para mejorar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="39fd2-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="39fd2-111">Por ejemplo, supongamos que quiere copiar el paquete en un recurso compartido de red después de empaquetarlo.</span><span class="sxs-lookup"><span data-stu-id="39fd2-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="39fd2-112">Puede hacer esto si agrega lo siguiente al archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="39fd2-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="39fd2-113">De forma similar, puede escribir una tarea de MSBuild, su propio destino y usar propiedades de NuGet en la tarea de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="39fd2-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="39fd2-114">Destino de pack</span><span class="sxs-lookup"><span data-stu-id="39fd2-114">pack target</span></span>

<span data-ttu-id="39fd2-115">En el caso de los proyectos de .net Standard con `msbuild -t:pack` el formato PackageReference, el uso de dibuja entradas del archivo de proyecto para usarlas en la creación de un paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="39fd2-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="39fd2-116">En la tabla siguiente se describen las propiedades de MSBuild que se pueden agregar a un archivo de proyecto en el primer nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="39fd2-117">Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="39fd2-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="39fd2-118">Para mayor comodidad, la tabla se organiza por la propiedad equivalente en un [archivo `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="39fd2-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="39fd2-119">Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="39fd2-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="39fd2-120">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="39fd2-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="39fd2-121">Propiedad de MSBuild</span><span class="sxs-lookup"><span data-stu-id="39fd2-121">MSBuild Property</span></span> | <span data-ttu-id="39fd2-122">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="39fd2-122">Default</span></span> | <span data-ttu-id="39fd2-123">Notas</span><span class="sxs-lookup"><span data-stu-id="39fd2-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="39fd2-124">Id</span><span class="sxs-lookup"><span data-stu-id="39fd2-124">Id</span></span> | <span data-ttu-id="39fd2-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="39fd2-125">PackageId</span></span> | <span data-ttu-id="39fd2-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="39fd2-126">AssemblyName</span></span> | <span data-ttu-id="39fd2-127">$(NombreDeEnsamblado) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="39fd2-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="39fd2-128">`Version`</span><span class="sxs-lookup"><span data-stu-id="39fd2-128">Version</span></span> | <span data-ttu-id="39fd2-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="39fd2-129">PackageVersion</span></span> | <span data-ttu-id="39fd2-130">`Version`</span><span class="sxs-lookup"><span data-stu-id="39fd2-130">Version</span></span> | <span data-ttu-id="39fd2-131">Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="39fd2-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="39fd2-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="39fd2-132">VersionPrefix</span></span> | <span data-ttu-id="39fd2-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="39fd2-133">PackageVersionPrefix</span></span> | <span data-ttu-id="39fd2-134">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-134">empty</span></span> | <span data-ttu-id="39fd2-135">Al establecer PackageVersion se sobrescribe PackageVersionPrefix.</span><span class="sxs-lookup"><span data-stu-id="39fd2-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="39fd2-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="39fd2-136">VersionSuffix</span></span> | <span data-ttu-id="39fd2-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="39fd2-137">PackageVersionSuffix</span></span> | <span data-ttu-id="39fd2-138">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-138">empty</span></span> | <span data-ttu-id="39fd2-139">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="39fd2-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="39fd2-140">Al establecer PackageVersion se sobrescribe PackageVersionSuffix.</span><span class="sxs-lookup"><span data-stu-id="39fd2-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="39fd2-141">Authors</span><span class="sxs-lookup"><span data-stu-id="39fd2-141">Authors</span></span> | <span data-ttu-id="39fd2-142">Authors</span><span class="sxs-lookup"><span data-stu-id="39fd2-142">Authors</span></span> | <span data-ttu-id="39fd2-143">Nombre del usuario actual</span><span class="sxs-lookup"><span data-stu-id="39fd2-143">Username of the current user</span></span> | |
| <span data-ttu-id="39fd2-144">Owners</span><span class="sxs-lookup"><span data-stu-id="39fd2-144">Owners</span></span> | <span data-ttu-id="39fd2-145">N/D</span><span class="sxs-lookup"><span data-stu-id="39fd2-145">N/A</span></span> | <span data-ttu-id="39fd2-146">No está presente en el archivo NuSpec</span><span class="sxs-lookup"><span data-stu-id="39fd2-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="39fd2-147">Título</span><span class="sxs-lookup"><span data-stu-id="39fd2-147">Title</span></span> | <span data-ttu-id="39fd2-148">Título</span><span class="sxs-lookup"><span data-stu-id="39fd2-148">Title</span></span> | <span data-ttu-id="39fd2-149">El identificador de paquete</span><span class="sxs-lookup"><span data-stu-id="39fd2-149">The PackageId</span></span>| |
| <span data-ttu-id="39fd2-150">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="39fd2-150">Description</span></span> | <span data-ttu-id="39fd2-151">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="39fd2-151">Description</span></span> | <span data-ttu-id="39fd2-152">"Descripción del paquete"</span><span class="sxs-lookup"><span data-stu-id="39fd2-152">"Package Description"</span></span> | |
| <span data-ttu-id="39fd2-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="39fd2-153">Copyright</span></span> | <span data-ttu-id="39fd2-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="39fd2-154">Copyright</span></span> | <span data-ttu-id="39fd2-155">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-155">empty</span></span> | |
| <span data-ttu-id="39fd2-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="39fd2-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="39fd2-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="39fd2-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="39fd2-158">false</span><span class="sxs-lookup"><span data-stu-id="39fd2-158">false</span></span> | |
| <span data-ttu-id="39fd2-159">Sin</span><span class="sxs-lookup"><span data-stu-id="39fd2-159">license</span></span> | <span data-ttu-id="39fd2-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="39fd2-160">PackageLicenseExpression</span></span> | <span data-ttu-id="39fd2-161">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-161">empty</span></span> | <span data-ttu-id="39fd2-162">Corresponde a`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="39fd2-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="39fd2-163">Sin</span><span class="sxs-lookup"><span data-stu-id="39fd2-163">license</span></span> | <span data-ttu-id="39fd2-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="39fd2-164">PackageLicenseFile</span></span> | <span data-ttu-id="39fd2-165">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-165">empty</span></span> | <span data-ttu-id="39fd2-166">Se corresponde con `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="39fd2-167">Es posible que deba empaquetar explícitamente el archivo de licencia al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="39fd2-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="39fd2-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-168">LicenseUrl</span></span> | <span data-ttu-id="39fd2-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-169">PackageLicenseUrl</span></span> | <span data-ttu-id="39fd2-170">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-170">empty</span></span> | <span data-ttu-id="39fd2-171">`licenseUrl`está en desuso, use la propiedad PackageLicenseExpression o PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="39fd2-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="39fd2-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-172">ProjectUrl</span></span> | <span data-ttu-id="39fd2-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-173">PackageProjectUrl</span></span> | <span data-ttu-id="39fd2-174">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-174">empty</span></span> | |
| <span data-ttu-id="39fd2-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-175">IconUrl</span></span> | <span data-ttu-id="39fd2-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-176">PackageIconUrl</span></span> | <span data-ttu-id="39fd2-177">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-177">empty</span></span> | |
| <span data-ttu-id="39fd2-178">`Tags`</span><span class="sxs-lookup"><span data-stu-id="39fd2-178">Tags</span></span> | <span data-ttu-id="39fd2-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="39fd2-179">PackageTags</span></span> | <span data-ttu-id="39fd2-180">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-180">empty</span></span> | <span data-ttu-id="39fd2-181">Las etiquetas están delimitadas mediante punto y coma.</span><span class="sxs-lookup"><span data-stu-id="39fd2-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="39fd2-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="39fd2-182">ReleaseNotes</span></span> | <span data-ttu-id="39fd2-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="39fd2-183">PackageReleaseNotes</span></span> | <span data-ttu-id="39fd2-184">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-184">empty</span></span> | |
| <span data-ttu-id="39fd2-185">Repositorio/dirección URL</span><span class="sxs-lookup"><span data-stu-id="39fd2-185">Repository/Url</span></span> | <span data-ttu-id="39fd2-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-186">RepositoryUrl</span></span> | <span data-ttu-id="39fd2-187">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-187">empty</span></span> | <span data-ttu-id="39fd2-188">Dirección URL del repositorio usada para clonar o recuperar el código fuente.</span><span class="sxs-lookup"><span data-stu-id="39fd2-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="39fd2-189">Ejemplo *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="39fd2-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="39fd2-190">Repositorio/tipo</span><span class="sxs-lookup"><span data-stu-id="39fd2-190">Repository/Type</span></span> | <span data-ttu-id="39fd2-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="39fd2-191">RepositoryType</span></span> | <span data-ttu-id="39fd2-192">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-192">empty</span></span> | <span data-ttu-id="39fd2-193">Tipo de repositorio.</span><span class="sxs-lookup"><span data-stu-id="39fd2-193">Repository type.</span></span> <span data-ttu-id="39fd2-194">Ejemplos: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="39fd2-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="39fd2-195">Repositorio/rama</span><span class="sxs-lookup"><span data-stu-id="39fd2-195">Repository/Branch</span></span> | <span data-ttu-id="39fd2-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="39fd2-196">RepositoryBranch</span></span> | <span data-ttu-id="39fd2-197">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-197">empty</span></span> | <span data-ttu-id="39fd2-198">Información opcional de la rama del repositorio.</span><span class="sxs-lookup"><span data-stu-id="39fd2-198">Optional repository branch information.</span></span> <span data-ttu-id="39fd2-199">También se debe especificar *RepositoryUrl* para que se incluya esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="39fd2-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="39fd2-200">Ejemplo: *maestra* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="39fd2-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="39fd2-201">Repositorio/confirmar</span><span class="sxs-lookup"><span data-stu-id="39fd2-201">Repository/Commit</span></span> | <span data-ttu-id="39fd2-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="39fd2-202">RepositoryCommit</span></span> | <span data-ttu-id="39fd2-203">vacío</span><span class="sxs-lookup"><span data-stu-id="39fd2-203">empty</span></span> | <span data-ttu-id="39fd2-204">Confirmación o conjunto de cambios de repositorio opcional para indicar en qué origen se compiló el paquete.</span><span class="sxs-lookup"><span data-stu-id="39fd2-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="39fd2-205">También se debe especificar *RepositoryUrl* para que se incluya esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="39fd2-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="39fd2-206">Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="39fd2-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="39fd2-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="39fd2-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="39fd2-208">Resumen</span><span class="sxs-lookup"><span data-stu-id="39fd2-208">Summary</span></span> | <span data-ttu-id="39fd2-209">No compatible</span><span class="sxs-lookup"><span data-stu-id="39fd2-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="39fd2-210">Entradas de destino de pack</span><span class="sxs-lookup"><span data-stu-id="39fd2-210">pack target inputs</span></span>

- <span data-ttu-id="39fd2-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="39fd2-211">IsPackable</span></span>
- <span data-ttu-id="39fd2-212">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="39fd2-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="39fd2-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="39fd2-213">PackageVersion</span></span>
- <span data-ttu-id="39fd2-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="39fd2-214">PackageId</span></span>
- <span data-ttu-id="39fd2-215">Authors</span><span class="sxs-lookup"><span data-stu-id="39fd2-215">Authors</span></span>
- <span data-ttu-id="39fd2-216">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="39fd2-216">Description</span></span>
- <span data-ttu-id="39fd2-217">Copyright</span><span class="sxs-lookup"><span data-stu-id="39fd2-217">Copyright</span></span>
- <span data-ttu-id="39fd2-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="39fd2-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="39fd2-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="39fd2-219">DevelopmentDependency</span></span>
- <span data-ttu-id="39fd2-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="39fd2-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="39fd2-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="39fd2-221">PackageLicenseFile</span></span>
- <span data-ttu-id="39fd2-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="39fd2-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-223">PackageProjectUrl</span></span>
- <span data-ttu-id="39fd2-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-224">PackageIconUrl</span></span>
- <span data-ttu-id="39fd2-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="39fd2-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="39fd2-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="39fd2-226">PackageTags</span></span>
- <span data-ttu-id="39fd2-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="39fd2-227">PackageOutputPath</span></span>
- <span data-ttu-id="39fd2-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="39fd2-228">IncludeSymbols</span></span>
- <span data-ttu-id="39fd2-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="39fd2-229">IncludeSource</span></span>
- <span data-ttu-id="39fd2-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="39fd2-230">PackageTypes</span></span>
- <span data-ttu-id="39fd2-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="39fd2-231">IsTool</span></span>
- <span data-ttu-id="39fd2-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-232">RepositoryUrl</span></span>
- <span data-ttu-id="39fd2-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="39fd2-233">RepositoryType</span></span>
- <span data-ttu-id="39fd2-234">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="39fd2-234">RepositoryBranch</span></span>
- <span data-ttu-id="39fd2-235">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="39fd2-235">RepositoryCommit</span></span>
- <span data-ttu-id="39fd2-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="39fd2-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="39fd2-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="39fd2-237">MinClientVersion</span></span>
- <span data-ttu-id="39fd2-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="39fd2-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="39fd2-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="39fd2-239">IncludeContentInPack</span></span>
- <span data-ttu-id="39fd2-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="39fd2-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="39fd2-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="39fd2-241">ContentTargetFolders</span></span>
- <span data-ttu-id="39fd2-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="39fd2-242">NuspecFile</span></span>
- <span data-ttu-id="39fd2-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="39fd2-243">NuspecBasePath</span></span>
- <span data-ttu-id="39fd2-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="39fd2-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="39fd2-245">Escenarios de pack</span><span class="sxs-lookup"><span data-stu-id="39fd2-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="39fd2-246">Suprimir dependencias</span><span class="sxs-lookup"><span data-stu-id="39fd2-246">Suppress dependencies</span></span>

<span data-ttu-id="39fd2-247">Para suprimir las dependencias de paquete del paquete NuGet `SuppressDependenciesWhenPacking` generado `true` , establezca en, lo que permitirá omitir todas las dependencias del archivo nupkg generado.</span><span class="sxs-lookup"><span data-stu-id="39fd2-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="39fd2-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="39fd2-248">PackageIconUrl</span></span>

<span data-ttu-id="39fd2-249">Como parte de la modificación del [problema 352](https://github.com/NuGet/Home/issues/352)de NuGet `PackageIconUrl` , se cambiará finalmente `PackageIconUri` a y puede ser una ruta de acceso relativa a un archivo de icono que se incluirá en la raíz del paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="39fd2-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="39fd2-250">Ensamblados de salida</span><span class="sxs-lookup"><span data-stu-id="39fd2-250">Output assemblies</span></span>

<span data-ttu-id="39fd2-251">`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="39fd2-252">Los archivos de salida que se copian dependen de lo que proporciona MSBuild desde el destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="39fd2-253">Hay dos propiedades de MSBuild que se pueden usar en el archivo de proyecto o la línea de comandos para controlar dónde van los ensamblados de salida:</span><span class="sxs-lookup"><span data-stu-id="39fd2-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="39fd2-254">`IncludeBuildOutput`: Un valor booleano que determina si los ensamblados de salida de la compilación deben incluirse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="39fd2-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="39fd2-255">`BuildOutputTargetFolder`: Especifica la carpeta en la que se deben colocar los ensamblados de salida.</span><span class="sxs-lookup"><span data-stu-id="39fd2-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="39fd2-256">Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.</span><span class="sxs-lookup"><span data-stu-id="39fd2-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="39fd2-257">Referencias de paquete</span><span class="sxs-lookup"><span data-stu-id="39fd2-257">Package references</span></span>

<span data-ttu-id="39fd2-258">Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="39fd2-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="39fd2-259">Referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="39fd2-259">Project to project references</span></span>

<span data-ttu-id="39fd2-260">Las referencias entre proyectos se consideran de forma predeterminada como referencias de paquetes NuGet, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="39fd2-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="39fd2-261">También puede agregar los metadatos siguientes a la referencia de proyecto:</span><span class="sxs-lookup"><span data-stu-id="39fd2-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="39fd2-262">Inclusión de contenido en un paquete</span><span class="sxs-lookup"><span data-stu-id="39fd2-262">Including content in a package</span></span>

<span data-ttu-id="39fd2-263">Para incluir contenido, agregue metadatos adicionales al elemento `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="39fd2-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="39fd2-264">De forma predeterminada todos los elementos de tipo "Content" se incluyen en el paquete a menos que los reemplace con entradas como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="39fd2-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="39fd2-265">De forma predeterminada, todo el contenido se agrega a la raíz de la carpeta `content` y `contentFiles\any\<target_framework>` dentro de un paquete y se conserva la estructura de carpetas relativa, a menos que se especifique una ruta de acceso de paquete:</span><span class="sxs-lookup"><span data-stu-id="39fd2-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="39fd2-266">Si quiere copiar todo el contenido a una carpeta raíz determinada (en lugar de `content` y `contentFiles`), puede usar la propiedad `ContentTargetFolders` de MSBuild, cuyo valor predeterminado es "content;contentFiles", pero que se puede establecer en cualquier otro nombre de carpeta.</span><span class="sxs-lookup"><span data-stu-id="39fd2-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="39fd2-267">Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="39fd2-268">`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="39fd2-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="39fd2-269">Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="39fd2-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="39fd2-270">Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:</span><span class="sxs-lookup"><span data-stu-id="39fd2-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="39fd2-271">También hay una propiedad `$(IncludeContentInPack)` de MSBuild, cuyo valor predeterminado es `true`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="39fd2-272">Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="39fd2-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="39fd2-273">Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen ```<PackageCopyToOutput>``` y ```<PackageFlatten>```, que establece los valores ```CopyToOutput``` y ```Flatten``` en la entrada ```contentFiles``` del archivo nuspec de salida.</span><span class="sxs-lookup"><span data-stu-id="39fd2-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="39fd2-274">Además de los elementos Content, los metadatos `<Pack>` y `<PackagePath>` también se pueden establecer en archivos con una acción de compilación Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="39fd2-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="39fd2-275">Para que el comando pack anexe el nombre de archivo a la ruta de acceso del paquete cuando se usan patrones globales, la ruta de acceso del paquete debe terminar con el carácter separador de carpeta; en caso contrario, la ruta de acceso del paquete se trata como la ruta de acceso completa, incluido el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="39fd2-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="39fd2-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="39fd2-276">IncludeSymbols</span></span>

<span data-ttu-id="39fd2-277">Cuando se usa `MSBuild -t:pack -p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="39fd2-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="39fd2-278">Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="39fd2-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="39fd2-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="39fd2-279">IncludeSource</span></span>

<span data-ttu-id="39fd2-280">Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="39fd2-281">Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="39fd2-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="39fd2-282">Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="39fd2-283">Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="39fd2-284">Empaquetado de una expresión de licencia o un archivo de licencia</span><span class="sxs-lookup"><span data-stu-id="39fd2-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="39fd2-285">Cuando se usa una expresión de licencia, se debe usar la propiedad PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="39fd2-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="39fd2-286">[Ejemplo de expresión de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="39fd2-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="39fd2-287">[Obtenga más información sobre las expresiones de licencia y las licencias que acepta NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="39fd2-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="39fd2-288">Al empaquetar un archivo de licencia, debe usar la propiedad PackageLicenseFile para especificar la ruta de acceso del paquete, relativa a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="39fd2-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="39fd2-289">Además, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="39fd2-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="39fd2-290">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="39fd2-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="39fd2-291">[Ejemplo de archivo de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="39fd2-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="39fd2-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="39fd2-292">IsTool</span></span>

<span data-ttu-id="39fd2-293">Cuando se usa `MSBuild -t:pack -p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="39fd2-294">Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="39fd2-295">Empaquetado mediante un archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="39fd2-295">Packing using a .nuspec</span></span>

<span data-ttu-id="39fd2-296">Aunque se recomienda [incluir todas las propiedades](../reference/msbuild-targets.md#pack-target) que suelen estar en el `.nuspec` archivo en el archivo del proyecto, puede optar por usar un `.nuspec` archivo para empaquetar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="39fd2-296">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="39fd2-297">Para un proyecto que no sea de estilo SDK que `PackageReference`use, debe importar `NuGet.Build.Tasks.Pack.targets` para que se pueda ejecutar la tarea del paquete.</span><span class="sxs-lookup"><span data-stu-id="39fd2-297">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="39fd2-298">Todavía es necesario restaurar el proyecto para poder empaquetar un archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="39fd2-298">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="39fd2-299">(Un proyecto de estilo SDK incluye los destinos Pack de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="39fd2-299">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="39fd2-300">El marco de trabajo de destino del archivo de proyecto es irrelevante y no se usa cuando se empaqueta un archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="39fd2-300">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="39fd2-301">Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="39fd2-301">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="39fd2-302">`NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.</span><span class="sxs-lookup"><span data-stu-id="39fd2-302">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="39fd2-303">`NuspecProperties`: lista de pares clave=valor separados por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="39fd2-303">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="39fd2-304">Debido al funcionamiento del análisis de línea de comandos de MSBuild, se deben especificar varias propiedades como se indica a continuación: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-304">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="39fd2-305">`NuspecBasePath`: Ruta de acceso base `.nuspec` del archivo.</span><span class="sxs-lookup"><span data-stu-id="39fd2-305">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="39fd2-306">Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="39fd2-306">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="39fd2-307">Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="39fd2-307">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="39fd2-308">Tenga en cuenta que al empaquetar un archivo nuspec mediante dotnet. exe o MSBuild también se genera el proyecto de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="39fd2-308">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="39fd2-309">Esto se puede evitar pasando ```--no-build``` la propiedad a dotnet. exe, que es el equivalente de la configuración ```<NoBuild>true</NoBuild> ``` en el archivo de proyecto, junto ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` con el valor en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="39fd2-309">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="39fd2-310">Un ejemplo de un archivo *. csproj* para empaquetar un archivo nuspec es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="39fd2-310">An example of a *.csproj* file to pack a nuspec file is:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="39fd2-311">Puntos de extensión avanzados para crear un paquete personalizado</span><span class="sxs-lookup"><span data-stu-id="39fd2-311">Advanced extension points to create customized package</span></span>

<span data-ttu-id="39fd2-312">El `pack` destino proporciona dos puntos de extensión que se ejecutan en la compilación interna específica de la plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="39fd2-312">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="39fd2-313">Los puntos de extensión admiten, incluidos los ensamblados y el contenido específico de la plataforma de destino en un paquete:</span><span class="sxs-lookup"><span data-stu-id="39fd2-313">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="39fd2-314">`TargetsForTfmSpecificBuildOutput`dirigir Se usa para los archivos `lib` dentro de la carpeta o en `BuildOutputTargetFolder`una carpeta especificada mediante.</span><span class="sxs-lookup"><span data-stu-id="39fd2-314">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="39fd2-315">`TargetsForTfmSpecificContentInPackage`dirigir Se usa para archivos fuera `BuildOutputTargetFolder`de.</span><span class="sxs-lookup"><span data-stu-id="39fd2-315">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="39fd2-316">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="39fd2-316">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="39fd2-317">Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificBuildOutput)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="39fd2-317">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="39fd2-318">En el caso de los archivos que necesiten `BuildOutputTargetFolder` entrar en (de forma predeterminada, lib), el destino debe escribir esos `BuildOutputInPackage` archivos en el ItemGroup y establecer los dos valores de metadatos siguientes:</span><span class="sxs-lookup"><span data-stu-id="39fd2-318">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="39fd2-319">`FinalOutputPath`: Ruta de acceso absoluta del archivo; Si no se proporciona, la identidad se utiliza para evaluar la ruta de acceso de origen.</span><span class="sxs-lookup"><span data-stu-id="39fd2-319">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="39fd2-320">`TargetPath`:  Opta Se establece cuando el archivo debe ir a una subcarpeta dentro de `lib\<TargetFramework>` , como los ensamblados satélite que se encuentran bajo sus respectivas carpetas de referencia cultural.</span><span class="sxs-lookup"><span data-stu-id="39fd2-320">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="39fd2-321">Tiene como valor predeterminado el nombre del archivo.</span><span class="sxs-lookup"><span data-stu-id="39fd2-321">Defaults to the name of the file.</span></span>

<span data-ttu-id="39fd2-322">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="39fd2-322">Example:</span></span>

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="39fd2-323">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="39fd2-323">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="39fd2-324">Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificContentInPackage)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="39fd2-324">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="39fd2-325">En el caso de los archivos que se van a incluir en el paquete, el destino debe `TfmSpecificPackageFile` escribir esos archivos en el ItemGroup y establecer los metadatos opcionales siguientes:</span><span class="sxs-lookup"><span data-stu-id="39fd2-325">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="39fd2-326">`PackagePath`: Ruta de acceso en la que el archivo debe generarse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="39fd2-326">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="39fd2-327">NuGet emite una advertencia si se agrega más de un archivo a la misma ruta de acceso del paquete.</span><span class="sxs-lookup"><span data-stu-id="39fd2-327">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="39fd2-328">`BuildAction`: Acción de compilación que se va a asignar al archivo, que solo es necesario si la ruta `contentFiles` de acceso del paquete está en la carpeta.</span><span class="sxs-lookup"><span data-stu-id="39fd2-328">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="39fd2-329">El valor predeterminado es "none".</span><span class="sxs-lookup"><span data-stu-id="39fd2-329">Defaults to "None".</span></span>

<span data-ttu-id="39fd2-330">Un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="39fd2-330">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="39fd2-331">Destino de restore</span><span class="sxs-lookup"><span data-stu-id="39fd2-331">restore target</span></span>

<span data-ttu-id="39fd2-332">`MSBuild -t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="39fd2-332">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="39fd2-333">Leer todas las referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="39fd2-333">Read all project to project references</span></span>
1. <span data-ttu-id="39fd2-334">Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias</span><span class="sxs-lookup"><span data-stu-id="39fd2-334">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="39fd2-335">Pasar datos de MSBuild a NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="39fd2-335">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="39fd2-336">Ejecutar la restauración</span><span class="sxs-lookup"><span data-stu-id="39fd2-336">Run restore</span></span>
1. <span data-ttu-id="39fd2-337">Descargar los paquetes</span><span class="sxs-lookup"><span data-stu-id="39fd2-337">Download packages</span></span>
1. <span data-ttu-id="39fd2-338">Escribir el archivo de activos, destinos y propiedades</span><span class="sxs-lookup"><span data-stu-id="39fd2-338">Write assets file, targets, and props</span></span>

<span data-ttu-id="39fd2-339">El `restore` destino **solo** funciona con los proyectos que usan el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="39fd2-339">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="39fd2-340">**No** funciona para los proyectos que usan el `packages.config` formato; use la [restauración de Nuget](../reference/cli-reference/cli-ref-restore.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="39fd2-340">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="39fd2-341">Restaurar las propiedades</span><span class="sxs-lookup"><span data-stu-id="39fd2-341">Restore properties</span></span>

<span data-ttu-id="39fd2-342">Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="39fd2-342">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="39fd2-343">También se pueden establecer valores desde la línea de comandos mediante el modificador `-p:` (vea los ejemplos siguientes).</span><span class="sxs-lookup"><span data-stu-id="39fd2-343">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="39fd2-344">Propiedad</span><span class="sxs-lookup"><span data-stu-id="39fd2-344">Property</span></span> | <span data-ttu-id="39fd2-345">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="39fd2-345">Description</span></span> |
|--------|--------|
| <span data-ttu-id="39fd2-346">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="39fd2-346">RestoreSources</span></span> | <span data-ttu-id="39fd2-347">Lista delimitada por punto y coma de orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="39fd2-347">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="39fd2-348">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="39fd2-348">RestorePackagesPath</span></span> | <span data-ttu-id="39fd2-349">Ruta de acceso de la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="39fd2-349">User packages folder path.</span></span> |
| <span data-ttu-id="39fd2-350">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="39fd2-350">RestoreDisableParallel</span></span> | <span data-ttu-id="39fd2-351">Limitar las descargas a una cada vez.</span><span class="sxs-lookup"><span data-stu-id="39fd2-351">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="39fd2-352">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="39fd2-352">RestoreConfigFile</span></span> | <span data-ttu-id="39fd2-353">Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="39fd2-353">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="39fd2-354">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="39fd2-354">RestoreNoCache</span></span> | <span data-ttu-id="39fd2-355">Si es true, evita el uso de paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="39fd2-355">If true, avoids using cached packages.</span></span> <span data-ttu-id="39fd2-356">Consulte [Administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="39fd2-356">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="39fd2-357">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="39fd2-357">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="39fd2-358">Si es true, ignora los orígenes de paquetes que producen errores o faltan.</span><span class="sxs-lookup"><span data-stu-id="39fd2-358">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="39fd2-359">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="39fd2-359">RestoreFallbackFolders</span></span> | <span data-ttu-id="39fd2-360">Carpetas de reserva que se usan de la misma manera que se usa la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="39fd2-360">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="39fd2-361">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="39fd2-361">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="39fd2-362">Fuentes adicionales para usar durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="39fd2-362">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="39fd2-363">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="39fd2-363">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="39fd2-364">Carpetas de reserva adicionales para usar durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="39fd2-364">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="39fd2-365">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="39fd2-365">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="39fd2-366">Excluye las carpetas de reserva especificadas en`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="39fd2-366">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="39fd2-367">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="39fd2-367">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="39fd2-368">Ruta de acceso a `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-368">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="39fd2-369">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="39fd2-369">RestoreGraphProjectInput</span></span> | <span data-ttu-id="39fd2-370">Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="39fd2-370">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="39fd2-371">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="39fd2-371">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="39fd2-372">Cuando los proyectos se recopilan a través de MSBuild, determina si se recopilan con la `SkipNonexistentTargets` optimización.</span><span class="sxs-lookup"><span data-stu-id="39fd2-372">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="39fd2-373">Cuando no se `true`establece, el valor predeterminado es.</span><span class="sxs-lookup"><span data-stu-id="39fd2-373">When not set, defaults to `true`.</span></span> <span data-ttu-id="39fd2-374">La consecuencia es un comportamiento de error rápido cuando no se pueden importar los destinos de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="39fd2-374">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="39fd2-375">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="39fd2-375">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="39fd2-376">Carpeta de salida, que `BaseIntermediateOutputPath` tiene como valor predeterminado y la `obj` carpeta.</span><span class="sxs-lookup"><span data-stu-id="39fd2-376">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="39fd2-377">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="39fd2-377">Examples</span></span>

<span data-ttu-id="39fd2-378">Línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="39fd2-378">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="39fd2-379">Archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="39fd2-379">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="39fd2-380">Restaurar salidas</span><span class="sxs-lookup"><span data-stu-id="39fd2-380">Restore outputs</span></span>

<span data-ttu-id="39fd2-381">La restauración crea los archivos siguientes en la carpeta `obj` de compilación:</span><span class="sxs-lookup"><span data-stu-id="39fd2-381">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="39fd2-382">Archivo</span><span class="sxs-lookup"><span data-stu-id="39fd2-382">File</span></span> | <span data-ttu-id="39fd2-383">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="39fd2-383">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="39fd2-384">Contiene el gráfico de dependencias de todas las referencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="39fd2-384">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="39fd2-385">Referencias a propiedades de MSBuild incluidas en paquetes</span><span class="sxs-lookup"><span data-stu-id="39fd2-385">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="39fd2-386">Referencias a destinos de MSBuild incluidos en paquetes</span><span class="sxs-lookup"><span data-stu-id="39fd2-386">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="39fd2-387">Restaurar y compilar con un comando de MSBuild</span><span class="sxs-lookup"><span data-stu-id="39fd2-387">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="39fd2-388">Debido al hecho de que NuGet puede restaurar paquetes que desactivan los destinos y las propiedades de MSBuild, las evaluaciones de la restauración y de la compilación se ejecutan con propiedades globales diferentes.</span><span class="sxs-lookup"><span data-stu-id="39fd2-388">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="39fd2-389">Esto significa que el siguiente tendrá un comportamiento imprevisible y a menudo incorrecto.</span><span class="sxs-lookup"><span data-stu-id="39fd2-389">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="39fd2-390">En su lugar, el enfoque recomendado es:</span><span class="sxs-lookup"><span data-stu-id="39fd2-390">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="39fd2-391">La misma lógica se aplica a otros destinos similares `build`a.</span><span class="sxs-lookup"><span data-stu-id="39fd2-391">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="39fd2-392">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="39fd2-392">PackageTargetFallback</span></span>

<span data-ttu-id="39fd2-393">El elemento `PackageTargetFallback` permite especificar un conjunto de destinos compatibles que se usarán al restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="39fd2-393">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="39fd2-394">Está diseñado para permitir que los paquetes que usan un [TxM](../reference/target-frameworks.md) de dotnet funcionen con paquetes compatibles que no declaran un TxM de dotnet.</span><span class="sxs-lookup"><span data-stu-id="39fd2-394">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="39fd2-395">Es decir, si el proyecto usa el TxM de dotnet, todos los paquetes de los que depende también deben tener un TxM de dotnet, a menos que agregue `<PackageTargetFallback>` al proyecto para permitir que las plataformas que no sean de dotnet sean compatibles con dotnet.</span><span class="sxs-lookup"><span data-stu-id="39fd2-395">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="39fd2-396">Por ejemplo, si el proyecto usa el TxM `netstandard1.6` y un paquete dependiente solo contiene `lib/net45/a.dll` y `lib/portable-net45+win81/a.dll`, se producirá un error al compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="39fd2-396">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="39fd2-397">Si lo que quiere incluir es el último archivo DLL, puede agregar `PackageTargetFallback` como se indica a continuación para indicar que el archivo DLL `portable-net45+win81` es compatible:</span><span class="sxs-lookup"><span data-stu-id="39fd2-397">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="39fd2-398">Para declarar una reserva para todos los destinos del proyecto, excluya el atributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="39fd2-398">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="39fd2-399">También puede extender cualquier `PackageTargetFallback` existente mediante la inclusión de `$(PackageTargetFallback)` como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="39fd2-399">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="39fd2-400">Reemplazo de una biblioteca desde un gráfico de restauración</span><span class="sxs-lookup"><span data-stu-id="39fd2-400">Replacing one library from a restore graph</span></span>

<span data-ttu-id="39fd2-401">Si una restauración agrega el ensamblado equivocado, se puede excluir la opción predeterminada de ese paquete y reemplazarla por una de su propia elección.</span><span class="sxs-lookup"><span data-stu-id="39fd2-401">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="39fd2-402">En primer lugar, con una `PackageReference` de nivel superior, excluya todos los activos:</span><span class="sxs-lookup"><span data-stu-id="39fd2-402">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="39fd2-403">Después, agregue su propia referencia a la copia local correspondiente del archivo DLL:</span><span class="sxs-lookup"><span data-stu-id="39fd2-403">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
