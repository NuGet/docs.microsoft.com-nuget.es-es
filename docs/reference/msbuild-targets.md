---
title: pack y restore de NuGet como destinos de MSBuild
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: a9331ad2ea0482737d84f4ea9a9babf95da8d66f
ms.sourcegitcommit: d5cc3f01a92c2d69b794343c09aff07ba9e912e5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2019
ms.locfileid: "70385901"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="c7dac-103">pack y restore de NuGet como destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="c7dac-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="c7dac-104">*NuGet 4.0 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="c7dac-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="c7dac-105">Con el formato [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + puede almacenar todos los metadatos del manifiesto directamente dentro de un archivo de proyecto `.nuspec` en lugar de usar un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="c7dac-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="c7dac-106">Con MSBuild 15.1 y versiones posteriores, NuGet es también un ciudadano de MSBuild de primera clase con los destinos `pack` y `restore` como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="c7dac-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="c7dac-107">Estos destinos permiten trabajar con NuGet como lo haría con cualquier otra tarea o destino de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c7dac-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="c7dac-108">Para obtener instrucciones sobre cómo crear un paquete NuGet con MSBuild, consulte [crear un paquete Nuget con MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="c7dac-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="c7dac-109">(Para NuGet 3.x y versiones anteriores, los comandos [pack](../reference/cli-reference/cli-ref-pack.md) y [restore](../reference/cli-reference/cli-ref-restore.md) se usan a través de la CLI de NuGet en su lugar).</span><span class="sxs-lookup"><span data-stu-id="c7dac-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="c7dac-110">Orden de compilación de destinos</span><span class="sxs-lookup"><span data-stu-id="c7dac-110">Target build order</span></span>

<span data-ttu-id="c7dac-111">Dado que `pack` y `restore` son destinos de MSBuild, puede tener acceso a ellos para mejorar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c7dac-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="c7dac-112">Por ejemplo, supongamos que quiere copiar el paquete en un recurso compartido de red después de empaquetarlo.</span><span class="sxs-lookup"><span data-stu-id="c7dac-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="c7dac-113">Puede hacer esto si agrega lo siguiente al archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="c7dac-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="c7dac-114">De forma similar, puede escribir una tarea de MSBuild, su propio destino y usar propiedades de NuGet en la tarea de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c7dac-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="c7dac-115">`$(OutputPath)`es relativo y espera que se ejecute el comando desde la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c7dac-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="c7dac-116">Destino de pack</span><span class="sxs-lookup"><span data-stu-id="c7dac-116">pack target</span></span>

<span data-ttu-id="c7dac-117">En el caso de los proyectos de .net Standard con `msbuild -t:pack` el formato PackageReference, el uso de dibuja entradas del archivo de proyecto para usarlas en la creación de un paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="c7dac-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="c7dac-118">En la tabla siguiente se describen las propiedades de MSBuild que se pueden agregar a un archivo de proyecto en el primer nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="c7dac-119">Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="c7dac-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="c7dac-120">Para mayor comodidad, la tabla se organiza por la propiedad equivalente en un [archivo `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="c7dac-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="c7dac-121">Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c7dac-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="c7dac-122">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="c7dac-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="c7dac-123">Propiedad de MSBuild</span><span class="sxs-lookup"><span data-stu-id="c7dac-123">MSBuild Property</span></span> | <span data-ttu-id="c7dac-124">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c7dac-124">Default</span></span> | <span data-ttu-id="c7dac-125">Notas</span><span class="sxs-lookup"><span data-stu-id="c7dac-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="c7dac-126">Id</span><span class="sxs-lookup"><span data-stu-id="c7dac-126">Id</span></span> | <span data-ttu-id="c7dac-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="c7dac-127">PackageId</span></span> | <span data-ttu-id="c7dac-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="c7dac-128">AssemblyName</span></span> | <span data-ttu-id="c7dac-129">$(NombreDeEnsamblado) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="c7dac-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="c7dac-130">`Version`</span><span class="sxs-lookup"><span data-stu-id="c7dac-130">Version</span></span> | <span data-ttu-id="c7dac-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="c7dac-131">PackageVersion</span></span> | <span data-ttu-id="c7dac-132">`Version`</span><span class="sxs-lookup"><span data-stu-id="c7dac-132">Version</span></span> | <span data-ttu-id="c7dac-133">Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="c7dac-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="c7dac-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c7dac-134">VersionPrefix</span></span> | <span data-ttu-id="c7dac-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c7dac-135">PackageVersionPrefix</span></span> | <span data-ttu-id="c7dac-136">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-136">empty</span></span> | <span data-ttu-id="c7dac-137">Al establecer PackageVersion se sobrescribe PackageVersionPrefix.</span><span class="sxs-lookup"><span data-stu-id="c7dac-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="c7dac-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c7dac-138">VersionSuffix</span></span> | <span data-ttu-id="c7dac-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c7dac-139">PackageVersionSuffix</span></span> | <span data-ttu-id="c7dac-140">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-140">empty</span></span> | <span data-ttu-id="c7dac-141">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c7dac-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="c7dac-142">Al establecer PackageVersion se sobrescribe PackageVersionSuffix.</span><span class="sxs-lookup"><span data-stu-id="c7dac-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="c7dac-143">Authors</span><span class="sxs-lookup"><span data-stu-id="c7dac-143">Authors</span></span> | <span data-ttu-id="c7dac-144">Authors</span><span class="sxs-lookup"><span data-stu-id="c7dac-144">Authors</span></span> | <span data-ttu-id="c7dac-145">Nombre del usuario actual</span><span class="sxs-lookup"><span data-stu-id="c7dac-145">Username of the current user</span></span> | |
| <span data-ttu-id="c7dac-146">Owners</span><span class="sxs-lookup"><span data-stu-id="c7dac-146">Owners</span></span> | <span data-ttu-id="c7dac-147">N/D</span><span class="sxs-lookup"><span data-stu-id="c7dac-147">N/A</span></span> | <span data-ttu-id="c7dac-148">No está presente en el archivo NuSpec</span><span class="sxs-lookup"><span data-stu-id="c7dac-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="c7dac-149">Título</span><span class="sxs-lookup"><span data-stu-id="c7dac-149">Title</span></span> | <span data-ttu-id="c7dac-150">Título</span><span class="sxs-lookup"><span data-stu-id="c7dac-150">Title</span></span> | <span data-ttu-id="c7dac-151">El identificador de paquete</span><span class="sxs-lookup"><span data-stu-id="c7dac-151">The PackageId</span></span>| |
| <span data-ttu-id="c7dac-152">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="c7dac-152">Description</span></span> | <span data-ttu-id="c7dac-153">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="c7dac-153">Description</span></span> | <span data-ttu-id="c7dac-154">"Descripción del paquete"</span><span class="sxs-lookup"><span data-stu-id="c7dac-154">"Package Description"</span></span> | |
| <span data-ttu-id="c7dac-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="c7dac-155">Copyright</span></span> | <span data-ttu-id="c7dac-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="c7dac-156">Copyright</span></span> | <span data-ttu-id="c7dac-157">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-157">empty</span></span> | |
| <span data-ttu-id="c7dac-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c7dac-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="c7dac-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c7dac-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="c7dac-160">false</span><span class="sxs-lookup"><span data-stu-id="c7dac-160">false</span></span> | |
| <span data-ttu-id="c7dac-161">sin</span><span class="sxs-lookup"><span data-stu-id="c7dac-161">license</span></span> | <span data-ttu-id="c7dac-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="c7dac-162">PackageLicenseExpression</span></span> | <span data-ttu-id="c7dac-163">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-163">empty</span></span> | <span data-ttu-id="c7dac-164">Corresponde a`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="c7dac-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="c7dac-165">sin</span><span class="sxs-lookup"><span data-stu-id="c7dac-165">license</span></span> | <span data-ttu-id="c7dac-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c7dac-166">PackageLicenseFile</span></span> | <span data-ttu-id="c7dac-167">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-167">empty</span></span> | <span data-ttu-id="c7dac-168">Se corresponde con `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="c7dac-169">Es posible que deba empaquetar explícitamente el archivo de licencia al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="c7dac-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="c7dac-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-170">LicenseUrl</span></span> | <span data-ttu-id="c7dac-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-171">PackageLicenseUrl</span></span> | <span data-ttu-id="c7dac-172">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-172">empty</span></span> | <span data-ttu-id="c7dac-173">`PackageLicenseUrl`está en desuso, use la propiedad PackageLicenseExpression o PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c7dac-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="c7dac-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-174">ProjectUrl</span></span> | <span data-ttu-id="c7dac-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-175">PackageProjectUrl</span></span> | <span data-ttu-id="c7dac-176">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-176">empty</span></span> | |
| <span data-ttu-id="c7dac-177">Iconos</span><span class="sxs-lookup"><span data-stu-id="c7dac-177">Icon</span></span> | <span data-ttu-id="c7dac-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="c7dac-178">PackageIcon</span></span> | <span data-ttu-id="c7dac-179">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-179">empty</span></span> | <span data-ttu-id="c7dac-180">Es posible que deba empaquetar explícitamente el archivo de imagen de icono al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="c7dac-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="c7dac-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-181">IconUrl</span></span> | <span data-ttu-id="c7dac-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-182">PackageIconUrl</span></span> | <span data-ttu-id="c7dac-183">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-183">empty</span></span> | <span data-ttu-id="c7dac-184">`PackageIconUrl`está en desuso, use la propiedad PackageIcon</span><span class="sxs-lookup"><span data-stu-id="c7dac-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="c7dac-185">`Tags`</span><span class="sxs-lookup"><span data-stu-id="c7dac-185">Tags</span></span> | <span data-ttu-id="c7dac-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="c7dac-186">PackageTags</span></span> | <span data-ttu-id="c7dac-187">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-187">empty</span></span> | <span data-ttu-id="c7dac-188">Las etiquetas están delimitadas mediante punto y coma.</span><span class="sxs-lookup"><span data-stu-id="c7dac-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="c7dac-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c7dac-189">ReleaseNotes</span></span> | <span data-ttu-id="c7dac-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c7dac-190">PackageReleaseNotes</span></span> | <span data-ttu-id="c7dac-191">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-191">empty</span></span> | |
| <span data-ttu-id="c7dac-192">Repositorio/dirección URL</span><span class="sxs-lookup"><span data-stu-id="c7dac-192">Repository/Url</span></span> | <span data-ttu-id="c7dac-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-193">RepositoryUrl</span></span> | <span data-ttu-id="c7dac-194">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-194">empty</span></span> | <span data-ttu-id="c7dac-195">Dirección URL del repositorio usada para clonar o recuperar el código fuente.</span><span class="sxs-lookup"><span data-stu-id="c7dac-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="c7dac-196">Ejemplo *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="c7dac-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="c7dac-197">Repositorio/tipo</span><span class="sxs-lookup"><span data-stu-id="c7dac-197">Repository/Type</span></span> | <span data-ttu-id="c7dac-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="c7dac-198">RepositoryType</span></span> | <span data-ttu-id="c7dac-199">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-199">empty</span></span> | <span data-ttu-id="c7dac-200">Tipo de repositorio.</span><span class="sxs-lookup"><span data-stu-id="c7dac-200">Repository type.</span></span> <span data-ttu-id="c7dac-201">Ejemplos: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="c7dac-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="c7dac-202">Repositorio/rama</span><span class="sxs-lookup"><span data-stu-id="c7dac-202">Repository/Branch</span></span> | <span data-ttu-id="c7dac-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="c7dac-203">RepositoryBranch</span></span> | <span data-ttu-id="c7dac-204">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-204">empty</span></span> | <span data-ttu-id="c7dac-205">Información opcional de la rama del repositorio.</span><span class="sxs-lookup"><span data-stu-id="c7dac-205">Optional repository branch information.</span></span> <span data-ttu-id="c7dac-206">También se debe especificar *RepositoryUrl* para que se incluya esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="c7dac-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="c7dac-207">Ejemplo: *maestra* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="c7dac-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="c7dac-208">Repositorio/confirmar</span><span class="sxs-lookup"><span data-stu-id="c7dac-208">Repository/Commit</span></span> | <span data-ttu-id="c7dac-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="c7dac-209">RepositoryCommit</span></span> | <span data-ttu-id="c7dac-210">vacío</span><span class="sxs-lookup"><span data-stu-id="c7dac-210">empty</span></span> | <span data-ttu-id="c7dac-211">Confirmación o conjunto de cambios de repositorio opcional para indicar en qué origen se compiló el paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="c7dac-212">También se debe especificar *RepositoryUrl* para que se incluya esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="c7dac-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="c7dac-213">Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="c7dac-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="c7dac-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="c7dac-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="c7dac-215">Resumen</span><span class="sxs-lookup"><span data-stu-id="c7dac-215">Summary</span></span> | <span data-ttu-id="c7dac-216">No compatible</span><span class="sxs-lookup"><span data-stu-id="c7dac-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="c7dac-217">Entradas de destino de pack</span><span class="sxs-lookup"><span data-stu-id="c7dac-217">pack target inputs</span></span>

- <span data-ttu-id="c7dac-218">IsPackable</span><span class="sxs-lookup"><span data-stu-id="c7dac-218">IsPackable</span></span>
- <span data-ttu-id="c7dac-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="c7dac-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="c7dac-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="c7dac-220">PackageVersion</span></span>
- <span data-ttu-id="c7dac-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="c7dac-221">PackageId</span></span>
- <span data-ttu-id="c7dac-222">Authors</span><span class="sxs-lookup"><span data-stu-id="c7dac-222">Authors</span></span>
- <span data-ttu-id="c7dac-223">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="c7dac-223">Description</span></span>
- <span data-ttu-id="c7dac-224">Copyright</span><span class="sxs-lookup"><span data-stu-id="c7dac-224">Copyright</span></span>
- <span data-ttu-id="c7dac-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c7dac-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="c7dac-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="c7dac-226">DevelopmentDependency</span></span>
- <span data-ttu-id="c7dac-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="c7dac-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="c7dac-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c7dac-228">PackageLicenseFile</span></span>
- <span data-ttu-id="c7dac-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="c7dac-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-230">PackageProjectUrl</span></span>
- <span data-ttu-id="c7dac-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-231">PackageIconUrl</span></span>
- <span data-ttu-id="c7dac-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c7dac-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="c7dac-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="c7dac-233">PackageTags</span></span>
- <span data-ttu-id="c7dac-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="c7dac-234">PackageOutputPath</span></span>
- <span data-ttu-id="c7dac-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="c7dac-235">IncludeSymbols</span></span>
- <span data-ttu-id="c7dac-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="c7dac-236">IncludeSource</span></span>
- <span data-ttu-id="c7dac-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="c7dac-237">PackageTypes</span></span>
- <span data-ttu-id="c7dac-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="c7dac-238">IsTool</span></span>
- <span data-ttu-id="c7dac-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-239">RepositoryUrl</span></span>
- <span data-ttu-id="c7dac-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="c7dac-240">RepositoryType</span></span>
- <span data-ttu-id="c7dac-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="c7dac-241">RepositoryBranch</span></span>
- <span data-ttu-id="c7dac-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="c7dac-242">RepositoryCommit</span></span>
- <span data-ttu-id="c7dac-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="c7dac-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="c7dac-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="c7dac-244">MinClientVersion</span></span>
- <span data-ttu-id="c7dac-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="c7dac-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="c7dac-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="c7dac-246">IncludeContentInPack</span></span>
- <span data-ttu-id="c7dac-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="c7dac-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="c7dac-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="c7dac-248">ContentTargetFolders</span></span>
- <span data-ttu-id="c7dac-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="c7dac-249">NuspecFile</span></span>
- <span data-ttu-id="c7dac-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="c7dac-250">NuspecBasePath</span></span>
- <span data-ttu-id="c7dac-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="c7dac-251">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="c7dac-252">Escenarios de pack</span><span class="sxs-lookup"><span data-stu-id="c7dac-252">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="c7dac-253">Suprimir dependencias</span><span class="sxs-lookup"><span data-stu-id="c7dac-253">Suppress dependencies</span></span>

<span data-ttu-id="c7dac-254">Para suprimir las dependencias de paquete del paquete NuGet `SuppressDependenciesWhenPacking` generado `true` , establezca en, lo que permitirá omitir todas las dependencias del archivo nupkg generado.</span><span class="sxs-lookup"><span data-stu-id="c7dac-254">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="c7dac-255">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c7dac-255">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="c7dac-256">PackageIconUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="c7dac-256">PackageIconUrl is deprecated.</span></span> <span data-ttu-id="c7dac-257">Use [PackageIcon](#packing-an-icon-image-file) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="c7dac-257">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="c7dac-258">Empaquetar un archivo de imagen de icono</span><span class="sxs-lookup"><span data-stu-id="c7dac-258">Packing an icon image file</span></span>

<span data-ttu-id="c7dac-259">Al empaquetar un archivo de imagen de icono, debe usar la propiedad PackageIcon para especificar la ruta de acceso del paquete, relativa a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-259">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="c7dac-260">Además, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-260">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="c7dac-261">El tamaño del archivo de imagen está limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="c7dac-261">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="c7dac-262">Entre los formatos de archivo admitidos se incluyen JPEG y PNG.</span><span class="sxs-lookup"><span data-stu-id="c7dac-262">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="c7dac-263">Se recomienda una resolución de imagen de 64 x 64.</span><span class="sxs-lookup"><span data-stu-id="c7dac-263">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="c7dac-264">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c7dac-264">For example:</span></span>

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

<span data-ttu-id="c7dac-265">[Ejemplo de icono de paquete](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="c7dac-265">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="c7dac-266">En el caso del equivalente de nuspec, eche un vistazo a la [referencia de nuspec para el icono](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="c7dac-266">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="c7dac-267">Ensamblados de salida</span><span class="sxs-lookup"><span data-stu-id="c7dac-267">Output assemblies</span></span>

<span data-ttu-id="c7dac-268">`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-268">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="c7dac-269">Los archivos de salida que se copian dependen de lo que proporciona MSBuild desde el destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-269">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="c7dac-270">Hay dos propiedades de MSBuild que se pueden usar en el archivo de proyecto o la línea de comandos para controlar dónde van los ensamblados de salida:</span><span class="sxs-lookup"><span data-stu-id="c7dac-270">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="c7dac-271">`IncludeBuildOutput`: Un valor booleano que determina si los ensamblados de salida de la compilación deben incluirse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-271">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="c7dac-272">`BuildOutputTargetFolder`: Especifica la carpeta en la que se deben colocar los ensamblados de salida.</span><span class="sxs-lookup"><span data-stu-id="c7dac-272">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="c7dac-273">Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.</span><span class="sxs-lookup"><span data-stu-id="c7dac-273">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="c7dac-274">Referencias de paquete</span><span class="sxs-lookup"><span data-stu-id="c7dac-274">Package references</span></span>

<span data-ttu-id="c7dac-275">Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="c7dac-275">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="c7dac-276">Referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="c7dac-276">Project to project references</span></span>

<span data-ttu-id="c7dac-277">Las referencias entre proyectos se consideran de forma predeterminada como referencias de paquetes NuGet, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c7dac-277">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="c7dac-278">También puede agregar los metadatos siguientes a la referencia de proyecto:</span><span class="sxs-lookup"><span data-stu-id="c7dac-278">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="c7dac-279">Inclusión de contenido en un paquete</span><span class="sxs-lookup"><span data-stu-id="c7dac-279">Including content in a package</span></span>

<span data-ttu-id="c7dac-280">Para incluir contenido, agregue metadatos adicionales al elemento `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="c7dac-280">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="c7dac-281">De forma predeterminada todos los elementos de tipo "Content" se incluyen en el paquete a menos que los reemplace con entradas como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7dac-281">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="c7dac-282">De forma predeterminada, todo el contenido se agrega a la raíz de la carpeta `content` y `contentFiles\any\<target_framework>` dentro de un paquete y se conserva la estructura de carpetas relativa, a menos que se especifique una ruta de acceso de paquete:</span><span class="sxs-lookup"><span data-stu-id="c7dac-282">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="c7dac-283">Si quiere copiar todo el contenido a una carpeta raíz determinada (en lugar de `content` y `contentFiles`), puede usar la propiedad `ContentTargetFolders` de MSBuild, cuyo valor predeterminado es "content;contentFiles", pero que se puede establecer en cualquier otro nombre de carpeta.</span><span class="sxs-lookup"><span data-stu-id="c7dac-283">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="c7dac-284">Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-284">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="c7dac-285">`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="c7dac-285">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="c7dac-286">Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-286">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="c7dac-287">Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:</span><span class="sxs-lookup"><span data-stu-id="c7dac-287">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="c7dac-288">También hay una propiedad `$(IncludeContentInPack)` de MSBuild, cuyo valor predeterminado es `true`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-288">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="c7dac-289">Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="c7dac-289">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="c7dac-290">Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen ```<PackageCopyToOutput>``` y ```<PackageFlatten>```, que establece los valores ```CopyToOutput``` y ```Flatten``` en la entrada ```contentFiles``` del archivo nuspec de salida.</span><span class="sxs-lookup"><span data-stu-id="c7dac-290">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="c7dac-291">Además de los elementos Content, los metadatos `<Pack>` y `<PackagePath>` también se pueden establecer en archivos con una acción de compilación Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="c7dac-291">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="c7dac-292">Para que el comando pack anexe el nombre de archivo a la ruta de acceso del paquete cuando se usan patrones globales, la ruta de acceso del paquete debe terminar con el carácter separador de carpeta; en caso contrario, la ruta de acceso del paquete se trata como la ruta de acceso completa, incluido el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="c7dac-292">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="c7dac-293">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="c7dac-293">IncludeSymbols</span></span>

<span data-ttu-id="c7dac-294">Cuando se usa `MSBuild -t:pack -p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="c7dac-294">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="c7dac-295">Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="c7dac-295">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="c7dac-296">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="c7dac-296">IncludeSource</span></span>

<span data-ttu-id="c7dac-297">Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-297">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="c7dac-298">Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="c7dac-298">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="c7dac-299">Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-299">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="c7dac-300">Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-300">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="c7dac-301">Empaquetado de una expresión de licencia o un archivo de licencia</span><span class="sxs-lookup"><span data-stu-id="c7dac-301">Packing a license expression or a license file</span></span>

<span data-ttu-id="c7dac-302">Cuando se usa una expresión de licencia, se debe usar la propiedad PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="c7dac-302">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="c7dac-303">[Ejemplo de expresión de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="c7dac-303">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="c7dac-304">[Obtenga más información sobre las expresiones de licencia y las licencias que acepta NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="c7dac-304">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="c7dac-305">Al empaquetar un archivo de licencia, debe usar la propiedad PackageLicenseFile para especificar la ruta de acceso del paquete, relativa a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-305">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="c7dac-306">Además, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-306">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="c7dac-307">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c7dac-307">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="c7dac-308">[Ejemplo de archivo de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="c7dac-308">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="c7dac-309">IsTool</span><span class="sxs-lookup"><span data-stu-id="c7dac-309">IsTool</span></span>

<span data-ttu-id="c7dac-310">Cuando se usa `MSBuild -t:pack -p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-310">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="c7dac-311">Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-311">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="c7dac-312">Empaquetado mediante un archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="c7dac-312">Packing using a .nuspec</span></span>

<span data-ttu-id="c7dac-313">Aunque se recomienda [incluir todas las propiedades](../reference/msbuild-targets.md#pack-target) que suelen estar en el `.nuspec` archivo en el archivo del proyecto, puede optar por usar un `.nuspec` archivo para empaquetar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="c7dac-313">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="c7dac-314">Para un proyecto que no sea de estilo SDK que `PackageReference`use, debe importar `NuGet.Build.Tasks.Pack.targets` para que se pueda ejecutar la tarea del paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-314">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="c7dac-315">Todavía es necesario restaurar el proyecto para poder empaquetar un archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="c7dac-315">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="c7dac-316">(Un proyecto de estilo SDK incluye los destinos Pack de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="c7dac-316">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="c7dac-317">El marco de trabajo de destino del archivo de proyecto es irrelevante y no se usa cuando se empaqueta un archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="c7dac-317">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="c7dac-318">Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="c7dac-318">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="c7dac-319">`NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.</span><span class="sxs-lookup"><span data-stu-id="c7dac-319">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="c7dac-320">`NuspecProperties`: lista de pares clave=valor separados por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="c7dac-320">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="c7dac-321">Debido al funcionamiento del análisis de línea de comandos de MSBuild, se deben especificar varias propiedades como se indica a continuación: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-321">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="c7dac-322">`NuspecBasePath`: Ruta de acceso base `.nuspec` del archivo.</span><span class="sxs-lookup"><span data-stu-id="c7dac-322">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="c7dac-323">Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7dac-323">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="c7dac-324">Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7dac-324">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="c7dac-325">Tenga en cuenta que al empaquetar un archivo nuspec mediante dotnet. exe o MSBuild también se genera el proyecto de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c7dac-325">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="c7dac-326">Esto se puede evitar pasando ```--no-build``` la propiedad a dotnet. exe, que es el equivalente de la configuración ```<NoBuild>true</NoBuild> ``` en el archivo de proyecto, junto ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` con el valor en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="c7dac-326">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="c7dac-327">Un ejemplo de un archivo *. csproj* para empaquetar un archivo nuspec es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7dac-327">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="c7dac-328">Puntos de extensión avanzados para crear un paquete personalizado</span><span class="sxs-lookup"><span data-stu-id="c7dac-328">Advanced extension points to create customized package</span></span>

<span data-ttu-id="c7dac-329">El `pack` destino proporciona dos puntos de extensión que se ejecutan en la compilación interna específica de la plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="c7dac-329">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="c7dac-330">Los puntos de extensión admiten, incluidos los ensamblados y el contenido específico de la plataforma de destino en un paquete:</span><span class="sxs-lookup"><span data-stu-id="c7dac-330">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="c7dac-331">`TargetsForTfmSpecificBuildOutput`dirigir Se usa para los archivos `lib` dentro de la carpeta o en `BuildOutputTargetFolder`una carpeta especificada mediante.</span><span class="sxs-lookup"><span data-stu-id="c7dac-331">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="c7dac-332">`TargetsForTfmSpecificContentInPackage`dirigir Se usa para archivos fuera `BuildOutputTargetFolder`de.</span><span class="sxs-lookup"><span data-stu-id="c7dac-332">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="c7dac-333">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="c7dac-333">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="c7dac-334">Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificBuildOutput)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="c7dac-334">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="c7dac-335">En el caso de los archivos que necesiten `BuildOutputTargetFolder` entrar en (de forma predeterminada, lib), el destino debe escribir esos `BuildOutputInPackage` archivos en el ItemGroup y establecer los dos valores de metadatos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7dac-335">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="c7dac-336">`FinalOutputPath`: Ruta de acceso absoluta del archivo; Si no se proporciona, la identidad se utiliza para evaluar la ruta de acceso de origen.</span><span class="sxs-lookup"><span data-stu-id="c7dac-336">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="c7dac-337">`TargetPath`:  Opta Se establece cuando el archivo debe ir a una subcarpeta dentro de `lib\<TargetFramework>` , como los ensamblados satélite que se encuentran bajo sus respectivas carpetas de referencia cultural.</span><span class="sxs-lookup"><span data-stu-id="c7dac-337">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="c7dac-338">Tiene como valor predeterminado el nombre del archivo.</span><span class="sxs-lookup"><span data-stu-id="c7dac-338">Defaults to the name of the file.</span></span>

<span data-ttu-id="c7dac-339">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c7dac-339">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="c7dac-340">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="c7dac-340">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="c7dac-341">Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificContentInPackage)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="c7dac-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="c7dac-342">En el caso de los archivos que se van a incluir en el paquete, el destino debe `TfmSpecificPackageFile` escribir esos archivos en el ItemGroup y establecer los metadatos opcionales siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7dac-342">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="c7dac-343">`PackagePath`: Ruta de acceso en la que el archivo debe generarse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-343">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="c7dac-344">NuGet emite una advertencia si se agrega más de un archivo a la misma ruta de acceso del paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-344">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="c7dac-345">`BuildAction`: Acción de compilación que se va a asignar al archivo, que solo es necesario si la ruta `contentFiles` de acceso del paquete está en la carpeta.</span><span class="sxs-lookup"><span data-stu-id="c7dac-345">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="c7dac-346">El valor predeterminado es "none".</span><span class="sxs-lookup"><span data-stu-id="c7dac-346">Defaults to "None".</span></span>

<span data-ttu-id="c7dac-347">Un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c7dac-347">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="c7dac-348">Destino de restore</span><span class="sxs-lookup"><span data-stu-id="c7dac-348">restore target</span></span>

<span data-ttu-id="c7dac-349">`MSBuild -t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c7dac-349">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="c7dac-350">Leer todas las referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="c7dac-350">Read all project to project references</span></span>
1. <span data-ttu-id="c7dac-351">Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias</span><span class="sxs-lookup"><span data-stu-id="c7dac-351">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="c7dac-352">Pasar datos de MSBuild a NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="c7dac-352">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="c7dac-353">Ejecutar la restauración</span><span class="sxs-lookup"><span data-stu-id="c7dac-353">Run restore</span></span>
1. <span data-ttu-id="c7dac-354">Descargar los paquetes</span><span class="sxs-lookup"><span data-stu-id="c7dac-354">Download packages</span></span>
1. <span data-ttu-id="c7dac-355">Escribir el archivo de activos, destinos y propiedades</span><span class="sxs-lookup"><span data-stu-id="c7dac-355">Write assets file, targets, and props</span></span>

<span data-ttu-id="c7dac-356">El `restore` destino **solo** funciona con los proyectos que usan el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c7dac-356">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="c7dac-357">**No** funciona para los proyectos que usan el `packages.config` formato; use la [restauración de Nuget](../reference/cli-reference/cli-ref-restore.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="c7dac-357">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="c7dac-358">Restaurar las propiedades</span><span class="sxs-lookup"><span data-stu-id="c7dac-358">Restore properties</span></span>

<span data-ttu-id="c7dac-359">Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="c7dac-359">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="c7dac-360">También se pueden establecer valores desde la línea de comandos mediante el modificador `-p:` (vea los ejemplos siguientes).</span><span class="sxs-lookup"><span data-stu-id="c7dac-360">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="c7dac-361">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c7dac-361">Property</span></span> | <span data-ttu-id="c7dac-362">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="c7dac-362">Description</span></span> |
|--------|--------|
| <span data-ttu-id="c7dac-363">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="c7dac-363">RestoreSources</span></span> | <span data-ttu-id="c7dac-364">Lista delimitada por punto y coma de orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c7dac-364">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="c7dac-365">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="c7dac-365">RestorePackagesPath</span></span> | <span data-ttu-id="c7dac-366">Ruta de acceso de la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="c7dac-366">User packages folder path.</span></span> |
| <span data-ttu-id="c7dac-367">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="c7dac-367">RestoreDisableParallel</span></span> | <span data-ttu-id="c7dac-368">Limitar las descargas a una cada vez.</span><span class="sxs-lookup"><span data-stu-id="c7dac-368">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="c7dac-369">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="c7dac-369">RestoreConfigFile</span></span> | <span data-ttu-id="c7dac-370">Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="c7dac-370">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="c7dac-371">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="c7dac-371">RestoreNoCache</span></span> | <span data-ttu-id="c7dac-372">Si es true, evita el uso de paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="c7dac-372">If true, avoids using cached packages.</span></span> <span data-ttu-id="c7dac-373">Consulte [Administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c7dac-373">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c7dac-374">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="c7dac-374">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="c7dac-375">Si es true, ignora los orígenes de paquetes que producen errores o faltan.</span><span class="sxs-lookup"><span data-stu-id="c7dac-375">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="c7dac-376">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="c7dac-376">RestoreFallbackFolders</span></span> | <span data-ttu-id="c7dac-377">Carpetas de reserva que se usan de la misma manera que se usa la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="c7dac-377">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="c7dac-378">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="c7dac-378">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="c7dac-379">Fuentes adicionales para usar durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="c7dac-379">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="c7dac-380">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="c7dac-380">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="c7dac-381">Carpetas de reserva adicionales para usar durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="c7dac-381">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="c7dac-382">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="c7dac-382">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="c7dac-383">Excluye las carpetas de reserva especificadas en`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="c7dac-383">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="c7dac-384">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="c7dac-384">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="c7dac-385">Ruta de acceso a `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="c7dac-386">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="c7dac-386">RestoreGraphProjectInput</span></span> | <span data-ttu-id="c7dac-387">Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="c7dac-387">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="c7dac-388">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="c7dac-388">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="c7dac-389">Cuando los proyectos se recopilan a través de MSBuild, determina si se recopilan con la `SkipNonexistentTargets` optimización.</span><span class="sxs-lookup"><span data-stu-id="c7dac-389">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="c7dac-390">Cuando no se `true`establece, el valor predeterminado es.</span><span class="sxs-lookup"><span data-stu-id="c7dac-390">When not set, defaults to `true`.</span></span> <span data-ttu-id="c7dac-391">La consecuencia es un comportamiento de error rápido cuando no se pueden importar los destinos de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="c7dac-391">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="c7dac-392">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="c7dac-392">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="c7dac-393">Carpeta de salida, que `BaseIntermediateOutputPath` tiene como valor predeterminado y la `obj` carpeta.</span><span class="sxs-lookup"><span data-stu-id="c7dac-393">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="c7dac-394">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c7dac-394">Examples</span></span>

<span data-ttu-id="c7dac-395">Línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="c7dac-395">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="c7dac-396">Archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="c7dac-396">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="c7dac-397">Restaurar salidas</span><span class="sxs-lookup"><span data-stu-id="c7dac-397">Restore outputs</span></span>

<span data-ttu-id="c7dac-398">La restauración crea los archivos siguientes en la carpeta `obj` de compilación:</span><span class="sxs-lookup"><span data-stu-id="c7dac-398">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="c7dac-399">Archivo</span><span class="sxs-lookup"><span data-stu-id="c7dac-399">File</span></span> | <span data-ttu-id="c7dac-400">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="c7dac-400">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="c7dac-401">Contiene el gráfico de dependencias de todas las referencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="c7dac-401">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="c7dac-402">Referencias a propiedades de MSBuild incluidas en paquetes</span><span class="sxs-lookup"><span data-stu-id="c7dac-402">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="c7dac-403">Referencias a destinos de MSBuild incluidos en paquetes</span><span class="sxs-lookup"><span data-stu-id="c7dac-403">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="c7dac-404">Restaurar y compilar con un comando de MSBuild</span><span class="sxs-lookup"><span data-stu-id="c7dac-404">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="c7dac-405">Debido al hecho de que NuGet puede restaurar paquetes que desactivan los destinos y las propiedades de MSBuild, las evaluaciones de la restauración y de la compilación se ejecutan con propiedades globales diferentes.</span><span class="sxs-lookup"><span data-stu-id="c7dac-405">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="c7dac-406">Esto significa que el siguiente tendrá un comportamiento imprevisible y a menudo incorrecto.</span><span class="sxs-lookup"><span data-stu-id="c7dac-406">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="c7dac-407">En su lugar, el enfoque recomendado es:</span><span class="sxs-lookup"><span data-stu-id="c7dac-407">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="c7dac-408">La misma lógica se aplica a otros destinos similares `build`a.</span><span class="sxs-lookup"><span data-stu-id="c7dac-408">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="c7dac-409">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="c7dac-409">PackageTargetFallback</span></span>

<span data-ttu-id="c7dac-410">El elemento `PackageTargetFallback` permite especificar un conjunto de destinos compatibles que se usarán al restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="c7dac-410">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="c7dac-411">Está diseñado para permitir que los paquetes que usan un [TxM](../reference/target-frameworks.md) de dotnet funcionen con paquetes compatibles que no declaran un TxM de dotnet.</span><span class="sxs-lookup"><span data-stu-id="c7dac-411">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="c7dac-412">Es decir, si el proyecto usa el TxM de dotnet, todos los paquetes de los que depende también deben tener un TxM de dotnet, a menos que agregue `<PackageTargetFallback>` al proyecto para permitir que las plataformas que no sean de dotnet sean compatibles con dotnet.</span><span class="sxs-lookup"><span data-stu-id="c7dac-412">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="c7dac-413">Por ejemplo, si el proyecto usa el TxM `netstandard1.6` y un paquete dependiente solo contiene `lib/net45/a.dll` y `lib/portable-net45+win81/a.dll`, se producirá un error al compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="c7dac-413">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="c7dac-414">Si lo que quiere incluir es el último archivo DLL, puede agregar `PackageTargetFallback` como se indica a continuación para indicar que el archivo DLL `portable-net45+win81` es compatible:</span><span class="sxs-lookup"><span data-stu-id="c7dac-414">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="c7dac-415">Para declarar una reserva para todos los destinos del proyecto, excluya el atributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="c7dac-415">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="c7dac-416">También puede extender cualquier `PackageTargetFallback` existente mediante la inclusión de `$(PackageTargetFallback)` como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="c7dac-416">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="c7dac-417">Reemplazo de una biblioteca desde un gráfico de restauración</span><span class="sxs-lookup"><span data-stu-id="c7dac-417">Replacing one library from a restore graph</span></span>

<span data-ttu-id="c7dac-418">Si una restauración agrega el ensamblado equivocado, se puede excluir la opción predeterminada de ese paquete y reemplazarla por una de su propia elección.</span><span class="sxs-lookup"><span data-stu-id="c7dac-418">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="c7dac-419">En primer lugar, con una `PackageReference` de nivel superior, excluya todos los activos:</span><span class="sxs-lookup"><span data-stu-id="c7dac-419">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="c7dac-420">Después, agregue su propia referencia a la copia local correspondiente del archivo DLL:</span><span class="sxs-lookup"><span data-stu-id="c7dac-420">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
