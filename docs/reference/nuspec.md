---
title: Referencia de archivo .nuspec para NuGet
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: a8a8058032b0b6c6ddcd5eed1cf22e75f0e3af72
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387418"
---
# <a name="nuspec-reference"></a><span data-ttu-id="7808c-103">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="7808c-103">.nuspec reference</span></span>

<span data-ttu-id="7808c-104">Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="7808c-105">Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores.</span><span class="sxs-lookup"><span data-stu-id="7808c-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="7808c-106">El manifiesto siempre se incluye en un paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="7808c-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="7808c-107">In this topic:</span></span>

- [<span data-ttu-id="7808c-108">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="7808c-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="7808c-109">[Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7808c-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="7808c-110">Dependencias</span><span class="sxs-lookup"><span data-stu-id="7808c-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="7808c-111">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="7808c-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="7808c-112">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="7808c-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="7808c-113">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="7808c-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="7808c-114">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="7808c-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="7808c-115">Archivos nuspec de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7808c-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="7808c-116">Compatibilidad con tipos de proyecto</span><span class="sxs-lookup"><span data-stu-id="7808c-116">Project type compatibility</span></span>

- <span data-ttu-id="7808c-117">Use `.nuspec` con para proyectos que no son de estilo SDK que usan `nuget.exe pack` `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="7808c-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="7808c-118">No se necesita un archivo para crear paquetes para proyectos de estilo `.nuspec` [SDK](../resources/check-project-format.md) (normalmente .NET Core y .NET Standard que usan el [atributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="7808c-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="7808c-119">(Tenga en cuenta `.nuspec` que se genera un al crear el paquete).</span><span class="sxs-lookup"><span data-stu-id="7808c-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="7808c-120">Si va a crear un paquete mediante o , se recomienda incluir en su lugar todas las propiedades que normalmente se encuentran en el archivo `dotnet.exe pack` en el archivo del `msbuild pack target` [](../reference/msbuild-targets.md#pack-target) `.nuspec` proyecto.</span><span class="sxs-lookup"><span data-stu-id="7808c-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="7808c-121">Sin embargo, puede elegir usar un [archivo `.nuspec` para empaquetar mediante `dotnet.exe` o `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="7808c-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span></span>

- <span data-ttu-id="7808c-122">Para los proyectos migrados de `packages.config` a [PackageReference](../consume-packages/package-references-in-project-files.md), no se necesita `.nuspec` un archivo para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="7808c-123">En su lugar, [use msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="7808c-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="7808c-124">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="7808c-124">General form and schema</span></span>

<span data-ttu-id="7808c-125">El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="7808c-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="7808c-126">En este esquema, los archivos `.nuspec` tienen el siguiente formato general:</span><span class="sxs-lookup"><span data-stu-id="7808c-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="7808c-127">Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="7808c-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="7808c-128">Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="7808c-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="7808c-129">En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):</span><span class="sxs-lookup"><span data-stu-id="7808c-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

<span data-ttu-id="7808c-131">Todos los nombres de elementos XML del archivo .nuspec distinguen mayúsculas de minúsculas, como es el caso de XML en general.</span><span class="sxs-lookup"><span data-stu-id="7808c-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="7808c-132">Por ejemplo, el uso del elemento metadata `<description>` es correcto y no es `<Description>` correcto.</span><span class="sxs-lookup"><span data-stu-id="7808c-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="7808c-133">A continuación se documenta el uso adecuado de mayúsculas y minúsculas para cada nombre de elemento.</span><span class="sxs-lookup"><span data-stu-id="7808c-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="7808c-134">Elementos de metadatos necesarios</span><span class="sxs-lookup"><span data-stu-id="7808c-134">Required metadata elements</span></span>

<span data-ttu-id="7808c-135">Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="7808c-136">Estos elementos deben aparecer dentro de un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="7808c-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="7808c-137">id</span><span class="sxs-lookup"><span data-stu-id="7808c-137">id</span></span> 
<span data-ttu-id="7808c-138">El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="7808c-139">Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET.</span><span class="sxs-lookup"><span data-stu-id="7808c-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="7808c-140">Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="7808c-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="7808c-141">Al cargar un paquete en nuget.org, `id` el campo está limitado a 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="7808c-142">version</span><span class="sxs-lookup"><span data-stu-id="7808c-142">version</span></span>
<span data-ttu-id="7808c-143">La versión del paquete, siguiendo el patrón *mayor.menor.revisión*.</span><span class="sxs-lookup"><span data-stu-id="7808c-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="7808c-144">Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="7808c-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="7808c-145">Al cargar un paquete en nuget.org, `version` el campo está limitado a 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="7808c-146">description</span><span class="sxs-lookup"><span data-stu-id="7808c-146">description</span></span>
<span data-ttu-id="7808c-147">Descripción del paquete para la presentación de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="7808c-147">A description of the package for UI display.</span></span>

<span data-ttu-id="7808c-148">Al cargar un paquete en nuget.org, `description` el campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="7808c-149">authors</span><span class="sxs-lookup"><span data-stu-id="7808c-149">authors</span></span>
<span data-ttu-id="7808c-150">Lista separada por comas de los autores de paquetes que coinciden con los nombres de perfil en nuget.org. Estos se muestran en la Galería de NuGet en nuget.org y los mismos autores usan para hacer referencia cruzada a los paquetes.</span><span class="sxs-lookup"><span data-stu-id="7808c-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="7808c-151">Al cargar un paquete en nuget.org, `authors` el campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="7808c-152">Elementos de metadatos opcionales</span><span class="sxs-lookup"><span data-stu-id="7808c-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="7808c-153">owners</span><span class="sxs-lookup"><span data-stu-id="7808c-153">owners</span></span>
> [!Important]
> <span data-ttu-id="7808c-154">los propietarios están en desuso.</span><span class="sxs-lookup"><span data-stu-id="7808c-154">owners is deprecated.</span></span> <span data-ttu-id="7808c-155">En su lugar, use autores.</span><span class="sxs-lookup"><span data-stu-id="7808c-155">Use authors instead.</span></span>

<span data-ttu-id="7808c-156">Lista separada por comas de los creadores de paquetes que usan nombres de perfil en nuget.org. Suele ser la misma lista que en y se omite al `authors` cargar el paquete en nuget.org. Consulte [Administración de propietarios de paquetes nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="7808c-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="7808c-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="7808c-157">projectUrl</span></span>
<span data-ttu-id="7808c-158">Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7808c-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="7808c-159">Al cargar un paquete en nuget.org, `projectUrl` el campo se limita a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="7808c-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="7808c-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="7808c-161">licenseUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="7808c-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="7808c-162">Use la licencia en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7808c-162">Use license instead.</span></span>

<span data-ttu-id="7808c-163">Una dirección URL para la licencia del paquete, que a menudo se muestra en uri como nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7808c-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="7808c-164">Al cargar un paquete en nuget.org, `licenseUrl` el campo se limita a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="7808c-165">license</span><span class="sxs-lookup"><span data-stu-id="7808c-165">license</span></span>

<span data-ttu-id="7808c-166">*Compatible con **NuGet 4.9.0** y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="7808c-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="7808c-167">Una expresión de licencia de SPDX o una ruta de acceso a un archivo de licencia dentro del paquete, que a menudo se muestra en uri como nuget.org. Si va a otorgar licencias al paquete con una licencia común, como MIT o BSD-2-Clause, use el identificador de [licencia SPDX asociado.](https://spdx.org/licenses/)</span><span class="sxs-lookup"><span data-stu-id="7808c-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="7808c-168">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7808c-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="7808c-169">NuGet.org solo acepta expresiones de licencia aprobadas por la iniciativa de código abierto o Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="7808c-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="7808c-170">Si el paquete tiene licencia con varias licencias comunes, puede especificar una licencia compuesta mediante la sintaxis de [expresiones SPDX versión 2.0.](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)</span><span class="sxs-lookup"><span data-stu-id="7808c-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="7808c-171">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7808c-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="7808c-172">Si usa una licencia personalizada que no es compatible con las expresiones de licencia, puede empaquetar un archivo `.txt` o con el texto de la `.md` licencia.</span><span class="sxs-lookup"><span data-stu-id="7808c-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="7808c-173">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7808c-173">For example:</span></span>

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

<span data-ttu-id="7808c-174">Para el equivalente de MSBuild, vea [Empaquetado de una expresión de licencia o un archivo de licencia.](msbuild-targets.md#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="7808c-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="7808c-175">La sintaxis exacta de las expresiones de licencia de NuGet se describe a continuación en [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="7808c-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

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

#### <a name="iconurl"></a><span data-ttu-id="7808c-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="7808c-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="7808c-177">iconUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="7808c-177">iconUrl is deprecated.</span></span> <span data-ttu-id="7808c-178">Use el icono en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7808c-178">Use icon instead.</span></span>

<span data-ttu-id="7808c-179">Una dirección URL para una imagen de 128 x 128 con fondo de transparencia que se usará como icono para el paquete en la presentación de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="7808c-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="7808c-180">Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen.</span><span class="sxs-lookup"><span data-stu-id="7808c-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="7808c-181">Por ejemplo, para usar una imagen de GitHub, use la dirección URL del archivo sin formato como <em> https://github.com/ \<username\> / \<repository\> /raw/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="7808c-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="7808c-182">Al cargar un paquete en nuget.org, `iconUrl` el campo se limita a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="7808c-183">icon</span><span class="sxs-lookup"><span data-stu-id="7808c-183">icon</span></span>

<span data-ttu-id="7808c-184">*Compatible con **NuGet 5.3.0** y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="7808c-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="7808c-185">Es una ruta de acceso a un archivo de imagen dentro del paquete, que a menudo se muestra en uri como nuget.org como icono de paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="7808c-186">El tamaño del archivo de imagen está limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="7808c-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="7808c-187">Los formatos de archivo admitidos incluyen JPEG y PNG.</span><span class="sxs-lookup"><span data-stu-id="7808c-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="7808c-188">Se recomienda una resolución de imagen de 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="7808c-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="7808c-189">Por ejemplo, agregaría lo siguiente a nuspec al crear un paquete mediante nuget.exe:</span><span class="sxs-lookup"><span data-stu-id="7808c-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="7808c-190">Ejemplo nuspec de icono de paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

<span data-ttu-id="7808c-191">Para el equivalente de MSBuild, vea [Empaquetado de un archivo de imagen de icono.](msbuild-targets.md#packing-an-icon-image-file)</span><span class="sxs-lookup"><span data-stu-id="7808c-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="7808c-192">Puede especificar y para `icon` mantener la compatibilidad con versiones anteriores con orígenes que no `iconUrl` admiten `icon` .</span><span class="sxs-lookup"><span data-stu-id="7808c-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="7808c-193">Visual Studio admitirá `icon` los paquetes procedentes de un origen basado en carpetas en una versión futura.</span><span class="sxs-lookup"><span data-stu-id="7808c-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="readme"></a><span data-ttu-id="7808c-194">Archivo Léame</span><span class="sxs-lookup"><span data-stu-id="7808c-194">readme</span></span>

<span data-ttu-id="7808c-195">Al empaquetar un archivo Léame, debe usar el elemento para especificar la ruta de acceso del paquete, en relación con la `readme` raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-195">When packing a readme file, you need to use the `readme` element to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="7808c-196">Además de esto, debe asegurarse de que el archivo está incluido en el paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-196">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="7808c-197">Los formatos de archivo admitidos incluyen solo Markdown (*.md*).</span><span class="sxs-lookup"><span data-stu-id="7808c-197">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="7808c-198">Por ejemplo, agregaría lo siguiente a nuspec para empaquetar un archivo Léame con el proyecto:</span><span class="sxs-lookup"><span data-stu-id="7808c-198">For example, you would add the following to your nuspec in order to pack a readme file with your project:</span></span>

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

<span data-ttu-id="7808c-199">Para el equivalente de MSBuild, consulte [Empaquetado de un archivo Léame.](msbuild-targets.md#packagereadmefile)</span><span class="sxs-lookup"><span data-stu-id="7808c-199">For the MSBuild equivalent, take a look at [Packing a readme file](msbuild-targets.md#packagereadmefile).</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="7808c-200">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="7808c-200">requireLicenseAcceptance</span></span>
<span data-ttu-id="7808c-201">Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="7808c-201">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="7808c-202">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="7808c-202">developmentDependency</span></span>
<span data-ttu-id="7808c-203">*(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="7808c-203">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="7808c-204">Con PackageReference (NuGet 4.8 +) , esta marca también significa que excluirá los recursos en tiempo de compilación de la compilación.</span><span class="sxs-lookup"><span data-stu-id="7808c-204">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="7808c-205">Consulte [DevelopmentDependency support for PackageReference (Compatibilidad de DevelopmentDependency con PackageReference).](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="7808c-205">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="7808c-206">Resumen</span><span class="sxs-lookup"><span data-stu-id="7808c-206">summary</span></span>
> [!Important]
> <span data-ttu-id="7808c-207">`summary` está en desuso.</span><span class="sxs-lookup"><span data-stu-id="7808c-207">`summary` is being deprecated.</span></span> <span data-ttu-id="7808c-208">En su lugar, use `description`.</span><span class="sxs-lookup"><span data-stu-id="7808c-208">Use `description` instead.</span></span>

<span data-ttu-id="7808c-209">Descripción breve del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="7808c-209">A short description of the package for UI display.</span></span> <span data-ttu-id="7808c-210">Si se omite, se usará una versión truncada de `description`.</span><span class="sxs-lookup"><span data-stu-id="7808c-210">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="7808c-211">Al cargar un paquete en nuget.org, `summary` el campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-211">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="7808c-212">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="7808c-212">releaseNotes</span></span>
<span data-ttu-id="7808c-213">*(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-213">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="7808c-214">Al cargar un paquete en nuget.org, el `releaseNotes` campo está limitado a 35 000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-214">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="7808c-215">copyright</span><span class="sxs-lookup"><span data-stu-id="7808c-215">copyright</span></span>
<span data-ttu-id="7808c-216">*(1.5+)* Información de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-216">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="7808c-217">Al cargar un paquete en nuget.org, `copyright` el campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-217">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="7808c-218">language</span><span class="sxs-lookup"><span data-stu-id="7808c-218">language</span></span>
<span data-ttu-id="7808c-219">Identificador de configuración regional del paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-219">The locale ID for the package.</span></span> <span data-ttu-id="7808c-220">Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7808c-220">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="7808c-221">etiquetas</span><span class="sxs-lookup"><span data-stu-id="7808c-221">tags</span></span>
<span data-ttu-id="7808c-222">Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados.</span><span class="sxs-lookup"><span data-stu-id="7808c-222">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="7808c-223">Al cargar un paquete en nuget.org, `tags` el campo está limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-223">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="7808c-224">serviceable</span><span class="sxs-lookup"><span data-stu-id="7808c-224">serviceable</span></span> 
<span data-ttu-id="7808c-225">*(3.3+)* Solo para uso interno de NuGet.</span><span class="sxs-lookup"><span data-stu-id="7808c-225">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="7808c-226">repository</span><span class="sxs-lookup"><span data-stu-id="7808c-226">repository</span></span>
<span data-ttu-id="7808c-227">Metadatos del repositorio, que consta de cuatro atributos opcionales: `type` y `url` *(4.0+)*, `branch` y y `commit` *(4.6+)*.</span><span class="sxs-lookup"><span data-stu-id="7808c-227">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="7808c-228">Estos atributos le permiten asignar al repositorio que lo comcreó, con el potencial de obtener tan detallado como el nombre de rama individual y/o confirmar el hash SHA-1 que comcreó el `.nupkg` paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-228">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="7808c-229">Debe ser una dirección URL disponible públicamente que un software de control de versiones pueda invocar directamente.</span><span class="sxs-lookup"><span data-stu-id="7808c-229">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="7808c-230">No debe ser una página HTML, ya que está pensada para el equipo.</span><span class="sxs-lookup"><span data-stu-id="7808c-230">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="7808c-231">Para vincular a la página del proyecto, use `projectUrl` el campo en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7808c-231">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="7808c-232">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7808c-232">For example:</span></span>
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

<span data-ttu-id="7808c-233">Al cargar un paquete en nuget.org, el atributo se limita a 100 caracteres y el atributo se limita a `type` `url` 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-233">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="7808c-234">title</span><span class="sxs-lookup"><span data-stu-id="7808c-234">title</span></span>
<span data-ttu-id="7808c-235">Título descriptivo del paquete que se puede usar en algunas pantallas de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="7808c-235">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="7808c-236">(nuget.org y el Administrador de paquetes en Visual Studio no muestran el título)</span><span class="sxs-lookup"><span data-stu-id="7808c-236">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="7808c-237">Al cargar un paquete en nuget.org, el campo se limita a 256 caracteres, pero no se usa con fines `title` de presentación.</span><span class="sxs-lookup"><span data-stu-id="7808c-237">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="7808c-238">Elementos de colección</span><span class="sxs-lookup"><span data-stu-id="7808c-238">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="7808c-239">packageTypes</span><span class="sxs-lookup"><span data-stu-id="7808c-239">packageTypes</span></span>
<span data-ttu-id="7808c-240">*(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional.</span><span class="sxs-lookup"><span data-stu-id="7808c-240">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="7808c-241">Cada tipo de paquete tiene atributos de *name* y *version*.</span><span class="sxs-lookup"><span data-stu-id="7808c-241">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="7808c-242">Vea [Establecimiento de un tipo de paquete](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="7808c-242">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="7808c-243">dependencies</span><span class="sxs-lookup"><span data-stu-id="7808c-243">dependencies</span></span>
<span data-ttu-id="7808c-244">Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-244">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="7808c-245">Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="7808c-245">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="7808c-246">Vea [Dependencias](#dependencies-element) a continuación.</span><span class="sxs-lookup"><span data-stu-id="7808c-246">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="7808c-247">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="7808c-247">frameworkAssemblies</span></span>
<span data-ttu-id="7808c-248">*(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-248">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="7808c-249">Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="7808c-249">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="7808c-250">Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación.</span><span class="sxs-lookup"><span data-stu-id="7808c-250">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="7808c-251">references</span><span class="sxs-lookup"><span data-stu-id="7808c-251">references</span></span>
<span data-ttu-id="7808c-252">*(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="7808c-252">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="7808c-253">Cada referencia tiene un atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="7808c-253">Each reference has a *file* attribute.</span></span> <span data-ttu-id="7808c-254">`<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="7808c-254">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="7808c-255">Si se omite, se incluyen todas las referencias de `lib`.</span><span class="sxs-lookup"><span data-stu-id="7808c-255">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="7808c-256">Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación.</span><span class="sxs-lookup"><span data-stu-id="7808c-256">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="7808c-257">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7808c-257">contentFiles</span></span>
<span data-ttu-id="7808c-258">*(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="7808c-258">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="7808c-259">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7808c-259">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="7808c-260">Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación.</span><span class="sxs-lookup"><span data-stu-id="7808c-260">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="7808c-261">archivos</span><span class="sxs-lookup"><span data-stu-id="7808c-261">files</span></span> 
<span data-ttu-id="7808c-262">El nodo puede contener un nodo como un nodo relacionado con y un elemento secundario en , para especificar los archivos de ensamblado y contenido que se `<package>` `<files>` `<metadata>` `<contentFiles>` `<metadata>` incluirán en el paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-262">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="7808c-263">Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.</span><span class="sxs-lookup"><span data-stu-id="7808c-263">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="7808c-264">atributos de metadatos</span><span class="sxs-lookup"><span data-stu-id="7808c-264">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="7808c-265">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="7808c-265">minClientVersion</span></span>
<span data-ttu-id="7808c-266">Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7808c-266">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="7808c-267">Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="7808c-267">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="7808c-268">Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="7808c-268">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="7808c-269">Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3".</span><span class="sxs-lookup"><span data-stu-id="7808c-269">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="7808c-270">Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="7808c-270">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

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

## <a name="replacement-tokens"></a><span data-ttu-id="7808c-271">Tokens de reemplazo</span><span class="sxs-lookup"><span data-stu-id="7808c-271">Replacement tokens</span></span>

<span data-ttu-id="7808c-272">Al crear un [ `nuget pack` ](../reference/cli-reference/cli-ref-pack.md) paquete, el comando reemplaza los tokens delimitados por $en el nodo del archivo por valores que proceden de un archivo de proyecto o del `.nuspec` modificador del `<metadata>` `pack` `-properties` comando.</span><span class="sxs-lookup"><span data-stu-id="7808c-272">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="7808c-273">En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="7808c-273">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="7808c-274">Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="7808c-274">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="7808c-275">Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="7808c-275">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="7808c-276">Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="7808c-276">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="7808c-277">Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="7808c-277">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="7808c-278">Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares.</span><span class="sxs-lookup"><span data-stu-id="7808c-278">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="7808c-279">Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="7808c-279">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="7808c-280">Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="7808c-280">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="7808c-281">Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="7808c-281">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="7808c-282">Token</span><span class="sxs-lookup"><span data-stu-id="7808c-282">Token</span></span> | <span data-ttu-id="7808c-283">Origen del valor</span><span class="sxs-lookup"><span data-stu-id="7808c-283">Value source</span></span> | <span data-ttu-id="7808c-284">Value</span><span class="sxs-lookup"><span data-stu-id="7808c-284">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="7808c-285">**$id$**</span><span class="sxs-lookup"><span data-stu-id="7808c-285">**$id$**</span></span> | <span data-ttu-id="7808c-286">Archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="7808c-286">Project file</span></span> | <span data-ttu-id="7808c-287">AssemblyName (título) del archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="7808c-287">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="7808c-288">**$version$**</span><span class="sxs-lookup"><span data-stu-id="7808c-288">**$version$**</span></span> | <span data-ttu-id="7808c-289">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7808c-289">AssemblyInfo</span></span> | <span data-ttu-id="7808c-290">AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="7808c-290">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="7808c-291">**$author$**</span><span class="sxs-lookup"><span data-stu-id="7808c-291">**$author$**</span></span> | <span data-ttu-id="7808c-292">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7808c-292">AssemblyInfo</span></span> | <span data-ttu-id="7808c-293">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="7808c-293">AssemblyCompany</span></span> |
| <span data-ttu-id="7808c-294">**$title$**</span><span class="sxs-lookup"><span data-stu-id="7808c-294">**$title$**</span></span> | <span data-ttu-id="7808c-295">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7808c-295">AssemblyInfo</span></span> | <span data-ttu-id="7808c-296">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="7808c-296">AssemblyTitle</span></span> |
| <span data-ttu-id="7808c-297">**$description$**</span><span class="sxs-lookup"><span data-stu-id="7808c-297">**$description$**</span></span> | <span data-ttu-id="7808c-298">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7808c-298">AssemblyInfo</span></span> | <span data-ttu-id="7808c-299">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="7808c-299">AssemblyDescription</span></span> |
| <span data-ttu-id="7808c-300">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="7808c-300">**$copyright$**</span></span> | <span data-ttu-id="7808c-301">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="7808c-301">AssemblyInfo</span></span> | <span data-ttu-id="7808c-302">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="7808c-302">AssemblyCopyright</span></span> |
| <span data-ttu-id="7808c-303">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="7808c-303">**$configuration$**</span></span> | <span data-ttu-id="7808c-304">Archivo DLL del ensamblado</span><span class="sxs-lookup"><span data-stu-id="7808c-304">Assembly DLL</span></span> | <span data-ttu-id="7808c-305">Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar.</span><span class="sxs-lookup"><span data-stu-id="7808c-305">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="7808c-306">Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="7808c-306">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="7808c-307">Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="7808c-307">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="7808c-308">Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual.</span><span class="sxs-lookup"><span data-stu-id="7808c-308">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="7808c-309">Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="7808c-309">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="7808c-310">Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:</span><span class="sxs-lookup"><span data-stu-id="7808c-310">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="7808c-311">Elemento Dependencies</span><span class="sxs-lookup"><span data-stu-id="7808c-311">Dependencies element</span></span>

<span data-ttu-id="7808c-312">El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="7808c-312">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="7808c-313">Los atributos de cada `<dependency>` son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="7808c-313">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="7808c-314">Atributo</span><span class="sxs-lookup"><span data-stu-id="7808c-314">Attribute</span></span> | <span data-ttu-id="7808c-315">Descripción</span><span class="sxs-lookup"><span data-stu-id="7808c-315">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="7808c-316">(Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-316">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="7808c-317">(Obligatorio) Intervalo de versiones aceptable como dependencia.</span><span class="sxs-lookup"><span data-stu-id="7808c-317">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="7808c-318">Vea [Control de versiones de paquetes](../concepts/package-versioning.md#version-ranges) para consultar la sintaxis exacta.</span><span class="sxs-lookup"><span data-stu-id="7808c-318">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="7808c-319">No se admiten versiones flotantes.</span><span class="sxs-lookup"><span data-stu-id="7808c-319">Floating versions are not supported.</span></span> |
| <span data-ttu-id="7808c-320">include</span><span class="sxs-lookup"><span data-stu-id="7808c-320">include</span></span> | <span data-ttu-id="7808c-321">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="7808c-321">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="7808c-322">El valor predeterminado es `all`.</span><span class="sxs-lookup"><span data-stu-id="7808c-322">The default value is `all`.</span></span> |
| <span data-ttu-id="7808c-323">exclude</span><span class="sxs-lookup"><span data-stu-id="7808c-323">exclude</span></span> | <span data-ttu-id="7808c-324">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="7808c-324">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="7808c-325">El valor predeterminado es `build,analyzers` que se puede escribir en exceso.</span><span class="sxs-lookup"><span data-stu-id="7808c-325">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="7808c-326">Pero `content/ ContentFiles` también se excluyen implícitamente en el paquete final que no se puede escribir en exceso.</span><span class="sxs-lookup"><span data-stu-id="7808c-326">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="7808c-327">Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`.</span><span class="sxs-lookup"><span data-stu-id="7808c-327">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="7808c-328">Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="7808c-328">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="7808c-329">Al cargar un paquete en nuget.org, el atributo de cada dependencia está limitado a 128 caracteres y el atributo está limitado a `id` `version` 256 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7808c-329">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="7808c-330">Etiqueta Include o Exclude</span><span class="sxs-lookup"><span data-stu-id="7808c-330">Include/Exclude tag</span></span> | <span data-ttu-id="7808c-331">Carpetas afectadas del destino</span><span class="sxs-lookup"><span data-stu-id="7808c-331">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="7808c-332">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7808c-332">contentFiles</span></span> | <span data-ttu-id="7808c-333">Contenido</span><span class="sxs-lookup"><span data-stu-id="7808c-333">Content</span></span> |
| <span data-ttu-id="7808c-334">en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="7808c-334">runtime</span></span> | <span data-ttu-id="7808c-335">Runtime, Resources y FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="7808c-335">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="7808c-336">compile</span><span class="sxs-lookup"><span data-stu-id="7808c-336">compile</span></span> | <span data-ttu-id="7808c-337">lib</span><span class="sxs-lookup"><span data-stu-id="7808c-337">lib</span></span> |
| <span data-ttu-id="7808c-338">build</span><span class="sxs-lookup"><span data-stu-id="7808c-338">build</span></span> | <span data-ttu-id="7808c-339">build (propiedades y destinos de MSBuild)</span><span class="sxs-lookup"><span data-stu-id="7808c-339">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="7808c-340">nativas</span><span class="sxs-lookup"><span data-stu-id="7808c-340">native</span></span> | <span data-ttu-id="7808c-341">nativas</span><span class="sxs-lookup"><span data-stu-id="7808c-341">native</span></span> |
| <span data-ttu-id="7808c-342">ninguno</span><span class="sxs-lookup"><span data-stu-id="7808c-342">none</span></span> | <span data-ttu-id="7808c-343">Sin carpetas</span><span class="sxs-lookup"><span data-stu-id="7808c-343">No folders</span></span> |
| <span data-ttu-id="7808c-344">all</span><span class="sxs-lookup"><span data-stu-id="7808c-344">all</span></span> | <span data-ttu-id="7808c-345">Todas las carpetas</span><span class="sxs-lookup"><span data-stu-id="7808c-345">All folders</span></span> |

<span data-ttu-id="7808c-346">Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="7808c-346">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="7808c-347">Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="7808c-347">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="7808c-348">Al crear un a partir de un proyecto mediante , las dependencias que existen en ese proyecto no se `.nuspec` incluyen automáticamente en el archivo `nuget spec` `.nuspec` resultante.</span><span class="sxs-lookup"><span data-stu-id="7808c-348">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="7808c-349">En su lugar, `nuget pack myproject.csproj` use y obtenga el archivo *.nuspec* desde dentro del *archivo .nupkg* generado.</span><span class="sxs-lookup"><span data-stu-id="7808c-349">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="7808c-350">Este *archivo .nuspec* contiene las dependencias.</span><span class="sxs-lookup"><span data-stu-id="7808c-350">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="7808c-351">Grupos de dependencia</span><span class="sxs-lookup"><span data-stu-id="7808c-351">Dependency groups</span></span>

<span data-ttu-id="7808c-352">*Versión 2.0+*</span><span class="sxs-lookup"><span data-stu-id="7808c-352">*Version 2.0+*</span></span>

<span data-ttu-id="7808c-353">Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="7808c-353">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="7808c-354">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="7808c-354">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="7808c-355">Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7808c-355">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="7808c-356">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias.</span><span class="sxs-lookup"><span data-stu-id="7808c-356">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="7808c-357">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="7808c-357">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="7808c-358">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="7808c-358">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="7808c-359">El formato del [Moniker de la plataforma de destino (TFM)](../reference/target-frameworks.md) usado en la carpeta es diferente en comparación con `lib/ref` el TFM usado en `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="7808c-359">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="7808c-360">Si las plataformas de destino declaradas en y la carpeta del archivo no tienen coincidencias exactas, el comando genera la advertencia `dependencies group` `lib/ref` `.nuspec` `pack` [nuget NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="7808c-360">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="7808c-361">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="7808c-361">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="7808c-362">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="7808c-362">Explicit assembly references</span></span>

<span data-ttu-id="7808c-363">Los proyectos usan el elemento para especificar explícitamente los ensamblados a los que el proyecto de destino debe hacer `<references>` referencia al usar el `packages.config` paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-363">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="7808c-364">Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="7808c-364">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="7808c-365">Para obtener más información, vea la página sobre [la selección de ensamblados](../create-packages/select-assemblies-referenced-by-projects.md) a los que hacen referencia los proyectos.</span><span class="sxs-lookup"><span data-stu-id="7808c-365">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="7808c-366">Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:</span><span class="sxs-lookup"><span data-stu-id="7808c-366">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="7808c-367">Grupos de referencias</span><span class="sxs-lookup"><span data-stu-id="7808c-367">Reference groups</span></span>

<span data-ttu-id="7808c-368">Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="7808c-368">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="7808c-369">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="7808c-369">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="7808c-370">Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7808c-370">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="7808c-371">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias.</span><span class="sxs-lookup"><span data-stu-id="7808c-371">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="7808c-372">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="7808c-372">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="7808c-373">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="7808c-373">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="7808c-374">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="7808c-374">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="7808c-375">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="7808c-375">Framework assembly references</span></span>

<span data-ttu-id="7808c-376">Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo.</span><span class="sxs-lookup"><span data-stu-id="7808c-376">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="7808c-377">Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias.</span><span class="sxs-lookup"><span data-stu-id="7808c-377">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="7808c-378">Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-378">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="7808c-379">El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="7808c-379">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="7808c-380">Atributo</span><span class="sxs-lookup"><span data-stu-id="7808c-380">Attribute</span></span> | <span data-ttu-id="7808c-381">Descripción</span><span class="sxs-lookup"><span data-stu-id="7808c-381">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7808c-382">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="7808c-382">**assemblyName**</span></span> | <span data-ttu-id="7808c-383">(Obligatorio) Nombre completo del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="7808c-383">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="7808c-384">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="7808c-384">**targetFramework**</span></span> | <span data-ttu-id="7808c-385">(Opcional) Especifica la plataforma de destino a la que se aplica esta referencia.</span><span class="sxs-lookup"><span data-stu-id="7808c-385">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="7808c-386">Si se omite, indica que la referencia se aplica a todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="7808c-386">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="7808c-387">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="7808c-387">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="7808c-388">En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="7808c-388">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="7808c-389">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="7808c-389">Including assembly files</span></span>

<span data-ttu-id="7808c-390">Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="7808c-390">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="7808c-391">El comando `nuget pack` selecciona automáticamente los archivos necesarios.</span><span class="sxs-lookup"><span data-stu-id="7808c-391">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="7808c-392">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados.</span><span class="sxs-lookup"><span data-stu-id="7808c-392">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="7808c-393">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-393">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="7808c-394">Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente.</span><span class="sxs-lookup"><span data-stu-id="7808c-394">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="7808c-395">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7808c-395">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="7808c-396">Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="7808c-396">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="7808c-397">Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7808c-397">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="7808c-398">Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="7808c-398">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="7808c-399">Atributos del elemento File</span><span class="sxs-lookup"><span data-stu-id="7808c-399">File element attributes</span></span>

<span data-ttu-id="7808c-400">Cada elemento `<file>` especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="7808c-400">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="7808c-401">Atributo</span><span class="sxs-lookup"><span data-stu-id="7808c-401">Attribute</span></span> | <span data-ttu-id="7808c-402">Descripción</span><span class="sxs-lookup"><span data-stu-id="7808c-402">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7808c-403">**src**</span><span class="sxs-lookup"><span data-stu-id="7808c-403">**src**</span></span> | <span data-ttu-id="7808c-404">Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="7808c-404">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="7808c-405">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="7808c-405">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="7808c-406">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="7808c-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="7808c-407">**Destino**</span><span class="sxs-lookup"><span data-stu-id="7808c-407">**target**</span></span> | <span data-ttu-id="7808c-408">La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="7808c-408">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="7808c-409">Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones).</span><span class="sxs-lookup"><span data-stu-id="7808c-409">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="7808c-410">**Excluir**</span><span class="sxs-lookup"><span data-stu-id="7808c-410">**exclude**</span></span> | <span data-ttu-id="7808c-411">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="7808c-411">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="7808c-412">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="7808c-412">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="7808c-413">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7808c-413">Examples</span></span>

<span data-ttu-id="7808c-414">**Ensamblado único**</span><span class="sxs-lookup"><span data-stu-id="7808c-414">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="7808c-415">**Ensamblado único específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="7808c-415">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="7808c-416">**Conjunto de archivos DLL que usan un carácter comodín**</span><span class="sxs-lookup"><span data-stu-id="7808c-416">**Set of DLLs using a wildcard**</span></span>

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

<span data-ttu-id="7808c-417">**Archivos DLL para distintas plataformas**</span><span class="sxs-lookup"><span data-stu-id="7808c-417">**DLLs for different frameworks**</span></span>

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

<span data-ttu-id="7808c-418">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="7808c-418">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="7808c-419">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="7808c-419">Including content files</span></span>

<span data-ttu-id="7808c-420">Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="7808c-420">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="7808c-421">Como son inmutables, no se prevé que el proyecto de consumo los modifique.</span><span class="sxs-lookup"><span data-stu-id="7808c-421">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="7808c-422">Entre los archivos de contenido se encuentran los siguientes:</span><span class="sxs-lookup"><span data-stu-id="7808c-422">Example content files include:</span></span>

- <span data-ttu-id="7808c-423">Imágenes que se insertan como recursos</span><span class="sxs-lookup"><span data-stu-id="7808c-423">Images that are embedded as resources</span></span>
- <span data-ttu-id="7808c-424">Archivos de código fuente que ya están compilados</span><span class="sxs-lookup"><span data-stu-id="7808c-424">Source files that are already compiled</span></span>
- <span data-ttu-id="7808c-425">Scripts que se deben incluir con la salida de la compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="7808c-425">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="7808c-426">Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto</span><span class="sxs-lookup"><span data-stu-id="7808c-426">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="7808c-427">Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="7808c-427">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="7808c-428">Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7808c-428">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="7808c-429">Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.</span><span class="sxs-lookup"><span data-stu-id="7808c-429">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="7808c-430">Usar el elemento files para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="7808c-430">Using the files element for content files</span></span>

<span data-ttu-id="7808c-431">En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="7808c-431">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="7808c-432">**Archivos de contenido básicos**</span><span class="sxs-lookup"><span data-stu-id="7808c-432">**Basic content files**</span></span>

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

<span data-ttu-id="7808c-433">**Archivos de contenido con estructura de directorios**</span><span class="sxs-lookup"><span data-stu-id="7808c-433">**Content files with directory structure**</span></span>

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

<span data-ttu-id="7808c-434">**Archivo de contenido específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="7808c-434">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="7808c-435">**Archivo de contenido copiado en una carpeta con un punto en el nombre**</span><span class="sxs-lookup"><span data-stu-id="7808c-435">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="7808c-436">En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:</span><span class="sxs-lookup"><span data-stu-id="7808c-436">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="7808c-437">**Archivos de contenido sin extensión**</span><span class="sxs-lookup"><span data-stu-id="7808c-437">**Content files without extensions**</span></span>

<span data-ttu-id="7808c-438">Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="7808c-438">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="7808c-439">**Archivos de contenido con una ruta de acceso y un destino profundos**</span><span class="sxs-lookup"><span data-stu-id="7808c-439">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="7808c-440">En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:</span><span class="sxs-lookup"><span data-stu-id="7808c-440">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

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

<span data-ttu-id="7808c-441">**Cambiar el nombre de un archivo de contenido del paquete**</span><span class="sxs-lookup"><span data-stu-id="7808c-441">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="7808c-442">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="7808c-442">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="7808c-443">Usar el elemento contentFiles para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="7808c-443">Using the contentFiles element for content files</span></span>

<span data-ttu-id="7808c-444">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="7808c-444">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="7808c-445">De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados.</span><span class="sxs-lookup"><span data-stu-id="7808c-445">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="7808c-446">En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="7808c-446">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="7808c-447">Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.</span><span class="sxs-lookup"><span data-stu-id="7808c-447">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="7808c-448">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:</span><span class="sxs-lookup"><span data-stu-id="7808c-448">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="7808c-449">Atributo</span><span class="sxs-lookup"><span data-stu-id="7808c-449">Attribute</span></span> | <span data-ttu-id="7808c-450">Descripción</span><span class="sxs-lookup"><span data-stu-id="7808c-450">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7808c-451">**incluír**</span><span class="sxs-lookup"><span data-stu-id="7808c-451">**include**</span></span> | <span data-ttu-id="7808c-452">(Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="7808c-452">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="7808c-453">La ruta de acceso es relativa a la `contentFiles` carpeta a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="7808c-453">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="7808c-454">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="7808c-454">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="7808c-455">**Excluir**</span><span class="sxs-lookup"><span data-stu-id="7808c-455">**exclude**</span></span> | <span data-ttu-id="7808c-456">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="7808c-456">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="7808c-457">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="7808c-457">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="7808c-458">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="7808c-458">**buildAction**</span></span> | <span data-ttu-id="7808c-459">Acción de compilación que se asigna al elemento de contenido de MSBuild, como `Content` , , , , `None` `Embedded Resource` `Compile` etc. El valor predeterminado es `Compile` .</span><span class="sxs-lookup"><span data-stu-id="7808c-459">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="7808c-460">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="7808c-460">**copyToOutput**</span></span> | <span data-ttu-id="7808c-461">Valor booleano que indica si se copian elementos de contenido en la carpeta de salida de compilación (o publicación).</span><span class="sxs-lookup"><span data-stu-id="7808c-461">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="7808c-462">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="7808c-462">The default is false.</span></span> |
| <span data-ttu-id="7808c-463">**flatten**</span><span class="sxs-lookup"><span data-stu-id="7808c-463">**flatten**</span></span> | <span data-ttu-id="7808c-464">Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false).</span><span class="sxs-lookup"><span data-stu-id="7808c-464">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="7808c-465">Esta marca solo funciona cuando la marca copyToOutput está establecida en true.</span><span class="sxs-lookup"><span data-stu-id="7808c-465">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="7808c-466">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="7808c-466">The default is false.</span></span> |

<span data-ttu-id="7808c-467">Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo.</span><span class="sxs-lookup"><span data-stu-id="7808c-467">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="7808c-468">Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas.</span><span class="sxs-lookup"><span data-stu-id="7808c-468">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="7808c-469">La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.</span><span class="sxs-lookup"><span data-stu-id="7808c-469">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="7808c-470">Estructura de carpetas de los paquetes</span><span class="sxs-lookup"><span data-stu-id="7808c-470">Package folder structure</span></span>

<span data-ttu-id="7808c-471">El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="7808c-471">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="7808c-472">`codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.</span><span class="sxs-lookup"><span data-stu-id="7808c-472">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="7808c-473">`TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="7808c-473">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="7808c-474">Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.</span><span class="sxs-lookup"><span data-stu-id="7808c-474">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="7808c-475">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7808c-475">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="7808c-476">Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7808c-476">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="7808c-477">Sección contentFiles de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7808c-477">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="7808c-478">Grupos de referencia de marco</span><span class="sxs-lookup"><span data-stu-id="7808c-478">Framework reference groups</span></span>

<span data-ttu-id="7808c-479">*Versión 5.1+ wih PackageReference solo*</span><span class="sxs-lookup"><span data-stu-id="7808c-479">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="7808c-480">Las referencias de marco son un concepto de .NET Core que representa marcos compartidos como WPF o Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="7808c-480">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="7808c-481">Al especificar un marco compartido, el paquete garantiza que todas sus dependencias de marco se incluyen en el proyecto de referencia.</span><span class="sxs-lookup"><span data-stu-id="7808c-481">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="7808c-482">Cada `<group>` elemento requiere un atributo y cero o más `targetFramework` `<frameworkReference>` elementos.</span><span class="sxs-lookup"><span data-stu-id="7808c-482">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="7808c-483">En el ejemplo siguiente se muestra un nuspec generado para un proyecto de WPF de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7808c-483">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="7808c-484">Tenga en cuenta que no se recomienda crear a mano elementos nuspec que contengan referencias de marco.</span><span class="sxs-lookup"><span data-stu-id="7808c-484">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="7808c-485">Considere la posibilidad de [usar el](msbuild-targets.md) paquete de destinos en su lugar, que los deducirá automáticamente del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7808c-485">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="7808c-486">Archivos nuspec de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7808c-486">Example nuspec files</span></span>

<span data-ttu-id="7808c-487">**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**</span><span class="sxs-lookup"><span data-stu-id="7808c-487">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="7808c-488">**Un archivo `.nuspec` con dependencias**</span><span class="sxs-lookup"><span data-stu-id="7808c-488">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="7808c-489">**Un archivo `.nuspec` con archivos**</span><span class="sxs-lookup"><span data-stu-id="7808c-489">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="7808c-490">**Un archivo `.nuspec` con ensamblados de plataforma**</span><span class="sxs-lookup"><span data-stu-id="7808c-490">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="7808c-491">En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:</span><span class="sxs-lookup"><span data-stu-id="7808c-491">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="7808c-492">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="7808c-492">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="7808c-493">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="7808c-493">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="7808c-494">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="7808c-494">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="7808c-495">Windows Phone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="7808c-495">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
