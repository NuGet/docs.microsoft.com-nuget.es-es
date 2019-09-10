---
title: pack y restore de NuGet como destinos de MSBuild
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 16b8ff532b87a3e3f96029e77dd166eb39294c0b
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815348"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="0fa26-103">pack y restore de NuGet como destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="0fa26-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="0fa26-104">*NuGet 4.0 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="0fa26-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="0fa26-105">Con el formato [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + puede almacenar todos los metadatos del manifiesto directamente dentro de un archivo de proyecto `.nuspec` en lugar de usar un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="0fa26-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="0fa26-106">Con MSBuild 15.1 y versiones posteriores, NuGet es también un ciudadano de MSBuild de primera clase con los destinos `pack` y `restore` como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="0fa26-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="0fa26-107">Estos destinos permiten trabajar con NuGet como lo haría con cualquier otra tarea o destino de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0fa26-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="0fa26-108">Para obtener instrucciones sobre cómo crear un paquete NuGet con MSBuild, consulte [crear un paquete Nuget con MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="0fa26-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="0fa26-109">(Para NuGet 3.x y versiones anteriores, los comandos [pack](../reference/cli-reference/cli-ref-pack.md) y [restore](../reference/cli-reference/cli-ref-restore.md) se usan a través de la CLI de NuGet en su lugar).</span><span class="sxs-lookup"><span data-stu-id="0fa26-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="0fa26-110">Orden de compilación de destinos</span><span class="sxs-lookup"><span data-stu-id="0fa26-110">Target build order</span></span>

<span data-ttu-id="0fa26-111">Dado que `pack` y `restore` son destinos de MSBuild, puede tener acceso a ellos para mejorar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0fa26-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="0fa26-112">Por ejemplo, supongamos que quiere copiar el paquete en un recurso compartido de red después de empaquetarlo.</span><span class="sxs-lookup"><span data-stu-id="0fa26-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="0fa26-113">Puede hacer esto si agrega lo siguiente al archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="0fa26-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="0fa26-114">De forma similar, puede escribir una tarea de MSBuild, su propio destino y usar propiedades de NuGet en la tarea de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0fa26-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="0fa26-115">`$(OutputPath)`es relativo y espera que se ejecute el comando desde la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="0fa26-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="0fa26-116">Destino de pack</span><span class="sxs-lookup"><span data-stu-id="0fa26-116">pack target</span></span>

<span data-ttu-id="0fa26-117">En el caso de los proyectos de .net Standard con `msbuild -t:pack` el formato PackageReference, el uso de dibuja entradas del archivo de proyecto para usarlas en la creación de un paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="0fa26-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="0fa26-118">En la tabla siguiente se describen las propiedades de MSBuild que se pueden agregar a un archivo de proyecto en el primer nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="0fa26-119">Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="0fa26-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="0fa26-120">Para mayor comodidad, la tabla se organiza por la propiedad equivalente en un [archivo `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="0fa26-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="0fa26-121">Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0fa26-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="0fa26-122">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="0fa26-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="0fa26-123">Propiedad de MSBuild</span><span class="sxs-lookup"><span data-stu-id="0fa26-123">MSBuild Property</span></span> | <span data-ttu-id="0fa26-124">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="0fa26-124">Default</span></span> | <span data-ttu-id="0fa26-125">Notas</span><span class="sxs-lookup"><span data-stu-id="0fa26-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="0fa26-126">Id</span><span class="sxs-lookup"><span data-stu-id="0fa26-126">Id</span></span> | <span data-ttu-id="0fa26-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="0fa26-127">PackageId</span></span> | <span data-ttu-id="0fa26-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="0fa26-128">AssemblyName</span></span> | <span data-ttu-id="0fa26-129">$(NombreDeEnsamblado) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="0fa26-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="0fa26-130">`Version`</span><span class="sxs-lookup"><span data-stu-id="0fa26-130">Version</span></span> | <span data-ttu-id="0fa26-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0fa26-131">PackageVersion</span></span> | <span data-ttu-id="0fa26-132">`Version`</span><span class="sxs-lookup"><span data-stu-id="0fa26-132">Version</span></span> | <span data-ttu-id="0fa26-133">Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="0fa26-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="0fa26-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0fa26-134">VersionPrefix</span></span> | <span data-ttu-id="0fa26-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0fa26-135">PackageVersionPrefix</span></span> | <span data-ttu-id="0fa26-136">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-136">empty</span></span> | <span data-ttu-id="0fa26-137">Al establecer PackageVersion se sobrescribe PackageVersionPrefix.</span><span class="sxs-lookup"><span data-stu-id="0fa26-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="0fa26-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0fa26-138">VersionSuffix</span></span> | <span data-ttu-id="0fa26-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0fa26-139">PackageVersionSuffix</span></span> | <span data-ttu-id="0fa26-140">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-140">empty</span></span> | <span data-ttu-id="0fa26-141">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0fa26-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="0fa26-142">Al establecer PackageVersion se sobrescribe PackageVersionSuffix.</span><span class="sxs-lookup"><span data-stu-id="0fa26-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="0fa26-143">Authors</span><span class="sxs-lookup"><span data-stu-id="0fa26-143">Authors</span></span> | <span data-ttu-id="0fa26-144">Authors</span><span class="sxs-lookup"><span data-stu-id="0fa26-144">Authors</span></span> | <span data-ttu-id="0fa26-145">Nombre del usuario actual</span><span class="sxs-lookup"><span data-stu-id="0fa26-145">Username of the current user</span></span> | |
| <span data-ttu-id="0fa26-146">Owners</span><span class="sxs-lookup"><span data-stu-id="0fa26-146">Owners</span></span> | <span data-ttu-id="0fa26-147">N/D</span><span class="sxs-lookup"><span data-stu-id="0fa26-147">N/A</span></span> | <span data-ttu-id="0fa26-148">No está presente en el archivo NuSpec</span><span class="sxs-lookup"><span data-stu-id="0fa26-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="0fa26-149">Título</span><span class="sxs-lookup"><span data-stu-id="0fa26-149">Title</span></span> | <span data-ttu-id="0fa26-150">Título</span><span class="sxs-lookup"><span data-stu-id="0fa26-150">Title</span></span> | <span data-ttu-id="0fa26-151">El identificador de paquete</span><span class="sxs-lookup"><span data-stu-id="0fa26-151">The PackageId</span></span>| |
| <span data-ttu-id="0fa26-152">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="0fa26-152">Description</span></span> | <span data-ttu-id="0fa26-153">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="0fa26-153">Description</span></span> | <span data-ttu-id="0fa26-154">"Descripción del paquete"</span><span class="sxs-lookup"><span data-stu-id="0fa26-154">"Package Description"</span></span> | |
| <span data-ttu-id="0fa26-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="0fa26-155">Copyright</span></span> | <span data-ttu-id="0fa26-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="0fa26-156">Copyright</span></span> | <span data-ttu-id="0fa26-157">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-157">empty</span></span> | |
| <span data-ttu-id="0fa26-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0fa26-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="0fa26-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0fa26-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="0fa26-160">false</span><span class="sxs-lookup"><span data-stu-id="0fa26-160">false</span></span> | |
| <span data-ttu-id="0fa26-161">sin</span><span class="sxs-lookup"><span data-stu-id="0fa26-161">license</span></span> | <span data-ttu-id="0fa26-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="0fa26-162">PackageLicenseExpression</span></span> | <span data-ttu-id="0fa26-163">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-163">empty</span></span> | <span data-ttu-id="0fa26-164">Corresponde a`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="0fa26-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="0fa26-165">sin</span><span class="sxs-lookup"><span data-stu-id="0fa26-165">license</span></span> | <span data-ttu-id="0fa26-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="0fa26-166">PackageLicenseFile</span></span> | <span data-ttu-id="0fa26-167">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-167">empty</span></span> | <span data-ttu-id="0fa26-168">Se corresponde con `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="0fa26-169">Es posible que deba empaquetar explícitamente el archivo de licencia al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="0fa26-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="0fa26-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-170">LicenseUrl</span></span> | <span data-ttu-id="0fa26-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-171">PackageLicenseUrl</span></span> | <span data-ttu-id="0fa26-172">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-172">empty</span></span> | <span data-ttu-id="0fa26-173">`PackageLicenseUrl`está en desuso, use la propiedad PackageLicenseExpression o PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="0fa26-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="0fa26-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-174">ProjectUrl</span></span> | <span data-ttu-id="0fa26-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-175">PackageProjectUrl</span></span> | <span data-ttu-id="0fa26-176">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-176">empty</span></span> | |
| <span data-ttu-id="0fa26-177">Iconos</span><span class="sxs-lookup"><span data-stu-id="0fa26-177">Icon</span></span> | <span data-ttu-id="0fa26-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="0fa26-178">PackageIcon</span></span> | <span data-ttu-id="0fa26-179">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-179">empty</span></span> | <span data-ttu-id="0fa26-180">Es posible que deba empaquetar explícitamente el archivo de imagen de icono al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="0fa26-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="0fa26-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-181">IconUrl</span></span> | <span data-ttu-id="0fa26-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-182">PackageIconUrl</span></span> | <span data-ttu-id="0fa26-183">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-183">empty</span></span> | <span data-ttu-id="0fa26-184">`PackageIconUrl`está en desuso, use la propiedad PackageIcon</span><span class="sxs-lookup"><span data-stu-id="0fa26-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="0fa26-185">`Tags`</span><span class="sxs-lookup"><span data-stu-id="0fa26-185">Tags</span></span> | <span data-ttu-id="0fa26-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0fa26-186">PackageTags</span></span> | <span data-ttu-id="0fa26-187">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-187">empty</span></span> | <span data-ttu-id="0fa26-188">Las etiquetas están delimitadas mediante punto y coma.</span><span class="sxs-lookup"><span data-stu-id="0fa26-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="0fa26-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0fa26-189">ReleaseNotes</span></span> | <span data-ttu-id="0fa26-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0fa26-190">PackageReleaseNotes</span></span> | <span data-ttu-id="0fa26-191">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-191">empty</span></span> | |
| <span data-ttu-id="0fa26-192">Repositorio/dirección URL</span><span class="sxs-lookup"><span data-stu-id="0fa26-192">Repository/Url</span></span> | <span data-ttu-id="0fa26-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-193">RepositoryUrl</span></span> | <span data-ttu-id="0fa26-194">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-194">empty</span></span> | <span data-ttu-id="0fa26-195">Dirección URL del repositorio usada para clonar o recuperar el código fuente.</span><span class="sxs-lookup"><span data-stu-id="0fa26-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="0fa26-196">Ejemplo *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="0fa26-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="0fa26-197">Repositorio/tipo</span><span class="sxs-lookup"><span data-stu-id="0fa26-197">Repository/Type</span></span> | <span data-ttu-id="0fa26-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0fa26-198">RepositoryType</span></span> | <span data-ttu-id="0fa26-199">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-199">empty</span></span> | <span data-ttu-id="0fa26-200">Tipo de repositorio.</span><span class="sxs-lookup"><span data-stu-id="0fa26-200">Repository type.</span></span> <span data-ttu-id="0fa26-201">Ejemplos: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="0fa26-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="0fa26-202">Repositorio/rama</span><span class="sxs-lookup"><span data-stu-id="0fa26-202">Repository/Branch</span></span> | <span data-ttu-id="0fa26-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="0fa26-203">RepositoryBranch</span></span> | <span data-ttu-id="0fa26-204">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-204">empty</span></span> | <span data-ttu-id="0fa26-205">Información opcional de la rama del repositorio.</span><span class="sxs-lookup"><span data-stu-id="0fa26-205">Optional repository branch information.</span></span> <span data-ttu-id="0fa26-206">También se debe especificar *RepositoryUrl* para que se incluya esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="0fa26-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="0fa26-207">Ejemplo: *maestra* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="0fa26-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="0fa26-208">Repositorio/confirmar</span><span class="sxs-lookup"><span data-stu-id="0fa26-208">Repository/Commit</span></span> | <span data-ttu-id="0fa26-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="0fa26-209">RepositoryCommit</span></span> | <span data-ttu-id="0fa26-210">vacío</span><span class="sxs-lookup"><span data-stu-id="0fa26-210">empty</span></span> | <span data-ttu-id="0fa26-211">Confirmación o conjunto de cambios de repositorio opcional para indicar en qué origen se compiló el paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="0fa26-212">También se debe especificar *RepositoryUrl* para que se incluya esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="0fa26-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="0fa26-213">Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="0fa26-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="0fa26-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="0fa26-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="0fa26-215">Resumen</span><span class="sxs-lookup"><span data-stu-id="0fa26-215">Summary</span></span> | <span data-ttu-id="0fa26-216">No compatible</span><span class="sxs-lookup"><span data-stu-id="0fa26-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="0fa26-217">Entradas de destino de pack</span><span class="sxs-lookup"><span data-stu-id="0fa26-217">pack target inputs</span></span>

- <span data-ttu-id="0fa26-218">IsPackable</span><span class="sxs-lookup"><span data-stu-id="0fa26-218">IsPackable</span></span>
- <span data-ttu-id="0fa26-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="0fa26-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="0fa26-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0fa26-220">PackageVersion</span></span>
- <span data-ttu-id="0fa26-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="0fa26-221">PackageId</span></span>
- <span data-ttu-id="0fa26-222">Authors</span><span class="sxs-lookup"><span data-stu-id="0fa26-222">Authors</span></span>
- <span data-ttu-id="0fa26-223">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="0fa26-223">Description</span></span>
- <span data-ttu-id="0fa26-224">Copyright</span><span class="sxs-lookup"><span data-stu-id="0fa26-224">Copyright</span></span>
- <span data-ttu-id="0fa26-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0fa26-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="0fa26-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="0fa26-226">DevelopmentDependency</span></span>
- <span data-ttu-id="0fa26-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="0fa26-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="0fa26-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="0fa26-228">PackageLicenseFile</span></span>
- <span data-ttu-id="0fa26-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="0fa26-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-230">PackageProjectUrl</span></span>
- <span data-ttu-id="0fa26-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-231">PackageIconUrl</span></span>
- <span data-ttu-id="0fa26-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0fa26-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="0fa26-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0fa26-233">PackageTags</span></span>
- <span data-ttu-id="0fa26-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="0fa26-234">PackageOutputPath</span></span>
- <span data-ttu-id="0fa26-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0fa26-235">IncludeSymbols</span></span>
- <span data-ttu-id="0fa26-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0fa26-236">IncludeSource</span></span>
- <span data-ttu-id="0fa26-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="0fa26-237">PackageTypes</span></span>
- <span data-ttu-id="0fa26-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="0fa26-238">IsTool</span></span>
- <span data-ttu-id="0fa26-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-239">RepositoryUrl</span></span>
- <span data-ttu-id="0fa26-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0fa26-240">RepositoryType</span></span>
- <span data-ttu-id="0fa26-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="0fa26-241">RepositoryBranch</span></span>
- <span data-ttu-id="0fa26-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="0fa26-242">RepositoryCommit</span></span>
- <span data-ttu-id="0fa26-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="0fa26-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="0fa26-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="0fa26-244">MinClientVersion</span></span>
- <span data-ttu-id="0fa26-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="0fa26-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="0fa26-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="0fa26-246">IncludeContentInPack</span></span>
- <span data-ttu-id="0fa26-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="0fa26-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="0fa26-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="0fa26-248">ContentTargetFolders</span></span>
- <span data-ttu-id="0fa26-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="0fa26-249">NuspecFile</span></span>
- <span data-ttu-id="0fa26-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="0fa26-250">NuspecBasePath</span></span>
- <span data-ttu-id="0fa26-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="0fa26-251">NuspecProperties</span></span>
- <span data-ttu-id="0fa26-252">Determinista</span><span class="sxs-lookup"><span data-stu-id="0fa26-252">Deterministic</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="0fa26-253">Escenarios de pack</span><span class="sxs-lookup"><span data-stu-id="0fa26-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="0fa26-254">Suprimir dependencias</span><span class="sxs-lookup"><span data-stu-id="0fa26-254">Suppress dependencies</span></span>

<span data-ttu-id="0fa26-255">Para suprimir las dependencias de paquete del paquete NuGet `SuppressDependenciesWhenPacking` generado `true` , establezca en, lo que permitirá omitir todas las dependencias del archivo nupkg generado.</span><span class="sxs-lookup"><span data-stu-id="0fa26-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="0fa26-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0fa26-256">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="0fa26-257">PackageIconUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="0fa26-257">PackageIconUrl is deprecated.</span></span> <span data-ttu-id="0fa26-258">Use [PackageIcon](#packing-an-icon-image-file) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="0fa26-258">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="0fa26-259">Empaquetar un archivo de imagen de icono</span><span class="sxs-lookup"><span data-stu-id="0fa26-259">Packing an icon image file</span></span>

<span data-ttu-id="0fa26-260">Al empaquetar un archivo de imagen de icono, debe usar la propiedad PackageIcon para especificar la ruta de acceso del paquete, relativa a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-260">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="0fa26-261">Además, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-261">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="0fa26-262">El tamaño del archivo de imagen está limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0fa26-262">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="0fa26-263">Entre los formatos de archivo admitidos se incluyen JPEG y PNG.</span><span class="sxs-lookup"><span data-stu-id="0fa26-263">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="0fa26-264">Se recomienda una resolución de imagen de 64 x 64.</span><span class="sxs-lookup"><span data-stu-id="0fa26-264">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="0fa26-265">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0fa26-265">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="0fa26-266">[Ejemplo de icono de paquete](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="0fa26-266">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="0fa26-267">En el caso del equivalente de nuspec, eche un vistazo a la [referencia de nuspec para el icono](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="0fa26-267">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="0fa26-268">Ensamblados de salida</span><span class="sxs-lookup"><span data-stu-id="0fa26-268">Output assemblies</span></span>

<span data-ttu-id="0fa26-269">`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-269">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="0fa26-270">Los archivos de salida que se copian dependen de lo que proporciona MSBuild desde el destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-270">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="0fa26-271">Hay dos propiedades de MSBuild que se pueden usar en el archivo de proyecto o la línea de comandos para controlar dónde van los ensamblados de salida:</span><span class="sxs-lookup"><span data-stu-id="0fa26-271">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="0fa26-272">`IncludeBuildOutput`: Un valor booleano que determina si los ensamblados de salida de la compilación deben incluirse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-272">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="0fa26-273">`BuildOutputTargetFolder`: Especifica la carpeta en la que se deben colocar los ensamblados de salida.</span><span class="sxs-lookup"><span data-stu-id="0fa26-273">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="0fa26-274">Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.</span><span class="sxs-lookup"><span data-stu-id="0fa26-274">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="0fa26-275">Referencias de paquete</span><span class="sxs-lookup"><span data-stu-id="0fa26-275">Package references</span></span>

<span data-ttu-id="0fa26-276">Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="0fa26-276">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="0fa26-277">Referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="0fa26-277">Project to project references</span></span>

<span data-ttu-id="0fa26-278">Las referencias entre proyectos se consideran de forma predeterminada como referencias de paquetes NuGet, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0fa26-278">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="0fa26-279">También puede agregar los metadatos siguientes a la referencia de proyecto:</span><span class="sxs-lookup"><span data-stu-id="0fa26-279">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="deterministic"></a><span data-ttu-id="0fa26-280">Determinista</span><span class="sxs-lookup"><span data-stu-id="0fa26-280">Deterministic</span></span>

<span data-ttu-id="0fa26-281">Cuando se `MSBuild -t:pack -p:Deterministic=true`usa, varias invocaciones del destino del paquete generarán el mismo paquete exacto.</span><span class="sxs-lookup"><span data-stu-id="0fa26-281">When using `MSBuild -t:pack -p:Deterministic=true`, multiple invocations of the the pack target will generate the exact same package.</span></span>
<span data-ttu-id="0fa26-282">La salida del comando Pack no se ve afectada por el estado ambiente de la máquina.</span><span class="sxs-lookup"><span data-stu-id="0fa26-282">The output of the pack command is not affected by the ambient state of the machine.</span></span> <span data-ttu-id="0fa26-283">En concreto, las entradas zip se marcarán como 1980-01-01.</span><span class="sxs-lookup"><span data-stu-id="0fa26-283">Specifically zip entries will be timestamped as 1980-01-01.</span></span> <span data-ttu-id="0fa26-284">Para lograr un determinismo completo, los ensamblados deben compilarse con la opción del compilador respectivo [-determinista](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span><span class="sxs-lookup"><span data-stu-id="0fa26-284">To achieve full determinism, the assemblies should be built with the respective compiler option [-deterministic](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span></span>
<span data-ttu-id="0fa26-285">Se recomienda especificar la propiedad determinista como la siguiente, por lo que el compilador y NuGet lo respetarán.</span><span class="sxs-lookup"><span data-stu-id="0fa26-285">It is recommended that you specify the deterministic property like following, so both the compiler and NuGet will respect it.</span></span>

```xml
<PropertyGroup>
  <Deterministic>true</Deterministic>
</PropertyGroup>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="0fa26-286">Inclusión de contenido en un paquete</span><span class="sxs-lookup"><span data-stu-id="0fa26-286">Including content in a package</span></span>

<span data-ttu-id="0fa26-287">Para incluir contenido, agregue metadatos adicionales al elemento `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="0fa26-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="0fa26-288">De forma predeterminada todos los elementos de tipo "Content" se incluyen en el paquete a menos que los reemplace con entradas como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fa26-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="0fa26-289">De forma predeterminada, todo el contenido se agrega a la raíz de la carpeta `content` y `contentFiles\any\<target_framework>` dentro de un paquete y se conserva la estructura de carpetas relativa, a menos que se especifique una ruta de acceso de paquete:</span><span class="sxs-lookup"><span data-stu-id="0fa26-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="0fa26-290">Si quiere copiar todo el contenido a una carpeta raíz determinada (en lugar de `content` y `contentFiles`), puede usar la propiedad `ContentTargetFolders` de MSBuild, cuyo valor predeterminado es "content;contentFiles", pero que se puede establecer en cualquier otro nombre de carpeta.</span><span class="sxs-lookup"><span data-stu-id="0fa26-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="0fa26-291">Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="0fa26-292">`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="0fa26-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="0fa26-293">Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="0fa26-294">Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:</span><span class="sxs-lookup"><span data-stu-id="0fa26-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="0fa26-295">También hay una propiedad `$(IncludeContentInPack)` de MSBuild, cuyo valor predeterminado es `true`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="0fa26-296">Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="0fa26-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="0fa26-297">Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen ```<PackageCopyToOutput>``` y ```<PackageFlatten>```, que establece los valores ```CopyToOutput``` y ```Flatten``` en la entrada ```contentFiles``` del archivo nuspec de salida.</span><span class="sxs-lookup"><span data-stu-id="0fa26-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="0fa26-298">Además de los elementos Content, los metadatos `<Pack>` y `<PackagePath>` también se pueden establecer en archivos con una acción de compilación Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="0fa26-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="0fa26-299">Para que el comando pack anexe el nombre de archivo a la ruta de acceso del paquete cuando se usan patrones globales, la ruta de acceso del paquete debe terminar con el carácter separador de carpeta; en caso contrario, la ruta de acceso del paquete se trata como la ruta de acceso completa, incluido el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="0fa26-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="0fa26-300">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0fa26-300">IncludeSymbols</span></span>

<span data-ttu-id="0fa26-301">Cuando se usa `MSBuild -t:pack -p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="0fa26-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="0fa26-302">Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="0fa26-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="0fa26-303">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0fa26-303">IncludeSource</span></span>

<span data-ttu-id="0fa26-304">Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="0fa26-305">Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="0fa26-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="0fa26-306">Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="0fa26-307">Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="0fa26-308">Empaquetado de una expresión de licencia o un archivo de licencia</span><span class="sxs-lookup"><span data-stu-id="0fa26-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="0fa26-309">Cuando se usa una expresión de licencia, se debe usar la propiedad PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="0fa26-309">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="0fa26-310">[Ejemplo de expresión de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="0fa26-310">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="0fa26-311">[Obtenga más información sobre las expresiones de licencia y las licencias que acepta NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="0fa26-311">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="0fa26-312">Al empaquetar un archivo de licencia, debe usar la propiedad PackageLicenseFile para especificar la ruta de acceso del paquete, relativa a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-312">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="0fa26-313">Además, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-313">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="0fa26-314">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0fa26-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="0fa26-315">[Ejemplo de archivo de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="0fa26-315">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="0fa26-316">IsTool</span><span class="sxs-lookup"><span data-stu-id="0fa26-316">IsTool</span></span>

<span data-ttu-id="0fa26-317">Cuando se usa `MSBuild -t:pack -p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-317">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="0fa26-318">Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-318">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="0fa26-319">Empaquetado mediante un archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="0fa26-319">Packing using a .nuspec</span></span>

<span data-ttu-id="0fa26-320">Aunque se recomienda [incluir todas las propiedades](../reference/msbuild-targets.md#pack-target) que suelen estar en el `.nuspec` archivo en el archivo del proyecto, puede optar por usar un `.nuspec` archivo para empaquetar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0fa26-320">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="0fa26-321">Para un proyecto que no sea de estilo SDK que `PackageReference`use, debe importar `NuGet.Build.Tasks.Pack.targets` para que se pueda ejecutar la tarea del paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-321">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="0fa26-322">Todavía es necesario restaurar el proyecto para poder empaquetar un archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="0fa26-322">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="0fa26-323">(Un proyecto de estilo SDK incluye los destinos Pack de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="0fa26-323">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="0fa26-324">El marco de trabajo de destino del archivo de proyecto es irrelevante y no se usa cuando se empaqueta un archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="0fa26-324">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="0fa26-325">Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="0fa26-325">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="0fa26-326">`NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.</span><span class="sxs-lookup"><span data-stu-id="0fa26-326">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="0fa26-327">`NuspecProperties`: lista de pares clave=valor separados por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="0fa26-327">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="0fa26-328">Debido al funcionamiento del análisis de línea de comandos de MSBuild, se deben especificar varias propiedades como se indica a continuación: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-328">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="0fa26-329">`NuspecBasePath`: Ruta de acceso base `.nuspec` del archivo.</span><span class="sxs-lookup"><span data-stu-id="0fa26-329">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="0fa26-330">Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fa26-330">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="0fa26-331">Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fa26-331">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="0fa26-332">Tenga en cuenta que al empaquetar un archivo nuspec mediante dotnet. exe o MSBuild también se genera el proyecto de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0fa26-332">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="0fa26-333">Esto se puede evitar pasando ```--no-build``` la propiedad a dotnet. exe, que es el equivalente de la configuración ```<NoBuild>true</NoBuild> ``` en el archivo de proyecto, junto ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` con el valor en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="0fa26-333">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="0fa26-334">Un ejemplo de un archivo *. csproj* para empaquetar un archivo nuspec es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fa26-334">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="0fa26-335">Puntos de extensión avanzados para crear un paquete personalizado</span><span class="sxs-lookup"><span data-stu-id="0fa26-335">Advanced extension points to create customized package</span></span>

<span data-ttu-id="0fa26-336">El `pack` destino proporciona dos puntos de extensión que se ejecutan en la compilación interna específica de la plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="0fa26-336">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="0fa26-337">Los puntos de extensión admiten, incluidos los ensamblados y el contenido específico de la plataforma de destino en un paquete:</span><span class="sxs-lookup"><span data-stu-id="0fa26-337">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="0fa26-338">`TargetsForTfmSpecificBuildOutput`dirigir Se usa para los archivos `lib` dentro de la carpeta o en `BuildOutputTargetFolder`una carpeta especificada mediante.</span><span class="sxs-lookup"><span data-stu-id="0fa26-338">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="0fa26-339">`TargetsForTfmSpecificContentInPackage`dirigir Se usa para archivos fuera `BuildOutputTargetFolder`de.</span><span class="sxs-lookup"><span data-stu-id="0fa26-339">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="0fa26-340">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="0fa26-340">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="0fa26-341">Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificBuildOutput)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="0fa26-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="0fa26-342">En el caso de los archivos que necesiten `BuildOutputTargetFolder` entrar en (de forma predeterminada, lib), el destino debe escribir esos `BuildOutputInPackage` archivos en el ItemGroup y establecer los dos valores de metadatos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0fa26-342">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="0fa26-343">`FinalOutputPath`: Ruta de acceso absoluta del archivo; Si no se proporciona, la identidad se utiliza para evaluar la ruta de acceso de origen.</span><span class="sxs-lookup"><span data-stu-id="0fa26-343">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="0fa26-344">`TargetPath`:  Opta Se establece cuando el archivo debe ir a una subcarpeta dentro de `lib\<TargetFramework>` , como los ensamblados satélite que se encuentran bajo sus respectivas carpetas de referencia cultural.</span><span class="sxs-lookup"><span data-stu-id="0fa26-344">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="0fa26-345">Tiene como valor predeterminado el nombre del archivo.</span><span class="sxs-lookup"><span data-stu-id="0fa26-345">Defaults to the name of the file.</span></span>

<span data-ttu-id="0fa26-346">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0fa26-346">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="0fa26-347">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="0fa26-347">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="0fa26-348">Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificContentInPackage)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="0fa26-348">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="0fa26-349">En el caso de los archivos que se van a incluir en el paquete, el destino debe `TfmSpecificPackageFile` escribir esos archivos en el ItemGroup y establecer los metadatos opcionales siguientes:</span><span class="sxs-lookup"><span data-stu-id="0fa26-349">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="0fa26-350">`PackagePath`: Ruta de acceso en la que el archivo debe generarse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-350">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="0fa26-351">NuGet emite una advertencia si se agrega más de un archivo a la misma ruta de acceso del paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-351">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="0fa26-352">`BuildAction`: Acción de compilación que se va a asignar al archivo, que solo es necesario si la ruta `contentFiles` de acceso del paquete está en la carpeta.</span><span class="sxs-lookup"><span data-stu-id="0fa26-352">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="0fa26-353">El valor predeterminado es "none".</span><span class="sxs-lookup"><span data-stu-id="0fa26-353">Defaults to "None".</span></span>

<span data-ttu-id="0fa26-354">Un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0fa26-354">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="0fa26-355">Destino de restore</span><span class="sxs-lookup"><span data-stu-id="0fa26-355">restore target</span></span>

<span data-ttu-id="0fa26-356">`MSBuild -t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="0fa26-356">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="0fa26-357">Leer todas las referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="0fa26-357">Read all project to project references</span></span>
1. <span data-ttu-id="0fa26-358">Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias</span><span class="sxs-lookup"><span data-stu-id="0fa26-358">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="0fa26-359">Pasar datos de MSBuild a NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="0fa26-359">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="0fa26-360">Ejecutar la restauración</span><span class="sxs-lookup"><span data-stu-id="0fa26-360">Run restore</span></span>
1. <span data-ttu-id="0fa26-361">Descargar los paquetes</span><span class="sxs-lookup"><span data-stu-id="0fa26-361">Download packages</span></span>
1. <span data-ttu-id="0fa26-362">Escribir el archivo de activos, destinos y propiedades</span><span class="sxs-lookup"><span data-stu-id="0fa26-362">Write assets file, targets, and props</span></span>

<span data-ttu-id="0fa26-363">El `restore` destino **solo** funciona con los proyectos que usan el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0fa26-363">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="0fa26-364">**No** funciona para los proyectos que usan el `packages.config` formato; use la [restauración de Nuget](../reference/cli-reference/cli-ref-restore.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="0fa26-364">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="0fa26-365">Restaurar las propiedades</span><span class="sxs-lookup"><span data-stu-id="0fa26-365">Restore properties</span></span>

<span data-ttu-id="0fa26-366">Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="0fa26-366">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="0fa26-367">También se pueden establecer valores desde la línea de comandos mediante el modificador `-p:` (vea los ejemplos siguientes).</span><span class="sxs-lookup"><span data-stu-id="0fa26-367">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="0fa26-368">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0fa26-368">Property</span></span> | <span data-ttu-id="0fa26-369">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="0fa26-369">Description</span></span> |
|--------|--------|
| <span data-ttu-id="0fa26-370">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="0fa26-370">RestoreSources</span></span> | <span data-ttu-id="0fa26-371">Lista delimitada por punto y coma de orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="0fa26-371">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="0fa26-372">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="0fa26-372">RestorePackagesPath</span></span> | <span data-ttu-id="0fa26-373">Ruta de acceso de la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="0fa26-373">User packages folder path.</span></span> |
| <span data-ttu-id="0fa26-374">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="0fa26-374">RestoreDisableParallel</span></span> | <span data-ttu-id="0fa26-375">Limitar las descargas a una cada vez.</span><span class="sxs-lookup"><span data-stu-id="0fa26-375">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="0fa26-376">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="0fa26-376">RestoreConfigFile</span></span> | <span data-ttu-id="0fa26-377">Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="0fa26-377">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="0fa26-378">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="0fa26-378">RestoreNoCache</span></span> | <span data-ttu-id="0fa26-379">Si es true, evita el uso de paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="0fa26-379">If true, avoids using cached packages.</span></span> <span data-ttu-id="0fa26-380">Consulte [Administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="0fa26-380">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="0fa26-381">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="0fa26-381">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="0fa26-382">Si es true, ignora los orígenes de paquetes que producen errores o faltan.</span><span class="sxs-lookup"><span data-stu-id="0fa26-382">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="0fa26-383">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="0fa26-383">RestoreFallbackFolders</span></span> | <span data-ttu-id="0fa26-384">Carpetas de reserva que se usan de la misma manera que se usa la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="0fa26-384">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="0fa26-385">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="0fa26-385">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="0fa26-386">Fuentes adicionales para usar durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="0fa26-386">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="0fa26-387">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="0fa26-387">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="0fa26-388">Carpetas de reserva adicionales para usar durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="0fa26-388">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="0fa26-389">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="0fa26-389">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="0fa26-390">Excluye las carpetas de reserva especificadas en`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="0fa26-390">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="0fa26-391">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="0fa26-391">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="0fa26-392">Ruta de acceso a `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-392">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="0fa26-393">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="0fa26-393">RestoreGraphProjectInput</span></span> | <span data-ttu-id="0fa26-394">Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="0fa26-394">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="0fa26-395">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="0fa26-395">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="0fa26-396">Cuando los proyectos se recopilan a través de MSBuild, determina si se recopilan con la `SkipNonexistentTargets` optimización.</span><span class="sxs-lookup"><span data-stu-id="0fa26-396">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="0fa26-397">Cuando no se `true`establece, el valor predeterminado es.</span><span class="sxs-lookup"><span data-stu-id="0fa26-397">When not set, defaults to `true`.</span></span> <span data-ttu-id="0fa26-398">La consecuencia es un comportamiento de error rápido cuando no se pueden importar los destinos de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="0fa26-398">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="0fa26-399">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="0fa26-399">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="0fa26-400">Carpeta de salida, que `BaseIntermediateOutputPath` tiene como valor predeterminado y la `obj` carpeta.</span><span class="sxs-lookup"><span data-stu-id="0fa26-400">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="0fa26-401">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="0fa26-401">Examples</span></span>

<span data-ttu-id="0fa26-402">Línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="0fa26-402">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="0fa26-403">Archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="0fa26-403">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="0fa26-404">Restaurar salidas</span><span class="sxs-lookup"><span data-stu-id="0fa26-404">Restore outputs</span></span>

<span data-ttu-id="0fa26-405">La restauración crea los archivos siguientes en la carpeta `obj` de compilación:</span><span class="sxs-lookup"><span data-stu-id="0fa26-405">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="0fa26-406">Archivo</span><span class="sxs-lookup"><span data-stu-id="0fa26-406">File</span></span> | <span data-ttu-id="0fa26-407">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="0fa26-407">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="0fa26-408">Contiene el gráfico de dependencias de todas las referencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="0fa26-408">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="0fa26-409">Referencias a propiedades de MSBuild incluidas en paquetes</span><span class="sxs-lookup"><span data-stu-id="0fa26-409">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="0fa26-410">Referencias a destinos de MSBuild incluidos en paquetes</span><span class="sxs-lookup"><span data-stu-id="0fa26-410">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="0fa26-411">Restaurar y compilar con un comando de MSBuild</span><span class="sxs-lookup"><span data-stu-id="0fa26-411">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="0fa26-412">Debido al hecho de que NuGet puede restaurar paquetes que desactivan los destinos y las propiedades de MSBuild, las evaluaciones de la restauración y de la compilación se ejecutan con propiedades globales diferentes.</span><span class="sxs-lookup"><span data-stu-id="0fa26-412">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="0fa26-413">Esto significa que el siguiente tendrá un comportamiento imprevisible y a menudo incorrecto.</span><span class="sxs-lookup"><span data-stu-id="0fa26-413">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="0fa26-414">En su lugar, el enfoque recomendado es:</span><span class="sxs-lookup"><span data-stu-id="0fa26-414">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="0fa26-415">La misma lógica se aplica a otros destinos similares `build`a.</span><span class="sxs-lookup"><span data-stu-id="0fa26-415">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="0fa26-416">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="0fa26-416">PackageTargetFallback</span></span>

<span data-ttu-id="0fa26-417">El elemento `PackageTargetFallback` permite especificar un conjunto de destinos compatibles que se usarán al restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="0fa26-417">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="0fa26-418">Está diseñado para permitir que los paquetes que usan un [TxM](../reference/target-frameworks.md) de dotnet funcionen con paquetes compatibles que no declaran un TxM de dotnet.</span><span class="sxs-lookup"><span data-stu-id="0fa26-418">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="0fa26-419">Es decir, si el proyecto usa el TxM de dotnet, todos los paquetes de los que depende también deben tener un TxM de dotnet, a menos que agregue `<PackageTargetFallback>` al proyecto para permitir que las plataformas que no sean de dotnet sean compatibles con dotnet.</span><span class="sxs-lookup"><span data-stu-id="0fa26-419">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="0fa26-420">Por ejemplo, si el proyecto usa el TxM `netstandard1.6` y un paquete dependiente solo contiene `lib/net45/a.dll` y `lib/portable-net45+win81/a.dll`, se producirá un error al compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0fa26-420">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="0fa26-421">Si lo que quiere incluir es el último archivo DLL, puede agregar `PackageTargetFallback` como se indica a continuación para indicar que el archivo DLL `portable-net45+win81` es compatible:</span><span class="sxs-lookup"><span data-stu-id="0fa26-421">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="0fa26-422">Para declarar una reserva para todos los destinos del proyecto, excluya el atributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="0fa26-422">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="0fa26-423">También puede extender cualquier `PackageTargetFallback` existente mediante la inclusión de `$(PackageTargetFallback)` como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="0fa26-423">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="0fa26-424">Reemplazo de una biblioteca desde un gráfico de restauración</span><span class="sxs-lookup"><span data-stu-id="0fa26-424">Replacing one library from a restore graph</span></span>

<span data-ttu-id="0fa26-425">Si una restauración agrega el ensamblado equivocado, se puede excluir la opción predeterminada de ese paquete y reemplazarla por una de su propia elección.</span><span class="sxs-lookup"><span data-stu-id="0fa26-425">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="0fa26-426">En primer lugar, con una `PackageReference` de nivel superior, excluya todos los activos:</span><span class="sxs-lookup"><span data-stu-id="0fa26-426">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="0fa26-427">Después, agregue su propia referencia a la copia local correspondiente del archivo DLL:</span><span class="sxs-lookup"><span data-stu-id="0fa26-427">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
