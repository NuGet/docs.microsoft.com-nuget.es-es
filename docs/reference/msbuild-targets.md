---
title: pack y restore de NuGet como destinos de MSBuild
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235703"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="23c6f-103">pack y restore de NuGet como destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="23c6f-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="23c6f-104">*NuGet 4.0 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="23c6f-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="23c6f-105">Con el formato [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + puede almacenar todos los metadatos del manifiesto directamente dentro de un archivo de proyecto en lugar de usar un `.nuspec` archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="23c6f-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="23c6f-106">Con MSBuild 15.1 y versiones posteriores, NuGet es también un ciudadano de MSBuild de primera clase con los destinos `pack` y `restore` como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="23c6f-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="23c6f-107">Estos destinos permiten trabajar con NuGet como lo haría con cualquier otra tarea o destino de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="23c6f-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="23c6f-108">Para obtener instrucciones sobre cómo crear un paquete NuGet con MSBuild, consulte [crear un paquete Nuget con MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="23c6f-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="23c6f-109">(Para NuGet 3.x y versiones anteriores, los comandos [pack](../reference/cli-reference/cli-ref-pack.md) y [restore](../reference/cli-reference/cli-ref-restore.md) se usan a través de la CLI de NuGet en su lugar).</span><span class="sxs-lookup"><span data-stu-id="23c6f-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="23c6f-110">Orden de compilación de destinos</span><span class="sxs-lookup"><span data-stu-id="23c6f-110">Target build order</span></span>

<span data-ttu-id="23c6f-111">Dado que `pack` y `restore` son destinos de MSBuild, puede tener acceso a ellos para mejorar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="23c6f-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="23c6f-112">Por ejemplo, supongamos que quiere copiar el paquete en un recurso compartido de red después de empaquetarlo.</span><span class="sxs-lookup"><span data-stu-id="23c6f-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="23c6f-113">Puede hacer esto si agrega lo siguiente al archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="23c6f-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="23c6f-114">De forma similar, puede escribir una tarea de MSBuild, su propio destino y usar propiedades de NuGet en la tarea de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="23c6f-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="23c6f-115">`$(OutputPath)` es relativo y espera que se ejecute el comando desde la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="23c6f-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="23c6f-116">Destino de pack</span><span class="sxs-lookup"><span data-stu-id="23c6f-116">pack target</span></span>

<span data-ttu-id="23c6f-117">En el caso de los proyectos de .NET Standard con el formato PackageReference, el uso de `msbuild -t:pack` dibuja entradas del archivo de proyecto para usarlas en la creación de un paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="23c6f-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="23c6f-118">En la tabla siguiente se describen las propiedades de MSBuild que se pueden agregar a un archivo de proyecto en el primer nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="23c6f-119">Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="23c6f-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="23c6f-120">Para mayor comodidad, la tabla está organizada por la propiedad equivalente en un [ `.nuspec` archivo](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="23c6f-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="23c6f-121">Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="23c6f-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="23c6f-122">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="23c6f-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="23c6f-123">Propiedad de MSBuild</span><span class="sxs-lookup"><span data-stu-id="23c6f-123">MSBuild Property</span></span> | <span data-ttu-id="23c6f-124">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="23c6f-124">Default</span></span> | <span data-ttu-id="23c6f-125">Notas</span><span class="sxs-lookup"><span data-stu-id="23c6f-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="23c6f-126">Identificador</span><span class="sxs-lookup"><span data-stu-id="23c6f-126">Id</span></span> | <span data-ttu-id="23c6f-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="23c6f-127">PackageId</span></span> | <span data-ttu-id="23c6f-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="23c6f-128">AssemblyName</span></span> | <span data-ttu-id="23c6f-129">$(NombreDeEnsamblado) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="23c6f-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="23c6f-130">Versión</span><span class="sxs-lookup"><span data-stu-id="23c6f-130">Version</span></span> | <span data-ttu-id="23c6f-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="23c6f-131">PackageVersion</span></span> | <span data-ttu-id="23c6f-132">Versión</span><span class="sxs-lookup"><span data-stu-id="23c6f-132">Version</span></span> | <span data-ttu-id="23c6f-133">Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="23c6f-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="23c6f-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="23c6f-134">VersionPrefix</span></span> | <span data-ttu-id="23c6f-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="23c6f-135">PackageVersionPrefix</span></span> | <span data-ttu-id="23c6f-136">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-136">empty</span></span> | <span data-ttu-id="23c6f-137">Al establecer PackageVersion se sobrescribe PackageVersionPrefix.</span><span class="sxs-lookup"><span data-stu-id="23c6f-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="23c6f-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="23c6f-138">VersionSuffix</span></span> | <span data-ttu-id="23c6f-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="23c6f-139">PackageVersionSuffix</span></span> | <span data-ttu-id="23c6f-140">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-140">empty</span></span> | <span data-ttu-id="23c6f-141">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="23c6f-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="23c6f-142">Al establecer PackageVersion se sobrescribe PackageVersionSuffix.</span><span class="sxs-lookup"><span data-stu-id="23c6f-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="23c6f-143">Authors</span><span class="sxs-lookup"><span data-stu-id="23c6f-143">Authors</span></span> | <span data-ttu-id="23c6f-144">Authors</span><span class="sxs-lookup"><span data-stu-id="23c6f-144">Authors</span></span> | <span data-ttu-id="23c6f-145">Nombre del usuario actual</span><span class="sxs-lookup"><span data-stu-id="23c6f-145">Username of the current user</span></span> | |
| <span data-ttu-id="23c6f-146">Propietarios</span><span class="sxs-lookup"><span data-stu-id="23c6f-146">Owners</span></span> | <span data-ttu-id="23c6f-147">N/A</span><span class="sxs-lookup"><span data-stu-id="23c6f-147">N/A</span></span> | <span data-ttu-id="23c6f-148">No está presente en el archivo NuSpec</span><span class="sxs-lookup"><span data-stu-id="23c6f-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="23c6f-149">Título</span><span class="sxs-lookup"><span data-stu-id="23c6f-149">Title</span></span> | <span data-ttu-id="23c6f-150">Título</span><span class="sxs-lookup"><span data-stu-id="23c6f-150">Title</span></span> | <span data-ttu-id="23c6f-151">El identificador de paquete</span><span class="sxs-lookup"><span data-stu-id="23c6f-151">The PackageId</span></span>| |
| <span data-ttu-id="23c6f-152">Descripción</span><span class="sxs-lookup"><span data-stu-id="23c6f-152">Description</span></span> | <span data-ttu-id="23c6f-153">Descripción</span><span class="sxs-lookup"><span data-stu-id="23c6f-153">Description</span></span> | <span data-ttu-id="23c6f-154">"Descripción del paquete"</span><span class="sxs-lookup"><span data-stu-id="23c6f-154">"Package Description"</span></span> | |
| <span data-ttu-id="23c6f-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="23c6f-155">Copyright</span></span> | <span data-ttu-id="23c6f-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="23c6f-156">Copyright</span></span> | <span data-ttu-id="23c6f-157">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-157">empty</span></span> | |
| <span data-ttu-id="23c6f-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="23c6f-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="23c6f-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="23c6f-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="23c6f-160">false</span><span class="sxs-lookup"><span data-stu-id="23c6f-160">false</span></span> | |
| <span data-ttu-id="23c6f-161">license</span><span class="sxs-lookup"><span data-stu-id="23c6f-161">license</span></span> | <span data-ttu-id="23c6f-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="23c6f-162">PackageLicenseExpression</span></span> | <span data-ttu-id="23c6f-163">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-163">empty</span></span> | <span data-ttu-id="23c6f-164">Se corresponde con `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="23c6f-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="23c6f-165">license</span><span class="sxs-lookup"><span data-stu-id="23c6f-165">license</span></span> | <span data-ttu-id="23c6f-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="23c6f-166">PackageLicenseFile</span></span> | <span data-ttu-id="23c6f-167">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-167">empty</span></span> | <span data-ttu-id="23c6f-168">Se corresponde con `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="23c6f-169">Debe empaquetar explícitamente el archivo de licencia al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="23c6f-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="23c6f-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-170">LicenseUrl</span></span> | <span data-ttu-id="23c6f-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-171">PackageLicenseUrl</span></span> | <span data-ttu-id="23c6f-172">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-172">empty</span></span> | <span data-ttu-id="23c6f-173">`PackageLicenseUrl` está en desuso, use la propiedad PackageLicenseExpression o PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="23c6f-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="23c6f-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-174">ProjectUrl</span></span> | <span data-ttu-id="23c6f-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-175">PackageProjectUrl</span></span> | <span data-ttu-id="23c6f-176">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-176">empty</span></span> | |
| <span data-ttu-id="23c6f-177">Iconos</span><span class="sxs-lookup"><span data-stu-id="23c6f-177">Icon</span></span> | <span data-ttu-id="23c6f-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="23c6f-178">PackageIcon</span></span> | <span data-ttu-id="23c6f-179">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-179">empty</span></span> | <span data-ttu-id="23c6f-180">Debe empaquetar explícitamente el archivo de imagen de icono al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="23c6f-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="23c6f-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-181">IconUrl</span></span> | <span data-ttu-id="23c6f-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-182">PackageIconUrl</span></span> | <span data-ttu-id="23c6f-183">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-183">empty</span></span> | <span data-ttu-id="23c6f-184">Para la mejor experiencia de nivel inferior, `PackageIconUrl` debe especificarse además de `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="23c6f-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="23c6f-185">A largo plazo, estará en `PackageIconUrl` desuso.</span><span class="sxs-lookup"><span data-stu-id="23c6f-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="23c6f-186">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="23c6f-186">Tags</span></span> | <span data-ttu-id="23c6f-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="23c6f-187">PackageTags</span></span> | <span data-ttu-id="23c6f-188">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-188">empty</span></span> | <span data-ttu-id="23c6f-189">Las etiquetas están delimitadas mediante punto y coma.</span><span class="sxs-lookup"><span data-stu-id="23c6f-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="23c6f-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="23c6f-190">ReleaseNotes</span></span> | <span data-ttu-id="23c6f-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="23c6f-191">PackageReleaseNotes</span></span> | <span data-ttu-id="23c6f-192">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-192">empty</span></span> | |
| <span data-ttu-id="23c6f-193">Repositorio/dirección URL</span><span class="sxs-lookup"><span data-stu-id="23c6f-193">Repository/Url</span></span> | <span data-ttu-id="23c6f-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-194">RepositoryUrl</span></span> | <span data-ttu-id="23c6f-195">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-195">empty</span></span> | <span data-ttu-id="23c6f-196">Dirección URL del repositorio usada para clonar o recuperar el código fuente.</span><span class="sxs-lookup"><span data-stu-id="23c6f-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="23c6f-197">Ejemplo *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="23c6f-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="23c6f-198">Repositorio/tipo</span><span class="sxs-lookup"><span data-stu-id="23c6f-198">Repository/Type</span></span> | <span data-ttu-id="23c6f-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="23c6f-199">RepositoryType</span></span> | <span data-ttu-id="23c6f-200">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-200">empty</span></span> | <span data-ttu-id="23c6f-201">Tipo de repositorio.</span><span class="sxs-lookup"><span data-stu-id="23c6f-201">Repository type.</span></span> <span data-ttu-id="23c6f-202">Ejemplos: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="23c6f-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="23c6f-203">Repositorio/rama</span><span class="sxs-lookup"><span data-stu-id="23c6f-203">Repository/Branch</span></span> | <span data-ttu-id="23c6f-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="23c6f-204">RepositoryBranch</span></span> | <span data-ttu-id="23c6f-205">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-205">empty</span></span> | <span data-ttu-id="23c6f-206">Información opcional de la rama del repositorio.</span><span class="sxs-lookup"><span data-stu-id="23c6f-206">Optional repository branch information.</span></span> <span data-ttu-id="23c6f-207">También se debe especificar *RepositoryUrl* para que se incluya esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="23c6f-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="23c6f-208">Ejemplo: *maestra* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="23c6f-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="23c6f-209">Repositorio/confirmar</span><span class="sxs-lookup"><span data-stu-id="23c6f-209">Repository/Commit</span></span> | <span data-ttu-id="23c6f-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="23c6f-210">RepositoryCommit</span></span> | <span data-ttu-id="23c6f-211">empty</span><span class="sxs-lookup"><span data-stu-id="23c6f-211">empty</span></span> | <span data-ttu-id="23c6f-212">Confirmación o conjunto de cambios opcionales de repositorio para indicar en qué origen se ha compilado el paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="23c6f-213">También se debe especificar *RepositoryUrl* para que se incluya esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="23c6f-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="23c6f-214">Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="23c6f-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="23c6f-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="23c6f-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="23c6f-216">Resumen</span><span class="sxs-lookup"><span data-stu-id="23c6f-216">Summary</span></span> | <span data-ttu-id="23c6f-217">No compatible</span><span class="sxs-lookup"><span data-stu-id="23c6f-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="23c6f-218">Entradas de destino de pack</span><span class="sxs-lookup"><span data-stu-id="23c6f-218">pack target inputs</span></span>

- <span data-ttu-id="23c6f-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="23c6f-219">IsPackable</span></span>
- <span data-ttu-id="23c6f-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="23c6f-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="23c6f-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="23c6f-221">PackageVersion</span></span>
- <span data-ttu-id="23c6f-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="23c6f-222">PackageId</span></span>
- <span data-ttu-id="23c6f-223">Authors</span><span class="sxs-lookup"><span data-stu-id="23c6f-223">Authors</span></span>
- <span data-ttu-id="23c6f-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="23c6f-224">Description</span></span>
- <span data-ttu-id="23c6f-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="23c6f-225">Copyright</span></span>
- <span data-ttu-id="23c6f-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="23c6f-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="23c6f-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="23c6f-227">DevelopmentDependency</span></span>
- <span data-ttu-id="23c6f-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="23c6f-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="23c6f-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="23c6f-229">PackageLicenseFile</span></span>
- <span data-ttu-id="23c6f-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="23c6f-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-231">PackageProjectUrl</span></span>
- <span data-ttu-id="23c6f-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-232">PackageIconUrl</span></span>
- <span data-ttu-id="23c6f-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="23c6f-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="23c6f-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="23c6f-234">PackageTags</span></span>
- <span data-ttu-id="23c6f-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="23c6f-235">PackageOutputPath</span></span>
- <span data-ttu-id="23c6f-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="23c6f-236">IncludeSymbols</span></span>
- <span data-ttu-id="23c6f-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="23c6f-237">IncludeSource</span></span>
- <span data-ttu-id="23c6f-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="23c6f-238">PackageTypes</span></span>
- <span data-ttu-id="23c6f-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="23c6f-239">IsTool</span></span>
- <span data-ttu-id="23c6f-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-240">RepositoryUrl</span></span>
- <span data-ttu-id="23c6f-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="23c6f-241">RepositoryType</span></span>
- <span data-ttu-id="23c6f-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="23c6f-242">RepositoryBranch</span></span>
- <span data-ttu-id="23c6f-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="23c6f-243">RepositoryCommit</span></span>
- <span data-ttu-id="23c6f-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="23c6f-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="23c6f-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="23c6f-245">MinClientVersion</span></span>
- <span data-ttu-id="23c6f-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="23c6f-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="23c6f-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="23c6f-247">IncludeContentInPack</span></span>
- <span data-ttu-id="23c6f-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="23c6f-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="23c6f-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="23c6f-249">ContentTargetFolders</span></span>
- <span data-ttu-id="23c6f-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="23c6f-250">NuspecFile</span></span>
- <span data-ttu-id="23c6f-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="23c6f-251">NuspecBasePath</span></span>
- <span data-ttu-id="23c6f-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="23c6f-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="23c6f-253">Escenarios de pack</span><span class="sxs-lookup"><span data-stu-id="23c6f-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="23c6f-254">Suprimir dependencias</span><span class="sxs-lookup"><span data-stu-id="23c6f-254">Suppress dependencies</span></span>

<span data-ttu-id="23c6f-255">Para suprimir las dependencias de paquete del paquete NuGet generado, establezca `SuppressDependenciesWhenPacking` en, `true` lo que permitirá omitir todas las dependencias del archivo nupkg generado.</span><span class="sxs-lookup"><span data-stu-id="23c6f-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="23c6f-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="23c6f-256">PackageIconUrl</span></span>

<span data-ttu-id="23c6f-257">`PackageIconUrl` quedará en desuso en favor de la nueva [`PackageIcon`](#packageicon) propiedad.</span><span class="sxs-lookup"><span data-stu-id="23c6f-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="23c6f-258">A partir de NuGet 5,3 & Visual Studio 2019 versión 16,3, `pack` se generará una advertencia [NU5048](./errors-and-warnings/nu5048.md) si los metadatos del paquete solo especifican `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="23c6f-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="23c6f-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="23c6f-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="23c6f-260">Debe especificar `PackageIcon` y `PackageIconUrl` para mantener la compatibilidad con versiones anteriores de clientes y orígenes que aún no admiten `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="23c6f-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="23c6f-261">Visual Studio será compatible con los `PackageIcon` paquetes procedentes de un origen basado en carpetas en una versión futura.</span><span class="sxs-lookup"><span data-stu-id="23c6f-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="23c6f-262">Empaquetar un archivo de imagen de icono</span><span class="sxs-lookup"><span data-stu-id="23c6f-262">Packing an icon image file</span></span>

<span data-ttu-id="23c6f-263">Al empaquetar un archivo de imagen de icono, debe usar `PackageIcon` la propiedad para especificar la ruta de acceso del paquete, relativa a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="23c6f-264">Además, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="23c6f-265">El tamaño del archivo de imagen está limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="23c6f-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="23c6f-266">Entre los formatos de archivo admitidos se incluyen JPEG y PNG.</span><span class="sxs-lookup"><span data-stu-id="23c6f-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="23c6f-267">Se recomienda una resolución de imagen de 128x128.</span><span class="sxs-lookup"><span data-stu-id="23c6f-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="23c6f-268">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="23c6f-268">For example:</span></span>

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

<span data-ttu-id="23c6f-269">[Ejemplo de icono de paquete](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="23c6f-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="23c6f-270">En el caso del equivalente de nuspec, eche un vistazo a la [referencia de nuspec para el icono](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="23c6f-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="23c6f-271">Ensamblados de salida</span><span class="sxs-lookup"><span data-stu-id="23c6f-271">Output assemblies</span></span>

<span data-ttu-id="23c6f-272">`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="23c6f-273">Los archivos de salida que se copian dependen de lo que proporciona MSBuild desde el destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="23c6f-274">Hay dos propiedades de MSBuild que se pueden usar en el archivo de proyecto o la línea de comandos para controlar dónde van los ensamblados de salida:</span><span class="sxs-lookup"><span data-stu-id="23c6f-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="23c6f-275">`IncludeBuildOutput`: un valor booleano que determina si los ensamblados de salida de compilación deben incluirse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="23c6f-276">`BuildOutputTargetFolder`: especifica la carpeta en la que se deben colocar los ensamblados de salida.</span><span class="sxs-lookup"><span data-stu-id="23c6f-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="23c6f-277">Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.</span><span class="sxs-lookup"><span data-stu-id="23c6f-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="23c6f-278">Referencias de paquete</span><span class="sxs-lookup"><span data-stu-id="23c6f-278">Package references</span></span>

<span data-ttu-id="23c6f-279">Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="23c6f-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="23c6f-280">Referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="23c6f-280">Project to project references</span></span>

<span data-ttu-id="23c6f-281">Las referencias entre proyectos se consideran de forma predeterminada como referencias de paquetes NuGet, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="23c6f-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="23c6f-282">También puede agregar los metadatos siguientes a la referencia de proyecto:</span><span class="sxs-lookup"><span data-stu-id="23c6f-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="23c6f-283">Inclusión de contenido en un paquete</span><span class="sxs-lookup"><span data-stu-id="23c6f-283">Including content in a package</span></span>

<span data-ttu-id="23c6f-284">Para incluir contenido, agregue metadatos adicionales al elemento `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="23c6f-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="23c6f-285">De forma predeterminada todos los elementos de tipo "Content" se incluyen en el paquete a menos que los reemplace con entradas como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="23c6f-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="23c6f-286">De forma predeterminada, todo el contenido se agrega a la raíz de la carpeta `content` y `contentFiles\any\<target_framework>` dentro de un paquete y se conserva la estructura de carpetas relativa, a menos que se especifique una ruta de acceso de paquete:</span><span class="sxs-lookup"><span data-stu-id="23c6f-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="23c6f-287">Si quiere copiar todo el contenido a una carpeta raíz determinada (en lugar de `content` y `contentFiles`), puede usar la propiedad `ContentTargetFolders` de MSBuild, cuyo valor predeterminado es "content;contentFiles", pero que se puede establecer en cualquier otro nombre de carpeta.</span><span class="sxs-lookup"><span data-stu-id="23c6f-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="23c6f-288">Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="23c6f-289">`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="23c6f-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="23c6f-290">Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="23c6f-291">Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:</span><span class="sxs-lookup"><span data-stu-id="23c6f-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="23c6f-292">También hay una propiedad `$(IncludeContentInPack)` de MSBuild, cuyo valor predeterminado es `true`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="23c6f-293">Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="23c6f-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="23c6f-294">Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen ```<PackageCopyToOutput>``` y ```<PackageFlatten>```, que establece los valores ```CopyToOutput``` y ```Flatten``` en la entrada ```contentFiles``` del archivo nuspec de salida.</span><span class="sxs-lookup"><span data-stu-id="23c6f-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="23c6f-295">Además de los elementos Content, los metadatos `<Pack>` y `<PackagePath>` también se pueden establecer en archivos con una acción de compilación Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="23c6f-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="23c6f-296">Para que el comando pack anexe el nombre de archivo a la ruta de acceso del paquete cuando se usan patrones globales, la ruta de acceso del paquete debe terminar con el carácter separador de carpeta; en caso contrario, la ruta de acceso del paquete se trata como la ruta de acceso completa, incluido el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="23c6f-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="23c6f-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="23c6f-297">IncludeSymbols</span></span>

<span data-ttu-id="23c6f-298">Cuando se usa `MSBuild -t:pack -p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="23c6f-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="23c6f-299">Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="23c6f-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="23c6f-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="23c6f-300">IncludeSource</span></span>

<span data-ttu-id="23c6f-301">Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="23c6f-302">Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="23c6f-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="23c6f-303">Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="23c6f-304">Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="23c6f-305">Empaquetado de una expresión de licencia o un archivo de licencia</span><span class="sxs-lookup"><span data-stu-id="23c6f-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="23c6f-306">Cuando se usa una expresión de licencia, se debe usar la propiedad PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="23c6f-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="23c6f-307">[Ejemplo de expresión de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="23c6f-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="23c6f-308">[Obtenga más información sobre las expresiones de licencia y las licencias que acepta NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="23c6f-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="23c6f-309">Al empaquetar un archivo de licencia, debe usar la propiedad PackageLicenseFile para especificar la ruta de acceso del paquete, relativa a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="23c6f-310">Además, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="23c6f-311">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="23c6f-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="23c6f-312">[Ejemplo de archivo de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="23c6f-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="23c6f-313">Empaquetado de un archivo sin extensión</span><span class="sxs-lookup"><span data-stu-id="23c6f-313">Packing a file without an extension</span></span>

<span data-ttu-id="23c6f-314">En algunos escenarios, como cuando se empaqueta un archivo de licencia, puede que desee incluir un archivo sin una extensión.</span><span class="sxs-lookup"><span data-stu-id="23c6f-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="23c6f-315">Por motivos históricos, NuGet & MSBuild tratan las rutas de acceso sin una extensión como directorios.</span><span class="sxs-lookup"><span data-stu-id="23c6f-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="23c6f-316">[Archivo sin un ejemplo de extensión](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="23c6f-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="23c6f-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="23c6f-317">IsTool</span></span>

<span data-ttu-id="23c6f-318">Cuando se usa `MSBuild -t:pack -p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="23c6f-319">Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="23c6f-320">Empaquetado mediante un archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="23c6f-320">Packing using a .nuspec</span></span>

<span data-ttu-id="23c6f-321">Aunque se recomienda [incluir todas las propiedades](../reference/msbuild-targets.md#pack-target) que suelen estar en el archivo `.nuspec` en el archivo del proyecto, puede optar por usar un `.nuspec` archivo para empaquetar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="23c6f-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="23c6f-322">Para un proyecto que no sea de estilo SDK que use `PackageReference` , debe importar `NuGet.Build.Tasks.Pack.targets` para que se pueda ejecutar la tarea del paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="23c6f-323">Todavía es necesario restaurar el proyecto para poder empaquetar un archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="23c6f-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="23c6f-324">(Un proyecto de estilo SDK incluye los destinos Pack de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="23c6f-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="23c6f-325">El marco de trabajo de destino del archivo de proyecto es irrelevante y no se usa cuando se empaqueta un archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="23c6f-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="23c6f-326">Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="23c6f-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="23c6f-327">`NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.</span><span class="sxs-lookup"><span data-stu-id="23c6f-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="23c6f-328">`NuspecProperties`: lista de pares clave=valor separados por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="23c6f-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="23c6f-329">Debido al funcionamiento del análisis de línea de comandos de MSBuild, se deben especificar varias propiedades como se indica a continuación: `-p:NuspecProperties="key1=value1;key2=value2"`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="23c6f-330">`NuspecBasePath`: ruta de acceso base para el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="23c6f-331">Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="23c6f-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="23c6f-332">Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="23c6f-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="23c6f-333">Tenga en cuenta que al empaquetar un nuspec mediante dotnet.exe o MSBuild también se genera el proyecto de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="23c6f-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="23c6f-334">Esto se puede evitar pasando ```--no-build``` Property a dotnet.exe, que es el equivalente de la configuración ```<NoBuild>true</NoBuild> ``` en el archivo de proyecto, junto con ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` el valor en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="23c6f-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="23c6f-335">Un ejemplo de un archivo *. csproj* para empaquetar un archivo nuspec es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="23c6f-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="23c6f-336">Puntos de extensión avanzados para crear un paquete personalizado</span><span class="sxs-lookup"><span data-stu-id="23c6f-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="23c6f-337">El `pack` destino proporciona dos puntos de extensión que se ejecutan en la compilación interna específica de la plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="23c6f-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="23c6f-338">Los puntos de extensión admiten, incluidos los ensamblados y el contenido específico de la plataforma de destino en un paquete:</span><span class="sxs-lookup"><span data-stu-id="23c6f-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="23c6f-339">`TargetsForTfmSpecificBuildOutput` destino: se usa para los archivos dentro de la `lib` carpeta o en una carpeta especificada mediante `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="23c6f-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="23c6f-340">`TargetsForTfmSpecificContentInPackage` destino: se usa para archivos fuera de `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="23c6f-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="23c6f-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="23c6f-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="23c6f-342">Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificBuildOutput)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="23c6f-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="23c6f-343">En el caso de los archivos que necesiten entrar en `BuildOutputTargetFolder` (de forma predeterminada, lib), el destino debe escribir esos archivos en el ItemGroup `BuildOutputInPackage` y establecer los dos valores de metadatos siguientes:</span><span class="sxs-lookup"><span data-stu-id="23c6f-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="23c6f-344">`FinalOutputPath`: Ruta de acceso absoluta del archivo; Si no se proporciona, la identidad se utiliza para evaluar la ruta de acceso de origen.</span><span class="sxs-lookup"><span data-stu-id="23c6f-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="23c6f-345">`TargetPath`: (Opcional) se establece cuando el archivo debe ir a una subcarpeta dentro de `lib\<TargetFramework>` , como los ensamblados satélite que se encuentran bajo sus respectivas carpetas de referencia cultural.</span><span class="sxs-lookup"><span data-stu-id="23c6f-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="23c6f-346">Tiene como valor predeterminado el nombre del archivo.</span><span class="sxs-lookup"><span data-stu-id="23c6f-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="23c6f-347">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="23c6f-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="23c6f-348">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="23c6f-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="23c6f-349">Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificContentInPackage)` propiedad.</span><span class="sxs-lookup"><span data-stu-id="23c6f-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="23c6f-350">En el caso de los archivos que se van a incluir en el paquete, el destino debe escribir esos archivos en el ItemGroup `TfmSpecificPackageFile` y establecer los metadatos opcionales siguientes:</span><span class="sxs-lookup"><span data-stu-id="23c6f-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="23c6f-351">`PackagePath`: Ruta de acceso en la que el archivo debe generarse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="23c6f-352">NuGet emite una advertencia si se agrega más de un archivo a la misma ruta de acceso del paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="23c6f-353">`BuildAction`: Acción de compilación que se va a asignar al archivo, que solo es necesario si la ruta de acceso del paquete está en la `contentFiles` carpeta.</span><span class="sxs-lookup"><span data-stu-id="23c6f-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="23c6f-354">El valor predeterminado es "none".</span><span class="sxs-lookup"><span data-stu-id="23c6f-354">Defaults to "None".</span></span>

<span data-ttu-id="23c6f-355">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="23c6f-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="23c6f-356">Destino de restore</span><span class="sxs-lookup"><span data-stu-id="23c6f-356">restore target</span></span>

<span data-ttu-id="23c6f-357">`MSBuild -t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="23c6f-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="23c6f-358">Leer todas las referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="23c6f-358">Read all project to project references</span></span>
1. <span data-ttu-id="23c6f-359">Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias</span><span class="sxs-lookup"><span data-stu-id="23c6f-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="23c6f-360">Pasar datos de MSBuild a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="23c6f-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="23c6f-361">Ejecutar la restauración</span><span class="sxs-lookup"><span data-stu-id="23c6f-361">Run restore</span></span>
1. <span data-ttu-id="23c6f-362">Descarga de paquetes</span><span class="sxs-lookup"><span data-stu-id="23c6f-362">Download packages</span></span>
1. <span data-ttu-id="23c6f-363">Escribir el archivo de activos, destinos y propiedades</span><span class="sxs-lookup"><span data-stu-id="23c6f-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="23c6f-364">El `restore` destino funciona con los proyectos que usan el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="23c6f-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="23c6f-365">`MSBuild 16.5+` también tiene [compatibilidad con](#restoring-packagereference-and-packagesconfig-with-msbuild) el `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="23c6f-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="23c6f-366">El `restore` destino [no debe ejecutarse](#restoring-and-building-with-one-msbuild-command) en combinación con el `build` destino.</span><span class="sxs-lookup"><span data-stu-id="23c6f-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="23c6f-367">Restaurar las propiedades</span><span class="sxs-lookup"><span data-stu-id="23c6f-367">Restore properties</span></span>

<span data-ttu-id="23c6f-368">Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="23c6f-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="23c6f-369">También se pueden establecer valores desde la línea de comandos mediante el modificador `-p:` (vea los ejemplos siguientes).</span><span class="sxs-lookup"><span data-stu-id="23c6f-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="23c6f-370">Propiedad</span><span class="sxs-lookup"><span data-stu-id="23c6f-370">Property</span></span> | <span data-ttu-id="23c6f-371">Descripción</span><span class="sxs-lookup"><span data-stu-id="23c6f-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="23c6f-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="23c6f-372">RestoreSources</span></span> | <span data-ttu-id="23c6f-373">Lista delimitada por punto y coma de orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="23c6f-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="23c6f-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="23c6f-374">RestorePackagesPath</span></span> | <span data-ttu-id="23c6f-375">Ruta de acceso de la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="23c6f-375">User packages folder path.</span></span> |
| <span data-ttu-id="23c6f-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="23c6f-376">RestoreDisableParallel</span></span> | <span data-ttu-id="23c6f-377">Limitar las descargas a una cada vez.</span><span class="sxs-lookup"><span data-stu-id="23c6f-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="23c6f-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="23c6f-378">RestoreConfigFile</span></span> | <span data-ttu-id="23c6f-379">Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="23c6f-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="23c6f-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="23c6f-380">RestoreNoCache</span></span> | <span data-ttu-id="23c6f-381">Si es true, evita el uso de paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="23c6f-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="23c6f-382">Consulte [Administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="23c6f-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="23c6f-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="23c6f-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="23c6f-384">Si es true, ignora los orígenes de paquetes que producen errores o faltan.</span><span class="sxs-lookup"><span data-stu-id="23c6f-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="23c6f-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="23c6f-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="23c6f-386">Carpetas de reserva que se usan de la misma manera que se usa la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="23c6f-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="23c6f-387">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="23c6f-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="23c6f-388">Fuentes adicionales para usar durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="23c6f-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="23c6f-389">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="23c6f-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="23c6f-390">Carpetas de reserva adicionales para usar durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="23c6f-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="23c6f-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="23c6f-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="23c6f-392">Excluye las carpetas de reserva especificadas en `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="23c6f-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="23c6f-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="23c6f-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="23c6f-394">Ruta de acceso a `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="23c6f-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="23c6f-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="23c6f-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="23c6f-396">Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="23c6f-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="23c6f-397">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="23c6f-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="23c6f-398">Cuando los proyectos se recopilan a través de MSBuild, determina si se recopilan con la `SkipNonexistentTargets` optimización.</span><span class="sxs-lookup"><span data-stu-id="23c6f-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="23c6f-399">Cuando no se establece, el valor predeterminado es `true` .</span><span class="sxs-lookup"><span data-stu-id="23c6f-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="23c6f-400">La consecuencia es un comportamiento de error rápido cuando no se pueden importar los destinos de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="23c6f-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="23c6f-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="23c6f-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="23c6f-402">Carpeta de salida, que tiene como valor predeterminado `BaseIntermediateOutputPath` y la `obj` carpeta.</span><span class="sxs-lookup"><span data-stu-id="23c6f-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="23c6f-403">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="23c6f-403">RestoreForce</span></span> | <span data-ttu-id="23c6f-404">En los proyectos basados en PackageReference, fuerza la resolución de todas las dependencias, incluso si la última restauración se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="23c6f-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="23c6f-405">Especificar esta marca es similar a eliminar el `project.assets.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="23c6f-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="23c6f-406">Esto no omite la memoria caché http.</span><span class="sxs-lookup"><span data-stu-id="23c6f-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="23c6f-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="23c6f-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="23c6f-408">Opta por el uso de un archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="23c6f-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="23c6f-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="23c6f-409">RestoreLockedMode</span></span> | <span data-ttu-id="23c6f-410">Ejecutar restauración en modo bloqueado.</span><span class="sxs-lookup"><span data-stu-id="23c6f-410">Run restore in locked mode.</span></span> <span data-ttu-id="23c6f-411">Esto significa que la restauración no volverá a evaluar las dependencias.</span><span class="sxs-lookup"><span data-stu-id="23c6f-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="23c6f-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="23c6f-412">NuGetLockFilePath</span></span> | <span data-ttu-id="23c6f-413">Una ubicación personalizada para el archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="23c6f-413">A custom location for the lock file.</span></span> <span data-ttu-id="23c6f-414">La ubicación predeterminada es junto al proyecto y se denomina `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="23c6f-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="23c6f-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="23c6f-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="23c6f-416">Fuerza la restauración para volver a calcular las dependencias y actualizar el archivo de bloqueo sin ninguna advertencia.</span><span class="sxs-lookup"><span data-stu-id="23c6f-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="23c6f-417">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="23c6f-417">RestorePackagesConfig</span></span> | <span data-ttu-id="23c6f-418">Un modificador opcional, que restaura los proyectos con packages.config. Compatibilidad con `MSBuild -t:restore` solo.</span><span class="sxs-lookup"><span data-stu-id="23c6f-418">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="23c6f-419">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="23c6f-419">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="23c6f-420">Un modificador opcional para usar la evaluación de MSBuild de gráficos estáticos en lugar de la evaluación estándar.</span><span class="sxs-lookup"><span data-stu-id="23c6f-420">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="23c6f-421">La evaluación de gráficos estáticos es una característica experimental que es significativamente más rápida para soluciones y repositorioss de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="23c6f-421">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="23c6f-422">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="23c6f-422">Examples</span></span>

<span data-ttu-id="23c6f-423">Línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="23c6f-423">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="23c6f-424">Archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="23c6f-424">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="23c6f-425">Restaurar salidas</span><span class="sxs-lookup"><span data-stu-id="23c6f-425">Restore outputs</span></span>

<span data-ttu-id="23c6f-426">La restauración crea los archivos siguientes en la carpeta `obj` de compilación:</span><span class="sxs-lookup"><span data-stu-id="23c6f-426">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="23c6f-427">Archivo</span><span class="sxs-lookup"><span data-stu-id="23c6f-427">File</span></span> | <span data-ttu-id="23c6f-428">Descripción</span><span class="sxs-lookup"><span data-stu-id="23c6f-428">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="23c6f-429">Contiene el gráfico de dependencias de todas las referencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="23c6f-429">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="23c6f-430">Referencias a propiedades de MSBuild incluidas en paquetes</span><span class="sxs-lookup"><span data-stu-id="23c6f-430">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="23c6f-431">Referencias a destinos de MSBuild incluidos en paquetes</span><span class="sxs-lookup"><span data-stu-id="23c6f-431">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="23c6f-432">Restaurar y compilar con un comando de MSBuild</span><span class="sxs-lookup"><span data-stu-id="23c6f-432">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="23c6f-433">Debido al hecho de que NuGet puede restaurar paquetes que desactivan los destinos y las propiedades de MSBuild, las evaluaciones de la restauración y de la compilación se ejecutan con propiedades globales diferentes.</span><span class="sxs-lookup"><span data-stu-id="23c6f-433">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="23c6f-434">Esto significa que el siguiente tendrá un comportamiento imprevisible y a menudo incorrecto.</span><span class="sxs-lookup"><span data-stu-id="23c6f-434">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="23c6f-435">En su lugar, el enfoque recomendado es:</span><span class="sxs-lookup"><span data-stu-id="23c6f-435">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="23c6f-436">La misma lógica se aplica a otros destinos similares a `build` .</span><span class="sxs-lookup"><span data-stu-id="23c6f-436">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="23c6f-437">Restaurar PackageReference y packages.config con MSBuild</span><span class="sxs-lookup"><span data-stu-id="23c6f-437">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="23c6f-438">Con MSBuild 16,5 +, packages.config también se admiten para `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="23c6f-438">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="23c6f-439">`packages.config` restore solo está disponible con `MSBuild 16.5+` , y no con `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="23c6f-439">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="23c6f-440">Restaurar con la evaluación de gráficos estáticos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="23c6f-440">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="23c6f-441">Con MSBuild 16.6 +, NuGet ha agregado una característica experimental para usar la evaluación de gráficos estáticos desde la línea de comandos que mejora significativamente el tiempo de restauración de repositorios grandes.</span><span class="sxs-lookup"><span data-stu-id="23c6f-441">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="23c6f-442">También puede habilitarlo estableciendo la propiedad en un directorio. Build. props.</span><span class="sxs-lookup"><span data-stu-id="23c6f-442">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="23c6f-443">A partir de Visual Studio 2019. x y NuGet 5. x, esta característica se considera experimental y opcional.</span><span class="sxs-lookup"><span data-stu-id="23c6f-443">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="23c6f-444">Siga [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) para más información sobre cuándo se habilitará esta característica de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="23c6f-444">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="23c6f-445">La restauración de gráficos estáticos cambia la parte de MSBuild de restore, la lectura y evaluación del proyecto, pero no el algoritmo de restauración.</span><span class="sxs-lookup"><span data-stu-id="23c6f-445">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="23c6f-446">El algoritmo restore es el mismo en todas las herramientas de NuGet (NuGet.exe, MSBuild.exe, dotnet.exe y Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="23c6f-446">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="23c6f-447">En muy pocos escenarios, la restauración de gráficos estáticos puede comportarse de forma diferente a la restauración actual y es posible que falten ciertos PackageReferences declarados o referencias.</span><span class="sxs-lookup"><span data-stu-id="23c6f-447">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="23c6f-448">Para que le resulte más fácil, como una única comprobación, al migrar a la restauración de gráficos estáticos, considere la posibilidad de ejecutar:</span><span class="sxs-lookup"><span data-stu-id="23c6f-448">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="23c6f-449">NuGet *no* debe notificar ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="23c6f-449">NuGet should *not* report any changes.</span></span> <span data-ttu-id="23c6f-450">Si ve una discrepancia, registre un problema en [NuGet/Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="23c6f-450">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="23c6f-451">Reemplazo de una biblioteca desde un gráfico de restauración</span><span class="sxs-lookup"><span data-stu-id="23c6f-451">Replacing one library from a restore graph</span></span>

<span data-ttu-id="23c6f-452">Si una restauración agrega el ensamblado equivocado, se puede excluir la opción predeterminada de ese paquete y reemplazarla por una de su propia elección.</span><span class="sxs-lookup"><span data-stu-id="23c6f-452">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="23c6f-453">En primer lugar, con una `PackageReference` de nivel superior, excluya todos los activos:</span><span class="sxs-lookup"><span data-stu-id="23c6f-453">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="23c6f-454">Después, agregue su propia referencia a la copia local correspondiente del archivo DLL:</span><span class="sxs-lookup"><span data-stu-id="23c6f-454">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
