---
title: Referencia de .nuspec para NuGet
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: fd6ecab05a392a2a0b4ddf1ac15eb108f2653703
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842413"
---
# <a name="nuspec-reference"></a><span data-ttu-id="d63d7-103">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="d63d7-103">.nuspec reference</span></span>

<span data-ttu-id="d63d7-104">Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="d63d7-105">Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores.</span><span class="sxs-lookup"><span data-stu-id="d63d7-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="d63d7-106">El manifiesto siempre se incluye en un paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="d63d7-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="d63d7-107">In this topic:</span></span>

- [<span data-ttu-id="d63d7-108">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="d63d7-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="d63d7-109">[Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d63d7-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="d63d7-110">Dependencias</span><span class="sxs-lookup"><span data-stu-id="d63d7-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="d63d7-111">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="d63d7-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="d63d7-112">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="d63d7-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="d63d7-113">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="d63d7-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="d63d7-114">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="d63d7-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="d63d7-115">Archivos de ejemplo de nuspec</span><span class="sxs-lookup"><span data-stu-id="d63d7-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="d63d7-116">Compatibilidad del tipo de proyecto</span><span class="sxs-lookup"><span data-stu-id="d63d7-116">Project type compatibility</span></span>

- <span data-ttu-id="d63d7-117">Usar `.nuspec` con `nuget.exe pack` para el estilo de SDK que no son proyectos que usen `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="d63d7-118">Un `.nuspec` archivo no es necesario para crear paquetes para [proyectos del SDK de estilo](../resources/check-project-format.md) (normalmente, .NET Core y .NET Standard proyectos que usen el [atributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="d63d7-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="d63d7-119">(Tenga en cuenta que un `.nuspec` se genera cuando se crea el paquete.)</span><span class="sxs-lookup"><span data-stu-id="d63d7-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="d63d7-120">Si va a crear un paquete mediante `dotnet.exe pack` o `msbuild pack target`, se recomienda que se [incluyen todas las propiedades](../reference/msbuild-targets.md#pack-target) que están normalmente en el `.nuspec` de archivos en el archivo de proyecto en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d63d7-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="d63d7-121">Sin embargo, en su lugar, puede elegir a [utilizar un `.nuspec` archivo empaquetar mediante `dotnet.exe` o `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="d63d7-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="d63d7-122">Para los proyectos migran desde `packages.config` a [PackageReference](../consume-packages/package-references-in-project-files.md), un `.nuspec` archivo no es necesario para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="d63d7-123">En su lugar, use [paquete msbuild](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="d63d7-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="d63d7-124">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="d63d7-124">General form and schema</span></span>

<span data-ttu-id="d63d7-125">El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="d63d7-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="d63d7-126">En este esquema, los archivos `.nuspec` tienen el siguiente formato general:</span><span class="sxs-lookup"><span data-stu-id="d63d7-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="d63d7-127">Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="d63d7-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="d63d7-128">Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="d63d7-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="d63d7-129">En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):</span><span class="sxs-lookup"><span data-stu-id="d63d7-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="d63d7-131">Elementos de metadatos necesarios</span><span class="sxs-lookup"><span data-stu-id="d63d7-131">Required metadata elements</span></span>

<span data-ttu-id="d63d7-132">Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="d63d7-133">Estos elementos deben aparecer dentro de un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="d63d7-134">id</span><span class="sxs-lookup"><span data-stu-id="d63d7-134">id</span></span> 
<span data-ttu-id="d63d7-135">El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="d63d7-136">Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET.</span><span class="sxs-lookup"><span data-stu-id="d63d7-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="d63d7-137">Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="d63d7-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="d63d7-138">version</span><span class="sxs-lookup"><span data-stu-id="d63d7-138">version</span></span>
<span data-ttu-id="d63d7-139">La versión del paquete, siguiendo el patrón *mayor.menor.revisión*.</span><span class="sxs-lookup"><span data-stu-id="d63d7-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="d63d7-140">Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="d63d7-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="d63d7-141">description</span><span class="sxs-lookup"><span data-stu-id="d63d7-141">description</span></span>
<span data-ttu-id="d63d7-142">Una descripción larga del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="d63d7-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="d63d7-143">authors</span><span class="sxs-lookup"><span data-stu-id="d63d7-143">authors</span></span>
<span data-ttu-id="d63d7-144">Una lista separada por comas de los autores de los paquetes, que coinciden con los nombres de perfil de nuget.org. Estos se muestran en la galería de NuGet, en nuget.org, y se usan para hacer referencias cruzadas a paquetes de los mismos autores.</span><span class="sxs-lookup"><span data-stu-id="d63d7-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="d63d7-145">Elementos de metadatos opcionales</span><span class="sxs-lookup"><span data-stu-id="d63d7-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="d63d7-146">owners</span><span class="sxs-lookup"><span data-stu-id="d63d7-146">owners</span></span>
<span data-ttu-id="d63d7-147">Lista separada por comas de los creadores del paquete usando nombres de perfil en nuget.org. Suele ser la misma lista que en `authors` y se ignora al cargar el paquete en nuget.org. Vea [Administrar los propietarios de paquetes en nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="d63d7-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="d63d7-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="d63d7-148">projectUrl</span></span>
<span data-ttu-id="d63d7-149">Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d63d7-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="d63d7-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="d63d7-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="d63d7-151">licenseUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="d63d7-151">licenseUrl is being deprecated.</span></span> <span data-ttu-id="d63d7-152">Usar la licencia en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d63d7-152">Use license instead.</span></span>

<span data-ttu-id="d63d7-153">Una dirección URL de la licencia del paquete, a menudo se muestra en las interfaces de usuario como nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d63d7-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="d63d7-154">licencia</span><span class="sxs-lookup"><span data-stu-id="d63d7-154">license</span></span>
<span data-ttu-id="d63d7-155">Una expresión de la licencia SPDX o la ruta de acceso a un archivo de licencia dentro del paquete, a menudo se muestra en las interfaces de usuario como nuget.org. Si obtiene la licencia del paquete bajo una licencia comunes, como MIT o BSD cláusula 2, utilice asociado [identificador de licencia SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="d63d7-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="d63d7-156">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d63d7-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="d63d7-157">NuGet.org solo acepta expresiones de licencia que están aprobadas por la iniciativa de código fuente abierto o Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="d63d7-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="d63d7-158">Si el paquete con licencia bajo varias licencias común, puede especificar una licencia compuesto utilizando el [SPDX versión 2.0 de la sintaxis de expresión](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="d63d7-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="d63d7-159">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d63d7-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="d63d7-160">Si usa una licencia personalizada que no es compatible con expresiones de licencia, puede empaquetar un `.txt` o `.md` archivo con el texto de la licencia.</span><span class="sxs-lookup"><span data-stu-id="d63d7-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="d63d7-161">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d63d7-161">For example:</span></span>

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

<span data-ttu-id="d63d7-162">Para el equivalente en MSBuild, eche un vistazo a [empaquetado de una expresión de licencia o un archivo de licencia](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="d63d7-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="d63d7-163">Se describe en la sintaxis exacta de las expresiones de licencia de NuGet [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="d63d7-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="d63d7-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="d63d7-164">iconUrl</span></span>
<span data-ttu-id="d63d7-165">Dirección URL para una imagen de 64 x 64 con fondo transparente para usarla como icono para el paquete en la visualización de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="d63d7-165">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="d63d7-166">Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen.</span><span class="sxs-lookup"><span data-stu-id="d63d7-166">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="d63d7-167">Por ejemplo, para utilizar una imagen desde GitHub, use el archivo sin formato, como la dirección URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="d63d7-167">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="d63d7-168">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d63d7-168">requireLicenseAcceptance</span></span>
<span data-ttu-id="d63d7-169">Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="d63d7-169">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="d63d7-170">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="d63d7-170">developmentDependency</span></span>
<span data-ttu-id="d63d7-171">*(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="d63d7-171">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="d63d7-172">Con PackageReference (NuGet 4.8), esta marca también significa que excluirá los activos de tiempo de compilación de la compilación.</span><span class="sxs-lookup"><span data-stu-id="d63d7-172">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="d63d7-173">Consulte [DevelopmentDependency compatibilidad con PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="d63d7-173">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="d63d7-174">resumen</span><span class="sxs-lookup"><span data-stu-id="d63d7-174">summary</span></span>
<span data-ttu-id="d63d7-175">Descripción breve del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="d63d7-175">A short description of the package for UI display.</span></span> <span data-ttu-id="d63d7-176">Si se omite, se usará una versión truncada de `description`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-176">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="d63d7-177">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="d63d7-177">releaseNotes</span></span>
<span data-ttu-id="d63d7-178">*(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="d63d7-179">copyright</span><span class="sxs-lookup"><span data-stu-id="d63d7-179">copyright</span></span>
<span data-ttu-id="d63d7-180">*(1.5+)* Información de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-180">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="d63d7-181">language</span><span class="sxs-lookup"><span data-stu-id="d63d7-181">language</span></span>
<span data-ttu-id="d63d7-182">Identificador de configuración regional del paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-182">The locale ID for the package.</span></span> <span data-ttu-id="d63d7-183">Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d63d7-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="d63d7-184">tags</span><span class="sxs-lookup"><span data-stu-id="d63d7-184">tags</span></span>
<span data-ttu-id="d63d7-185">Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados.</span><span class="sxs-lookup"><span data-stu-id="d63d7-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="d63d7-186">serviceable</span><span class="sxs-lookup"><span data-stu-id="d63d7-186">serviceable</span></span> 
<span data-ttu-id="d63d7-187">*(3.3+)* Solo para uso interno de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d63d7-187">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="d63d7-188">repository</span><span class="sxs-lookup"><span data-stu-id="d63d7-188">repository</span></span>
<span data-ttu-id="d63d7-189">Repositorio de metadatos, que consta de cuatro atributos opcionales: *tipo* y *url* *(4.0 y versiones posteriores)* , y *rama* y  *confirmación* *(4.6 y versiones posteriores)* .</span><span class="sxs-lookup"><span data-stu-id="d63d7-189">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="d63d7-190">Estos atributos permiten asignar los archivos .nupkg en el repositorio que se crearon, con la posibilidad de obtener tal como se detalla como la rama individual o la confirmación de que se creó el paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-190">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="d63d7-191">Debe ser una dirección url disponible públicamente que se puede invocar directamente mediante un software de control de versión.</span><span class="sxs-lookup"><span data-stu-id="d63d7-191">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="d63d7-192">No debe ser una página html tal como está pensado para el equipo.</span><span class="sxs-lookup"><span data-stu-id="d63d7-192">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="d63d7-193">Para vincular a la página del proyecto, use el `projectUrl` campo, en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d63d7-193">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="d63d7-194">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="d63d7-194">minClientVersion</span></span>
<span data-ttu-id="d63d7-195">Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d63d7-195">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="d63d7-196">Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d63d7-196">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="d63d7-197">Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-197">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="d63d7-198">Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3".</span><span class="sxs-lookup"><span data-stu-id="d63d7-198">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="d63d7-199">Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-199">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="title"></a><span data-ttu-id="d63d7-200">title</span><span class="sxs-lookup"><span data-stu-id="d63d7-200">title</span></span>
<span data-ttu-id="d63d7-201">Muestra un título fácil de usar del paquete que se puede usar en alguna interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="d63d7-201">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="d63d7-202">(nuget.org y el Administrador de paquetes en Visual Studio no Mostrar título)</span><span class="sxs-lookup"><span data-stu-id="d63d7-202">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="d63d7-203">Elementos de colección</span><span class="sxs-lookup"><span data-stu-id="d63d7-203">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="d63d7-204">packageTypes</span><span class="sxs-lookup"><span data-stu-id="d63d7-204">packageTypes</span></span>
<span data-ttu-id="d63d7-205">*(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional.</span><span class="sxs-lookup"><span data-stu-id="d63d7-205">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="d63d7-206">Cada tipo de paquete tiene atributos de *name* y *version*.</span><span class="sxs-lookup"><span data-stu-id="d63d7-206">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="d63d7-207">Vea [Establecimiento de un tipo de paquete](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="d63d7-207">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="d63d7-208">dependencias</span><span class="sxs-lookup"><span data-stu-id="d63d7-208">dependencies</span></span>
<span data-ttu-id="d63d7-209">Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-209">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="d63d7-210">Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="d63d7-210">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="d63d7-211">Vea [Dependencias](#dependencies-element) a continuación.</span><span class="sxs-lookup"><span data-stu-id="d63d7-211">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="d63d7-212">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d63d7-212">frameworkAssemblies</span></span>
<span data-ttu-id="d63d7-213">*(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-213">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="d63d7-214">Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="d63d7-214">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="d63d7-215">Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación.</span><span class="sxs-lookup"><span data-stu-id="d63d7-215">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="d63d7-216">referencias</span><span class="sxs-lookup"><span data-stu-id="d63d7-216">references</span></span>
<span data-ttu-id="d63d7-217">*(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="d63d7-217">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="d63d7-218">Cada referencia tiene un atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="d63d7-218">Each reference has a *file* attribute.</span></span> <span data-ttu-id="d63d7-219">`<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-219">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="d63d7-220">Si se omite, se incluyen todas las referencias de `lib`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-220">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="d63d7-221">Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación.</span><span class="sxs-lookup"><span data-stu-id="d63d7-221">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="d63d7-222">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d63d7-222">contentFiles</span></span>
<span data-ttu-id="d63d7-223">*(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="d63d7-223">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="d63d7-224">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d63d7-224">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="d63d7-225">Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación.</span><span class="sxs-lookup"><span data-stu-id="d63d7-225">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="d63d7-226">files</span><span class="sxs-lookup"><span data-stu-id="d63d7-226">files</span></span> 
<span data-ttu-id="d63d7-227">El `<package>` nodo puede contener un `<files>` nodo como un elemento relacionado con `<metadata>`y un `<contentFiles>` elemento secundario bajo `<metadata>`, para especificar qué archivos de ensamblado y el contenido va a incluir en el paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-227">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="d63d7-228">Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.</span><span class="sxs-lookup"><span data-stu-id="d63d7-228">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="d63d7-229">Tokens de reemplazo</span><span class="sxs-lookup"><span data-stu-id="d63d7-229">Replacement tokens</span></span>

<span data-ttu-id="d63d7-230">Al crear un paquete, el [comando `nuget pack`](../tools/cli-ref-pack.md) reemplaza los tokens delimitados por $ en el nodo `<metadata>` del archivo `.nuspec` por valores procedentes de un archivo de proyecto o del conmutador `-properties` del comando `pack`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-230">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="d63d7-231">En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-231">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="d63d7-232">Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="d63d7-232">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="d63d7-233">Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="d63d7-233">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="d63d7-234">Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-234">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="d63d7-235">Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="d63d7-235">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="d63d7-236">Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares.</span><span class="sxs-lookup"><span data-stu-id="d63d7-236">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="d63d7-237">Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-237">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="d63d7-238">Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="d63d7-238">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="d63d7-239">Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d63d7-239">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="d63d7-240">Token</span><span class="sxs-lookup"><span data-stu-id="d63d7-240">Token</span></span> | <span data-ttu-id="d63d7-241">Origen del valor</span><span class="sxs-lookup"><span data-stu-id="d63d7-241">Value source</span></span> | <span data-ttu-id="d63d7-242">Valor</span><span class="sxs-lookup"><span data-stu-id="d63d7-242">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="d63d7-243">**$id$**</span><span class="sxs-lookup"><span data-stu-id="d63d7-243">**$id$**</span></span> | <span data-ttu-id="d63d7-244">Archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="d63d7-244">Project file</span></span> | <span data-ttu-id="d63d7-245">AssemblyName (título) del archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="d63d7-245">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="d63d7-246">**$version$**</span><span class="sxs-lookup"><span data-stu-id="d63d7-246">**$version$**</span></span> | <span data-ttu-id="d63d7-247">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d63d7-247">AssemblyInfo</span></span> | <span data-ttu-id="d63d7-248">AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="d63d7-248">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="d63d7-249">**$author$**</span><span class="sxs-lookup"><span data-stu-id="d63d7-249">**$author$**</span></span> | <span data-ttu-id="d63d7-250">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d63d7-250">AssemblyInfo</span></span> | <span data-ttu-id="d63d7-251">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="d63d7-251">AssemblyCompany</span></span> |
| <span data-ttu-id="d63d7-252">**$title$**</span><span class="sxs-lookup"><span data-stu-id="d63d7-252">**$title$**</span></span> | <span data-ttu-id="d63d7-253">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d63d7-253">AssemblyInfo</span></span> | <span data-ttu-id="d63d7-254">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="d63d7-254">AssemblyTitle</span></span> |
| <span data-ttu-id="d63d7-255">**$description$**</span><span class="sxs-lookup"><span data-stu-id="d63d7-255">**$description$**</span></span> | <span data-ttu-id="d63d7-256">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d63d7-256">AssemblyInfo</span></span> | <span data-ttu-id="d63d7-257">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="d63d7-257">AssemblyDescription</span></span> |
| <span data-ttu-id="d63d7-258">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="d63d7-258">**$copyright$**</span></span> | <span data-ttu-id="d63d7-259">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d63d7-259">AssemblyInfo</span></span> | <span data-ttu-id="d63d7-260">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="d63d7-260">AssemblyCopyright</span></span> |
| <span data-ttu-id="d63d7-261">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="d63d7-261">**$configuration$**</span></span> | <span data-ttu-id="d63d7-262">Archivo DLL del ensamblado</span><span class="sxs-lookup"><span data-stu-id="d63d7-262">Assembly DLL</span></span> | <span data-ttu-id="d63d7-263">Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar.</span><span class="sxs-lookup"><span data-stu-id="d63d7-263">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="d63d7-264">Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d63d7-264">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="d63d7-265">Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="d63d7-265">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="d63d7-266">Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual.</span><span class="sxs-lookup"><span data-stu-id="d63d7-266">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="d63d7-267">Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="d63d7-267">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="d63d7-268">Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:</span><span class="sxs-lookup"><span data-stu-id="d63d7-268">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="d63d7-269">Elemento de dependencias</span><span class="sxs-lookup"><span data-stu-id="d63d7-269">Dependencies element</span></span>

<span data-ttu-id="d63d7-270">El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="d63d7-270">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="d63d7-271">Los atributos de cada `<dependency>` son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d63d7-271">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="d63d7-272">Atributo</span><span class="sxs-lookup"><span data-stu-id="d63d7-272">Attribute</span></span> | <span data-ttu-id="d63d7-273">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="d63d7-273">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="d63d7-274">(Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-274">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="d63d7-275">(Obligatorio) Intervalo de versiones aceptable como dependencia.</span><span class="sxs-lookup"><span data-stu-id="d63d7-275">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="d63d7-276">Vea [Control de versiones de paquetes](../reference/package-versioning.md#version-ranges-and-wildcards) para consultar la sintaxis exacta.</span><span class="sxs-lookup"><span data-stu-id="d63d7-276">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="d63d7-277">include</span><span class="sxs-lookup"><span data-stu-id="d63d7-277">include</span></span> | <span data-ttu-id="d63d7-278">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="d63d7-278">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="d63d7-279">El valor predeterminado es `all`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-279">The default value is `all`.</span></span> |
| <span data-ttu-id="d63d7-280">exclude</span><span class="sxs-lookup"><span data-stu-id="d63d7-280">exclude</span></span> | <span data-ttu-id="d63d7-281">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="d63d7-281">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="d63d7-282">El valor predeterminado es `build,analyzers` que puede que se sobrescriban.</span><span class="sxs-lookup"><span data-stu-id="d63d7-282">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="d63d7-283">Pero `content/ ContentFiles` implícitamente también se excluyen en el paquete final que no se sobrescribe.</span><span class="sxs-lookup"><span data-stu-id="d63d7-283">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="d63d7-284">Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-284">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="d63d7-285">Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-285">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="d63d7-286">Etiqueta Include o Exclude</span><span class="sxs-lookup"><span data-stu-id="d63d7-286">Include/Exclude tag</span></span> | <span data-ttu-id="d63d7-287">Carpetas afectadas del destino</span><span class="sxs-lookup"><span data-stu-id="d63d7-287">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="d63d7-288">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d63d7-288">contentFiles</span></span> | <span data-ttu-id="d63d7-289">Contenido</span><span class="sxs-lookup"><span data-stu-id="d63d7-289">Content</span></span> |
| <span data-ttu-id="d63d7-290">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="d63d7-290">runtime</span></span> | <span data-ttu-id="d63d7-291">Runtime, Resources y FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d63d7-291">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="d63d7-292">compile</span><span class="sxs-lookup"><span data-stu-id="d63d7-292">compile</span></span> | <span data-ttu-id="d63d7-293">lib</span><span class="sxs-lookup"><span data-stu-id="d63d7-293">lib</span></span> |
| <span data-ttu-id="d63d7-294">compilación</span><span class="sxs-lookup"><span data-stu-id="d63d7-294">build</span></span> | <span data-ttu-id="d63d7-295">build (propiedades y destinos de MSBuild)</span><span class="sxs-lookup"><span data-stu-id="d63d7-295">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="d63d7-296">nativas</span><span class="sxs-lookup"><span data-stu-id="d63d7-296">native</span></span> | <span data-ttu-id="d63d7-297">nativas</span><span class="sxs-lookup"><span data-stu-id="d63d7-297">native</span></span> |
| <span data-ttu-id="d63d7-298">ninguna</span><span class="sxs-lookup"><span data-stu-id="d63d7-298">none</span></span> | <span data-ttu-id="d63d7-299">Sin carpetas</span><span class="sxs-lookup"><span data-stu-id="d63d7-299">No folders</span></span> |
| <span data-ttu-id="d63d7-300">todo</span><span class="sxs-lookup"><span data-stu-id="d63d7-300">all</span></span> | <span data-ttu-id="d63d7-301">Todas las carpetas</span><span class="sxs-lookup"><span data-stu-id="d63d7-301">All folders</span></span> |

<span data-ttu-id="d63d7-302">Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="d63d7-302">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="d63d7-303">Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-303">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="d63d7-304">Nota: Al crear un `.nuspec` desde un proyecto mediante `nuget spec`, las dependencias que existen en ese proyecto se incluyen automáticamente en el cuadro `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="d63d7-304">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="d63d7-305">Grupos de dependencia</span><span class="sxs-lookup"><span data-stu-id="d63d7-305">Dependency groups</span></span>

<span data-ttu-id="d63d7-306">*Versión 2.0+*</span><span class="sxs-lookup"><span data-stu-id="d63d7-306">*Version 2.0+*</span></span>

<span data-ttu-id="d63d7-307">Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-307">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="d63d7-308">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-308">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="d63d7-309">Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d63d7-309">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d63d7-310">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias.</span><span class="sxs-lookup"><span data-stu-id="d63d7-310">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="d63d7-311">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="d63d7-311">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d63d7-312">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="d63d7-312">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d63d7-313">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="d63d7-313">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="d63d7-314">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="d63d7-314">Explicit assembly references</span></span>

<span data-ttu-id="d63d7-315">El `<references>` elemento se usa en proyectos que usen `packages.config` especificar explícitamente los ensamblados que debe hacer referencia en el proyecto de destino cuando se usa el paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-315">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="d63d7-316">Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="d63d7-316">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="d63d7-317">Para obtener más información, vea la página en [seleccionar ensamblados referenciados por proyectos](../create-packages/select-assemblies-referenced-by-projects.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="d63d7-317">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="d63d7-318">Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:</span><span class="sxs-lookup"><span data-stu-id="d63d7-318">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="d63d7-319">Grupos de referencias</span><span class="sxs-lookup"><span data-stu-id="d63d7-319">Reference groups</span></span>

<span data-ttu-id="d63d7-320">Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-320">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="d63d7-321">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-321">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="d63d7-322">Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d63d7-322">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d63d7-323">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias.</span><span class="sxs-lookup"><span data-stu-id="d63d7-323">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="d63d7-324">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="d63d7-324">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d63d7-325">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="d63d7-325">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d63d7-326">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="d63d7-326">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="d63d7-327">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="d63d7-327">Framework assembly references</span></span>

<span data-ttu-id="d63d7-328">Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo.</span><span class="sxs-lookup"><span data-stu-id="d63d7-328">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="d63d7-329">Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias.</span><span class="sxs-lookup"><span data-stu-id="d63d7-329">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="d63d7-330">Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-330">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="d63d7-331">El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="d63d7-331">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="d63d7-332">Atributo</span><span class="sxs-lookup"><span data-stu-id="d63d7-332">Attribute</span></span> | <span data-ttu-id="d63d7-333">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="d63d7-333">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d63d7-334">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="d63d7-334">**assemblyName**</span></span> | <span data-ttu-id="d63d7-335">(Obligatorio) Nombre completo del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="d63d7-335">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="d63d7-336">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="d63d7-336">**targetFramework**</span></span> | <span data-ttu-id="d63d7-337">(Opcional) Especifica la plataforma de destino a la que se aplica esta referencia.</span><span class="sxs-lookup"><span data-stu-id="d63d7-337">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="d63d7-338">Si se omite, indica que la referencia se aplica a todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="d63d7-338">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="d63d7-339">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="d63d7-339">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="d63d7-340">En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="d63d7-340">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="d63d7-341">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="d63d7-341">Including assembly files</span></span>

<span data-ttu-id="d63d7-342">Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-342">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="d63d7-343">El comando `nuget pack` selecciona automáticamente los archivos necesarios.</span><span class="sxs-lookup"><span data-stu-id="d63d7-343">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="d63d7-344">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados.</span><span class="sxs-lookup"><span data-stu-id="d63d7-344">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="d63d7-345">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-345">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="d63d7-346">Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente.</span><span class="sxs-lookup"><span data-stu-id="d63d7-346">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="d63d7-347">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d63d7-347">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="d63d7-348">Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="d63d7-348">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="d63d7-349">Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d63d7-349">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="d63d7-350">Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="d63d7-350">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="d63d7-351">Atributos del elemento File</span><span class="sxs-lookup"><span data-stu-id="d63d7-351">File element attributes</span></span>

<span data-ttu-id="d63d7-352">Cada elemento `<file>` especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="d63d7-352">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="d63d7-353">Atributo</span><span class="sxs-lookup"><span data-stu-id="d63d7-353">Attribute</span></span> | <span data-ttu-id="d63d7-354">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="d63d7-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d63d7-355">**src**</span><span class="sxs-lookup"><span data-stu-id="d63d7-355">**src**</span></span> | <span data-ttu-id="d63d7-356">Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-356">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d63d7-357">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="d63d7-357">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d63d7-358">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="d63d7-358">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d63d7-359">**target**</span><span class="sxs-lookup"><span data-stu-id="d63d7-359">**target**</span></span> | <span data-ttu-id="d63d7-360">La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-360">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="d63d7-361">Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones).</span><span class="sxs-lookup"><span data-stu-id="d63d7-361">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="d63d7-362">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d63d7-362">**exclude**</span></span> | <span data-ttu-id="d63d7-363">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-363">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d63d7-364">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="d63d7-364">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="d63d7-365">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d63d7-365">Examples</span></span>

<span data-ttu-id="d63d7-366">**Ensamblado único**</span><span class="sxs-lookup"><span data-stu-id="d63d7-366">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="d63d7-367">**Ensamblado único específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="d63d7-367">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="d63d7-368">**Conjunto de archivos DLL que usan un carácter comodín**</span><span class="sxs-lookup"><span data-stu-id="d63d7-368">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="d63d7-369">**Archivos DLL para distintas plataformas**</span><span class="sxs-lookup"><span data-stu-id="d63d7-369">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="d63d7-370">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="d63d7-370">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="d63d7-371">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="d63d7-371">Including content files</span></span>

<span data-ttu-id="d63d7-372">Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="d63d7-372">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="d63d7-373">Como son inmutables, no se prevé que el proyecto de consumo los modifique.</span><span class="sxs-lookup"><span data-stu-id="d63d7-373">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="d63d7-374">Entre los archivos de contenido se encuentran los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d63d7-374">Example content files include:</span></span>

- <span data-ttu-id="d63d7-375">Imágenes que se insertan como recursos</span><span class="sxs-lookup"><span data-stu-id="d63d7-375">Images that are embedded as resources</span></span>
- <span data-ttu-id="d63d7-376">Archivos de código fuente que ya están compilados</span><span class="sxs-lookup"><span data-stu-id="d63d7-376">Source files that are already compiled</span></span>
- <span data-ttu-id="d63d7-377">Scripts que se deben incluir con la salida de la compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="d63d7-377">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="d63d7-378">Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto</span><span class="sxs-lookup"><span data-stu-id="d63d7-378">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="d63d7-379">Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-379">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="d63d7-380">Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d63d7-380">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="d63d7-381">Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.</span><span class="sxs-lookup"><span data-stu-id="d63d7-381">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="d63d7-382">Usar el elemento files para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="d63d7-382">Using the files element for content files</span></span>

<span data-ttu-id="d63d7-383">En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="d63d7-383">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="d63d7-384">**Archivos de contenido básicos**</span><span class="sxs-lookup"><span data-stu-id="d63d7-384">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="d63d7-385">**Archivos de contenido con estructura de directorios**</span><span class="sxs-lookup"><span data-stu-id="d63d7-385">**Content files with directory structure**</span></span>

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

<span data-ttu-id="d63d7-386">**Archivo de contenido específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="d63d7-386">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="d63d7-387">**Archivo de contenido copiado en una carpeta con un punto en el nombre**</span><span class="sxs-lookup"><span data-stu-id="d63d7-387">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="d63d7-388">En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:</span><span class="sxs-lookup"><span data-stu-id="d63d7-388">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="d63d7-389">**Archivos de contenido sin extensión**</span><span class="sxs-lookup"><span data-stu-id="d63d7-389">**Content files without extensions**</span></span>

<span data-ttu-id="d63d7-390">Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="d63d7-390">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="d63d7-391">**Archivos de contenido con una ruta de acceso y un destino profundos**</span><span class="sxs-lookup"><span data-stu-id="d63d7-391">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="d63d7-392">En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:</span><span class="sxs-lookup"><span data-stu-id="d63d7-392">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="d63d7-393">**Cambiar el nombre de un archivo de contenido del paquete**</span><span class="sxs-lookup"><span data-stu-id="d63d7-393">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="d63d7-394">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="d63d7-394">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="d63d7-395">Usar el elemento contentFiles para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="d63d7-395">Using the contentFiles element for content files</span></span>

<span data-ttu-id="d63d7-396">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="d63d7-396">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="d63d7-397">De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados.</span><span class="sxs-lookup"><span data-stu-id="d63d7-397">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="d63d7-398">En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-398">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="d63d7-399">Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.</span><span class="sxs-lookup"><span data-stu-id="d63d7-399">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="d63d7-400">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:</span><span class="sxs-lookup"><span data-stu-id="d63d7-400">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="d63d7-401">Atributo</span><span class="sxs-lookup"><span data-stu-id="d63d7-401">Attribute</span></span> | <span data-ttu-id="d63d7-402">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="d63d7-402">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d63d7-403">**include**</span><span class="sxs-lookup"><span data-stu-id="d63d7-403">**include**</span></span> | <span data-ttu-id="d63d7-404">(Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-404">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d63d7-405">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="d63d7-405">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d63d7-406">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="d63d7-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d63d7-407">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d63d7-407">**exclude**</span></span> | <span data-ttu-id="d63d7-408">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-408">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d63d7-409">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="d63d7-409">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d63d7-410">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="d63d7-410">**buildAction**</span></span> | <span data-ttu-id="d63d7-411">Acción de compilación que se debe asignar al elemento de contenido para MSBuild, como `Content`, `None`, `Embedded Resource`, `Compile`, etc. El valor predeterminado es `Compile`.</span><span class="sxs-lookup"><span data-stu-id="d63d7-411">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="d63d7-412">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="d63d7-412">**copyToOutput**</span></span> | <span data-ttu-id="d63d7-413">Un valor booleano que indica si se va a copiar los elementos de contenido a la compilación de carpeta de salida (o publicar).</span><span class="sxs-lookup"><span data-stu-id="d63d7-413">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="d63d7-414">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="d63d7-414">The default is false.</span></span> |
| <span data-ttu-id="d63d7-415">**flatten**</span><span class="sxs-lookup"><span data-stu-id="d63d7-415">**flatten**</span></span> | <span data-ttu-id="d63d7-416">Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false).</span><span class="sxs-lookup"><span data-stu-id="d63d7-416">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="d63d7-417">Esta marca solo funciona cuando la marca copyToOutput está establecida en true.</span><span class="sxs-lookup"><span data-stu-id="d63d7-417">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="d63d7-418">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="d63d7-418">The default is false.</span></span> |

<span data-ttu-id="d63d7-419">Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo.</span><span class="sxs-lookup"><span data-stu-id="d63d7-419">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="d63d7-420">Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas.</span><span class="sxs-lookup"><span data-stu-id="d63d7-420">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="d63d7-421">La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.</span><span class="sxs-lookup"><span data-stu-id="d63d7-421">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="d63d7-422">Estructura de carpetas de los paquetes</span><span class="sxs-lookup"><span data-stu-id="d63d7-422">Package folder structure</span></span>

<span data-ttu-id="d63d7-423">El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="d63d7-423">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="d63d7-424">`codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.</span><span class="sxs-lookup"><span data-stu-id="d63d7-424">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="d63d7-425">`TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="d63d7-425">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="d63d7-426">Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.</span><span class="sxs-lookup"><span data-stu-id="d63d7-426">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="d63d7-427">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d63d7-427">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="d63d7-428">Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d63d7-428">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="d63d7-429">Sección contentFiles de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d63d7-429">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="d63d7-430">Archivos de ejemplo de nuspec</span><span class="sxs-lookup"><span data-stu-id="d63d7-430">Example nuspec files</span></span>

<span data-ttu-id="d63d7-431">**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**</span><span class="sxs-lookup"><span data-stu-id="d63d7-431">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="d63d7-432">**Un archivo `.nuspec` con dependencias**</span><span class="sxs-lookup"><span data-stu-id="d63d7-432">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="d63d7-433">**Un archivo `.nuspec` con archivos**</span><span class="sxs-lookup"><span data-stu-id="d63d7-433">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="d63d7-434">**Un archivo `.nuspec` con ensamblados de plataforma**</span><span class="sxs-lookup"><span data-stu-id="d63d7-434">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="d63d7-435">En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:</span><span class="sxs-lookup"><span data-stu-id="d63d7-435">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="d63d7-436">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d63d7-436">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="d63d7-437">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d63d7-437">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="d63d7-438">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="d63d7-438">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="d63d7-439">Windows Phone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="d63d7-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
