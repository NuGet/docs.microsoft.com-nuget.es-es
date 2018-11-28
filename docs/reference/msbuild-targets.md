---
title: pack y restore de NuGet como destinos de MSBuild
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7b3fc72ddd3ad6c9185c2bd0f2563df59e77f1c8
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453551"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="3bdc0-103">pack y restore de NuGet como destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="3bdc0-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="3bdc0-104">*NuGet 4.0 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="3bdc0-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="3bdc0-105">Con el formato PackageReference, NuGet 4.0 + puede almacenar los metadatos de todos los manifiestos directamente en un archivo de proyecto, en lugar de usar un archivo `.nuspec` aparte.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="3bdc0-106">Con MSBuild 15.1 y versiones posteriores, NuGet es también un ciudadano de MSBuild de primera clase con los destinos `pack` y `restore` como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="3bdc0-107">Estos destinos permiten trabajar con NuGet como lo haría con cualquier otra tarea o destino de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="3bdc0-108">(Para NuGet 3.x y versiones anteriores, los comandos [pack](../tools/cli-ref-pack.md) y [restore](../tools/cli-ref-restore.md) se usan a través de la CLI de NuGet en su lugar).</span><span class="sxs-lookup"><span data-stu-id="3bdc0-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="3bdc0-109">Orden de compilación de destinos</span><span class="sxs-lookup"><span data-stu-id="3bdc0-109">Target build order</span></span>

<span data-ttu-id="3bdc0-110">Dado que `pack` y `restore` son destinos de MSBuild, puede tener acceso a ellos para mejorar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="3bdc0-111">Por ejemplo, supongamos que quiere copiar el paquete en un recurso compartido de red después de empaquetarlo.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="3bdc0-112">Puede hacer esto si agrega lo siguiente al archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="3bdc0-113">De forma similar, puede escribir una tarea de MSBuild, su propio destino y usar propiedades de NuGet en la tarea de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="3bdc0-114">Destino de pack</span><span class="sxs-lookup"><span data-stu-id="3bdc0-114">pack target</span></span>

<span data-ttu-id="3bdc0-115">Para los proyectos de .NET Standard con el formato PackageReference, utilizando `msbuild -t:pack` dibuja las entradas del archivo de proyecto debe utilizar para crear un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="3bdc0-116">En la tabla siguiente se describen las propiedades de MSBuild que se pueden agregar a un archivo de proyecto en el primer nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="3bdc0-117">Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="3bdc0-118">Para mayor comodidad, la tabla se organiza por la propiedad equivalente en un [archivo `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="3bdc0-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="3bdc0-119">Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="3bdc0-120">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="3bdc0-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="3bdc0-121">Propiedad de MSBuild</span><span class="sxs-lookup"><span data-stu-id="3bdc0-121">MSBuild Property</span></span> | <span data-ttu-id="3bdc0-122">Default</span><span class="sxs-lookup"><span data-stu-id="3bdc0-122">Default</span></span> | <span data-ttu-id="3bdc0-123">Notas</span><span class="sxs-lookup"><span data-stu-id="3bdc0-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="3bdc0-124">Id.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-124">Id</span></span> | <span data-ttu-id="3bdc0-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="3bdc0-125">PackageId</span></span> | <span data-ttu-id="3bdc0-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="3bdc0-126">AssemblyName</span></span> | <span data-ttu-id="3bdc0-127">$(NombreDeEnsamblado) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="3bdc0-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="3bdc0-128">Versión</span><span class="sxs-lookup"><span data-stu-id="3bdc0-128">Version</span></span> | <span data-ttu-id="3bdc0-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3bdc0-129">PackageVersion</span></span> | <span data-ttu-id="3bdc0-130">Versión</span><span class="sxs-lookup"><span data-stu-id="3bdc0-130">Version</span></span> | <span data-ttu-id="3bdc0-131">Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="3bdc0-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="3bdc0-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3bdc0-132">VersionPrefix</span></span> | <span data-ttu-id="3bdc0-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3bdc0-133">PackageVersionPrefix</span></span> | <span data-ttu-id="3bdc0-134">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-134">empty</span></span> | <span data-ttu-id="3bdc0-135">Al establecer PackageVersion se sobrescribe PackageVersionPrefix.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="3bdc0-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3bdc0-136">VersionSuffix</span></span> | <span data-ttu-id="3bdc0-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3bdc0-137">PackageVersionSuffix</span></span> | <span data-ttu-id="3bdc0-138">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-138">empty</span></span> | <span data-ttu-id="3bdc0-139">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="3bdc0-140">Al establecer PackageVersion se sobrescribe PackageVersionSuffix.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="3bdc0-141">Authors</span><span class="sxs-lookup"><span data-stu-id="3bdc0-141">Authors</span></span> | <span data-ttu-id="3bdc0-142">Authors</span><span class="sxs-lookup"><span data-stu-id="3bdc0-142">Authors</span></span> | <span data-ttu-id="3bdc0-143">Nombre del usuario actual</span><span class="sxs-lookup"><span data-stu-id="3bdc0-143">Username of the current user</span></span> | |
| <span data-ttu-id="3bdc0-144">Owners</span><span class="sxs-lookup"><span data-stu-id="3bdc0-144">Owners</span></span> | <span data-ttu-id="3bdc0-145">N/D</span><span class="sxs-lookup"><span data-stu-id="3bdc0-145">N/A</span></span> | <span data-ttu-id="3bdc0-146">No está presente en el archivo NuSpec</span><span class="sxs-lookup"><span data-stu-id="3bdc0-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="3bdc0-147">Title</span><span class="sxs-lookup"><span data-stu-id="3bdc0-147">Title</span></span> | <span data-ttu-id="3bdc0-148">Title</span><span class="sxs-lookup"><span data-stu-id="3bdc0-148">Title</span></span> | <span data-ttu-id="3bdc0-149">El identificador de paquete</span><span class="sxs-lookup"><span data-stu-id="3bdc0-149">The PackageId</span></span>| |
| <span data-ttu-id="3bdc0-150">Descripción</span><span class="sxs-lookup"><span data-stu-id="3bdc0-150">Description</span></span> | <span data-ttu-id="3bdc0-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="3bdc0-151">Description</span></span> | <span data-ttu-id="3bdc0-152">"Descripción del paquete"</span><span class="sxs-lookup"><span data-stu-id="3bdc0-152">"Package Description"</span></span> | |
| <span data-ttu-id="3bdc0-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="3bdc0-153">Copyright</span></span> | <span data-ttu-id="3bdc0-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="3bdc0-154">Copyright</span></span> | <span data-ttu-id="3bdc0-155">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-155">empty</span></span> | |
| <span data-ttu-id="3bdc0-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3bdc0-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="3bdc0-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3bdc0-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="3bdc0-158">False</span><span class="sxs-lookup"><span data-stu-id="3bdc0-158">false</span></span> | |
| <span data-ttu-id="3bdc0-159">licencia</span><span class="sxs-lookup"><span data-stu-id="3bdc0-159">license</span></span> | <span data-ttu-id="3bdc0-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="3bdc0-160">PackageLicenseExpression</span></span> | <span data-ttu-id="3bdc0-161">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-161">empty</span></span> | <span data-ttu-id="3bdc0-162">Corresponde a `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="3bdc0-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="3bdc0-163">licencia</span><span class="sxs-lookup"><span data-stu-id="3bdc0-163">license</span></span> | <span data-ttu-id="3bdc0-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="3bdc0-164">PackageLicenseFile</span></span> | <span data-ttu-id="3bdc0-165">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-165">empty</span></span> | <span data-ttu-id="3bdc0-166">Se corresponde con `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="3bdc0-167">Es posible que deba explícitamente el archivo de licencia que se hace referencia del módulo.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="3bdc0-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-168">LicenseUrl</span></span> | <span data-ttu-id="3bdc0-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-169">PackageLicenseUrl</span></span> | <span data-ttu-id="3bdc0-170">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-170">empty</span></span> | <span data-ttu-id="3bdc0-171">`licenseUrl` está en desuso, utilice la propiedad PackageLicenseExpression o PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="3bdc0-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="3bdc0-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-172">ProjectUrl</span></span> | <span data-ttu-id="3bdc0-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-173">PackageProjectUrl</span></span> | <span data-ttu-id="3bdc0-174">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-174">empty</span></span> | |
| <span data-ttu-id="3bdc0-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-175">IconUrl</span></span> | <span data-ttu-id="3bdc0-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-176">PackageIconUrl</span></span> | <span data-ttu-id="3bdc0-177">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-177">empty</span></span> | |
| <span data-ttu-id="3bdc0-178">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="3bdc0-178">Tags</span></span> | <span data-ttu-id="3bdc0-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3bdc0-179">PackageTags</span></span> | <span data-ttu-id="3bdc0-180">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-180">empty</span></span> | <span data-ttu-id="3bdc0-181">Las etiquetas están delimitadas mediante punto y coma.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="3bdc0-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3bdc0-182">ReleaseNotes</span></span> | <span data-ttu-id="3bdc0-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3bdc0-183">PackageReleaseNotes</span></span> | <span data-ttu-id="3bdc0-184">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-184">empty</span></span> | |
| <span data-ttu-id="3bdc0-185">Url del repositorio</span><span class="sxs-lookup"><span data-stu-id="3bdc0-185">Repository/Url</span></span> | <span data-ttu-id="3bdc0-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-186">RepositoryUrl</span></span> | <span data-ttu-id="3bdc0-187">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-187">empty</span></span> | <span data-ttu-id="3bdc0-188">Dirección URL del repositorio utilizado para clonar o recuperar el código fuente.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="3bdc0-189">Ejemplo: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="3bdc0-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="3bdc0-190">/ Tipo de repositorio</span><span class="sxs-lookup"><span data-stu-id="3bdc0-190">Repository/Type</span></span> | <span data-ttu-id="3bdc0-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3bdc0-191">RepositoryType</span></span> | <span data-ttu-id="3bdc0-192">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-192">empty</span></span> | <span data-ttu-id="3bdc0-193">Tipo de repositorio.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-193">Repository type.</span></span> <span data-ttu-id="3bdc0-194">Ejemplos: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="3bdc0-195">Rama del repositorio</span><span class="sxs-lookup"><span data-stu-id="3bdc0-195">Repository/Branch</span></span> | <span data-ttu-id="3bdc0-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="3bdc0-196">RepositoryBranch</span></span> | <span data-ttu-id="3bdc0-197">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-197">empty</span></span> | <span data-ttu-id="3bdc0-198">Información de rama del repositorio opcional.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-198">Optional repository branch information.</span></span> <span data-ttu-id="3bdc0-199">*RepositoryUrl* también debe especificarse para que se incluye esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="3bdc0-200">Ejemplo: *maestro* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="3bdc0-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="3bdc0-201">Repositorio/confirmación</span><span class="sxs-lookup"><span data-stu-id="3bdc0-201">Repository/Commit</span></span> | <span data-ttu-id="3bdc0-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="3bdc0-202">RepositoryCommit</span></span> | <span data-ttu-id="3bdc0-203">vacío</span><span class="sxs-lookup"><span data-stu-id="3bdc0-203">empty</span></span> | <span data-ttu-id="3bdc0-204">Confirmación del repositorio opcional o conjunto de cambios para indicar que el paquete de origen se compiló.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="3bdc0-205">*RepositoryUrl* también debe especificarse para que se incluye esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="3bdc0-206">Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="3bdc0-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="3bdc0-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="3bdc0-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="3bdc0-208">Resumen</span><span class="sxs-lookup"><span data-stu-id="3bdc0-208">Summary</span></span> | <span data-ttu-id="3bdc0-209">No compatibles</span><span class="sxs-lookup"><span data-stu-id="3bdc0-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="3bdc0-210">Entradas de destino de pack</span><span class="sxs-lookup"><span data-stu-id="3bdc0-210">pack target inputs</span></span>

- <span data-ttu-id="3bdc0-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="3bdc0-211">IsPackable</span></span>
- <span data-ttu-id="3bdc0-212">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3bdc0-212">PackageVersion</span></span>
- <span data-ttu-id="3bdc0-213">PackageId</span><span class="sxs-lookup"><span data-stu-id="3bdc0-213">PackageId</span></span>
- <span data-ttu-id="3bdc0-214">Authors</span><span class="sxs-lookup"><span data-stu-id="3bdc0-214">Authors</span></span>
- <span data-ttu-id="3bdc0-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="3bdc0-215">Description</span></span>
- <span data-ttu-id="3bdc0-216">Copyright</span><span class="sxs-lookup"><span data-stu-id="3bdc0-216">Copyright</span></span>
- <span data-ttu-id="3bdc0-217">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3bdc0-217">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="3bdc0-218">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="3bdc0-218">DevelopmentDependency</span></span>
- <span data-ttu-id="3bdc0-219">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="3bdc0-219">PackageLicenseExpression</span></span>
- <span data-ttu-id="3bdc0-220">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="3bdc0-220">PackageLicenseFile</span></span>
- <span data-ttu-id="3bdc0-221">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-221">PackageLicenseUrl</span></span>
- <span data-ttu-id="3bdc0-222">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-222">PackageProjectUrl</span></span>
- <span data-ttu-id="3bdc0-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-223">PackageIconUrl</span></span>
- <span data-ttu-id="3bdc0-224">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3bdc0-224">PackageReleaseNotes</span></span>
- <span data-ttu-id="3bdc0-225">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3bdc0-225">PackageTags</span></span>
- <span data-ttu-id="3bdc0-226">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="3bdc0-226">PackageOutputPath</span></span>
- <span data-ttu-id="3bdc0-227">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3bdc0-227">IncludeSymbols</span></span>
- <span data-ttu-id="3bdc0-228">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3bdc0-228">IncludeSource</span></span>
- <span data-ttu-id="3bdc0-229">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="3bdc0-229">PackageTypes</span></span>
- <span data-ttu-id="3bdc0-230">IsTool</span><span class="sxs-lookup"><span data-stu-id="3bdc0-230">IsTool</span></span>
- <span data-ttu-id="3bdc0-231">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-231">RepositoryUrl</span></span>
- <span data-ttu-id="3bdc0-232">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3bdc0-232">RepositoryType</span></span>
- <span data-ttu-id="3bdc0-233">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="3bdc0-233">RepositoryBranch</span></span>
- <span data-ttu-id="3bdc0-234">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="3bdc0-234">RepositoryCommit</span></span>
- <span data-ttu-id="3bdc0-235">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="3bdc0-235">NoPackageAnalysis</span></span>
- <span data-ttu-id="3bdc0-236">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="3bdc0-236">MinClientVersion</span></span>
- <span data-ttu-id="3bdc0-237">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3bdc0-237">IncludeBuildOutput</span></span>
- <span data-ttu-id="3bdc0-238">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="3bdc0-238">IncludeContentInPack</span></span>
- <span data-ttu-id="3bdc0-239">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="3bdc0-239">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="3bdc0-240">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="3bdc0-240">ContentTargetFolders</span></span>
- <span data-ttu-id="3bdc0-241">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="3bdc0-241">NuspecFile</span></span>
- <span data-ttu-id="3bdc0-242">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="3bdc0-242">NuspecBasePath</span></span>
- <span data-ttu-id="3bdc0-243">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="3bdc0-243">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="3bdc0-244">Escenarios de pack</span><span class="sxs-lookup"><span data-stu-id="3bdc0-244">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="3bdc0-245">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3bdc0-245">PackageIconUrl</span></span>

<span data-ttu-id="3bdc0-246">Como parte del cambio para [NuGet problema 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` se cambiará a `PackageIconUri` y puede ser una ruta de acceso relativa a un archivo de icono que se incluirá en la raíz del paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-246">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="3bdc0-247">Ensamblados de salida</span><span class="sxs-lookup"><span data-stu-id="3bdc0-247">Output assemblies</span></span>

<span data-ttu-id="3bdc0-248">`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-248">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="3bdc0-249">Los archivos de salida que se copian dependen de lo que proporciona MSBuild desde el destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-249">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="3bdc0-250">Hay dos propiedades de MSBuild que se pueden usar en el archivo de proyecto o la línea de comandos para controlar dónde van los ensamblados de salida:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-250">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="3bdc0-251">`IncludeBuildOutput`: un valor booleano que determina si los ensamblados de salida de compilación deben incluirse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-251">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="3bdc0-252">`BuildOutputTargetFolder`: especifica la carpeta en la que se deben colocar los ensamblados de salida.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-252">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="3bdc0-253">Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-253">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="3bdc0-254">Referencias de paquete</span><span class="sxs-lookup"><span data-stu-id="3bdc0-254">Package references</span></span>

<span data-ttu-id="3bdc0-255">Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="3bdc0-255">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="3bdc0-256">Referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="3bdc0-256">Project to project references</span></span>

<span data-ttu-id="3bdc0-257">Las referencias entre proyectos se consideran de forma predeterminada como referencias de paquetes NuGet, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-257">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="3bdc0-258">También puede agregar los metadatos siguientes a la referencia de proyecto:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-258">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="3bdc0-259">Inclusión de contenido en un paquete</span><span class="sxs-lookup"><span data-stu-id="3bdc0-259">Including content in a package</span></span>

<span data-ttu-id="3bdc0-260">Para incluir contenido, agregue metadatos adicionales al elemento `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-260">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="3bdc0-261">De forma predeterminada todos los elementos de tipo "Content" se incluyen en el paquete a menos que los reemplace con entradas como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-261">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="3bdc0-262">De forma predeterminada, todo el contenido se agrega a la raíz de la carpeta `content` y `contentFiles\any\<target_framework>` dentro de un paquete y se conserva la estructura de carpetas relativa, a menos que se especifique una ruta de acceso de paquete:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-262">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="3bdc0-263">Si quiere copiar todo el contenido a una carpeta raíz determinada (en lugar de `content` y `contentFiles`), puede usar la propiedad `ContentTargetFolders` de MSBuild, cuyo valor predeterminado es "content;contentFiles", pero que se puede establecer en cualquier otro nombre de carpeta.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-263">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="3bdc0-264">Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-264">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="3bdc0-265">`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-265">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="3bdc0-266">Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-266">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="3bdc0-267">Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-267">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="3bdc0-268">También hay una propiedad `$(IncludeContentInPack)` de MSBuild, cuyo valor predeterminado es `true`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-268">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="3bdc0-269">Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-269">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="3bdc0-270">Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen ```<PackageCopyToOutput>``` y ```<PackageFlatten>```, que establece los valores ```CopyToOutput``` y ```Flatten``` en la entrada ```contentFiles``` del archivo nuspec de salida.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-270">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="3bdc0-271">Además de los elementos Content, los metadatos `<Pack>` y `<PackagePath>` también se pueden establecer en archivos con una acción de compilación Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-271">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="3bdc0-272">Para que el comando pack anexe el nombre de archivo a la ruta de acceso del paquete cuando se usan patrones globales, la ruta de acceso del paquete debe terminar con el carácter separador de carpeta; en caso contrario, la ruta de acceso del paquete se trata como la ruta de acceso completa, incluido el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-272">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="3bdc0-273">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3bdc0-273">IncludeSymbols</span></span>

<span data-ttu-id="3bdc0-274">Cuando se usa `MSBuild -t:pack -p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="3bdc0-274">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="3bdc0-275">Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-275">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="3bdc0-276">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3bdc0-276">IncludeSource</span></span>

<span data-ttu-id="3bdc0-277">Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-277">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="3bdc0-278">Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-278">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="3bdc0-279">Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-279">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="3bdc0-280">Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-280">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="3bdc0-281">Empaquetado de una expresión de licencia o un archivo de licencia</span><span class="sxs-lookup"><span data-stu-id="3bdc0-281">Packing a license expression or a license file</span></span>

<span data-ttu-id="3bdc0-282">Cuando se usa una expresión de licencia, debe usarse la propiedad PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-282">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="3bdc0-283">[Ejemplo de expresión de licencia](#https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="3bdc0-283">[License expression sample](#https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

<span data-ttu-id="3bdc0-284">Cuando se empaqueta un archivo de licencia, deberá usar la propiedad PackageLicenseFile para especificar la ruta de acceso de paquete, relativa a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-284">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="3bdc0-285">Además, deberá asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-285">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="3bdc0-286">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-286">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```
<span data-ttu-id="3bdc0-287">[Ejemplo de la vida de licencia](#https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="3bdc0-287">[License life sample](#https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="3bdc0-288">IsTool</span><span class="sxs-lookup"><span data-stu-id="3bdc0-288">IsTool</span></span>

<span data-ttu-id="3bdc0-289">Cuando se usa `MSBuild -t:pack -p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-289">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="3bdc0-290">Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-290">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="3bdc0-291">Empaquetado mediante un archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="3bdc0-291">Packing using a .nuspec</span></span>

<span data-ttu-id="3bdc0-292">Puede usar un `.nuspec` archivo para empaquetar el proyecto siempre que tenga un archivo de proyecto SDK para importar `NuGet.Build.Tasks.Pack.targets` para que se puede ejecutar la tarea de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-292">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="3bdc0-293">Deberá restaurar el proyecto antes de que puede empaquetar un archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-293">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="3bdc0-294">La plataforma de destino del archivo del proyecto es irrelevante y no se utiliza cuando se empaqueta un nuspec.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-294">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="3bdc0-295">Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-295">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="3bdc0-296">`NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-296">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="3bdc0-297">`NuspecProperties`: lista de pares clave=valor separados por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-297">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="3bdc0-298">Debido al funcionamiento del análisis de línea de comandos de MSBuild, se deben especificar varias propiedades como se indica a continuación: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-298">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="3bdc0-299">`NuspecBasePath`: ruta de acceso base para el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-299">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="3bdc0-300">Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-300">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3bdc0-301">Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-301">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3bdc0-302">Tenga en cuenta que el empaquetado nuspec además utilizando dotnet.exe o msbuild conduce a compilar el proyecto de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-302">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="3bdc0-303">Esto puede evitarse pasando ```--no-build``` dotnet.exe, que es el equivalente del valor de propiedad ```<NoBuild>true</NoBuild> ``` en el archivo de proyecto, junto con la opción ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` en el archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="3bdc0-303">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="3bdc0-304">Un ejemplo de un archivo csproj para empaquetar un archivo nuspec es:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-304">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="3bdc0-305">Avanzada de puntos de extensión para crear el paquete personalizado</span><span class="sxs-lookup"><span data-stu-id="3bdc0-305">Advanced extension points to create customized package</span></span>

<span data-ttu-id="3bdc0-306">El `pack` destino proporciona dos puntos de extensión que se ejecutan en la compilación interna, de específica de framework de destino.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-306">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="3bdc0-307">Se admiten los puntos de extensión como contenido específico de framework de destino y los ensamblados en un paquete:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-307">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="3bdc0-308">`TargetsForTfmSpecificBuildOutput` destino: uso para los archivos en el `lib` carpeta o una carpeta especificada utilizando `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-308">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="3bdc0-309">`TargetsForTfmSpecificContentInPackage` destino: uso de archivos fuera de la `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-309">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="3bdc0-310">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3bdc0-310">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="3bdc0-311">Escribir un destino personalizado y lo especifica como el valor de la `$(TargetsForTfmSpecificBuildOutput)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-311">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="3bdc0-312">Para los archivos que deben entrar en el `BuildOutputTargetFolder` (lib de forma predeterminada), el destino debe escribir esos archivos en el elemento ItemGroup `BuildOutputInPackage` y establecer los dos valores de metadatos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-312">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="3bdc0-313">`FinalOutputPath`: La ruta de acceso absoluta del archivo; Si no se proporciona, la identidad se utiliza para evaluar la ruta de acceso de origen.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-313">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="3bdc0-314">`TargetPath`: (Opcional) establecer cuando el archivo debe ir en una subcarpeta dentro de `lib\<TargetFramework>` , como ensamblados satélite que van en sus carpetas respectivas de referencia cultural.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-314">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="3bdc0-315">El valor predeterminado es el nombre del archivo.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-315">Defaults to the name of the file.</span></span>

<span data-ttu-id="3bdc0-316">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-316">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="3bdc0-317">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="3bdc0-317">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="3bdc0-318">Escribir un destino personalizado y lo especifica como el valor de la `$(TargetsForTfmSpecificContentInPackage)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="3bdc0-319">Para que los archivos que se incluyen en el paquete, el destino debe escribir esos archivos en el elemento ItemGroup `TfmSpecificPackageFile` y establezca los siguientes metadatos opcionales:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-319">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="3bdc0-320">`PackagePath`: Ruta de acceso donde el archivo debe ser la salida en el paquete.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-320">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="3bdc0-321">NuGet emite una advertencia si se agrega más de un archivo a la misma ruta de acceso del paquete.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-321">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="3bdc0-322">`BuildAction`: La acción de compilación para asignar al archivo, solo es necesario si la ruta de acceso del paquete está en el `contentFiles` carpeta.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-322">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="3bdc0-323">El valor predeterminado es "None".</span><span class="sxs-lookup"><span data-stu-id="3bdc0-323">Defaults to "None".</span></span>

<span data-ttu-id="3bdc0-324">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-324">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="3bdc0-325">Destino de restore</span><span class="sxs-lookup"><span data-stu-id="3bdc0-325">restore target</span></span>

<span data-ttu-id="3bdc0-326">`MSBuild -t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-326">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="3bdc0-327">Leer todas las referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="3bdc0-327">Read all project to project references</span></span>
1. <span data-ttu-id="3bdc0-328">Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias</span><span class="sxs-lookup"><span data-stu-id="3bdc0-328">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="3bdc0-329">Pasar datos de MSBuild a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="3bdc0-329">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="3bdc0-330">Ejecutar la restauración</span><span class="sxs-lookup"><span data-stu-id="3bdc0-330">Run restore</span></span>
1. <span data-ttu-id="3bdc0-331">Descargar los paquetes</span><span class="sxs-lookup"><span data-stu-id="3bdc0-331">Download packages</span></span>
1. <span data-ttu-id="3bdc0-332">Escribir el archivo de activos, destinos y propiedades</span><span class="sxs-lookup"><span data-stu-id="3bdc0-332">Write assets file, targets, and props</span></span>

<span data-ttu-id="3bdc0-333">El `restore` destino funciona **sólo** para proyectos con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-333">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="3bdc0-334">Lo hace **no** profesional de proyectos que usan el `packages.config` dar formato; use [restauración de nuget](../tools/cli-ref-restore.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-334">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="3bdc0-335">Restaurar las propiedades</span><span class="sxs-lookup"><span data-stu-id="3bdc0-335">Restore properties</span></span>

<span data-ttu-id="3bdc0-336">Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-336">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="3bdc0-337">También se pueden establecer valores desde la línea de comandos mediante el modificador `-p:` (vea los ejemplos siguientes).</span><span class="sxs-lookup"><span data-stu-id="3bdc0-337">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="3bdc0-338">Property</span><span class="sxs-lookup"><span data-stu-id="3bdc0-338">Property</span></span> | <span data-ttu-id="3bdc0-339">Descripción</span><span class="sxs-lookup"><span data-stu-id="3bdc0-339">Description</span></span> |
|--------|--------|
| <span data-ttu-id="3bdc0-340">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="3bdc0-340">RestoreSources</span></span> | <span data-ttu-id="3bdc0-341">Lista delimitada por punto y coma de orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-341">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="3bdc0-342">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="3bdc0-342">RestorePackagesPath</span></span> | <span data-ttu-id="3bdc0-343">Ruta de acceso de la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-343">User packages folder path.</span></span> |
| <span data-ttu-id="3bdc0-344">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="3bdc0-344">RestoreDisableParallel</span></span> | <span data-ttu-id="3bdc0-345">Limitar las descargas a una cada vez.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-345">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="3bdc0-346">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="3bdc0-346">RestoreConfigFile</span></span> | <span data-ttu-id="3bdc0-347">Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-347">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="3bdc0-348">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="3bdc0-348">RestoreNoCache</span></span> | <span data-ttu-id="3bdc0-349">Si es true, evita el uso de paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-349">If true, avoids using cached packages.</span></span> <span data-ttu-id="3bdc0-350">Consulte [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3bdc0-350">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="3bdc0-351">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="3bdc0-351">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="3bdc0-352">Si es true, ignora los orígenes de paquetes que producen errores o faltan.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-352">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="3bdc0-353">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="3bdc0-353">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="3bdc0-354">Ruta de acceso a `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-354">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="3bdc0-355">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="3bdc0-355">RestoreGraphProjectInput</span></span> | <span data-ttu-id="3bdc0-356">Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-356">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="3bdc0-357">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="3bdc0-357">RestoreOutputPath</span></span> | <span data-ttu-id="3bdc0-358">Carpeta de salida, que de forma predeterminada es `obj`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-358">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="3bdc0-359">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="3bdc0-359">Examples</span></span>

<span data-ttu-id="3bdc0-360">Línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-360">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="3bdc0-361">Archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-361">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="3bdc0-362">Restaurar salidas</span><span class="sxs-lookup"><span data-stu-id="3bdc0-362">Restore outputs</span></span>

<span data-ttu-id="3bdc0-363">La restauración crea los archivos siguientes en la carpeta `obj` de compilación:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-363">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="3bdc0-364">Archivo</span><span class="sxs-lookup"><span data-stu-id="3bdc0-364">File</span></span> | <span data-ttu-id="3bdc0-365">Descripción</span><span class="sxs-lookup"><span data-stu-id="3bdc0-365">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="3bdc0-366">Contiene el gráfico de dependencias de todas las referencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-366">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="3bdc0-367">Referencias a propiedades de MSBuild incluidas en paquetes</span><span class="sxs-lookup"><span data-stu-id="3bdc0-367">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="3bdc0-368">Referencias a destinos de MSBuild incluidos en paquetes</span><span class="sxs-lookup"><span data-stu-id="3bdc0-368">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="3bdc0-369">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="3bdc0-369">PackageTargetFallback</span></span>

<span data-ttu-id="3bdc0-370">El elemento `PackageTargetFallback` permite especificar un conjunto de destinos compatibles que se usarán al restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-370">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="3bdc0-371">Está diseñado para permitir que los paquetes que usan un [TxM](../reference/target-frameworks.md) de dotnet funcionen con paquetes compatibles que no declaran un TxM de dotnet.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-371">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="3bdc0-372">Es decir, si el proyecto usa el TxM de dotnet, todos los paquetes de los que depende también deben tener un TxM de dotnet, a menos que agregue `<PackageTargetFallback>` al proyecto para permitir que las plataformas que no sean de dotnet sean compatibles con dotnet.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-372">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="3bdc0-373">Por ejemplo, si el proyecto usa el TxM `netstandard1.6` y un paquete dependiente solo contiene `lib/net45/a.dll` y `lib/portable-net45+win81/a.dll`, se producirá un error al compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-373">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="3bdc0-374">Si lo que quiere incluir es el último archivo DLL, puede agregar `PackageTargetFallback` como se indica a continuación para indicar que el archivo DLL `portable-net45+win81` es compatible:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-374">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="3bdc0-375">Para declarar una reserva para todos los destinos del proyecto, excluya el atributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-375">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="3bdc0-376">También puede extender cualquier `PackageTargetFallback` existente mediante la inclusión de `$(PackageTargetFallback)` como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-376">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="3bdc0-377">Reemplazo de una biblioteca desde un gráfico de restauración</span><span class="sxs-lookup"><span data-stu-id="3bdc0-377">Replacing one library from a restore graph</span></span>

<span data-ttu-id="3bdc0-378">Si una restauración agrega el ensamblado equivocado, se puede excluir la opción predeterminada de ese paquete y reemplazarla por una de su propia elección.</span><span class="sxs-lookup"><span data-stu-id="3bdc0-378">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="3bdc0-379">En primer lugar, con una `PackageReference` de nivel superior, excluya todos los activos:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-379">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="3bdc0-380">Después, agregue su propia referencia a la copia local correspondiente del archivo DLL:</span><span class="sxs-lookup"><span data-stu-id="3bdc0-380">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
