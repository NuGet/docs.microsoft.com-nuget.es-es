---
title: Referencia de archivo .nuspec para NuGet
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ed865aad6f72752adcf3e3921287a20b961c4a8a
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901816"
---
# <a name="nuspec-reference"></a><span data-ttu-id="9f8d9-103">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="9f8d9-103">.nuspec reference</span></span>

<span data-ttu-id="9f8d9-104">Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="9f8d9-105">Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="9f8d9-106">El manifiesto siempre se incluye en un paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="9f8d9-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-107">In this topic:</span></span>

- [<span data-ttu-id="9f8d9-108">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="9f8d9-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="9f8d9-109">[Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9f8d9-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="9f8d9-110">Dependencias</span><span class="sxs-lookup"><span data-stu-id="9f8d9-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="9f8d9-111">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="9f8d9-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="9f8d9-112">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="9f8d9-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="9f8d9-113">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="9f8d9-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="9f8d9-114">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="9f8d9-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="9f8d9-115">Archivos nuspec de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="9f8d9-116">Compatibilidad de tipos de proyecto</span><span class="sxs-lookup"><span data-stu-id="9f8d9-116">Project type compatibility</span></span>

- <span data-ttu-id="9f8d9-117">Use con para proyectos que no son `.nuspec` de estilo SDK que usan `nuget.exe pack` `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="9f8d9-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="9f8d9-118">No se necesita un archivo para crear paquetes para proyectos de estilo `.nuspec` [SDK](../resources/check-project-format.md) (normalmente. NET Core y .NET Standard que usan el [atributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="9f8d9-119">(Tenga en cuenta `.nuspec` que se genera un al crear el paquete).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="9f8d9-120">Si va a crear un paquete mediante o , se recomienda incluir en su lugar todas las propiedades que normalmente están en el archivo `dotnet.exe pack` `msbuild pack target` del [](../reference/msbuild-targets.md#pack-target) `.nuspec` proyecto.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="9f8d9-121">Sin embargo, puede elegir usar un [archivo `.nuspec` para empaquetar mediante `dotnet.exe` o `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span></span>

- <span data-ttu-id="9f8d9-122">En el caso de los proyectos `packages.config` migrados de a [PackageReference,](../consume-packages/package-references-in-project-files.md)no se requiere `.nuspec` un archivo para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="9f8d9-123">En su lugar, [use msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="9f8d9-124">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="9f8d9-124">General form and schema</span></span>

<span data-ttu-id="9f8d9-125">El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="9f8d9-126">En este esquema, los archivos `.nuspec` tienen el siguiente formato general:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="9f8d9-127">Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="9f8d9-128">Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="9f8d9-129">En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):</span><span class="sxs-lookup"><span data-stu-id="9f8d9-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

<span data-ttu-id="9f8d9-131">Todos los nombres de elementos XML del archivo .nuspec distinguen mayúsculas de minúsculas, como es el caso de XML en general.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="9f8d9-132">Por ejemplo, el uso del elemento de `<description>` metadatos es correcto `<Description>` y no es correcto.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="9f8d9-133">A continuación se documenta el uso adecuado de mayúsculas y minúsculas para cada nombre de elemento.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="9f8d9-134">Elementos de metadatos necesarios</span><span class="sxs-lookup"><span data-stu-id="9f8d9-134">Required metadata elements</span></span>

<span data-ttu-id="9f8d9-135">Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="9f8d9-136">Estos elementos deben aparecer dentro de un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="9f8d9-137">id</span><span class="sxs-lookup"><span data-stu-id="9f8d9-137">id</span></span> 
<span data-ttu-id="9f8d9-138">El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="9f8d9-139">Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="9f8d9-140">Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="9f8d9-141">Al cargar un paquete en nuget.org, `id` el campo está limitado a 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="9f8d9-142">version</span><span class="sxs-lookup"><span data-stu-id="9f8d9-142">version</span></span>
<span data-ttu-id="9f8d9-143">La versión del paquete, siguiendo el patrón *mayor.menor.revisión*.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="9f8d9-144">Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="9f8d9-145">Al cargar un paquete en nuget.org, `version` el campo se limita a 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="9f8d9-146">description</span><span class="sxs-lookup"><span data-stu-id="9f8d9-146">description</span></span>
<span data-ttu-id="9f8d9-147">Descripción del paquete para la presentación de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-147">A description of the package for UI display.</span></span>

<span data-ttu-id="9f8d9-148">Al cargar un paquete en nuget.org, `description` el campo se limita a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="9f8d9-149">authors</span><span class="sxs-lookup"><span data-stu-id="9f8d9-149">authors</span></span>
<span data-ttu-id="9f8d9-150">Lista separada por comas de los autores de paquetes que coinciden con los nombres de perfil de nuget.org. Estos se muestran en la Galería de NuGet en nuget.org y se usan para hacer referencia cruzada a los paquetes de los mismos autores.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="9f8d9-151">Al cargar un paquete en nuget.org, `authors` el campo se limita a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="9f8d9-152">Elementos de metadatos opcionales</span><span class="sxs-lookup"><span data-stu-id="9f8d9-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="9f8d9-153">owners</span><span class="sxs-lookup"><span data-stu-id="9f8d9-153">owners</span></span>
> [!Important]
> <span data-ttu-id="9f8d9-154">los propietarios están en desuso.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-154">owners is deprecated.</span></span> <span data-ttu-id="9f8d9-155">En su lugar, use autores.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-155">Use authors instead.</span></span>

<span data-ttu-id="9f8d9-156">Lista separada por comas de los creadores de paquetes que usan nombres de perfil en nuget.org. Suele ser la misma lista que en y se omite al `authors` cargar el paquete en nuget.org. Consulte [Administración de propietarios de paquetes nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="9f8d9-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="9f8d9-157">projectUrl</span></span>
<span data-ttu-id="9f8d9-158">Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="9f8d9-159">Al cargar un paquete en nuget.org, `projectUrl` el campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="9f8d9-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="9f8d9-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="9f8d9-161">licenseUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="9f8d9-162">Use la licencia en su lugar.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-162">Use license instead.</span></span>

<span data-ttu-id="9f8d9-163">Una dirección URL para la licencia del paquete, que a menudo se muestra en uri como nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="9f8d9-164">Al cargar un paquete en nuget.org, `licenseUrl` el campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="9f8d9-165">license</span><span class="sxs-lookup"><span data-stu-id="9f8d9-165">license</span></span>

<span data-ttu-id="9f8d9-166">*Compatible con **NuGet 4.9.0** y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="9f8d9-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="9f8d9-167">Una expresión de licencia de SPDX o una ruta de acceso a un archivo de licencia dentro del paquete, que a menudo se muestra en uri como nuget.org. Si va a otorgar licencias al paquete con una licencia común, como MIT o BSD-2-Clause, use el identificador de [licencia SPDX asociado.](https://spdx.org/licenses/)</span><span class="sxs-lookup"><span data-stu-id="9f8d9-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="9f8d9-168">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="9f8d9-169">NuGet.org solo acepta expresiones de licencia aprobadas por la iniciativa de código abierto o Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="9f8d9-170">Si el paquete tiene licencia con varias licencias comunes, puede especificar una licencia compuesta mediante la sintaxis [de expresiones SPDX versión 2.0.](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)</span><span class="sxs-lookup"><span data-stu-id="9f8d9-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="9f8d9-171">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="9f8d9-172">Si usa una licencia personalizada que no es compatible con las expresiones de licencia, puede empaquetar un archivo o con el texto `.txt` `.md` de la licencia.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="9f8d9-173">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-173">For example:</span></span>

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

<span data-ttu-id="9f8d9-174">Para el equivalente de MSBuild, vea [Empaquetado de una expresión de licencia o un archivo de licencia.](msbuild-targets.md#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="9f8d9-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="9f8d9-175">La sintaxis exacta de las expresiones de licencia de NuGet se describe a continuación en [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

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

#### <a name="iconurl"></a><span data-ttu-id="9f8d9-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="9f8d9-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="9f8d9-177">iconUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-177">iconUrl is deprecated.</span></span> <span data-ttu-id="9f8d9-178">Use el icono en su lugar.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-178">Use icon instead.</span></span>

<span data-ttu-id="9f8d9-179">Una dirección URL para una imagen de 128 x 128 con fondo de transparencia que se usará como icono para el paquete en la presentación de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="9f8d9-180">Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="9f8d9-181">Por ejemplo, para usar una imagen de GitHub, use la dirección URL del archivo sin formato como <em> https://github.com/ \<username\> / \<repository\> /raw/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="9f8d9-182">Al cargar un paquete en nuget.org, `iconUrl` el campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="9f8d9-183">icon</span><span class="sxs-lookup"><span data-stu-id="9f8d9-183">icon</span></span>

<span data-ttu-id="9f8d9-184">*Compatible con **NuGet 5.3.0** y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="9f8d9-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="9f8d9-185">Es una ruta de acceso a un archivo de imagen dentro del paquete, que a menudo se muestra en uri como nuget.org como icono de paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="9f8d9-186">El tamaño del archivo de imagen está limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="9f8d9-187">Entre los formatos de archivo admitidos se incluyen JPEG y PNG.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="9f8d9-188">Se recomienda una resolución de imagen de 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="9f8d9-189">Por ejemplo, agregaría lo siguiente a nuspec al crear un paquete mediante nuget.exe:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="9f8d9-190">Icono de paquete de ejemplo nuspec.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

<span data-ttu-id="9f8d9-191">Para el equivalente de MSBuild, vea [Empaquetado de un archivo de imagen de icono.](msbuild-targets.md#packing-an-icon-image-file)</span><span class="sxs-lookup"><span data-stu-id="9f8d9-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="9f8d9-192">Puede especificar y para mantener `icon` la compatibilidad con versiones anteriores con orígenes que no `iconUrl` admiten `icon` .</span><span class="sxs-lookup"><span data-stu-id="9f8d9-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="9f8d9-193">Visual Studio admitirá `icon` paquetes procedentes de un origen basado en carpetas en una versión futura.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="readme"></a><span data-ttu-id="9f8d9-194">Archivo Léame</span><span class="sxs-lookup"><span data-stu-id="9f8d9-194">readme</span></span>

<span data-ttu-id="9f8d9-195">*Compatible con **NuGet 5.10.0 preview 2** y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="9f8d9-195">*Supported with **NuGet 5.10.0 preview 2** and above*</span></span>

<span data-ttu-id="9f8d9-196">Al empaquetar un archivo Léame, debe usar el elemento para especificar la ruta de acceso del paquete, en relación con la `readme` raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-196">When packing a readme file, you need to use the `readme` element to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="9f8d9-197">Además de esto, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-197">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="9f8d9-198">Los formatos de archivo admitidos incluyen solo Markdown (*.md*).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-198">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="9f8d9-199">Por ejemplo, agregaría lo siguiente a nuspec para empaquetar un archivo Léame con el proyecto:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-199">For example, you would add the following to your nuspec in order to pack a readme file with your project:</span></span>

```xml
<package>
  <metadata>
    ...
    <readme>docs\readme.md</readme>
    ...
  </metadata>
  <files>
    ...
    <file src="..\readme.md" target="docs\" />
    ...
  </files>
</package>
```

<span data-ttu-id="9f8d9-200">Para el equivalente de MSBuild, consulte [Empaquetado de un archivo Léame](msbuild-targets.md#packagereadmefile).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-200">For the MSBuild equivalent, take a look at [Packing a readme file](msbuild-targets.md#packagereadmefile).</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="9f8d9-201">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="9f8d9-201">requireLicenseAcceptance</span></span>
<span data-ttu-id="9f8d9-202">Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-202">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="9f8d9-203">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="9f8d9-203">developmentDependency</span></span>
<span data-ttu-id="9f8d9-204">*(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-204">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="9f8d9-205">Con PackageReference (NuGet 4.8 +) , esta marca también significa que excluirá los recursos en tiempo de compilación de la compilación.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-205">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="9f8d9-206">Consulte [DevelopmentDependency support for PackageReference (Compatibilidad de DevelopmentDependency con PackageReference).](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="9f8d9-206">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="9f8d9-207">Resumen</span><span class="sxs-lookup"><span data-stu-id="9f8d9-207">summary</span></span>
> [!Important]
> <span data-ttu-id="9f8d9-208">`summary` está en desuso.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-208">`summary` is being deprecated.</span></span> <span data-ttu-id="9f8d9-209">En su lugar, use `description`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-209">Use `description` instead.</span></span>

<span data-ttu-id="9f8d9-210">Descripción breve del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-210">A short description of the package for UI display.</span></span> <span data-ttu-id="9f8d9-211">Si se omite, se usará una versión truncada de `description`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-211">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="9f8d9-212">Al cargar un paquete en nuget.org, `summary` el campo se limita a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-212">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="9f8d9-213">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="9f8d9-213">releaseNotes</span></span>
<span data-ttu-id="9f8d9-214">*(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-214">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="9f8d9-215">Al cargar un paquete en nuget.org, el campo está limitado `releaseNotes` a 35 000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-215">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="9f8d9-216">copyright</span><span class="sxs-lookup"><span data-stu-id="9f8d9-216">copyright</span></span>
<span data-ttu-id="9f8d9-217">*(1.5+)* Información de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-217">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="9f8d9-218">Al cargar un paquete en nuget.org, `copyright` el campo se limita a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-218">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="9f8d9-219">language</span><span class="sxs-lookup"><span data-stu-id="9f8d9-219">language</span></span>
<span data-ttu-id="9f8d9-220">Identificador de configuración regional del paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-220">The locale ID for the package.</span></span> <span data-ttu-id="9f8d9-221">Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-221">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="9f8d9-222">etiquetas</span><span class="sxs-lookup"><span data-stu-id="9f8d9-222">tags</span></span>
<span data-ttu-id="9f8d9-223">Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-223">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="9f8d9-224">Al cargar un paquete en nuget.org, `tags` el campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-224">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="9f8d9-225">serviceable</span><span class="sxs-lookup"><span data-stu-id="9f8d9-225">serviceable</span></span> 
<span data-ttu-id="9f8d9-226">*(3.3+)* Solo para uso interno de NuGet.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-226">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="9f8d9-227">repository</span><span class="sxs-lookup"><span data-stu-id="9f8d9-227">repository</span></span>
<span data-ttu-id="9f8d9-228">Metadatos del repositorio, que consta de cuatro atributos opcionales: `type` y `url` *(4.0+)* y `branch` y `commit` *(4.6+).*</span><span class="sxs-lookup"><span data-stu-id="9f8d9-228">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="9f8d9-229">Estos atributos permiten asignar el al repositorio que lo creó, con el potencial de obtener tan detallado como el nombre de rama `.nupkg` individual y/o confirmar el hash SHA-1 que comcreó el paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-229">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="9f8d9-230">Debe ser una dirección URL disponible públicamente que un software de control de versiones pueda invocar directamente.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-230">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="9f8d9-231">No debe ser una página HTML, ya que está pensada para el equipo.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-231">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="9f8d9-232">Para vincular a la página del proyecto, use `projectUrl` el campo en su lugar.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-232">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="9f8d9-233">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-233">For example:</span></span>
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

<span data-ttu-id="9f8d9-234">Al cargar un paquete en nuget.org, el atributo está limitado a 100 caracteres y el atributo está limitado a `type` `url` 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-234">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="9f8d9-235">title</span><span class="sxs-lookup"><span data-stu-id="9f8d9-235">title</span></span>
<span data-ttu-id="9f8d9-236">Un título descriptivo del paquete que se puede usar en algunas pantallas de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-236">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="9f8d9-237">(nuget.org y el Administrador de paquetes en Visual Studio no muestran el título)</span><span class="sxs-lookup"><span data-stu-id="9f8d9-237">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="9f8d9-238">Al cargar un paquete en nuget.org, el campo está limitado a 256 caracteres, pero no se usa `title` con fines de presentación.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-238">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="9f8d9-239">Elementos de colección</span><span class="sxs-lookup"><span data-stu-id="9f8d9-239">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="9f8d9-240">packageTypes</span><span class="sxs-lookup"><span data-stu-id="9f8d9-240">packageTypes</span></span>
<span data-ttu-id="9f8d9-241">*(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-241">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="9f8d9-242">Cada tipo de paquete tiene atributos de *name* y *version*.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-242">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="9f8d9-243">Vea [Establecimiento de un tipo de paquete](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-243">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="9f8d9-244">dependencies</span><span class="sxs-lookup"><span data-stu-id="9f8d9-244">dependencies</span></span>
<span data-ttu-id="9f8d9-245">Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-245">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="9f8d9-246">Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-246">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="9f8d9-247">Vea [Dependencias](#dependencies-element) a continuación.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-247">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="9f8d9-248">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="9f8d9-248">frameworkAssemblies</span></span>
<span data-ttu-id="9f8d9-249">*(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-249">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="9f8d9-250">Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-250">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="9f8d9-251">Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-251">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="9f8d9-252">references</span><span class="sxs-lookup"><span data-stu-id="9f8d9-252">references</span></span>
<span data-ttu-id="9f8d9-253">*(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-253">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="9f8d9-254">Cada referencia tiene un atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-254">Each reference has a *file* attribute.</span></span> <span data-ttu-id="9f8d9-255">`<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-255">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="9f8d9-256">Si se omite, se incluyen todas las referencias de `lib`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-256">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="9f8d9-257">Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-257">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="9f8d9-258">contentFiles</span><span class="sxs-lookup"><span data-stu-id="9f8d9-258">contentFiles</span></span>
<span data-ttu-id="9f8d9-259">*(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-259">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="9f8d9-260">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-260">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="9f8d9-261">Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-261">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="9f8d9-262">files</span><span class="sxs-lookup"><span data-stu-id="9f8d9-262">files</span></span> 
<span data-ttu-id="9f8d9-263">El nodo puede contener un nodo como un nodo relacionado con y un elemento secundario en , para especificar qué ensamblado y archivos de contenido se `<package>` `<files>` `<metadata>` `<contentFiles>` `<metadata>` incluirán en el paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-263">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="9f8d9-264">Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-264">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="9f8d9-265">atributos de metadatos</span><span class="sxs-lookup"><span data-stu-id="9f8d9-265">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="9f8d9-266">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="9f8d9-266">minClientVersion</span></span>
<span data-ttu-id="9f8d9-267">Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-267">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="9f8d9-268">Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-268">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="9f8d9-269">Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-269">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="9f8d9-270">Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3".</span><span class="sxs-lookup"><span data-stu-id="9f8d9-270">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="9f8d9-271">Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-271">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

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

## <a name="replacement-tokens"></a><span data-ttu-id="9f8d9-272">Tokens de reemplazo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-272">Replacement tokens</span></span>

<span data-ttu-id="9f8d9-273">Al crear un [ `nuget pack` ](../reference/cli-reference/cli-ref-pack.md) paquete, el comando reemplaza los tokens delimitados por $en el nodo del archivo por valores que proceden de un archivo de proyecto o del `.nuspec` modificador del `<metadata>` `pack` `-properties` comando.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-273">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="9f8d9-274">En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-274">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="9f8d9-275">Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-275">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="9f8d9-276">Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-276">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="9f8d9-277">Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-277">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="9f8d9-278">Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-278">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="9f8d9-279">Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-279">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="9f8d9-280">Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-280">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="9f8d9-281">Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-281">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="9f8d9-282">Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-282">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="9f8d9-283">Token</span><span class="sxs-lookup"><span data-stu-id="9f8d9-283">Token</span></span> | <span data-ttu-id="9f8d9-284">Origen del valor</span><span class="sxs-lookup"><span data-stu-id="9f8d9-284">Value source</span></span> | <span data-ttu-id="9f8d9-285">Value</span><span class="sxs-lookup"><span data-stu-id="9f8d9-285">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="9f8d9-286">**$id$**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-286">**$id$**</span></span> | <span data-ttu-id="9f8d9-287">Archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="9f8d9-287">Project file</span></span> | <span data-ttu-id="9f8d9-288">AssemblyName (título) del archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="9f8d9-288">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="9f8d9-289">**$version$**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-289">**$version$**</span></span> | <span data-ttu-id="9f8d9-290">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-290">AssemblyInfo</span></span> | <span data-ttu-id="9f8d9-291">AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="9f8d9-291">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="9f8d9-292">**$author$**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-292">**$author$**</span></span> | <span data-ttu-id="9f8d9-293">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-293">AssemblyInfo</span></span> | <span data-ttu-id="9f8d9-294">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="9f8d9-294">AssemblyCompany</span></span> |
| <span data-ttu-id="9f8d9-295">**$title$**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-295">**$title$**</span></span> | <span data-ttu-id="9f8d9-296">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-296">AssemblyInfo</span></span> | <span data-ttu-id="9f8d9-297">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="9f8d9-297">AssemblyTitle</span></span> |
| <span data-ttu-id="9f8d9-298">**$description$**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-298">**$description$**</span></span> | <span data-ttu-id="9f8d9-299">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-299">AssemblyInfo</span></span> | <span data-ttu-id="9f8d9-300">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="9f8d9-300">AssemblyDescription</span></span> |
| <span data-ttu-id="9f8d9-301">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-301">**$copyright$**</span></span> | <span data-ttu-id="9f8d9-302">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-302">AssemblyInfo</span></span> | <span data-ttu-id="9f8d9-303">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="9f8d9-303">AssemblyCopyright</span></span> |
| <span data-ttu-id="9f8d9-304">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-304">**$configuration$**</span></span> | <span data-ttu-id="9f8d9-305">Archivo DLL del ensamblado</span><span class="sxs-lookup"><span data-stu-id="9f8d9-305">Assembly DLL</span></span> | <span data-ttu-id="9f8d9-306">Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-306">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="9f8d9-307">Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-307">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="9f8d9-308">Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-308">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="9f8d9-309">Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-309">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="9f8d9-310">Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-310">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="9f8d9-311">Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-311">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="9f8d9-312">Elemento Dependencies</span><span class="sxs-lookup"><span data-stu-id="9f8d9-312">Dependencies element</span></span>

<span data-ttu-id="9f8d9-313">El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-313">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="9f8d9-314">Los atributos de cada `<dependency>` son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-314">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="9f8d9-315">Atributo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-315">Attribute</span></span> | <span data-ttu-id="9f8d9-316">Descripción</span><span class="sxs-lookup"><span data-stu-id="9f8d9-316">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="9f8d9-317">(Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-317">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="9f8d9-318">(Obligatorio) Intervalo de versiones aceptable como dependencia.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-318">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="9f8d9-319">Vea [Control de versiones de paquetes](../concepts/package-versioning.md#version-ranges) para consultar la sintaxis exacta.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-319">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="9f8d9-320">No se admiten versiones flotantes.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-320">Floating versions are not supported.</span></span> |
| <span data-ttu-id="9f8d9-321">include</span><span class="sxs-lookup"><span data-stu-id="9f8d9-321">include</span></span> | <span data-ttu-id="9f8d9-322">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-322">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="9f8d9-323">El valor predeterminado es `all`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-323">The default value is `all`.</span></span> |
| <span data-ttu-id="9f8d9-324">exclude</span><span class="sxs-lookup"><span data-stu-id="9f8d9-324">exclude</span></span> | <span data-ttu-id="9f8d9-325">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-325">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="9f8d9-326">El valor predeterminado es `build,analyzers` que se puede escribir en exceso.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-326">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="9f8d9-327">Pero `content/ ContentFiles` también se excluyen implícitamente en el paquete final que no se puede escribir en exceso.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-327">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="9f8d9-328">Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-328">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="9f8d9-329">Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-329">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="9f8d9-330">Al cargar un paquete en nuget.org, el atributo de cada dependencia se limita a 128 caracteres y el atributo se limita a `id` `version` 256 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-330">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="9f8d9-331">Etiqueta Include o Exclude</span><span class="sxs-lookup"><span data-stu-id="9f8d9-331">Include/Exclude tag</span></span> | <span data-ttu-id="9f8d9-332">Carpetas afectadas del destino</span><span class="sxs-lookup"><span data-stu-id="9f8d9-332">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="9f8d9-333">contentFiles</span><span class="sxs-lookup"><span data-stu-id="9f8d9-333">contentFiles</span></span> | <span data-ttu-id="9f8d9-334">Contenido</span><span class="sxs-lookup"><span data-stu-id="9f8d9-334">Content</span></span> |
| <span data-ttu-id="9f8d9-335">en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="9f8d9-335">runtime</span></span> | <span data-ttu-id="9f8d9-336">Runtime, Resources y FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="9f8d9-336">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="9f8d9-337">compile</span><span class="sxs-lookup"><span data-stu-id="9f8d9-337">compile</span></span> | <span data-ttu-id="9f8d9-338">lib</span><span class="sxs-lookup"><span data-stu-id="9f8d9-338">lib</span></span> |
| <span data-ttu-id="9f8d9-339">build</span><span class="sxs-lookup"><span data-stu-id="9f8d9-339">build</span></span> | <span data-ttu-id="9f8d9-340">build (propiedades y destinos de MSBuild)</span><span class="sxs-lookup"><span data-stu-id="9f8d9-340">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="9f8d9-341">nativas</span><span class="sxs-lookup"><span data-stu-id="9f8d9-341">native</span></span> | <span data-ttu-id="9f8d9-342">nativas</span><span class="sxs-lookup"><span data-stu-id="9f8d9-342">native</span></span> |
| <span data-ttu-id="9f8d9-343">ninguno</span><span class="sxs-lookup"><span data-stu-id="9f8d9-343">none</span></span> | <span data-ttu-id="9f8d9-344">Sin carpetas</span><span class="sxs-lookup"><span data-stu-id="9f8d9-344">No folders</span></span> |
| <span data-ttu-id="9f8d9-345">all</span><span class="sxs-lookup"><span data-stu-id="9f8d9-345">all</span></span> | <span data-ttu-id="9f8d9-346">Todas las carpetas</span><span class="sxs-lookup"><span data-stu-id="9f8d9-346">All folders</span></span> |

<span data-ttu-id="9f8d9-347">Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-347">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="9f8d9-348">Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-348">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="9f8d9-349">Al crear un desde un proyecto mediante , las dependencias que existen en ese proyecto no se incluyen `.nuspec` automáticamente en el archivo `nuget spec` `.nuspec` resultante.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-349">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="9f8d9-350">En su lugar, `nuget pack myproject.csproj` use y obtenga el archivo *.nuspec* desde el archivo *.nupkg* generado.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-350">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="9f8d9-351">Este *archivo .nuspec* contiene las dependencias.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-351">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="9f8d9-352">Grupos de dependencia</span><span class="sxs-lookup"><span data-stu-id="9f8d9-352">Dependency groups</span></span>

<span data-ttu-id="9f8d9-353">*Versión 2.0+*</span><span class="sxs-lookup"><span data-stu-id="9f8d9-353">*Version 2.0+*</span></span>

<span data-ttu-id="9f8d9-354">Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-354">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="9f8d9-355">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-355">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="9f8d9-356">Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-356">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="9f8d9-357">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-357">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="9f8d9-358">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-358">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="9f8d9-359">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-359">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="9f8d9-360">El formato del [Moniker de la plataforma de destino (TFM)](../reference/target-frameworks.md) usado en la carpeta es diferente en comparación con `lib/ref` el TFM usado en `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="9f8d9-360">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="9f8d9-361">Si las plataformas de destino declaradas en y la carpeta del archivo no tienen coincidencias exactas, el comando genera la advertencia `dependencies group` `lib/ref` de `.nuspec` `pack` [NuGet NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-361">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="9f8d9-362">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-362">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="9f8d9-363">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="9f8d9-363">Explicit assembly references</span></span>

<span data-ttu-id="9f8d9-364">Los proyectos usan el elemento para especificar explícitamente los ensamblados a los que el proyecto de destino debe hacer `<references>` referencia al usar el `packages.config` paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-364">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="9f8d9-365">Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-365">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="9f8d9-366">Para obtener más información, vea la página sobre la selección de ensamblados a los que [hacen referencia los proyectos.](../create-packages/select-assemblies-referenced-by-projects.md)</span><span class="sxs-lookup"><span data-stu-id="9f8d9-366">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="9f8d9-367">Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-367">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="9f8d9-368">Grupos de referencias</span><span class="sxs-lookup"><span data-stu-id="9f8d9-368">Reference groups</span></span>

<span data-ttu-id="9f8d9-369">Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-369">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="9f8d9-370">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-370">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="9f8d9-371">Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-371">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="9f8d9-372">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-372">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="9f8d9-373">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-373">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="9f8d9-374">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-374">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="9f8d9-375">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-375">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="9f8d9-376">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="9f8d9-376">Framework assembly references</span></span>

<span data-ttu-id="9f8d9-377">Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-377">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="9f8d9-378">Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-378">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="9f8d9-379">Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-379">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="9f8d9-380">El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-380">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="9f8d9-381">Atributo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-381">Attribute</span></span> | <span data-ttu-id="9f8d9-382">Descripción</span><span class="sxs-lookup"><span data-stu-id="9f8d9-382">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9f8d9-383">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-383">**assemblyName**</span></span> | <span data-ttu-id="9f8d9-384">(Obligatorio) Nombre completo del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-384">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="9f8d9-385">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-385">**targetFramework**</span></span> | <span data-ttu-id="9f8d9-386">(Opcional) Especifica la plataforma de destino a la que se aplica esta referencia.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-386">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="9f8d9-387">Si se omite, indica que la referencia se aplica a todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-387">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="9f8d9-388">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-388">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="9f8d9-389">En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-389">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="9f8d9-390">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="9f8d9-390">Including assembly files</span></span>

<span data-ttu-id="9f8d9-391">Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-391">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="9f8d9-392">El comando `nuget pack` selecciona automáticamente los archivos necesarios.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-392">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="9f8d9-393">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-393">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="9f8d9-394">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-394">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="9f8d9-395">Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-395">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="9f8d9-396">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-396">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="9f8d9-397">Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-397">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="9f8d9-398">Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-398">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="9f8d9-399">Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-399">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="9f8d9-400">Atributos del elemento File</span><span class="sxs-lookup"><span data-stu-id="9f8d9-400">File element attributes</span></span>

<span data-ttu-id="9f8d9-401">Cada elemento `<file>` especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-401">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="9f8d9-402">Atributo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-402">Attribute</span></span> | <span data-ttu-id="9f8d9-403">Descripción</span><span class="sxs-lookup"><span data-stu-id="9f8d9-403">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9f8d9-404">**src**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-404">**src**</span></span> | <span data-ttu-id="9f8d9-405">Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-405">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="9f8d9-406">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-406">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="9f8d9-407">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-407">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="9f8d9-408">**Destino**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-408">**target**</span></span> | <span data-ttu-id="9f8d9-409">La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-409">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="9f8d9-410">Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-410">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="9f8d9-411">**Excluir**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-411">**exclude**</span></span> | <span data-ttu-id="9f8d9-412">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-412">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="9f8d9-413">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-413">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="9f8d9-414">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9f8d9-414">Examples</span></span>

<span data-ttu-id="9f8d9-415">**Ensamblado único**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-415">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="9f8d9-416">**Ensamblado único específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-416">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="9f8d9-417">**Conjunto de archivos DLL que usan un carácter comodín**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-417">**Set of DLLs using a wildcard**</span></span>

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

<span data-ttu-id="9f8d9-418">**Archivos DLL para distintas plataformas**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-418">**DLLs for different frameworks**</span></span>

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

<span data-ttu-id="9f8d9-419">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-419">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="9f8d9-420">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="9f8d9-420">Including content files</span></span>

<span data-ttu-id="9f8d9-421">Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-421">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="9f8d9-422">Como son inmutables, no se prevé que el proyecto de consumo los modifique.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-422">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="9f8d9-423">Entre los archivos de contenido se encuentran los siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-423">Example content files include:</span></span>

- <span data-ttu-id="9f8d9-424">Imágenes que se insertan como recursos</span><span class="sxs-lookup"><span data-stu-id="9f8d9-424">Images that are embedded as resources</span></span>
- <span data-ttu-id="9f8d9-425">Archivos de código fuente que ya están compilados</span><span class="sxs-lookup"><span data-stu-id="9f8d9-425">Source files that are already compiled</span></span>
- <span data-ttu-id="9f8d9-426">Scripts que se deben incluir con la salida de la compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="9f8d9-426">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="9f8d9-427">Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto</span><span class="sxs-lookup"><span data-stu-id="9f8d9-427">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="9f8d9-428">Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-428">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="9f8d9-429">Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-429">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="9f8d9-430">Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-430">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="9f8d9-431">Usar el elemento files para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="9f8d9-431">Using the files element for content files</span></span>

<span data-ttu-id="9f8d9-432">En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-432">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="9f8d9-433">**Archivos de contenido básicos**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-433">**Basic content files**</span></span>

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

<span data-ttu-id="9f8d9-434">**Archivos de contenido con estructura de directorios**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-434">**Content files with directory structure**</span></span>

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

<span data-ttu-id="9f8d9-435">**Archivo de contenido específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-435">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="9f8d9-436">**Archivo de contenido copiado en una carpeta con un punto en el nombre**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-436">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="9f8d9-437">En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-437">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="9f8d9-438">**Archivos de contenido sin extensión**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-438">**Content files without extensions**</span></span>

<span data-ttu-id="9f8d9-439">Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-439">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="9f8d9-440">**Archivos de contenido con una ruta de acceso y un destino profundos**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-440">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="9f8d9-441">En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-441">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

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

<span data-ttu-id="9f8d9-442">**Cambiar el nombre de un archivo de contenido del paquete**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-442">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="9f8d9-443">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-443">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="9f8d9-444">Usar el elemento contentFiles para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="9f8d9-444">Using the contentFiles element for content files</span></span>

<span data-ttu-id="9f8d9-445">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="9f8d9-445">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="9f8d9-446">De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-446">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="9f8d9-447">En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-447">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="9f8d9-448">Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-448">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="9f8d9-449">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-449">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="9f8d9-450">Atributo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-450">Attribute</span></span> | <span data-ttu-id="9f8d9-451">Descripción</span><span class="sxs-lookup"><span data-stu-id="9f8d9-451">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9f8d9-452">**incluír**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-452">**include**</span></span> | <span data-ttu-id="9f8d9-453">(Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-453">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="9f8d9-454">La ruta de acceso es relativa a la `contentFiles` carpeta a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-454">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="9f8d9-455">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-455">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="9f8d9-456">**Excluir**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-456">**exclude**</span></span> | <span data-ttu-id="9f8d9-457">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-457">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="9f8d9-458">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-458">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="9f8d9-459">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-459">**buildAction**</span></span> | <span data-ttu-id="9f8d9-460">Acción de compilación que se asignará al elemento de contenido de MSBuild, como `Content` , , , , `None` `Embedded Resource` `Compile` etc. El valor predeterminado es `Compile` .</span><span class="sxs-lookup"><span data-stu-id="9f8d9-460">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="9f8d9-461">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-461">**copyToOutput**</span></span> | <span data-ttu-id="9f8d9-462">Valor booleano que indica si se copian elementos de contenido en la carpeta de salida de compilación (o publicación).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-462">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="9f8d9-463">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-463">The default is false.</span></span> |
| <span data-ttu-id="9f8d9-464">**flatten**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-464">**flatten**</span></span> | <span data-ttu-id="9f8d9-465">Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-465">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="9f8d9-466">Esta marca solo funciona cuando la marca copyToOutput está establecida en true.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-466">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="9f8d9-467">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-467">The default is false.</span></span> |

<span data-ttu-id="9f8d9-468">Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-468">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="9f8d9-469">Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-469">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="9f8d9-470">La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-470">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="9f8d9-471">Estructura de carpetas de los paquetes</span><span class="sxs-lookup"><span data-stu-id="9f8d9-471">Package folder structure</span></span>

<span data-ttu-id="9f8d9-472">El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-472">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="9f8d9-473">`codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-473">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="9f8d9-474">`TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="9f8d9-474">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="9f8d9-475">Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-475">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="9f8d9-476">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-476">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="9f8d9-477">Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-477">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="9f8d9-478">Sección contentFiles de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-478">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="9f8d9-479">Grupos de referencia de framework</span><span class="sxs-lookup"><span data-stu-id="9f8d9-479">Framework reference groups</span></span>

<span data-ttu-id="9f8d9-480">*Versión 5.1+ wih PackageReference solo*</span><span class="sxs-lookup"><span data-stu-id="9f8d9-480">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="9f8d9-481">Las referencias de marco son un concepto de .NET Core que representa marcos compartidos como WPF o Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-481">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="9f8d9-482">Al especificar un marco compartido, el paquete garantiza que todas sus dependencias de marco se incluyen en el proyecto de referencia.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-482">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="9f8d9-483">Cada `<group>` elemento requiere un atributo y cero o más `targetFramework` `<frameworkReference>` elementos.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-483">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="9f8d9-484">En el ejemplo siguiente se muestra un nuspec generado para un proyecto de WPF de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-484">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="9f8d9-485">Tenga en cuenta que no se recomienda crear a mano elementos nuspec que contengan referencias de marco.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-485">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="9f8d9-486">Considere la posibilidad de [usar el](msbuild-targets.md) paquete de destinos en su lugar, que los deducirá automáticamente desde el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9f8d9-486">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="9f8d9-487">Archivos nuspec de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9f8d9-487">Example nuspec files</span></span>

<span data-ttu-id="9f8d9-488">**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-488">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="9f8d9-489">**Un archivo `.nuspec` con dependencias**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-489">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="9f8d9-490">**Un archivo `.nuspec` con archivos**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-490">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="9f8d9-491">**Un archivo `.nuspec` con ensamblados de plataforma**</span><span class="sxs-lookup"><span data-stu-id="9f8d9-491">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="9f8d9-492">En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:</span><span class="sxs-lookup"><span data-stu-id="9f8d9-492">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="9f8d9-493">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="9f8d9-493">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="9f8d9-494">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="9f8d9-494">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="9f8d9-495">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="9f8d9-495">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="9f8d9-496">Windows Phone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="9f8d9-496">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
