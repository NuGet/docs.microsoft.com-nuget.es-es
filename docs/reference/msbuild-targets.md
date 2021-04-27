---
title: NuGet empaquetar y restaurar como MSBuild destinos
description: NuGet Pack y restore pueden funcionar directamente como MSBuild destinos con NuGet 4.0+.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067315"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="25015-103">NuGet empaquetar y restaurar como MSBuild destinos</span><span class="sxs-lookup"><span data-stu-id="25015-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="25015-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="25015-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="25015-105">Con el [formato PackageReference,](../consume-packages/package-references-in-project-files.md) 4.0+ puede almacenar todos los metadatos de manifiesto directamente dentro de un archivo de proyecto en lugar de NuGet usar un archivo `.nuspec` independiente.</span><span class="sxs-lookup"><span data-stu-id="25015-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="25015-106">Con MSBuild 15.1+, también es un ciudadano de primera clase con los destinos NuGet y , como se describe a MSBuild `pack` `restore` continuación.</span><span class="sxs-lookup"><span data-stu-id="25015-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="25015-107">Estos destinos le permiten trabajar con NuGet como lo haría con cualquier otra tarea o MSBuild destino.</span><span class="sxs-lookup"><span data-stu-id="25015-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="25015-108">Para obtener instrucciones sobre NuGet cómo crear un paquete mediante , vea Crear un paquete MSBuild [ NuGet mediante MSBuild ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="25015-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="25015-109">(Para NuGet 3.x y versiones anteriores, use los comandos [pack](../reference/cli-reference/cli-ref-pack.md) y [restore](../reference/cli-reference/cli-ref-restore.md) a través de la NuGet CLI en su lugar).</span><span class="sxs-lookup"><span data-stu-id="25015-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="25015-110">Orden de compilación de destinos</span><span class="sxs-lookup"><span data-stu-id="25015-110">Target build order</span></span>

<span data-ttu-id="25015-111">Dado `pack` que y son `restore`  MSBuild destinos, puede acceder a ellos para mejorar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="25015-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="25015-112">Por ejemplo, supongamos que desea copiar el paquete en un recurso compartido de red después de empaquetarlo.</span><span class="sxs-lookup"><span data-stu-id="25015-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="25015-113">Puede hacer esto si agrega lo siguiente al archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="25015-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="25015-114">De forma similar, puede escribir una MSBuild tarea, escribir su propio destino y consumir NuGet propiedades en la MSBuild tarea.</span><span class="sxs-lookup"><span data-stu-id="25015-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="25015-115">`$(OutputPath)` es relativo y espera que ejecute el comando desde la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="25015-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="25015-116">Destino de pack</span><span class="sxs-lookup"><span data-stu-id="25015-116">pack target</span></span>

<span data-ttu-id="25015-117">En el caso de los proyectos de .NET que usan el formato , el uso de dibuja entradas del archivo de proyecto para `PackageReference` `msbuild -t:pack` usarlas en la creación de un NuGet paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="25015-118">En la tabla siguiente se describen MSBuild las propiedades que se pueden agregar a un archivo de proyecto dentro del primer `<PropertyGroup>` nodo.</span><span class="sxs-lookup"><span data-stu-id="25015-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="25015-119">Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="25015-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="25015-120">Para mayor comodidad, la tabla se organiza mediante la propiedad equivalente en un [ `.nuspec` archivo](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="25015-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="25015-121">`Owners` Las `Summary` propiedades y de no se `.nuspec` admiten con MSBuild .</span><span class="sxs-lookup"><span data-stu-id="25015-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="25015-122">nuspecAtributo/valor</span><span class="sxs-lookup"><span data-stu-id="25015-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="25015-123">PropiedadMSBuild</span><span class="sxs-lookup"><span data-stu-id="25015-123">MSBuild Property</span></span> | <span data-ttu-id="25015-124">Default</span><span class="sxs-lookup"><span data-stu-id="25015-124">Default</span></span> | <span data-ttu-id="25015-125">Notas</span><span class="sxs-lookup"><span data-stu-id="25015-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="25015-126">`$(AssemblyName)` de MSBuild</span><span class="sxs-lookup"><span data-stu-id="25015-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="25015-127">Versión</span><span class="sxs-lookup"><span data-stu-id="25015-127">Version</span></span> | <span data-ttu-id="25015-128">Esto es compatible con semver, por `1.0.0` ejemplo, `1.0.0-beta` , o `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="25015-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="25015-129">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-129">empty</span></span> | <span data-ttu-id="25015-130">Configuración `PackageVersion` sobrescritura `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="25015-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="25015-131">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-131">empty</span></span> | <span data-ttu-id="25015-132">`$(VersionSuffix)` de MSBuild .</span><span class="sxs-lookup"><span data-stu-id="25015-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="25015-133">Configuración `PackageVersion` de sobrescrituras `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="25015-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="25015-134">Nombre del usuario actual</span><span class="sxs-lookup"><span data-stu-id="25015-134">Username of the current user</span></span> | <span data-ttu-id="25015-135">Lista separada por punto y coma de los autores de paquetes, que coincide con los nombres de perfil en nuget.org. Estos se muestran en la Galería en nuget.org y los mismos autores usan para hacer referencia cruzada NuGet a los paquetes.</span><span class="sxs-lookup"><span data-stu-id="25015-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="25015-136">N/D</span><span class="sxs-lookup"><span data-stu-id="25015-136">N/A</span></span> | <span data-ttu-id="25015-137">No está presente en nuspec</span><span class="sxs-lookup"><span data-stu-id="25015-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="25015-138">El `PackageId`</span><span class="sxs-lookup"><span data-stu-id="25015-138">The `PackageId`</span></span> | <span data-ttu-id="25015-139">Un título fácil de usar del paquete, que se usa normalmente en las visualizaciones de la interfaz de usuario, como en nuget.org, y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25015-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="25015-140">"Descripción del paquete"</span><span class="sxs-lookup"><span data-stu-id="25015-140">"Package Description"</span></span> | <span data-ttu-id="25015-141">Una descripción larga del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="25015-141">A long description for the assembly.</span></span> <span data-ttu-id="25015-142">Si `PackageDescription` no se especifica, esta propiedad también se utiliza como la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="25015-143">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-143">empty</span></span> | <span data-ttu-id="25015-144">Detalles de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="25015-145">Un valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="25015-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="25015-146">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-146">empty</span></span> | <span data-ttu-id="25015-147">Se corresponde con `<license type="expression">`.</span><span class="sxs-lookup"><span data-stu-id="25015-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="25015-148">Consulte [Empaquetado de una expresión de licencia o un archivo de licencia.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="25015-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="25015-149">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-149">empty</span></span> | <span data-ttu-id="25015-150">Ruta de acceso a un archivo de licencia dentro del paquete si usa una licencia personalizada o una licencia a la que no se le ha asignado un identificador SPDX.</span><span class="sxs-lookup"><span data-stu-id="25015-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="25015-151">Debe empaquetar explícitamente el archivo de licencia al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="25015-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="25015-152">Se corresponde con `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="25015-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="25015-153">Consulte [Empaquetado de una expresión de licencia o un archivo de licencia.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="25015-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="25015-154">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-154">empty</span></span> | <span data-ttu-id="25015-155">`PackageLicenseUrl` está desusada.</span><span class="sxs-lookup"><span data-stu-id="25015-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="25015-156">Use `PackageLicenseExpression` o `PackageLicenseFile` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="25015-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="25015-157">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="25015-158">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-158">empty</span></span> | <span data-ttu-id="25015-159">Ruta de acceso a una imagen del paquete que se va a usar como icono del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="25015-160">Debe empaquetar explícitamente el archivo de imagen de icono al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="25015-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="25015-161">Para obtener más información, vea [Empaquetado de un archivo de imagen de icono y](#packing-an-icon-image-file) [ `icon` metadatos.](./nuspec.md#icon)</span><span class="sxs-lookup"><span data-stu-id="25015-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="25015-162">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-162">empty</span></span> | <span data-ttu-id="25015-163">`PackageIconUrl` está en desuso en favor de `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="25015-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="25015-164">Sin embargo, para obtener la mejor experiencia de nivel inferior, debe especificar `PackageIconUrl` además de `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="25015-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="25015-165">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-165">empty</span></span> | <span data-ttu-id="25015-166">Debe empaquetar explícitamente el archivo Léame al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="25015-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="25015-167">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-167">empty</span></span> | <span data-ttu-id="25015-168">Una lista de etiquetas delimitada por punto y coma que designa el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="25015-169">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-169">empty</span></span> | <span data-ttu-id="25015-170">Notas de la versión para el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="25015-171">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-171">empty</span></span> | <span data-ttu-id="25015-172">Dirección URL del repositorio que se usa para clonar o recuperar el código fuente.</span><span class="sxs-lookup"><span data-stu-id="25015-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="25015-173">Ejemplo: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="25015-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="25015-174">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-174">empty</span></span> | <span data-ttu-id="25015-175">Tipo de repositorio.</span><span class="sxs-lookup"><span data-stu-id="25015-175">Repository type.</span></span> <span data-ttu-id="25015-176">Ejemplos: `git` (valor predeterminado), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="25015-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="25015-177">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-177">empty</span></span> | <span data-ttu-id="25015-178">Información opcional de la rama del repositorio.</span><span class="sxs-lookup"><span data-stu-id="25015-178">Optional repository branch information.</span></span> <span data-ttu-id="25015-179">`RepositoryUrl` también se debe especificar para que esta propiedad se incluya.</span><span class="sxs-lookup"><span data-stu-id="25015-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="25015-180">Ejemplo: *master* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="25015-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="25015-181">vacío</span><span class="sxs-lookup"><span data-stu-id="25015-181">empty</span></span> | <span data-ttu-id="25015-182">Confirmación o conjunto de cambios opcionales de repositorio para indicar en qué origen se ha compilado el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="25015-183">`RepositoryUrl` también se debe especificar para que esta propiedad se incluya.</span><span class="sxs-lookup"><span data-stu-id="25015-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="25015-184">Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="25015-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | <span data-ttu-id="25015-185">Indica el uso previsto del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-185">Indicates the package's intended use.</span></span> <span data-ttu-id="25015-186">Los tipos de paquete usan el mismo formato que los identificadores de paquete y están delimitados por `;` .</span><span class="sxs-lookup"><span data-stu-id="25015-186">Package types use the same format as package IDs and are delimited by `;`.</span></span> <span data-ttu-id="25015-187">Los tipos de paquetes pueden tener versiones anexando y `,` una [`Version`](/dotnet/api/system.version) cadena.</span><span class="sxs-lookup"><span data-stu-id="25015-187">Package types may be versioned by appending a `,` and a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="25015-188">Consulte [Establecer un tipo de NuGet paquete](../create-packages/set-package-type.md) ( NuGet 3.5.0+).</span><span class="sxs-lookup"><span data-stu-id="25015-188">See [Set a NuGet package type](../create-packages/set-package-type.md) (NuGet 3.5.0+).</span></span> |
| `Summary` | <span data-ttu-id="25015-189">No compatible</span><span class="sxs-lookup"><span data-stu-id="25015-189">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="25015-190">Entradas de destino de pack</span><span class="sxs-lookup"><span data-stu-id="25015-190">pack target inputs</span></span>

| <span data-ttu-id="25015-191">Propiedad</span><span class="sxs-lookup"><span data-stu-id="25015-191">Property</span></span> | <span data-ttu-id="25015-192">Description</span><span class="sxs-lookup"><span data-stu-id="25015-192">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="25015-193">Un valor booleano que especifica si se puede empaquetar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="25015-193">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="25015-194">El valor predeterminado es `true`.</span><span class="sxs-lookup"><span data-stu-id="25015-194">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="25015-195">Establezca en `true` para suprimir las dependencias del paquete NuGet generado.</span><span class="sxs-lookup"><span data-stu-id="25015-195">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="25015-196">Especifica la versión que tendrá el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="25015-196">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="25015-197">Acepta todas las formas de cadena NuGet de versión.</span><span class="sxs-lookup"><span data-stu-id="25015-197">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="25015-198">El valor predeterminado es `$(Version)`, es decir, de la propiedad `Version` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="25015-198">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="25015-199">Especifica el nombre para el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="25015-199">Specifies the name for the resulting package.</span></span> <span data-ttu-id="25015-200">Si no se especifica, la operación `pack` usará de forma predeterminada el elemento `AssemblyName` o el nombre del directorio como el nombre del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-200">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="25015-201">Una descripción larga del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="25015-201">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="25015-202">Lista separada por punto y coma de los autores de paquetes, que coincide con los nombres de perfil de nuget.org. Estos se muestran en la Galería en nuget.org y se usan para hacer referencia cruzada NuGet a paquetes de los mismos autores.</span><span class="sxs-lookup"><span data-stu-id="25015-202">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="25015-203">Una descripción larga del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="25015-203">A long description for the assembly.</span></span> <span data-ttu-id="25015-204">Si `PackageDescription` no se especifica, esta propiedad también se utiliza como la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-204">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="25015-205">Detalles de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-205">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="25015-206">Un valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="25015-206">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="25015-207">De manera predeterminada, es `false`.</span><span class="sxs-lookup"><span data-stu-id="25015-207">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="25015-208">Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="25015-208">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="25015-209">Con `PackageReference` ( 4.8+), esta marca también significa que los recursos en tiempo de compilación NuGet se excluyen de la compilación.</span><span class="sxs-lookup"><span data-stu-id="25015-209">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="25015-210">Para más información, consulte [Compatibilidad de DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="25015-210">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="25015-211">Una [expresión o identificador de licencia SPDX,](https://spdx.org/licenses/) por ejemplo, `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="25015-211">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="25015-212">Para obtener más información, vea [Empaquetado de una expresión de licencia o un archivo de licencia.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="25015-212">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="25015-213">Ruta de acceso a un archivo de licencia dentro del paquete si usa una licencia personalizada o una licencia a la que no se le ha asignado un identificador SPDX.</span><span class="sxs-lookup"><span data-stu-id="25015-213">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="25015-214">`PackageLicenseUrl` está desusada.</span><span class="sxs-lookup"><span data-stu-id="25015-214">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="25015-215">Use `PackageLicenseExpression` o `PackageLicenseFile` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="25015-215">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="25015-216">Especifica la ruta de acceso del icono del paquete, en relación con la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-216">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="25015-217">Para obtener más información, vea [Empaquetado de un archivo de imagen de icono.](#packing-an-icon-image-file)</span><span class="sxs-lookup"><span data-stu-id="25015-217">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="25015-218">Notas de la versión para el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-218">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="25015-219">Léame del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-219">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="25015-220">Una lista de etiquetas delimitada por punto y coma que designa el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-220">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="25015-221">Determina la ruta de acceso de salida en la que se va a quitar el paquete empaquetado.</span><span class="sxs-lookup"><span data-stu-id="25015-221">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="25015-222">El valor predeterminado es `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="25015-222">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="25015-223">Este valor booleano indica si el paquete debe crear un paquete de símbolos adicionales cuando se empaqueta el proyecto.</span><span class="sxs-lookup"><span data-stu-id="25015-223">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="25015-224">El formato del paquete de símbolos se controla mediante la propiedad `SymbolPackageFormat`.</span><span class="sxs-lookup"><span data-stu-id="25015-224">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="25015-225">Para obtener más información, [vea IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="25015-225">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="25015-226">Este valor booleano indica si el proceso de empaquetado debe crear un paquete de origen.</span><span class="sxs-lookup"><span data-stu-id="25015-226">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="25015-227">El paquete de origen contiene el código fuente de la biblioteca, así como archivos PDB.</span><span class="sxs-lookup"><span data-stu-id="25015-227">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="25015-228">Los archivos de origen se colocan en el directorio `src/ProjectName`, en el archivo de paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="25015-228">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="25015-229">Para obtener más información, [vea IncludeSource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="25015-229">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="25015-230">Especifica si se copian todos los archivos de salida en la carpeta *tools* en lugar de la carpeta *lib*.</span><span class="sxs-lookup"><span data-stu-id="25015-230">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="25015-231">Para obtener más información, [vea IsTool](#istool).</span><span class="sxs-lookup"><span data-stu-id="25015-231">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="25015-232">Dirección URL del repositorio que se usa para clonar o recuperar el código fuente.</span><span class="sxs-lookup"><span data-stu-id="25015-232">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="25015-233">Ejemplo: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="25015-233">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="25015-234">Tipo de repositorio.</span><span class="sxs-lookup"><span data-stu-id="25015-234">Repository type.</span></span> <span data-ttu-id="25015-235">Ejemplos: `git` (valor predeterminado), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="25015-235">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="25015-236">Información opcional de la rama del repositorio.</span><span class="sxs-lookup"><span data-stu-id="25015-236">Optional repository branch information.</span></span> <span data-ttu-id="25015-237">`RepositoryUrl` también se debe especificar para que esta propiedad se incluya.</span><span class="sxs-lookup"><span data-stu-id="25015-237">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="25015-238">Ejemplo: *master* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="25015-238">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="25015-239">Confirmación o conjunto de cambios opcionales de repositorio para indicar en qué origen se ha compilado el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-239">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="25015-240">`RepositoryUrl` también se debe especificar para que esta propiedad se incluya.</span><span class="sxs-lookup"><span data-stu-id="25015-240">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="25015-241">Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="25015-241">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="25015-242">Especifica el formato del paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="25015-242">Specifies the format of the symbols package.</span></span> <span data-ttu-id="25015-243">Si es "symbols.nupkg", se crea un paquete de símbolos heredado con una extensión *.symbols.nupkg* que contiene archivos PDB, DLL y otros archivos de salida.</span><span class="sxs-lookup"><span data-stu-id="25015-243">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="25015-244">Si es "snupkg", se crea un paquete de símbolos snupkg que contiene los archivos PB portátiles.</span><span class="sxs-lookup"><span data-stu-id="25015-244">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="25015-245">El valor predeterminado es "symbols.nupkg".</span><span class="sxs-lookup"><span data-stu-id="25015-245">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="25015-246">Especifica que no `pack` debe ejecutar el análisis de paquetes después de compilar el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-246">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="25015-247">Especifica la versión mínima del cliente que puede instalar este paquete, aplicada por nuget.exe NuGet y el Visual Studio Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="25015-247">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="25015-248">Este valor booleano especifica si se deben empaquetar los ensamblados de salida de la compilación en el archivo *.nupkg* o no.</span><span class="sxs-lookup"><span data-stu-id="25015-248">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="25015-249">Este valor booleano especifica si los elementos que tienen un tipo de `Content` se incluyen automáticamente en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="25015-249">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="25015-250">El valor predeterminado es `true`.</span><span class="sxs-lookup"><span data-stu-id="25015-250">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="25015-251">Especifica la carpeta en la que se colocarán los ensamblados de salida.</span><span class="sxs-lookup"><span data-stu-id="25015-251">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="25015-252">Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.</span><span class="sxs-lookup"><span data-stu-id="25015-252">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="25015-253">Para obtener más información, vea [Ensamblados de salida.](#output-assemblies)</span><span class="sxs-lookup"><span data-stu-id="25015-253">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="25015-254">Especifica la ubicación predeterminada de donde deben ir todos los archivos de contenido si `PackagePath` no se especifica para ellos.</span><span class="sxs-lookup"><span data-stu-id="25015-254">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="25015-255">El valor predeterminado es “content;contentFiles”.</span><span class="sxs-lookup"><span data-stu-id="25015-255">The default value is "content;contentFiles".</span></span> <span data-ttu-id="25015-256">Para obtener más información, consulte [Including content in a package](#including-content-in-a-package) (Incluir contenido en un paquete).</span><span class="sxs-lookup"><span data-stu-id="25015-256">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="25015-257">Ruta de acceso relativa o absoluta al *.nuspec* archivo que se usa para el empaquetado.</span><span class="sxs-lookup"><span data-stu-id="25015-257">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="25015-258">Si se especifica, se usa **exclusivamente** para empaquetar información y no se usa ninguna información de los proyectos.</span><span class="sxs-lookup"><span data-stu-id="25015-258">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="25015-259">Para obtener más información, [vea Empaquetado mediante un .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="25015-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="25015-260">Ruta de acceso base para el *.nuspec* archivo.</span><span class="sxs-lookup"><span data-stu-id="25015-260">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="25015-261">Para obtener más información, [vea Empaquetado mediante un .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="25015-261">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="25015-262">Lista separada por punto y coma de pares clave=valor.</span><span class="sxs-lookup"><span data-stu-id="25015-262">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="25015-263">Para obtener más información, [vea Empaquetado mediante .nuspec ](#packing-using-a-nuspec-file)un .</span><span class="sxs-lookup"><span data-stu-id="25015-263">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="25015-264">Escenarios de pack</span><span class="sxs-lookup"><span data-stu-id="25015-264">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="25015-265">Supresión de dependencias</span><span class="sxs-lookup"><span data-stu-id="25015-265">Suppressing dependencies</span></span>

<span data-ttu-id="25015-266">Para suprimir las dependencias de paquete del paquete generado, establezca en , que permitirá omitir NuGet `SuppressDependenciesWhenPacking` todas las `true` dependencias del archivo nupkg generado.</span><span class="sxs-lookup"><span data-stu-id="25015-266">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="25015-267">`PackageIconUrl` está en desuso en favor de la [`PackageIcon`](#packageicon) propiedad .</span><span class="sxs-lookup"><span data-stu-id="25015-267">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="25015-268">A partir NuGet de la versión 5.3 Visual Studio 2019 16.3, genera la advertencia `pack` [NU5048](./errors-and-warnings/nu5048.md) si los metadatos del paquete solo especifican `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="25015-268">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="25015-269">Para mantener la compatibilidad con versiones anteriores con clientes y orígenes que aún no admiten `PackageIcon` , especifique `PackageIcon` y `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="25015-269">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="25015-270">Visual Studio admite `PackageIcon` paquetes procedentes de un origen basado en carpetas.</span><span class="sxs-lookup"><span data-stu-id="25015-270">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="25015-271">Empaquetado de un archivo de imagen de icono</span><span class="sxs-lookup"><span data-stu-id="25015-271">Packing an icon image file</span></span>

<span data-ttu-id="25015-272">Al empaquetar un archivo de imagen de icono, use la propiedad para especificar la ruta de acceso del archivo de icono, en relación con `PackageIcon` la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-272">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="25015-273">Además, asegúrese de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-273">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="25015-274">El tamaño del archivo de imagen está limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="25015-274">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="25015-275">Entre los formatos de archivo admitidos se incluyen JPEG y PNG.</span><span class="sxs-lookup"><span data-stu-id="25015-275">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="25015-276">Se recomienda una resolución de imagen de 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="25015-276">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="25015-277">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="25015-277">For example:</span></span>

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

<span data-ttu-id="25015-278">[Ejemplo de icono de paquete](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="25015-278">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="25015-279">Para el nuspec equivalente, echa un vistazo a la [ nuspec referencia del icono](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="25015-279">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="25015-280">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="25015-280">PackageReadmeFile</span></span>

<span data-ttu-id="25015-281">*Compatible con **NuGet la versión preliminar 5.10.0 2** del SDK de  /  **.NET 5.0.300** y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="25015-281">*Supported with **NuGet 5.10.0 preview 2** / **.NET SDK 5.0.300** and above*</span></span>

<span data-ttu-id="25015-282">Al empaquetar un archivo Léame, debe usar la propiedad para especificar la ruta de acceso del paquete, en relación con la `PackageReadmeFile` raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-282">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="25015-283">Además de esto, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-283">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="25015-284">Los formatos de archivo admitidos incluyen solo Markdown (*.md*).</span><span class="sxs-lookup"><span data-stu-id="25015-284">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="25015-285">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="25015-285">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="25015-286">Para el nuspec equivalente, echa un vistazo a [ nuspec la referencia de léame](nuspec.md#readme).</span><span class="sxs-lookup"><span data-stu-id="25015-286">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="25015-287">Ensamblados de salida</span><span class="sxs-lookup"><span data-stu-id="25015-287">Output assemblies</span></span>

<span data-ttu-id="25015-288">`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`.</span><span class="sxs-lookup"><span data-stu-id="25015-288">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="25015-289">Los archivos de salida que se copian dependen de lo MSBuild que proporciona el `BuiltOutputProjectGroup` destino.</span><span class="sxs-lookup"><span data-stu-id="25015-289">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="25015-290">Hay dos propiedades que puede usar en el archivo del proyecto o en la línea de comandos MSBuild  para controlar dónde van los ensamblados de salida:</span><span class="sxs-lookup"><span data-stu-id="25015-290">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="25015-291">`IncludeBuildOutput`: un valor booleano que determina si los ensamblados de salida de compilación deben incluirse en el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-291">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="25015-292">`BuildOutputTargetFolder`: especifica la carpeta en la que se deben colocar los ensamblados de salida.</span><span class="sxs-lookup"><span data-stu-id="25015-292">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="25015-293">Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.</span><span class="sxs-lookup"><span data-stu-id="25015-293">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="25015-294">Referencias de paquete</span><span class="sxs-lookup"><span data-stu-id="25015-294">Package references</span></span>

<span data-ttu-id="25015-295">Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="25015-295">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="25015-296">Referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="25015-296">Project to project references</span></span>

<span data-ttu-id="25015-297">Las referencias de proyecto a proyecto se consideran de forma predeterminada como NuGet referencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-297">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="25015-298">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="25015-298">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="25015-299">También puede agregar los metadatos siguientes a la referencia de proyecto:</span><span class="sxs-lookup"><span data-stu-id="25015-299">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="25015-300">Inclusión de contenido en un paquete</span><span class="sxs-lookup"><span data-stu-id="25015-300">Including content in a package</span></span>

<span data-ttu-id="25015-301">Para incluir contenido, agregue metadatos adicionales al elemento `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="25015-301">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="25015-302">De forma predeterminada todos los elementos de tipo "Content" se incluyen en el paquete a menos que los reemplace con entradas como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="25015-302">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="25015-303">De forma predeterminada, todo el contenido se agrega a la raíz de la carpeta `content` y `contentFiles\any\<target_framework>` dentro de un paquete y se conserva la estructura de carpetas relativa, a menos que se especifique una ruta de acceso de paquete:</span><span class="sxs-lookup"><span data-stu-id="25015-303">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="25015-304">Si desea copiar todo el contenido solo en una carpeta raíz específica (en lugar de y en ambas), puede usar la propiedad , que tiene como valor predeterminado `content` `contentFiles` MSBuild "content;contentFiles", pero se puede establecer en cualquier otro nombre de `ContentTargetFolders` carpeta.</span><span class="sxs-lookup"><span data-stu-id="25015-304">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="25015-305">Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="25015-305">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="25015-306">`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="25015-306">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="25015-307">Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-307">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="25015-308">Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:</span><span class="sxs-lookup"><span data-stu-id="25015-308">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="25015-309">También hay una MSBuild propiedad , que tiene como valor predeterminado `$(IncludeContentInPack)` `true` .</span><span class="sxs-lookup"><span data-stu-id="25015-309">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="25015-310">Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="25015-310">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="25015-311">Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen y qué conjuntos y valores ```<PackageCopyToOutput>``` en la entrada de la ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` nuspec salida.</span><span class="sxs-lookup"><span data-stu-id="25015-311">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="25015-312">Además de los elementos Content, los metadatos `<Pack>` y `<PackagePath>` también se pueden establecer en archivos con una acción de compilación Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="25015-312">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="25015-313">Para que el comando pack anexe el nombre de archivo a la ruta de acceso del paquete cuando se usan patrones globales, la ruta de acceso del paquete debe terminar con el carácter separador de carpeta; en caso contrario, la ruta de acceso del paquete se trata como la ruta de acceso completa, incluido el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="25015-313">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="25015-314">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="25015-314">IncludeSymbols</span></span>

<span data-ttu-id="25015-315">Cuando se usa `MSBuild -t:pack -p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="25015-315">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="25015-316">Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.</span><span class="sxs-lookup"><span data-stu-id="25015-316">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="25015-317">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="25015-317">IncludeSource</span></span>

<span data-ttu-id="25015-318">Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="25015-318">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="25015-319">Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="25015-319">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="25015-320">Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.</span><span class="sxs-lookup"><span data-stu-id="25015-320">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="25015-321">Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="25015-321">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="25015-322">Empaquetado de una expresión de licencia o un archivo de licencia</span><span class="sxs-lookup"><span data-stu-id="25015-322">Packing a license expression or a license file</span></span>

<span data-ttu-id="25015-323">Cuando use una expresión de licencia, use la `PackageLicenseExpression` propiedad .</span><span class="sxs-lookup"><span data-stu-id="25015-323">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="25015-324">Para obtener un ejemplo, vea [Ejemplo de expresión de licencia](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="25015-324">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="25015-325">Para más información sobre las expresiones de licencia y las licencias aceptadas por NuGet .org, consulte metadatos [de licencia.](nuspec.md#license)</span><span class="sxs-lookup"><span data-stu-id="25015-325">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="25015-326">Al empaquetar un archivo de licencia, use `PackageLicenseFile` la propiedad para especificar la ruta de acceso del paquete, en relación con la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-326">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="25015-327">Además, asegúrese de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-327">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="25015-328">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="25015-328">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="25015-329">Para obtener un ejemplo, vea [Ejemplo de archivo de licencia](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="25015-329">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="25015-330">Solo se `PackageLicenseExpression` puede especificar uno de , y a la `PackageLicenseFile` `PackageLicenseUrl` vez.</span><span class="sxs-lookup"><span data-stu-id="25015-330">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="25015-331">Empaquetado de un archivo sin una extensión</span><span class="sxs-lookup"><span data-stu-id="25015-331">Packing a file without an extension</span></span>

<span data-ttu-id="25015-332">En algunos escenarios, como al empaquetar un archivo de licencia, es posible que quiera incluir un archivo sin una extensión.</span><span class="sxs-lookup"><span data-stu-id="25015-332">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="25015-333">Por motivos históricos, NuGet  &  MSBuild trate las rutas de acceso sin una extensión como directorios.</span><span class="sxs-lookup"><span data-stu-id="25015-333">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="25015-334">[Archivo sin un ejemplo de extensión](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="25015-334">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="25015-335">IsTool</span><span class="sxs-lookup"><span data-stu-id="25015-335">IsTool</span></span>

<span data-ttu-id="25015-336">Cuando se usa `MSBuild -t:pack -p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="25015-336">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="25015-337">Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="25015-337">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="25015-338">Empaquetado mediante un `.nuspec` archivo</span><span class="sxs-lookup"><span data-stu-id="25015-338">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="25015-339">Aunque se recomienda [](../reference/msbuild-targets.md#pack-target) incluir todas las propiedades que normalmente se encuentran en el archivo en el archivo de proyecto, puede optar por usar un archivo para `.nuspec` `.nuspec` empaquetar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="25015-339">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="25015-340">Para un proyecto que no sea de estilo SDK que use , debe importar para que se pueda ejecutar la tarea de `PackageReference` `NuGet.Build.Tasks.Pack.targets` paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-340">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="25015-341">Debe restaurar el proyecto para poder empaquetar un nuspec archivo.</span><span class="sxs-lookup"><span data-stu-id="25015-341">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="25015-342">(Un proyecto de estilo SDK incluye los destinos del paquete de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="25015-342">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="25015-343">La plataforma de destino del archivo de proyecto es irrelevante y no se usa al empaquetar nuspec un .</span><span class="sxs-lookup"><span data-stu-id="25015-343">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="25015-344">Las tres propiedades MSBuild siguientes son relevantes para el empaquetado mediante `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="25015-344">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="25015-345">`NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.</span><span class="sxs-lookup"><span data-stu-id="25015-345">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="25015-346">`NuspecProperties`: lista de pares clave=valor separados por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="25015-346">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="25015-347">Debido a la forma en que funciona el análisis de la línea de comandos, se deben especificar varias propiedades como MSBuild se indica a continuación: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="25015-347">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="25015-348">`NuspecBasePath`: ruta de acceso base para el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="25015-348">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="25015-349">Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="25015-349">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="25015-350">Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="25015-350">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="25015-351">Tenga en cuenta que el empaquetado de un dotnet.exe o msbuild también conduce a nuspec la creación del proyecto de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="25015-351">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="25015-352">Esto se puede evitar pasando la propiedad a dotnet.exe, que es el equivalente de establecer en el archivo de proyecto, junto con la configuración ```--no-build``` en el archivo del ```<NoBuild>true</NoBuild> ``` ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` proyecto.</span><span class="sxs-lookup"><span data-stu-id="25015-352">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="25015-353">Un ejemplo de un *archivo .csproj* para empaquetar un nuspec archivo es:</span><span class="sxs-lookup"><span data-stu-id="25015-353">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="25015-354">Puntos de extensión avanzados para crear un paquete personalizado</span><span class="sxs-lookup"><span data-stu-id="25015-354">Advanced extension points to create customized package</span></span>

<span data-ttu-id="25015-355">El `pack` destino proporciona dos puntos de extensión que se ejecutan en la compilación interna específica del marco de destino.</span><span class="sxs-lookup"><span data-stu-id="25015-355">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="25015-356">Los puntos de extensión admiten la inclusión de ensamblados y contenido específicos de la plataforma de destino en un paquete:</span><span class="sxs-lookup"><span data-stu-id="25015-356">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="25015-357">`TargetsForTfmSpecificBuildOutput` target: se usa para los archivos dentro `lib` de la carpeta o una carpeta especificada mediante `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="25015-357">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="25015-358">`TargetsForTfmSpecificContentInPackage` target: se usa para archivos fuera de `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="25015-358">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="25015-359">Escribir un destino personalizado y especificarlo como el valor de la `$(TargetsForTfmSpecificBuildOutput)` propiedad .</span><span class="sxs-lookup"><span data-stu-id="25015-359">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="25015-360">En el caso de los archivos que necesiten entrar en (lib de forma predeterminada), el destino debe escribir esos archivos en ItemGroup y establecer los dos valores de metadatos `BuildOutputTargetFolder` `BuildOutputInPackage` siguientes:</span><span class="sxs-lookup"><span data-stu-id="25015-360">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="25015-361">`FinalOutputPath`: ruta de acceso absoluta del archivo; Si no se proporciona, la identidad se usa para evaluar la ruta de acceso de origen.</span><span class="sxs-lookup"><span data-stu-id="25015-361">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="25015-362">`TargetPath`: (Opcional) Se establece cuando el archivo debe ir a una subcarpeta dentro de , como los ensamblados satélite que van bajo `lib\<TargetFramework>` sus respectivas carpetas de referencia cultural.</span><span class="sxs-lookup"><span data-stu-id="25015-362">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="25015-363">El valor predeterminado es el nombre del archivo.</span><span class="sxs-lookup"><span data-stu-id="25015-363">Defaults to the name of the file.</span></span>

<span data-ttu-id="25015-364">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="25015-364">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="25015-365">Escribir un destino personalizado y especificarlo como el valor de la `$(TargetsForTfmSpecificContentInPackage)` propiedad .</span><span class="sxs-lookup"><span data-stu-id="25015-365">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="25015-366">Para que los archivos se incluyan en el paquete, el destino debe escribir esos archivos en ItemGroup y `TfmSpecificPackageFile` establecer los siguientes metadatos opcionales:</span><span class="sxs-lookup"><span data-stu-id="25015-366">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="25015-367">`PackagePath`: ruta de acceso donde se debe generar el archivo en el paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-367">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="25015-368">NuGet emite una advertencia si se agrega más de un archivo a la misma ruta de acceso del paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-368">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="25015-369">`BuildAction`: la acción de compilación que se va a asignar al archivo, solo es necesaria si la ruta de acceso del paquete está en la `contentFiles` carpeta .</span><span class="sxs-lookup"><span data-stu-id="25015-369">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="25015-370">El valor predeterminado es "None".</span><span class="sxs-lookup"><span data-stu-id="25015-370">Defaults to "None".</span></span>

<span data-ttu-id="25015-371">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="25015-371">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="25015-372">Destino de restore</span><span class="sxs-lookup"><span data-stu-id="25015-372">restore target</span></span>

<span data-ttu-id="25015-373">`MSBuild -t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="25015-373">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="25015-374">Leer todas las referencias entre proyectos</span><span class="sxs-lookup"><span data-stu-id="25015-374">Read all project to project references</span></span>
1. <span data-ttu-id="25015-375">Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias</span><span class="sxs-lookup"><span data-stu-id="25015-375">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="25015-376">Pasar MSBuild datos a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="25015-376">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="25015-377">Ejecutar la restauración</span><span class="sxs-lookup"><span data-stu-id="25015-377">Run restore</span></span>
1. <span data-ttu-id="25015-378">Descarga de paquetes</span><span class="sxs-lookup"><span data-stu-id="25015-378">Download packages</span></span>
1. <span data-ttu-id="25015-379">Escribir el archivo de activos, destinos y propiedades</span><span class="sxs-lookup"><span data-stu-id="25015-379">Write assets file, targets, and props</span></span>

<span data-ttu-id="25015-380">El `restore` destino funciona para proyectos con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="25015-380">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="25015-381">`MSBuild 16.5+` también tiene [compatibilidad de opt-in](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) con el `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="25015-381">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="25015-382">El `restore` destino no debe [ejecutarse](#restoring-and-building-with-one-msbuild-command) en combinación con el `build` destino.</span><span class="sxs-lookup"><span data-stu-id="25015-382">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="25015-383">Restaurar las propiedades</span><span class="sxs-lookup"><span data-stu-id="25015-383">Restore properties</span></span>

<span data-ttu-id="25015-384">La configuración de restauración adicional puede procede de MSBuild las propiedades del archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="25015-384">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="25015-385">También se pueden establecer valores desde la línea de comandos mediante el modificador `-p:` (vea los ejemplos siguientes).</span><span class="sxs-lookup"><span data-stu-id="25015-385">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="25015-386">Propiedad</span><span class="sxs-lookup"><span data-stu-id="25015-386">Property</span></span> | <span data-ttu-id="25015-387">Description</span><span class="sxs-lookup"><span data-stu-id="25015-387">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="25015-388">Lista delimitada por punto y coma de orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="25015-388">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="25015-389">Ruta de acceso de la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="25015-389">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="25015-390">Limitar las descargas a una cada vez.</span><span class="sxs-lookup"><span data-stu-id="25015-390">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="25015-391">Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="25015-391">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="25015-392">Si es true, evita el uso de paquetes almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="25015-392">If true, avoids using cached packages.</span></span> <span data-ttu-id="25015-393">Consulte [Administración de paquetes globales y carpetas de caché.](../consume-packages/managing-the-global-packages-and-cache-folders.md)</span><span class="sxs-lookup"><span data-stu-id="25015-393">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="25015-394">Si es true, ignora los orígenes de paquetes que producen errores o faltan.</span><span class="sxs-lookup"><span data-stu-id="25015-394">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="25015-395">Carpetas de reserva, que se usan de la misma manera que se usa la carpeta de paquetes de usuario.</span><span class="sxs-lookup"><span data-stu-id="25015-395">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="25015-396">Orígenes adicionales que se usarán durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="25015-396">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="25015-397">Carpetas de reserva adicionales que se usarán durante la restauración.</span><span class="sxs-lookup"><span data-stu-id="25015-397">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="25015-398">Excluye las carpetas de reserva especificadas en `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="25015-398">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="25015-399">Ruta de acceso a `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="25015-399">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="25015-400">Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="25015-400">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="25015-401">Cuando los proyectos se recopilan MSBuild a través de , determina si se recopilan mediante la `SkipNonexistentTargets` optimización.</span><span class="sxs-lookup"><span data-stu-id="25015-401">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="25015-402">Cuando no se establece, el valor predeterminado es `true` .</span><span class="sxs-lookup"><span data-stu-id="25015-402">When not set, defaults to `true`.</span></span> <span data-ttu-id="25015-403">La consecuencia es un comportamiento de error rápido cuando no se pueden importar los destinos de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="25015-403">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="25015-404">Carpeta de salida, con el valor predeterminado `BaseIntermediateOutputPath` y la `obj` carpeta .</span><span class="sxs-lookup"><span data-stu-id="25015-404">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="25015-405">En los proyectos basados en PackageReference, fuerza que todas las dependencias se resuelvan incluso si la última restauración se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="25015-405">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="25015-406">Especificar esta marca es similar a eliminar el `project.assets.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="25015-406">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="25015-407">Esto no omite http-cache.</span><span class="sxs-lookup"><span data-stu-id="25015-407">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="25015-408">Opta por el uso de un archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="25015-408">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="25015-409">Ejecute la restauración en modo bloqueado.</span><span class="sxs-lookup"><span data-stu-id="25015-409">Run restore in locked mode.</span></span> <span data-ttu-id="25015-410">Esto significa que la restauración no volverá a evaluar las dependencias.</span><span class="sxs-lookup"><span data-stu-id="25015-410">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="25015-411">Ubicación personalizada para el archivo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="25015-411">A custom location for the lock file.</span></span> <span data-ttu-id="25015-412">La ubicación predeterminada está junto al proyecto y se denomina `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="25015-412">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="25015-413">Obliga a la restauración a volver a compilar las dependencias y actualizar el archivo de bloqueo sin ninguna advertencia.</span><span class="sxs-lookup"><span data-stu-id="25015-413">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="25015-414">Un modificador de suscripción que restaura los proyectos con packages.config. Compatibilidad solo `MSBuild -t:restore` con .</span><span class="sxs-lookup"><span data-stu-id="25015-414">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="25015-415">Un modificador opt-in para usar la evaluación de MSBuild grafos estáticos en lugar de la evaluación estándar.</span><span class="sxs-lookup"><span data-stu-id="25015-415">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="25015-416">La evaluación de grafos estáticos es una característica experimental que es significativamente más rápida para grandes repositorios y soluciones.</span><span class="sxs-lookup"><span data-stu-id="25015-416">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="25015-417">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="25015-417">Examples</span></span>

<span data-ttu-id="25015-418">Línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="25015-418">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="25015-419">Archivo del proyecto:</span><span class="sxs-lookup"><span data-stu-id="25015-419">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="25015-420">Restaurar salidas</span><span class="sxs-lookup"><span data-stu-id="25015-420">Restore outputs</span></span>

<span data-ttu-id="25015-421">La restauración crea los archivos siguientes en la carpeta `obj` de compilación:</span><span class="sxs-lookup"><span data-stu-id="25015-421">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="25015-422">Archivo</span><span class="sxs-lookup"><span data-stu-id="25015-422">File</span></span> | <span data-ttu-id="25015-423">Descripción</span><span class="sxs-lookup"><span data-stu-id="25015-423">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="25015-424">Contiene el gráfico de dependencias de todas las referencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="25015-424">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="25015-425">Referencias a MSBuild propiedades contenidas en paquetes</span><span class="sxs-lookup"><span data-stu-id="25015-425">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="25015-426">Referencias a MSBuild destinos contenidos en paquetes</span><span class="sxs-lookup"><span data-stu-id="25015-426">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="25015-427">Restauración y creación con un MSBuild comando</span><span class="sxs-lookup"><span data-stu-id="25015-427">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="25015-428">Debido al hecho de que puede restaurar paquetes que desanuren destinos y propiedades, las evaluaciones de restauración y compilación se ejecutan NuGet MSBuild con diferentes propiedades globales.</span><span class="sxs-lookup"><span data-stu-id="25015-428">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="25015-429">Esto significa que lo siguiente tendrá un comportamiento imprevisible y, a menudo, incorrecto.</span><span class="sxs-lookup"><span data-stu-id="25015-429">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="25015-430">En su lugar, el enfoque recomendado es:</span><span class="sxs-lookup"><span data-stu-id="25015-430">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="25015-431">La misma lógica se aplica a otros destinos similares a `build` .</span><span class="sxs-lookup"><span data-stu-id="25015-431">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="25015-432">Restaurar PackageReference y packages.config proyectos con MSBuild</span><span class="sxs-lookup"><span data-stu-id="25015-432">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="25015-433">Con MSBuild las versiones 16.5 y posteriores, packages.config también se admiten para `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="25015-433">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="25015-434">`packages.config` restore solo está disponible con `MSBuild 16.5+` y no con `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="25015-434">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="25015-435">Restauración con evaluación MSBuild de grafos estáticos</span><span class="sxs-lookup"><span data-stu-id="25015-435">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="25015-436">Con MSBuild 16.6+, ha agregado una característica experimental para usar la evaluación de grafos estáticos desde la línea de comandos que mejora significativamente el tiempo de restauración para repositorios NuGet grandes.</span><span class="sxs-lookup"><span data-stu-id="25015-436">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="25015-437">También puede habilitarla estableciendo la propiedad en Directory.Build.Props.</span><span class="sxs-lookup"><span data-stu-id="25015-437">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="25015-438">A partir Visual Studio 2019.x y 5.x, esta característica se considera NuGet experimental y opt-in.</span><span class="sxs-lookup"><span data-stu-id="25015-438">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="25015-439">Siga [ NuGet /Home#9803](https://github.com/NuGet/Home/issues/9803) para obtener más información sobre cuándo se habilitará esta característica de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="25015-439">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="25015-440">La restauración de grafos estáticos cambia la parte de msbuild de la restauración, la lectura y evaluación del proyecto, pero no el algoritmo de restauración.</span><span class="sxs-lookup"><span data-stu-id="25015-440">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="25015-441">El algoritmo de restauración es el mismo en todas las NuGet herramientas NuGet (.exe, MSBuild .exe, dotnet.exe y Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="25015-441">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="25015-442">En muy pocos escenarios, la restauración de grafos estáticos puede comportarse de forma diferente a la restauración actual y es posible que falte ciertas packageReferences o ProjectReferences declaradas.</span><span class="sxs-lookup"><span data-stu-id="25015-442">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="25015-443">Para facilitar la mente, como una comprobación única, al migrar a la restauración de grafos estáticos, considere la posibilidad de ejecutar:</span><span class="sxs-lookup"><span data-stu-id="25015-443">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="25015-444">NuGet no *debe notificar* ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="25015-444">NuGet should *not* report any changes.</span></span> <span data-ttu-id="25015-445">Si ve una discrepancia, envíe un problema a [ NuGet /Home.](https://github.com/nuget/home/issues/new)</span><span class="sxs-lookup"><span data-stu-id="25015-445">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="25015-446">Reemplazo de una biblioteca desde un gráfico de restauración</span><span class="sxs-lookup"><span data-stu-id="25015-446">Replacing one library from a restore graph</span></span>

<span data-ttu-id="25015-447">Si una restauración agrega el ensamblado equivocado, se puede excluir la opción predeterminada de ese paquete y reemplazarla por una de su propia elección.</span><span class="sxs-lookup"><span data-stu-id="25015-447">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="25015-448">En primer lugar, con una `PackageReference` de nivel superior, excluya todos los activos:</span><span class="sxs-lookup"><span data-stu-id="25015-448">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="25015-449">Después, agregue su propia referencia a la copia local correspondiente del archivo DLL:</span><span class="sxs-lookup"><span data-stu-id="25015-449">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
