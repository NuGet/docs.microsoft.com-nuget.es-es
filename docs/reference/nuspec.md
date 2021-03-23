---
title: Referencia del archivo. nuspec para NuGet
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 4028657862cfd56d0653b370e8344cab8392d69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859504"
---
# <a name="nuspec-reference"></a><span data-ttu-id="1e35b-103">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="1e35b-103">.nuspec reference</span></span>

<span data-ttu-id="1e35b-104">Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="1e35b-105">Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores.</span><span class="sxs-lookup"><span data-stu-id="1e35b-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="1e35b-106">El manifiesto siempre se incluye en un paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="1e35b-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="1e35b-107">In this topic:</span></span>

- [<span data-ttu-id="1e35b-108">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="1e35b-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="1e35b-109">[Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1e35b-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="1e35b-110">Dependencias</span><span class="sxs-lookup"><span data-stu-id="1e35b-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="1e35b-111">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="1e35b-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="1e35b-112">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="1e35b-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="1e35b-113">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="1e35b-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="1e35b-114">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="1e35b-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="1e35b-115">Archivos nuspec de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1e35b-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="1e35b-116">Compatibilidad de tipos de proyecto</span><span class="sxs-lookup"><span data-stu-id="1e35b-116">Project type compatibility</span></span>

- <span data-ttu-id="1e35b-117">Use `.nuspec` con `nuget.exe pack` para proyectos que no son de estilo SDK que usan `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="1e35b-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="1e35b-118">`.nuspec`No es necesario que un archivo cree paquetes para los [proyectos de estilo SDK](../resources/check-project-format.md) (normalmente, los proyectos de .net Core y .net Standard que usan el [atributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="1e35b-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="1e35b-119">(Tenga en cuenta que `.nuspec` se genera cuando se crea el paquete).</span><span class="sxs-lookup"><span data-stu-id="1e35b-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="1e35b-120">Si va a crear un paquete mediante `dotnet.exe pack` o `msbuild pack target` , le recomendamos que incluya en su lugar [todas las propiedades](../reference/msbuild-targets.md#pack-target) que suelen estar en el `.nuspec` archivo en el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e35b-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="1e35b-121">Sin embargo, en su lugar, puede elegir [usar un `.nuspec` archivo para empaquetar con `dotnet.exe` o `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="1e35b-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span></span>

- <span data-ttu-id="1e35b-122">En el caso de los proyectos migrados de `packages.config` a [PackageReference](../consume-packages/package-references-in-project-files.md), `.nuspec` no es necesario un archivo para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="1e35b-123">En su lugar, use [msbuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="1e35b-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="1e35b-124">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="1e35b-124">General form and schema</span></span>

<span data-ttu-id="1e35b-125">El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="1e35b-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="1e35b-126">En este esquema, los archivos `.nuspec` tienen el siguiente formato general:</span><span class="sxs-lookup"><span data-stu-id="1e35b-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="1e35b-127">Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="1e35b-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="1e35b-128">Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="1e35b-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="1e35b-129">En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):</span><span class="sxs-lookup"><span data-stu-id="1e35b-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

<span data-ttu-id="1e35b-131">Todos los nombres de elementos XML del archivo. nuspec distinguen mayúsculas de minúsculas, como sucede con XML en general.</span><span class="sxs-lookup"><span data-stu-id="1e35b-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="1e35b-132">Por ejemplo, el uso del elemento metadata `<description>` es correcto y `<Description>` no es correcto.</span><span class="sxs-lookup"><span data-stu-id="1e35b-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="1e35b-133">A continuación se documentan las mayúsculas y minúsculas adecuadas para cada nombre de elemento.</span><span class="sxs-lookup"><span data-stu-id="1e35b-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="1e35b-134">Elementos de metadatos necesarios</span><span class="sxs-lookup"><span data-stu-id="1e35b-134">Required metadata elements</span></span>

<span data-ttu-id="1e35b-135">Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="1e35b-136">Estos elementos deben aparecer dentro de un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="1e35b-137">id</span><span class="sxs-lookup"><span data-stu-id="1e35b-137">id</span></span> 
<span data-ttu-id="1e35b-138">El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="1e35b-139">Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET.</span><span class="sxs-lookup"><span data-stu-id="1e35b-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="1e35b-140">Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="1e35b-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="1e35b-141">Al cargar un paquete en nuget.org, el `id` campo está limitado a 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="1e35b-142">version</span><span class="sxs-lookup"><span data-stu-id="1e35b-142">version</span></span>
<span data-ttu-id="1e35b-143">La versión del paquete, siguiendo el patrón *mayor.menor.revisión*.</span><span class="sxs-lookup"><span data-stu-id="1e35b-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="1e35b-144">Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="1e35b-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="1e35b-145">Al cargar un paquete en nuget.org, el `version` campo está limitado a 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="1e35b-146">description</span><span class="sxs-lookup"><span data-stu-id="1e35b-146">description</span></span>
<span data-ttu-id="1e35b-147">Descripción del paquete para la presentación de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1e35b-147">A description of the package for UI display.</span></span>

<span data-ttu-id="1e35b-148">Al cargar un paquete en nuget.org, el `description` campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="1e35b-149">authors</span><span class="sxs-lookup"><span data-stu-id="1e35b-149">authors</span></span>
<span data-ttu-id="1e35b-150">Una lista separada por comas de autores de paquetes, que coincide con los nombres de perfil en nuget.org. Estos se muestran en la galería de NuGet en nuget.org y se usan para hacer referencias cruzadas de paquetes por los mismos autores.</span><span class="sxs-lookup"><span data-stu-id="1e35b-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="1e35b-151">Al cargar un paquete en nuget.org, el `authors` campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="1e35b-152">Elementos de metadatos opcionales</span><span class="sxs-lookup"><span data-stu-id="1e35b-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="1e35b-153">owners</span><span class="sxs-lookup"><span data-stu-id="1e35b-153">owners</span></span>
> [!Important]
> <span data-ttu-id="1e35b-154">los propietarios están desusados.</span><span class="sxs-lookup"><span data-stu-id="1e35b-154">owners is deprecated.</span></span> <span data-ttu-id="1e35b-155">En su lugar, use authors.</span><span class="sxs-lookup"><span data-stu-id="1e35b-155">Use authors instead.</span></span>

<span data-ttu-id="1e35b-156">Lista separada por comas de los creadores de paquetes que usan nombres de perfil en nuget.org. Esta suele ser la misma lista que en y `authors` se omite al cargar el paquete en Nuget.org. Consulte [Administración de propietarios de paquetes en Nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="1e35b-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="1e35b-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="1e35b-157">projectUrl</span></span>
<span data-ttu-id="1e35b-158">Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1e35b-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="1e35b-159">Al cargar un paquete en nuget.org, el `projectUrl` campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="1e35b-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="1e35b-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="1e35b-161">licenseUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="1e35b-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="1e35b-162">Use la licencia en su lugar.</span><span class="sxs-lookup"><span data-stu-id="1e35b-162">Use license instead.</span></span>

<span data-ttu-id="1e35b-163">Una dirección URL para la licencia del paquete, que a menudo se muestra en ius como nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1e35b-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="1e35b-164">Al cargar un paquete en nuget.org, el `licenseUrl` campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="1e35b-165">license</span><span class="sxs-lookup"><span data-stu-id="1e35b-165">license</span></span>

<span data-ttu-id="1e35b-166">*Compatible con **NuGet 4.9.0** y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="1e35b-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="1e35b-167">Una expresión de licencia de SPDX o una ruta de acceso a un archivo de licencia dentro del paquete, que a menudo se muestra en ius como nuget.org. Si tiene licencia para el paquete con una licencia común, como MIT o la cláusula BSD-2, use el identificador de [licencia de SPDX](https://spdx.org/licenses/)asociado.</span><span class="sxs-lookup"><span data-stu-id="1e35b-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="1e35b-168">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e35b-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="1e35b-169">NuGet.org solo acepta expresiones de licencia aprobadas por la iniciativa de código abierto o la Fundación gratuita de software.</span><span class="sxs-lookup"><span data-stu-id="1e35b-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="1e35b-170">Si el paquete tiene licencia con varias licencias comunes, puede especificar una licencia compuesta mediante la [Sintaxis de expresión SPDX versión 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="1e35b-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="1e35b-171">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e35b-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="1e35b-172">Si usa una licencia personalizada que no es compatible con las expresiones de licencia, puede empaquetar un `.txt` `.md` archivo o con el texto de la licencia.</span><span class="sxs-lookup"><span data-stu-id="1e35b-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="1e35b-173">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e35b-173">For example:</span></span>

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="1e35b-174">En el caso del equivalente de MSBuild, eche un vistazo a [empaquetar una expresión de licencia o un archivo de licencia](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="1e35b-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="1e35b-175">A continuación se describe la sintaxis exacta de las expresiones de licencia de NuGet en [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="1e35b-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="1e35b-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="1e35b-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="1e35b-177">el iconUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="1e35b-177">iconUrl is deprecated.</span></span> <span data-ttu-id="1e35b-178">En su lugar, use el icono.</span><span class="sxs-lookup"><span data-stu-id="1e35b-178">Use icon instead.</span></span>

<span data-ttu-id="1e35b-179">Una dirección URL para una imagen de 128x128 con fondo de transparencia que se usará como icono para el paquete en la visualización de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1e35b-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="1e35b-180">Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen.</span><span class="sxs-lookup"><span data-stu-id="1e35b-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="1e35b-181">Por ejemplo, para usar una imagen de Github, use la dirección URL de archivo sin formato, como <em> https://github.com/ \<username\> / \<repository\> /raw/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="1e35b-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="1e35b-182">Al cargar un paquete en nuget.org, el `iconUrl` campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="1e35b-183">icon</span><span class="sxs-lookup"><span data-stu-id="1e35b-183">icon</span></span>

<span data-ttu-id="1e35b-184">*Compatible con **NuGet 5.3.0** y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="1e35b-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="1e35b-185">Es una ruta de acceso a un archivo de imagen dentro del paquete, que a menudo se muestra en ius como nuget.org como el icono de paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="1e35b-186">El tamaño del archivo de imagen está limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1e35b-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="1e35b-187">Entre los formatos de archivo admitidos se incluyen JPEG y PNG.</span><span class="sxs-lookup"><span data-stu-id="1e35b-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="1e35b-188">Se recomienda una resolución de imagen de 128x128.</span><span class="sxs-lookup"><span data-stu-id="1e35b-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="1e35b-189">Por ejemplo, debe agregar lo siguiente a su archivo nuspec al crear un paquete mediante nuget.exe:</span><span class="sxs-lookup"><span data-stu-id="1e35b-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="1e35b-190">Icono de paquete de ejemplo de nuspec.</span><span class="sxs-lookup"><span data-stu-id="1e35b-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

<span data-ttu-id="1e35b-191">Para el equivalente de MSBuild, eche un vistazo a [empaquetar un archivo de imagen de icono](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="1e35b-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="1e35b-192">Puede especificar `icon` y `iconUrl` para mantener la compatibilidad con versiones anteriores de los orígenes que no admiten `icon` .</span><span class="sxs-lookup"><span data-stu-id="1e35b-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="1e35b-193">Visual Studio será compatible con los `icon` paquetes procedentes de un origen basado en carpetas en una versión futura.</span><span class="sxs-lookup"><span data-stu-id="1e35b-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="1e35b-194">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="1e35b-194">requireLicenseAcceptance</span></span>
<span data-ttu-id="1e35b-195">Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="1e35b-195">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="1e35b-196">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="1e35b-196">developmentDependency</span></span>
<span data-ttu-id="1e35b-197">*(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="1e35b-197">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="1e35b-198">Con PackageReference (NuGet 4.8 +) , esta marca también significa que excluirá los recursos en tiempo de compilación de la compilación.</span><span class="sxs-lookup"><span data-stu-id="1e35b-198">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="1e35b-199">Consulte [compatibilidad con DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="1e35b-199">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="1e35b-200">Resumen</span><span class="sxs-lookup"><span data-stu-id="1e35b-200">summary</span></span>
> [!Important]
> <span data-ttu-id="1e35b-201">`summary` está en desuso.</span><span class="sxs-lookup"><span data-stu-id="1e35b-201">`summary` is being deprecated.</span></span> <span data-ttu-id="1e35b-202">En su lugar, use `description`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-202">Use `description` instead.</span></span>

<span data-ttu-id="1e35b-203">Descripción breve del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1e35b-203">A short description of the package for UI display.</span></span> <span data-ttu-id="1e35b-204">Si se omite, se usará una versión truncada de `description`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-204">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="1e35b-205">Al cargar un paquete en nuget.org, el `summary` campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-205">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="1e35b-206">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="1e35b-206">releaseNotes</span></span>
<span data-ttu-id="1e35b-207">*(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-207">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="1e35b-208">Al cargar un paquete en nuget.org, el `releaseNotes` campo está limitado a 35.000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-208">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="1e35b-209">copyright</span><span class="sxs-lookup"><span data-stu-id="1e35b-209">copyright</span></span>
<span data-ttu-id="1e35b-210">*(1.5+)* Información de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-210">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="1e35b-211">Al cargar un paquete en nuget.org, el `copyright` campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-211">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="1e35b-212">language</span><span class="sxs-lookup"><span data-stu-id="1e35b-212">language</span></span>
<span data-ttu-id="1e35b-213">Identificador de configuración regional del paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-213">The locale ID for the package.</span></span> <span data-ttu-id="1e35b-214">Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="1e35b-214">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="1e35b-215">etiquetas</span><span class="sxs-lookup"><span data-stu-id="1e35b-215">tags</span></span>
<span data-ttu-id="1e35b-216">Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados.</span><span class="sxs-lookup"><span data-stu-id="1e35b-216">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="1e35b-217">Al cargar un paquete en nuget.org, el `tags` campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-217">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="1e35b-218">serviceable</span><span class="sxs-lookup"><span data-stu-id="1e35b-218">serviceable</span></span> 
<span data-ttu-id="1e35b-219">*(3.3+)* Solo para uso interno de NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e35b-219">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="1e35b-220">repository</span><span class="sxs-lookup"><span data-stu-id="1e35b-220">repository</span></span>
<span data-ttu-id="1e35b-221">Metadatos del repositorio, que constan de cuatro atributos opcionales: `type` y `url` *(4.0 +)*, y `branch` y `commit` *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="1e35b-221">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="1e35b-222">Estos atributos permiten asignar el `.nupkg` al repositorio que lo compiló, con la posibilidad de obtener el valor que se obtiene como el nombre de la rama individual o el hash de SHA-1 de confirmación que compiló el paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-222">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="1e35b-223">Debe ser una dirección URL disponible públicamente que un software de control de versiones pueda invocar directamente.</span><span class="sxs-lookup"><span data-stu-id="1e35b-223">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="1e35b-224">No debe ser una página HTML, ya que está destinada al equipo.</span><span class="sxs-lookup"><span data-stu-id="1e35b-224">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="1e35b-225">Para vincular a la página del proyecto, use el `projectUrl` campo en su lugar.</span><span class="sxs-lookup"><span data-stu-id="1e35b-225">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="1e35b-226">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e35b-226">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

<span data-ttu-id="1e35b-227">Al cargar un paquete en nuget.org, el `type` atributo está limitado a 100 caracteres y el `url` atributo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-227">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="1e35b-228">title</span><span class="sxs-lookup"><span data-stu-id="1e35b-228">title</span></span>
<span data-ttu-id="1e35b-229">Título descriptivo del paquete que se puede usar en algunas pantallas de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1e35b-229">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="1e35b-230">(nuget.org y el administrador de paquetes en Visual Studio no muestran el título)</span><span class="sxs-lookup"><span data-stu-id="1e35b-230">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="1e35b-231">Al cargar un paquete en nuget.org, el `title` campo está limitado a 256 caracteres, pero no se usa para ningún propósito de presentación.</span><span class="sxs-lookup"><span data-stu-id="1e35b-231">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="1e35b-232">Elementos de colección</span><span class="sxs-lookup"><span data-stu-id="1e35b-232">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="1e35b-233">packageTypes</span><span class="sxs-lookup"><span data-stu-id="1e35b-233">packageTypes</span></span>
<span data-ttu-id="1e35b-234">*(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional.</span><span class="sxs-lookup"><span data-stu-id="1e35b-234">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="1e35b-235">Cada tipo de paquete tiene atributos de *name* y *version*.</span><span class="sxs-lookup"><span data-stu-id="1e35b-235">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="1e35b-236">Vea [Establecimiento de un tipo de paquete](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="1e35b-236">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="1e35b-237">dependencies</span><span class="sxs-lookup"><span data-stu-id="1e35b-237">dependencies</span></span>
<span data-ttu-id="1e35b-238">Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-238">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="1e35b-239">Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="1e35b-239">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="1e35b-240">Vea [Dependencias](#dependencies-element) a continuación.</span><span class="sxs-lookup"><span data-stu-id="1e35b-240">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="1e35b-241">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="1e35b-241">frameworkAssemblies</span></span>
<span data-ttu-id="1e35b-242">*(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-242">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="1e35b-243">Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="1e35b-243">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="1e35b-244">Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación.</span><span class="sxs-lookup"><span data-stu-id="1e35b-244">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="1e35b-245">references</span><span class="sxs-lookup"><span data-stu-id="1e35b-245">references</span></span>
<span data-ttu-id="1e35b-246">*(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e35b-246">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="1e35b-247">Cada referencia tiene un atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="1e35b-247">Each reference has a *file* attribute.</span></span> <span data-ttu-id="1e35b-248">`<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-248">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="1e35b-249">Si se omite, se incluyen todas las referencias de `lib`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-249">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="1e35b-250">Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación.</span><span class="sxs-lookup"><span data-stu-id="1e35b-250">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="1e35b-251">contentFiles</span><span class="sxs-lookup"><span data-stu-id="1e35b-251">contentFiles</span></span>
<span data-ttu-id="1e35b-252">*(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="1e35b-252">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="1e35b-253">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e35b-253">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="1e35b-254">Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación.</span><span class="sxs-lookup"><span data-stu-id="1e35b-254">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="1e35b-255">archivos</span><span class="sxs-lookup"><span data-stu-id="1e35b-255">files</span></span> 
<span data-ttu-id="1e35b-256">El `<package>` nodo puede contener un `<files>` nodo como un elemento relacionado `<metadata>` y un `<contentFiles>` elemento secundario en `<metadata>` , para especificar qué archivos de ensamblado y de contenido se van a incluir en el paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-256">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="1e35b-257">Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.</span><span class="sxs-lookup"><span data-stu-id="1e35b-257">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="1e35b-258">atributos de metadatos</span><span class="sxs-lookup"><span data-stu-id="1e35b-258">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="1e35b-259">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="1e35b-259">minClientVersion</span></span>
<span data-ttu-id="1e35b-260">Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e35b-260">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="1e35b-261">Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e35b-261">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="1e35b-262">Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-262">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="1e35b-263">Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3".</span><span class="sxs-lookup"><span data-stu-id="1e35b-263">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="1e35b-264">Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-264">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="1e35b-265">Tokens de reemplazo</span><span class="sxs-lookup"><span data-stu-id="1e35b-265">Replacement tokens</span></span>

<span data-ttu-id="1e35b-266">Al crear un paquete, el [ `nuget pack` comando](../reference/cli-reference/cli-ref-pack.md) reemplaza los tokens delimitados por $ del `.nuspec` nodo del archivo `<metadata>` por valores que proceden de un archivo de proyecto o del `pack` `-properties` modificador del comando.</span><span class="sxs-lookup"><span data-stu-id="1e35b-266">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="1e35b-267">En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-267">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="1e35b-268">Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="1e35b-268">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="1e35b-269">Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="1e35b-269">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="1e35b-270">Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-270">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="1e35b-271">Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="1e35b-271">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="1e35b-272">Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares.</span><span class="sxs-lookup"><span data-stu-id="1e35b-272">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="1e35b-273">Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-273">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="1e35b-274">Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="1e35b-274">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="1e35b-275">Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="1e35b-275">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="1e35b-276">Token</span><span class="sxs-lookup"><span data-stu-id="1e35b-276">Token</span></span> | <span data-ttu-id="1e35b-277">Origen del valor</span><span class="sxs-lookup"><span data-stu-id="1e35b-277">Value source</span></span> | <span data-ttu-id="1e35b-278">Value</span><span class="sxs-lookup"><span data-stu-id="1e35b-278">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="1e35b-279">**$id $**</span><span class="sxs-lookup"><span data-stu-id="1e35b-279">**$id$**</span></span> | <span data-ttu-id="1e35b-280">Archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="1e35b-280">Project file</span></span> | <span data-ttu-id="1e35b-281">AssemblyName (title) del archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="1e35b-281">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="1e35b-282">**$version $**</span><span class="sxs-lookup"><span data-stu-id="1e35b-282">**$version$**</span></span> | <span data-ttu-id="1e35b-283">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1e35b-283">AssemblyInfo</span></span> | <span data-ttu-id="1e35b-284">AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="1e35b-284">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="1e35b-285">**$author $**</span><span class="sxs-lookup"><span data-stu-id="1e35b-285">**$author$**</span></span> | <span data-ttu-id="1e35b-286">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1e35b-286">AssemblyInfo</span></span> | <span data-ttu-id="1e35b-287">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="1e35b-287">AssemblyCompany</span></span> |
| <span data-ttu-id="1e35b-288">**$title $**</span><span class="sxs-lookup"><span data-stu-id="1e35b-288">**$title$**</span></span> | <span data-ttu-id="1e35b-289">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1e35b-289">AssemblyInfo</span></span> | <span data-ttu-id="1e35b-290">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="1e35b-290">AssemblyTitle</span></span> |
| <span data-ttu-id="1e35b-291">**$description $**</span><span class="sxs-lookup"><span data-stu-id="1e35b-291">**$description$**</span></span> | <span data-ttu-id="1e35b-292">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1e35b-292">AssemblyInfo</span></span> | <span data-ttu-id="1e35b-293">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="1e35b-293">AssemblyDescription</span></span> |
| <span data-ttu-id="1e35b-294">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="1e35b-294">**$copyright$**</span></span> | <span data-ttu-id="1e35b-295">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1e35b-295">AssemblyInfo</span></span> | <span data-ttu-id="1e35b-296">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="1e35b-296">AssemblyCopyright</span></span> |
| <span data-ttu-id="1e35b-297">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="1e35b-297">**$configuration$**</span></span> | <span data-ttu-id="1e35b-298">Archivo DLL del ensamblado</span><span class="sxs-lookup"><span data-stu-id="1e35b-298">Assembly DLL</span></span> | <span data-ttu-id="1e35b-299">Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar.</span><span class="sxs-lookup"><span data-stu-id="1e35b-299">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="1e35b-300">Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="1e35b-300">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="1e35b-301">Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="1e35b-301">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="1e35b-302">Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual.</span><span class="sxs-lookup"><span data-stu-id="1e35b-302">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="1e35b-303">Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="1e35b-303">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="1e35b-304">Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e35b-304">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="1e35b-305">Elemento Dependencies</span><span class="sxs-lookup"><span data-stu-id="1e35b-305">Dependencies element</span></span>

<span data-ttu-id="1e35b-306">El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="1e35b-306">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="1e35b-307">Los atributos de cada `<dependency>` son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e35b-307">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="1e35b-308">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e35b-308">Attribute</span></span> | <span data-ttu-id="1e35b-309">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e35b-309">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="1e35b-310">(Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-310">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="1e35b-311">(Obligatorio) Intervalo de versiones aceptable como dependencia.</span><span class="sxs-lookup"><span data-stu-id="1e35b-311">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="1e35b-312">Vea [Control de versiones de paquetes](../concepts/package-versioning.md#version-ranges) para consultar la sintaxis exacta.</span><span class="sxs-lookup"><span data-stu-id="1e35b-312">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="1e35b-313">No se admiten las versiones flotantes.</span><span class="sxs-lookup"><span data-stu-id="1e35b-313">Floating versions are not supported.</span></span> |
| <span data-ttu-id="1e35b-314">include</span><span class="sxs-lookup"><span data-stu-id="1e35b-314">include</span></span> | <span data-ttu-id="1e35b-315">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="1e35b-315">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="1e35b-316">El valor predeterminado es `all`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-316">The default value is `all`.</span></span> |
| <span data-ttu-id="1e35b-317">exclude</span><span class="sxs-lookup"><span data-stu-id="1e35b-317">exclude</span></span> | <span data-ttu-id="1e35b-318">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="1e35b-318">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="1e35b-319">El valor predeterminado es `build,analyzers` que se puede sobrescribir.</span><span class="sxs-lookup"><span data-stu-id="1e35b-319">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="1e35b-320">Pero `content/ ContentFiles` también se excluyen implícitamente en el paquete final que no se puede sobrescribir.</span><span class="sxs-lookup"><span data-stu-id="1e35b-320">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="1e35b-321">Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-321">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="1e35b-322">Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-322">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="1e35b-323">Al cargar un paquete en nuget.org, cada atributo de la dependencia `id` se limita a 128 caracteres y el `version` atributo está limitado a 256 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1e35b-323">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="1e35b-324">Etiqueta Include o Exclude</span><span class="sxs-lookup"><span data-stu-id="1e35b-324">Include/Exclude tag</span></span> | <span data-ttu-id="1e35b-325">Carpetas afectadas del destino</span><span class="sxs-lookup"><span data-stu-id="1e35b-325">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="1e35b-326">contentFiles</span><span class="sxs-lookup"><span data-stu-id="1e35b-326">contentFiles</span></span> | <span data-ttu-id="1e35b-327">Contenido</span><span class="sxs-lookup"><span data-stu-id="1e35b-327">Content</span></span> |
| <span data-ttu-id="1e35b-328">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="1e35b-328">runtime</span></span> | <span data-ttu-id="1e35b-329">Runtime, Resources y FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="1e35b-329">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="1e35b-330">compile</span><span class="sxs-lookup"><span data-stu-id="1e35b-330">compile</span></span> | <span data-ttu-id="1e35b-331">lib</span><span class="sxs-lookup"><span data-stu-id="1e35b-331">lib</span></span> |
| <span data-ttu-id="1e35b-332">build</span><span class="sxs-lookup"><span data-stu-id="1e35b-332">build</span></span> | <span data-ttu-id="1e35b-333">build (propiedades y destinos de MSBuild)</span><span class="sxs-lookup"><span data-stu-id="1e35b-333">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="1e35b-334">nativas</span><span class="sxs-lookup"><span data-stu-id="1e35b-334">native</span></span> | <span data-ttu-id="1e35b-335">nativas</span><span class="sxs-lookup"><span data-stu-id="1e35b-335">native</span></span> |
| <span data-ttu-id="1e35b-336">ninguno</span><span class="sxs-lookup"><span data-stu-id="1e35b-336">none</span></span> | <span data-ttu-id="1e35b-337">Sin carpetas</span><span class="sxs-lookup"><span data-stu-id="1e35b-337">No folders</span></span> |
| <span data-ttu-id="1e35b-338">todo</span><span class="sxs-lookup"><span data-stu-id="1e35b-338">all</span></span> | <span data-ttu-id="1e35b-339">Todas las carpetas</span><span class="sxs-lookup"><span data-stu-id="1e35b-339">All folders</span></span> |

<span data-ttu-id="1e35b-340">Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="1e35b-340">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="1e35b-341">Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-341">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="1e35b-342">Al crear un a `.nuspec` partir de un proyecto mediante `nuget spec` , las dependencias que existen en ese proyecto no se incluyen automáticamente en el `.nuspec` archivo resultante.</span><span class="sxs-lookup"><span data-stu-id="1e35b-342">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="1e35b-343">En su lugar, use `nuget pack myproject.csproj` y obtenga el archivo *. nuspec* desde el archivo *. nupkg* generado.</span><span class="sxs-lookup"><span data-stu-id="1e35b-343">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="1e35b-344">Este archivo *. nuspec* contiene las dependencias.</span><span class="sxs-lookup"><span data-stu-id="1e35b-344">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="1e35b-345">Grupos de dependencia</span><span class="sxs-lookup"><span data-stu-id="1e35b-345">Dependency groups</span></span>

<span data-ttu-id="1e35b-346">*Versión 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="1e35b-346">*Version 2.0+*</span></span>

<span data-ttu-id="1e35b-347">Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-347">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="1e35b-348">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-348">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="1e35b-349">Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e35b-349">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="1e35b-350">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias.</span><span class="sxs-lookup"><span data-stu-id="1e35b-350">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="1e35b-351">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="1e35b-351">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="1e35b-352">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="1e35b-352">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="1e35b-353">El formato del [moniker de la plataforma de destino (TFM)](../reference/target-frameworks.md) usado en la `lib/ref` carpeta es diferente cuando se compara con el TFM usado en `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="1e35b-353">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="1e35b-354">Si las plataformas de destino declaradas en `dependencies group` y la `lib/ref` carpeta del `.nuspec` archivo no tienen coincidencias exactas, el comando generará la advertencia de `pack` [NuGet NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="1e35b-354">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="1e35b-355">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="1e35b-355">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="1e35b-356">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="1e35b-356">Explicit assembly references</span></span>

<span data-ttu-id="1e35b-357">Los `<references>` proyectos utilizan el elemento `packages.config` para especificar explícitamente los ensamblados a los que debe hacer referencia el proyecto de destino al utilizar el paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-357">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="1e35b-358">Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="1e35b-358">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="1e35b-359">Para obtener más información, vea la página de [selección de ensamblados a los que se hace referencia en proyectos](../create-packages/select-assemblies-referenced-by-projects.md) .</span><span class="sxs-lookup"><span data-stu-id="1e35b-359">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="1e35b-360">Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:</span><span class="sxs-lookup"><span data-stu-id="1e35b-360">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="1e35b-361">Grupos de referencias</span><span class="sxs-lookup"><span data-stu-id="1e35b-361">Reference groups</span></span>

<span data-ttu-id="1e35b-362">Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-362">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="1e35b-363">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-363">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="1e35b-364">Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e35b-364">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="1e35b-365">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias.</span><span class="sxs-lookup"><span data-stu-id="1e35b-365">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="1e35b-366">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="1e35b-366">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="1e35b-367">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="1e35b-367">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="1e35b-368">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="1e35b-368">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="1e35b-369">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="1e35b-369">Framework assembly references</span></span>

<span data-ttu-id="1e35b-370">Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo.</span><span class="sxs-lookup"><span data-stu-id="1e35b-370">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="1e35b-371">Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias.</span><span class="sxs-lookup"><span data-stu-id="1e35b-371">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="1e35b-372">Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-372">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="1e35b-373">El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="1e35b-373">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="1e35b-374">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e35b-374">Attribute</span></span> | <span data-ttu-id="1e35b-375">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e35b-375">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e35b-376">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="1e35b-376">**assemblyName**</span></span> | <span data-ttu-id="1e35b-377">(Obligatorio) Nombre completo del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="1e35b-377">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="1e35b-378">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="1e35b-378">**targetFramework**</span></span> | <span data-ttu-id="1e35b-379">(Opcional) Especifica la plataforma de destino a la que se aplica esta referencia.</span><span class="sxs-lookup"><span data-stu-id="1e35b-379">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="1e35b-380">Si se omite, indica que la referencia se aplica a todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="1e35b-380">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="1e35b-381">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="1e35b-381">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="1e35b-382">En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="1e35b-382">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="1e35b-383">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="1e35b-383">Including assembly files</span></span>

<span data-ttu-id="1e35b-384">Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-384">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="1e35b-385">El comando `nuget pack` selecciona automáticamente los archivos necesarios.</span><span class="sxs-lookup"><span data-stu-id="1e35b-385">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="1e35b-386">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados.</span><span class="sxs-lookup"><span data-stu-id="1e35b-386">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="1e35b-387">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-387">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="1e35b-388">Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente.</span><span class="sxs-lookup"><span data-stu-id="1e35b-388">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="1e35b-389">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e35b-389">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="1e35b-390">Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="1e35b-390">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="1e35b-391">Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="1e35b-391">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="1e35b-392">Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="1e35b-392">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="1e35b-393">Atributos del elemento File</span><span class="sxs-lookup"><span data-stu-id="1e35b-393">File element attributes</span></span>

<span data-ttu-id="1e35b-394">Cada elemento `<file>` especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="1e35b-394">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="1e35b-395">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e35b-395">Attribute</span></span> | <span data-ttu-id="1e35b-396">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e35b-396">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e35b-397">**src**</span><span class="sxs-lookup"><span data-stu-id="1e35b-397">**src**</span></span> | <span data-ttu-id="1e35b-398">Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-398">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="1e35b-399">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="1e35b-399">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="1e35b-400">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="1e35b-400">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="1e35b-401">**Destino**</span><span class="sxs-lookup"><span data-stu-id="1e35b-401">**target**</span></span> | <span data-ttu-id="1e35b-402">La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-402">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="1e35b-403">Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones).</span><span class="sxs-lookup"><span data-stu-id="1e35b-403">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="1e35b-404">**evitar**</span><span class="sxs-lookup"><span data-stu-id="1e35b-404">**exclude**</span></span> | <span data-ttu-id="1e35b-405">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-405">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="1e35b-406">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="1e35b-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="1e35b-407">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="1e35b-407">Examples</span></span>

<span data-ttu-id="1e35b-408">**Ensamblado único**</span><span class="sxs-lookup"><span data-stu-id="1e35b-408">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="1e35b-409">**Ensamblado único específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="1e35b-409">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="1e35b-410">**Conjunto de archivos DLL que usan un carácter comodín**</span><span class="sxs-lookup"><span data-stu-id="1e35b-410">**Set of DLLs using a wildcard**</span></span>

```
Source files:
    bin\release\libraryA.dll
    bin\release\libraryB.dll

.nuspec entry:
    <file src="bin\release\*.dll" target="lib" />

Packaged result:
    lib\libraryA.dll
    lib\libraryB.dll
```

<span data-ttu-id="1e35b-411">**Archivos DLL para distintas plataformas**</span><span class="sxs-lookup"><span data-stu-id="1e35b-411">**DLLs for different frameworks**</span></span>

```
Source files:
    lib\net40\library.dll
    lib\net20\library.dll

.nuspec entry (using ** recursive search):
    <file src="lib\**" target="lib" />

Packaged result:
    lib\net40\library.dll
    lib\net20\library.dll
```

<span data-ttu-id="1e35b-412">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="1e35b-412">**Excluding files**</span></span>

```
Source files:
    \tools\fileA.bak
    \tools\fileB.bak
    \tools\fileA.log
    \tools\build\fileB.log

.nuspec entries:
    <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
    <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

Package result:
    (no files)
```

## <a name="including-content-files"></a><span data-ttu-id="1e35b-413">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="1e35b-413">Including content files</span></span>

<span data-ttu-id="1e35b-414">Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e35b-414">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="1e35b-415">Como son inmutables, no se prevé que el proyecto de consumo los modifique.</span><span class="sxs-lookup"><span data-stu-id="1e35b-415">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="1e35b-416">Entre los archivos de contenido se encuentran los siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e35b-416">Example content files include:</span></span>

- <span data-ttu-id="1e35b-417">Imágenes que se insertan como recursos</span><span class="sxs-lookup"><span data-stu-id="1e35b-417">Images that are embedded as resources</span></span>
- <span data-ttu-id="1e35b-418">Archivos de código fuente que ya están compilados</span><span class="sxs-lookup"><span data-stu-id="1e35b-418">Source files that are already compiled</span></span>
- <span data-ttu-id="1e35b-419">Scripts que se deben incluir con la salida de la compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="1e35b-419">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="1e35b-420">Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto</span><span class="sxs-lookup"><span data-stu-id="1e35b-420">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="1e35b-421">Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-421">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="1e35b-422">Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="1e35b-422">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="1e35b-423">Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.</span><span class="sxs-lookup"><span data-stu-id="1e35b-423">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="1e35b-424">Usar el elemento files para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="1e35b-424">Using the files element for content files</span></span>

<span data-ttu-id="1e35b-425">En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="1e35b-425">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="1e35b-426">**Archivos de contenido básicos**</span><span class="sxs-lookup"><span data-stu-id="1e35b-426">**Basic content files**</span></span>

```
Source files:
    css\mobile\style1.css
    css\mobile\style2.css

.nuspec entry:
    <file src="css\mobile\*.css" target="content\css\mobile" />

Packaged result:
    content\css\mobile\style1.css
    content\css\mobile\style2.css
```

<span data-ttu-id="1e35b-427">**Archivos de contenido con estructura de directorios**</span><span class="sxs-lookup"><span data-stu-id="1e35b-427">**Content files with directory structure**</span></span>

```
Source files:
    css\mobile\style.css
    css\mobile\wp7\style.css
    css\browser\style.css

.nuspec entry:
    <file src="css\**\*.css" target="content\css" />

Packaged result:
    content\css\mobile\style.css
    content\css\mobile\wp7\style.css
    content\css\browser\style.css
```

<span data-ttu-id="1e35b-428">**Archivo de contenido específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="1e35b-428">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="1e35b-429">**Archivo de contenido copiado en una carpeta con un punto en el nombre**</span><span class="sxs-lookup"><span data-stu-id="1e35b-429">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="1e35b-430">En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:</span><span class="sxs-lookup"><span data-stu-id="1e35b-430">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="1e35b-431">**Archivos de contenido sin extensión**</span><span class="sxs-lookup"><span data-stu-id="1e35b-431">**Content files without extensions**</span></span>

<span data-ttu-id="1e35b-432">Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="1e35b-432">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="1e35b-433">**Archivos de contenido con una ruta de acceso y un destino profundos**</span><span class="sxs-lookup"><span data-stu-id="1e35b-433">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="1e35b-434">En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:</span><span class="sxs-lookup"><span data-stu-id="1e35b-434">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry:
    <file src="css\cool\style.css" target="Content\css\cool" />
    or:
    <file src="css\cool\style.css" target="Content\css\cool\style.css" />

Packaged result:
    content\css\cool\style.css
```

<span data-ttu-id="1e35b-435">**Cambiar el nombre de un archivo de contenido del paquete**</span><span class="sxs-lookup"><span data-stu-id="1e35b-435">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="1e35b-436">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="1e35b-436">**Excluding files**</span></span>

```
Source file:
    docs\*.txt (multiple files)

.nuspec entry:
    <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
    or
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

Packaged result:
    All .txt files from docs except admin.txt (first example)
    All .txt files from docs except admin.txt and log.txt (second example)
```

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="1e35b-437">Usar el elemento contentFiles para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="1e35b-437">Using the contentFiles element for content files</span></span>

<span data-ttu-id="1e35b-438">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="1e35b-438">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="1e35b-439">De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados.</span><span class="sxs-lookup"><span data-stu-id="1e35b-439">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="1e35b-440">En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-440">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="1e35b-441">Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.</span><span class="sxs-lookup"><span data-stu-id="1e35b-441">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="1e35b-442">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:</span><span class="sxs-lookup"><span data-stu-id="1e35b-442">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="1e35b-443">Atributo</span><span class="sxs-lookup"><span data-stu-id="1e35b-443">Attribute</span></span> | <span data-ttu-id="1e35b-444">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e35b-444">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e35b-445">**inclui**</span><span class="sxs-lookup"><span data-stu-id="1e35b-445">**include**</span></span> | <span data-ttu-id="1e35b-446">(Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-446">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="1e35b-447">La ruta de acceso es relativa a la `contentFiles` carpeta a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="1e35b-447">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="1e35b-448">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="1e35b-448">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="1e35b-449">**evitar**</span><span class="sxs-lookup"><span data-stu-id="1e35b-449">**exclude**</span></span> | <span data-ttu-id="1e35b-450">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="1e35b-450">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="1e35b-451">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="1e35b-451">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="1e35b-452">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="1e35b-452">**buildAction**</span></span> | <span data-ttu-id="1e35b-453">Acción de compilación que se va a asignar al elemento de contenido de MSBuild, como,,, `Content` `None` `Embedded Resource` `Compile` , etc. El valor predeterminado es `Compile` .</span><span class="sxs-lookup"><span data-stu-id="1e35b-453">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="1e35b-454">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="1e35b-454">**copyToOutput**</span></span> | <span data-ttu-id="1e35b-455">Un valor booleano que indica si se deben copiar los elementos de contenido en la carpeta de salida de compilación (o publicación).</span><span class="sxs-lookup"><span data-stu-id="1e35b-455">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="1e35b-456">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="1e35b-456">The default is false.</span></span> |
| <span data-ttu-id="1e35b-457">**flatten**</span><span class="sxs-lookup"><span data-stu-id="1e35b-457">**flatten**</span></span> | <span data-ttu-id="1e35b-458">Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false).</span><span class="sxs-lookup"><span data-stu-id="1e35b-458">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="1e35b-459">Esta marca solo funciona cuando la marca copyToOutput está establecida en true.</span><span class="sxs-lookup"><span data-stu-id="1e35b-459">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="1e35b-460">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="1e35b-460">The default is false.</span></span> |

<span data-ttu-id="1e35b-461">Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo.</span><span class="sxs-lookup"><span data-stu-id="1e35b-461">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="1e35b-462">Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas.</span><span class="sxs-lookup"><span data-stu-id="1e35b-462">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="1e35b-463">La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.</span><span class="sxs-lookup"><span data-stu-id="1e35b-463">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="1e35b-464">Estructura de carpetas de los paquetes</span><span class="sxs-lookup"><span data-stu-id="1e35b-464">Package folder structure</span></span>

<span data-ttu-id="1e35b-465">El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="1e35b-465">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="1e35b-466">`codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.</span><span class="sxs-lookup"><span data-stu-id="1e35b-466">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="1e35b-467">`TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="1e35b-467">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="1e35b-468">Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.</span><span class="sxs-lookup"><span data-stu-id="1e35b-468">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="1e35b-469">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e35b-469">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="1e35b-470">Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e35b-470">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="1e35b-471">Sección contentFiles de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1e35b-471">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a><span data-ttu-id="1e35b-472">Grupos de referencia de marco</span><span class="sxs-lookup"><span data-stu-id="1e35b-472">Framework reference groups</span></span>

<span data-ttu-id="1e35b-473">*Versión 5.1 + valor PackageReference*</span><span class="sxs-lookup"><span data-stu-id="1e35b-473">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="1e35b-474">Las referencias de marco de trabajo son un concepto de .NET Core que representa Marcos compartidos como WPF o Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="1e35b-474">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="1e35b-475">Al especificar un marco de trabajo compartido, el paquete garantiza que todas sus dependencias de marco se incluyen en el proyecto de referencia.</span><span class="sxs-lookup"><span data-stu-id="1e35b-475">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="1e35b-476">Cada `<group>` elemento requiere un `targetFramework` atributo y cero o más `<frameworkReference>` elementos.</span><span class="sxs-lookup"><span data-stu-id="1e35b-476">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="1e35b-477">En el ejemplo siguiente se muestra un nuspec generado para un proyecto de WPF de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="1e35b-477">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="1e35b-478">Tenga en cuenta que no se recomienda la creación manual de nuspecs que contengan referencias de marco.</span><span class="sxs-lookup"><span data-stu-id="1e35b-478">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="1e35b-479">Considere la posibilidad de usar el paquete de [destinos](msbuild-targets.md) en su lugar, que los deducirá automáticamente del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e35b-479">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="1e35b-480">Archivos nuspec de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1e35b-480">Example nuspec files</span></span>

<span data-ttu-id="1e35b-481">**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**</span><span class="sxs-lookup"><span data-stu-id="1e35b-481">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="1e35b-482">**Un archivo `.nuspec` con dependencias**</span><span class="sxs-lookup"><span data-stu-id="1e35b-482">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="1e35b-483">**Un archivo `.nuspec` con archivos**</span><span class="sxs-lookup"><span data-stu-id="1e35b-483">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="1e35b-484">**Un archivo `.nuspec` con ensamblados de plataforma**</span><span class="sxs-lookup"><span data-stu-id="1e35b-484">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="1e35b-485">En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:</span><span class="sxs-lookup"><span data-stu-id="1e35b-485">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="1e35b-486">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="1e35b-486">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="1e35b-487">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="1e35b-487">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="1e35b-488">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="1e35b-488">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="1e35b-489">Windows Phone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="1e35b-489">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
