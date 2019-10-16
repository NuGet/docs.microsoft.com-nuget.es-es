---
title: Referencia del archivo. nuspec para NuGet
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6bd730db16d8e8783f0d949bb04cf3b52c642cd0
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380551"
---
# <a name="nuspec-reference"></a><span data-ttu-id="f8af9-103">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="f8af9-103">.nuspec reference</span></span>

<span data-ttu-id="f8af9-104">Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="f8af9-105">Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores.</span><span class="sxs-lookup"><span data-stu-id="f8af9-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="f8af9-106">El manifiesto siempre se incluye en un paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="f8af9-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="f8af9-107">In this topic:</span></span>

- [<span data-ttu-id="f8af9-108">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="f8af9-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="f8af9-109">[Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f8af9-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="f8af9-110">Dependencias</span><span class="sxs-lookup"><span data-stu-id="f8af9-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="f8af9-111">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="f8af9-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="f8af9-112">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="f8af9-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="f8af9-113">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="f8af9-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="f8af9-114">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="f8af9-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="f8af9-115">Archivos nuspec de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f8af9-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="f8af9-116">Compatibilidad de tipos de proyecto</span><span class="sxs-lookup"><span data-stu-id="f8af9-116">Project type compatibility</span></span>

- <span data-ttu-id="f8af9-117">Use `.nuspec` con `nuget.exe pack` para proyectos que no sean de estilo SDK y que utilicen `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="f8af9-118">No es necesario un archivo `.nuspec` para crear paquetes para los [proyectos de estilo SDK](../resources/check-project-format.md) (normalmente, los proyectos de .net Core y .net Standard que usan el [atributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="f8af9-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="f8af9-119">(Tenga en cuenta que se genera un `.nuspec` al crear el paquete).</span><span class="sxs-lookup"><span data-stu-id="f8af9-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="f8af9-120">Si va a crear un paquete con `dotnet.exe pack` o `msbuild pack target`, se recomienda [incluir todas las propiedades](../reference/msbuild-targets.md#pack-target) que normalmente están en el archivo `.nuspec` en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8af9-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="f8af9-121">Sin embargo, en su lugar, puede elegir [usar un archivo `.nuspec` para empaquetar con `dotnet.exe` o `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="f8af9-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="f8af9-122">En el caso de los proyectos migrados de `packages.config` a [PackageReference](../consume-packages/package-references-in-project-files.md), no es necesario un archivo `.nuspec` para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="f8af9-123">En su lugar, use [msbuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="f8af9-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="f8af9-124">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="f8af9-124">General form and schema</span></span>

<span data-ttu-id="f8af9-125">El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="f8af9-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="f8af9-126">En este esquema, los archivos `.nuspec` tienen el siguiente formato general:</span><span class="sxs-lookup"><span data-stu-id="f8af9-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="f8af9-127">Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="f8af9-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="f8af9-128">Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="f8af9-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="f8af9-129">En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):</span><span class="sxs-lookup"><span data-stu-id="f8af9-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="f8af9-131">Elementos de metadatos necesarios</span><span class="sxs-lookup"><span data-stu-id="f8af9-131">Required metadata elements</span></span>

<span data-ttu-id="f8af9-132">Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="f8af9-133">Estos elementos deben aparecer dentro de un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="f8af9-134">identificador</span><span class="sxs-lookup"><span data-stu-id="f8af9-134">id</span></span> 
<span data-ttu-id="f8af9-135">El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="f8af9-136">Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET.</span><span class="sxs-lookup"><span data-stu-id="f8af9-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="f8af9-137">Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="f8af9-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="f8af9-138">version</span><span class="sxs-lookup"><span data-stu-id="f8af9-138">version</span></span>
<span data-ttu-id="f8af9-139">La versión del paquete, siguiendo el patrón *mayor.menor.revisión*.</span><span class="sxs-lookup"><span data-stu-id="f8af9-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="f8af9-140">Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="f8af9-140">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="f8af9-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="f8af9-141">description</span></span>
<span data-ttu-id="f8af9-142">Descripción del paquete para la presentación de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="f8af9-142">A description of the package for UI display.</span></span>
#### <a name="authors"></a><span data-ttu-id="f8af9-143">authors</span><span class="sxs-lookup"><span data-stu-id="f8af9-143">authors</span></span>
<span data-ttu-id="f8af9-144">Una lista separada por comas de autores de paquetes, que coincide con los nombres de perfil en nuget.org. Estos se muestran en la galería de NuGet en nuget.org y se usan para hacer referencias cruzadas de paquetes por los mismos autores.</span><span class="sxs-lookup"><span data-stu-id="f8af9-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="f8af9-145">Elementos de metadatos opcionales</span><span class="sxs-lookup"><span data-stu-id="f8af9-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="f8af9-146">owners</span><span class="sxs-lookup"><span data-stu-id="f8af9-146">owners</span></span>
<span data-ttu-id="f8af9-147">Lista separada por comas de los creadores de paquetes que usan nombres de perfil en nuget.org. Esta suele ser la misma lista que en `authors` y se omite al cargar el paquete en nuget.org. Consulte [Administración de propietarios de paquetes en Nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="f8af9-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="f8af9-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="f8af9-148">projectUrl</span></span>
<span data-ttu-id="f8af9-149">Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f8af9-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="f8af9-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="f8af9-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="f8af9-151">licenseUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="f8af9-151">licenseUrl is deprecated.</span></span> <span data-ttu-id="f8af9-152">Use la licencia en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f8af9-152">Use license instead.</span></span>

<span data-ttu-id="f8af9-153">Una dirección URL para la licencia del paquete, que a menudo se muestra en ius como nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f8af9-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="f8af9-154">sin</span><span class="sxs-lookup"><span data-stu-id="f8af9-154">license</span></span>
<span data-ttu-id="f8af9-155">Una expresión de licencia de SPDX o una ruta de acceso a un archivo de licencia dentro del paquete, que a menudo se muestra en ius como nuget.org. Si tiene licencia para el paquete con una licencia común, como MIT o la cláusula BSD-2, use el identificador de [licencia de SPDX](https://spdx.org/licenses/)asociado.</span><span class="sxs-lookup"><span data-stu-id="f8af9-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="f8af9-156">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8af9-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="f8af9-157">NuGet.org solo acepta expresiones de licencia aprobadas por la iniciativa de código abierto o la Fundación gratuita de software.</span><span class="sxs-lookup"><span data-stu-id="f8af9-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="f8af9-158">Si el paquete tiene licencia con varias licencias comunes, puede especificar una licencia compuesta mediante la [Sintaxis de expresión SPDX versión 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="f8af9-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="f8af9-159">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8af9-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="f8af9-160">Si usa una licencia personalizada que no es compatible con las expresiones de licencia, puede empaquetar un archivo `.txt` o `.md` con el texto de la licencia.</span><span class="sxs-lookup"><span data-stu-id="f8af9-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="f8af9-161">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8af9-161">For example:</span></span>

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

<span data-ttu-id="f8af9-162">En el caso del equivalente de MSBuild, eche un vistazo a [empaquetar una expresión de licencia o un archivo de licencia](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="f8af9-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="f8af9-163">A continuación se describe la sintaxis exacta de las expresiones de licencia de NuGet en [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="f8af9-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="f8af9-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="f8af9-164">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="f8af9-165">el iconUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="f8af9-165">iconUrl is deprecated.</span></span> <span data-ttu-id="f8af9-166">En su lugar, use el icono.</span><span class="sxs-lookup"><span data-stu-id="f8af9-166">Use icon instead.</span></span>

<span data-ttu-id="f8af9-167">Dirección URL para una imagen de 64 x 64 con fondo transparente para usarla como icono para el paquete en la visualización de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="f8af9-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="f8af9-168">Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen.</span><span class="sxs-lookup"><span data-stu-id="f8af9-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="f8af9-169">Por ejemplo, para usar una imagen de GitHub, use la dirección URL de archivo sin formato, como <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="f8af9-169">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
#### <a name="icon"></a><span data-ttu-id="f8af9-170">Icono</span><span class="sxs-lookup"><span data-stu-id="f8af9-170">icon</span></span>

<span data-ttu-id="f8af9-171">Es una ruta de acceso a un archivo de imagen dentro del paquete, que a menudo se muestra en ius como nuget.org como el icono de paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-171">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="f8af9-172">El tamaño del archivo de imagen está limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="f8af9-172">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="f8af9-173">Entre los formatos de archivo admitidos se incluyen JPEG y PNG.</span><span class="sxs-lookup"><span data-stu-id="f8af9-173">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="f8af9-174">Se recomienda una imagen resoulution de 64 x 64.</span><span class="sxs-lookup"><span data-stu-id="f8af9-174">We recommend an image resoulution of 64x64.</span></span>

<span data-ttu-id="f8af9-175">Por ejemplo, debe agregar lo siguiente a su archivo nuspec al crear un paquete con Nuget. exe:</span><span class="sxs-lookup"><span data-stu-id="f8af9-175">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="f8af9-176">Icono de paquete de ejemplo de nuspec.</span><span class="sxs-lookup"><span data-stu-id="f8af9-176">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="f8af9-177">Para el equivalente de MSBuild, eche un vistazo a [empaquetar un archivo de imagen de icono](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="f8af9-177">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="f8af9-178">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f8af9-178">requireLicenseAcceptance</span></span>
<span data-ttu-id="f8af9-179">Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="f8af9-179">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="f8af9-180">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="f8af9-180">developmentDependency</span></span>
<span data-ttu-id="f8af9-181">*(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="f8af9-181">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="f8af9-182">Con PackageReference (NuGet 4.8 +), esta marca también significa que excluirá los recursos en tiempo de compilación de la compilación.</span><span class="sxs-lookup"><span data-stu-id="f8af9-182">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="f8af9-183">Consulte [compatibilidad con DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="f8af9-183">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="f8af9-184">resumen</span><span class="sxs-lookup"><span data-stu-id="f8af9-184">summary</span></span>
> [!Important]
> <span data-ttu-id="f8af9-185">`summary` está en desuso.</span><span class="sxs-lookup"><span data-stu-id="f8af9-185">`summary` is being deprecated.</span></span> <span data-ttu-id="f8af9-186">Utilice `description` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f8af9-186">Use `description` instead.</span></span>

<span data-ttu-id="f8af9-187">Descripción breve del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="f8af9-187">A short description of the package for UI display.</span></span> <span data-ttu-id="f8af9-188">Si se omite, se usará una versión truncada de `description`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-188">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="f8af9-189">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="f8af9-189">releaseNotes</span></span>
<span data-ttu-id="f8af9-190">*(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-190">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="f8af9-191">copyright</span><span class="sxs-lookup"><span data-stu-id="f8af9-191">copyright</span></span>
<span data-ttu-id="f8af9-192">*(1.5+)* Información de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-192">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="f8af9-193">lenguaje</span><span class="sxs-lookup"><span data-stu-id="f8af9-193">language</span></span>
<span data-ttu-id="f8af9-194">Identificador de configuración regional del paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-194">The locale ID for the package.</span></span> <span data-ttu-id="f8af9-195">Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f8af9-195">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="f8af9-196">etiquetas</span><span class="sxs-lookup"><span data-stu-id="f8af9-196">tags</span></span>
<span data-ttu-id="f8af9-197">Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados.</span><span class="sxs-lookup"><span data-stu-id="f8af9-197">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="f8af9-198">reparables por</span><span class="sxs-lookup"><span data-stu-id="f8af9-198">serviceable</span></span> 
<span data-ttu-id="f8af9-199">*(3.3+)* Solo para uso interno de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8af9-199">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="f8af9-200">repositorio</span><span class="sxs-lookup"><span data-stu-id="f8af9-200">repository</span></span>
<span data-ttu-id="f8af9-201">Metadatos del repositorio, que constan de cuatro atributos opcionales: `type` y `url` *(4.0 +)* , y `branch` y `commit` *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="f8af9-201">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="f8af9-202">Estos atributos le permiten asignar el `.nupkg` al repositorio que lo compiló, con la posibilidad de obtener el valor de nombre de rama individual y/o el hash de SHA-1 de confirmación que compiló el paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-202">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="f8af9-203">Debe ser una dirección URL disponible públicamente que un software de control de versiones pueda invocar directamente.</span><span class="sxs-lookup"><span data-stu-id="f8af9-203">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="f8af9-204">No debe ser una página HTML, ya que está destinada al equipo.</span><span class="sxs-lookup"><span data-stu-id="f8af9-204">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="f8af9-205">Para vincular a la página del proyecto, use el campo `projectUrl`, en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f8af9-205">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="f8af9-206">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8af9-206">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a><span data-ttu-id="f8af9-207">título</span><span class="sxs-lookup"><span data-stu-id="f8af9-207">title</span></span>
<span data-ttu-id="f8af9-208">Título descriptivo del paquete que se puede usar en algunas pantallas de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="f8af9-208">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="f8af9-209">(nuget.org y el administrador de paquetes en Visual Studio no muestran el título)</span><span class="sxs-lookup"><span data-stu-id="f8af9-209">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="f8af9-210">Elementos de colección</span><span class="sxs-lookup"><span data-stu-id="f8af9-210">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="f8af9-211">Elemento packagetypes</span><span class="sxs-lookup"><span data-stu-id="f8af9-211">packageTypes</span></span>
<span data-ttu-id="f8af9-212">*(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional.</span><span class="sxs-lookup"><span data-stu-id="f8af9-212">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="f8af9-213">Cada tipo de paquete tiene atributos de *name* y *version*.</span><span class="sxs-lookup"><span data-stu-id="f8af9-213">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="f8af9-214">Vea [Establecimiento de un tipo de paquete](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="f8af9-214">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="f8af9-215">dependencias</span><span class="sxs-lookup"><span data-stu-id="f8af9-215">dependencies</span></span>
<span data-ttu-id="f8af9-216">Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-216">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="f8af9-217">Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="f8af9-217">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="f8af9-218">Vea [Dependencias](#dependencies-element) a continuación.</span><span class="sxs-lookup"><span data-stu-id="f8af9-218">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="f8af9-219">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="f8af9-219">frameworkAssemblies</span></span>
<span data-ttu-id="f8af9-220">*(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-220">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="f8af9-221">Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="f8af9-221">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="f8af9-222">Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación.</span><span class="sxs-lookup"><span data-stu-id="f8af9-222">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="f8af9-223">referencias</span><span class="sxs-lookup"><span data-stu-id="f8af9-223">references</span></span>
<span data-ttu-id="f8af9-224">*(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8af9-224">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="f8af9-225">Cada referencia tiene un atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="f8af9-225">Each reference has a *file* attribute.</span></span> <span data-ttu-id="f8af9-226">`<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-226">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="f8af9-227">Si se omite, se incluyen todas las referencias de `lib`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-227">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="f8af9-228">Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación.</span><span class="sxs-lookup"><span data-stu-id="f8af9-228">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="f8af9-229">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f8af9-229">contentFiles</span></span>
<span data-ttu-id="f8af9-230">*(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="f8af9-230">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="f8af9-231">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8af9-231">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="f8af9-232">Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación.</span><span class="sxs-lookup"><span data-stu-id="f8af9-232">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="f8af9-233">archivos</span><span class="sxs-lookup"><span data-stu-id="f8af9-233">files</span></span> 
<span data-ttu-id="f8af9-234">El nodo `<package>` puede contener un nodo `<files>` como un elemento relacionado con `<metadata>` y un elemento secundario `<contentFiles>` en `<metadata>`, para especificar qué archivos de ensamblado y de contenido se van a incluir en el paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-234">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="f8af9-235">Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.</span><span class="sxs-lookup"><span data-stu-id="f8af9-235">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="f8af9-236">atributos de metadatos</span><span class="sxs-lookup"><span data-stu-id="f8af9-236">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="f8af9-237">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="f8af9-237">minClientVersion</span></span>
<span data-ttu-id="f8af9-238">Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8af9-238">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="f8af9-239">Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8af9-239">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="f8af9-240">Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-240">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="f8af9-241">Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3".</span><span class="sxs-lookup"><span data-stu-id="f8af9-241">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="f8af9-242">Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-242">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
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

## <a name="replacement-tokens"></a><span data-ttu-id="f8af9-243">Tokens de reemplazo</span><span class="sxs-lookup"><span data-stu-id="f8af9-243">Replacement tokens</span></span>

<span data-ttu-id="f8af9-244">Al crear un paquete, el [comando `nuget pack`](../reference/cli-reference/cli-ref-pack.md) reemplaza los tokens delimitados por $ en el nodo `<metadata>` del archivo `.nuspec` por valores procedentes de un archivo de proyecto o del conmutador `-properties` del comando `pack`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-244">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="f8af9-245">En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-245">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="f8af9-246">Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="f8af9-246">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="f8af9-247">Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="f8af9-247">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="f8af9-248">Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-248">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="f8af9-249">Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="f8af9-249">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="f8af9-250">Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares.</span><span class="sxs-lookup"><span data-stu-id="f8af9-250">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="f8af9-251">Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-251">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="f8af9-252">Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="f8af9-252">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="f8af9-253">Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="f8af9-253">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="f8af9-254">Token</span><span class="sxs-lookup"><span data-stu-id="f8af9-254">Token</span></span> | <span data-ttu-id="f8af9-255">Origen del valor</span><span class="sxs-lookup"><span data-stu-id="f8af9-255">Value source</span></span> | <span data-ttu-id="f8af9-256">Valor</span><span class="sxs-lookup"><span data-stu-id="f8af9-256">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="f8af9-257">**$id$**</span><span class="sxs-lookup"><span data-stu-id="f8af9-257">**$id$**</span></span> | <span data-ttu-id="f8af9-258">Archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="f8af9-258">Project file</span></span> | <span data-ttu-id="f8af9-259">AssemblyName (title) del archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="f8af9-259">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="f8af9-260">**$version$**</span><span class="sxs-lookup"><span data-stu-id="f8af9-260">**$version$**</span></span> | <span data-ttu-id="f8af9-261">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f8af9-261">AssemblyInfo</span></span> | <span data-ttu-id="f8af9-262">AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="f8af9-262">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="f8af9-263">**$author$**</span><span class="sxs-lookup"><span data-stu-id="f8af9-263">**$author$**</span></span> | <span data-ttu-id="f8af9-264">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f8af9-264">AssemblyInfo</span></span> | <span data-ttu-id="f8af9-265">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="f8af9-265">AssemblyCompany</span></span> |
| <span data-ttu-id="f8af9-266">**$title $**</span><span class="sxs-lookup"><span data-stu-id="f8af9-266">**$title$**</span></span> | <span data-ttu-id="f8af9-267">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f8af9-267">AssemblyInfo</span></span> | <span data-ttu-id="f8af9-268">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="f8af9-268">AssemblyTitle</span></span> |
| <span data-ttu-id="f8af9-269">**$description$**</span><span class="sxs-lookup"><span data-stu-id="f8af9-269">**$description$**</span></span> | <span data-ttu-id="f8af9-270">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f8af9-270">AssemblyInfo</span></span> | <span data-ttu-id="f8af9-271">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="f8af9-271">AssemblyDescription</span></span> |
| <span data-ttu-id="f8af9-272">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="f8af9-272">**$copyright$**</span></span> | <span data-ttu-id="f8af9-273">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f8af9-273">AssemblyInfo</span></span> | <span data-ttu-id="f8af9-274">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="f8af9-274">AssemblyCopyright</span></span> |
| <span data-ttu-id="f8af9-275">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="f8af9-275">**$configuration$**</span></span> | <span data-ttu-id="f8af9-276">Archivo DLL del ensamblado</span><span class="sxs-lookup"><span data-stu-id="f8af9-276">Assembly DLL</span></span> | <span data-ttu-id="f8af9-277">Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar.</span><span class="sxs-lookup"><span data-stu-id="f8af9-277">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="f8af9-278">Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="f8af9-278">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="f8af9-279">Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="f8af9-279">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="f8af9-280">Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual.</span><span class="sxs-lookup"><span data-stu-id="f8af9-280">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="f8af9-281">Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="f8af9-281">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="f8af9-282">Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8af9-282">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="f8af9-283">Elemento Dependencies</span><span class="sxs-lookup"><span data-stu-id="f8af9-283">Dependencies element</span></span>

<span data-ttu-id="f8af9-284">El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="f8af9-284">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="f8af9-285">Los atributos de cada `<dependency>` son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8af9-285">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="f8af9-286">Atributo</span><span class="sxs-lookup"><span data-stu-id="f8af9-286">Attribute</span></span> | <span data-ttu-id="f8af9-287">Descripción</span><span class="sxs-lookup"><span data-stu-id="f8af9-287">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="f8af9-288">(Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-288">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="f8af9-289">(Obligatorio) Intervalo de versiones aceptable como dependencia.</span><span class="sxs-lookup"><span data-stu-id="f8af9-289">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="f8af9-290">Vea [Control de versiones de paquetes](../concepts/package-versioning.md#version-ranges-and-wildcards) para consultar la sintaxis exacta.</span><span class="sxs-lookup"><span data-stu-id="f8af9-290">See [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> <span data-ttu-id="f8af9-291">No se admiten las versiones de carácter comodín (flotante).</span><span class="sxs-lookup"><span data-stu-id="f8af9-291">Wildcard (floating) versions are not supported.</span></span> |
| <span data-ttu-id="f8af9-292">include</span><span class="sxs-lookup"><span data-stu-id="f8af9-292">include</span></span> | <span data-ttu-id="f8af9-293">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="f8af9-293">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="f8af9-294">El valor predeterminado es `all`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-294">The default value is `all`.</span></span> |
| <span data-ttu-id="f8af9-295">exclude</span><span class="sxs-lookup"><span data-stu-id="f8af9-295">exclude</span></span> | <span data-ttu-id="f8af9-296">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="f8af9-296">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="f8af9-297">El valor predeterminado es `build,analyzers` que se puede sobrescribir.</span><span class="sxs-lookup"><span data-stu-id="f8af9-297">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="f8af9-298">Pero `content/ ContentFiles` también se excluyen implícitamente en el paquete final que no se puede sobrescribir.</span><span class="sxs-lookup"><span data-stu-id="f8af9-298">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="f8af9-299">Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-299">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="f8af9-300">Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-300">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="f8af9-301">Etiqueta Include o Exclude</span><span class="sxs-lookup"><span data-stu-id="f8af9-301">Include/Exclude tag</span></span> | <span data-ttu-id="f8af9-302">Carpetas afectadas del destino</span><span class="sxs-lookup"><span data-stu-id="f8af9-302">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="f8af9-303">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f8af9-303">contentFiles</span></span> | <span data-ttu-id="f8af9-304">Contenido</span><span class="sxs-lookup"><span data-stu-id="f8af9-304">Content</span></span> |
| <span data-ttu-id="f8af9-305">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="f8af9-305">runtime</span></span> | <span data-ttu-id="f8af9-306">Runtime, Resources y FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="f8af9-306">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="f8af9-307">compile</span><span class="sxs-lookup"><span data-stu-id="f8af9-307">compile</span></span> | <span data-ttu-id="f8af9-308">lib</span><span class="sxs-lookup"><span data-stu-id="f8af9-308">lib</span></span> |
| <span data-ttu-id="f8af9-309">compilación</span><span class="sxs-lookup"><span data-stu-id="f8af9-309">build</span></span> | <span data-ttu-id="f8af9-310">build (propiedades y destinos de MSBuild)</span><span class="sxs-lookup"><span data-stu-id="f8af9-310">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="f8af9-311">nativas</span><span class="sxs-lookup"><span data-stu-id="f8af9-311">native</span></span> | <span data-ttu-id="f8af9-312">nativas</span><span class="sxs-lookup"><span data-stu-id="f8af9-312">native</span></span> |
| <span data-ttu-id="f8af9-313">ninguna</span><span class="sxs-lookup"><span data-stu-id="f8af9-313">none</span></span> | <span data-ttu-id="f8af9-314">Sin carpetas</span><span class="sxs-lookup"><span data-stu-id="f8af9-314">No folders</span></span> |
| <span data-ttu-id="f8af9-315">todo</span><span class="sxs-lookup"><span data-stu-id="f8af9-315">all</span></span> | <span data-ttu-id="f8af9-316">Todas las carpetas</span><span class="sxs-lookup"><span data-stu-id="f8af9-316">All folders</span></span> |

<span data-ttu-id="f8af9-317">Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="f8af9-317">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="f8af9-318">Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-318">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="f8af9-319">Al crear un `.nuspec` desde un proyecto con `nuget spec`, las dependencias que existen en ese proyecto no se incluyen automáticamente en el archivo @no__t 2 resultante.</span><span class="sxs-lookup"><span data-stu-id="f8af9-319">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="f8af9-320">En su lugar, use `nuget pack myproject.csproj` y obtenga el archivo *. nuspec* en el archivo *. nupkg* generado.</span><span class="sxs-lookup"><span data-stu-id="f8af9-320">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="f8af9-321">Este archivo *. nuspec* contiene las dependencias.</span><span class="sxs-lookup"><span data-stu-id="f8af9-321">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="f8af9-322">Grupos de dependencia</span><span class="sxs-lookup"><span data-stu-id="f8af9-322">Dependency groups</span></span>

<span data-ttu-id="f8af9-323">*Versión 2.0+*</span><span class="sxs-lookup"><span data-stu-id="f8af9-323">*Version 2.0+*</span></span>

<span data-ttu-id="f8af9-324">Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-324">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="f8af9-325">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-325">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="f8af9-326">Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8af9-326">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="f8af9-327">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias.</span><span class="sxs-lookup"><span data-stu-id="f8af9-327">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="f8af9-328">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="f8af9-328">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="f8af9-329">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="f8af9-329">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="f8af9-330">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="f8af9-330">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="f8af9-331">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="f8af9-331">Explicit assembly references</span></span>

<span data-ttu-id="f8af9-332">Los proyectos utilizan el elemento `<references>` con `packages.config` para especificar explícitamente los ensamblados a los que debe hacer referencia el proyecto de destino al utilizar el paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-332">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="f8af9-333">Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="f8af9-333">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="f8af9-334">Para obtener más información, vea la página de [selección de ensamblados a los que se hace referencia en proyectos](../create-packages/select-assemblies-referenced-by-projects.md) .</span><span class="sxs-lookup"><span data-stu-id="f8af9-334">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="f8af9-335">Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:</span><span class="sxs-lookup"><span data-stu-id="f8af9-335">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="f8af9-336">Grupos de referencias</span><span class="sxs-lookup"><span data-stu-id="f8af9-336">Reference groups</span></span>

<span data-ttu-id="f8af9-337">Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-337">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="f8af9-338">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-338">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="f8af9-339">Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8af9-339">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="f8af9-340">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias.</span><span class="sxs-lookup"><span data-stu-id="f8af9-340">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="f8af9-341">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="f8af9-341">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="f8af9-342">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="f8af9-342">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="f8af9-343">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="f8af9-343">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="f8af9-344">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="f8af9-344">Framework assembly references</span></span>

<span data-ttu-id="f8af9-345">Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo.</span><span class="sxs-lookup"><span data-stu-id="f8af9-345">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="f8af9-346">Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias.</span><span class="sxs-lookup"><span data-stu-id="f8af9-346">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="f8af9-347">Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-347">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="f8af9-348">El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="f8af9-348">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="f8af9-349">Atributo</span><span class="sxs-lookup"><span data-stu-id="f8af9-349">Attribute</span></span> | <span data-ttu-id="f8af9-350">Descripción</span><span class="sxs-lookup"><span data-stu-id="f8af9-350">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8af9-351">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="f8af9-351">**assemblyName**</span></span> | <span data-ttu-id="f8af9-352">(Obligatorio) Nombre completo del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="f8af9-352">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="f8af9-353">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="f8af9-353">**targetFramework**</span></span> | <span data-ttu-id="f8af9-354">(Opcional) Especifica la plataforma de destino a la que se aplica esta referencia.</span><span class="sxs-lookup"><span data-stu-id="f8af9-354">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="f8af9-355">Si se omite, indica que la referencia se aplica a todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="f8af9-355">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="f8af9-356">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="f8af9-356">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="f8af9-357">En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="f8af9-357">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="f8af9-358">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="f8af9-358">Including assembly files</span></span>

<span data-ttu-id="f8af9-359">Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-359">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="f8af9-360">El comando `nuget pack` selecciona automáticamente los archivos necesarios.</span><span class="sxs-lookup"><span data-stu-id="f8af9-360">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="f8af9-361">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados.</span><span class="sxs-lookup"><span data-stu-id="f8af9-361">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="f8af9-362">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-362">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="f8af9-363">Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente.</span><span class="sxs-lookup"><span data-stu-id="f8af9-363">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="f8af9-364">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8af9-364">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="f8af9-365">Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="f8af9-365">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="f8af9-366">Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f8af9-366">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="f8af9-367">Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="f8af9-367">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="f8af9-368">Atributos del elemento File</span><span class="sxs-lookup"><span data-stu-id="f8af9-368">File element attributes</span></span>

<span data-ttu-id="f8af9-369">Cada elemento `<file>` especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="f8af9-369">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="f8af9-370">Atributo</span><span class="sxs-lookup"><span data-stu-id="f8af9-370">Attribute</span></span> | <span data-ttu-id="f8af9-371">Descripción</span><span class="sxs-lookup"><span data-stu-id="f8af9-371">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8af9-372">**src**</span><span class="sxs-lookup"><span data-stu-id="f8af9-372">**src**</span></span> | <span data-ttu-id="f8af9-373">Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-373">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="f8af9-374">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="f8af9-374">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="f8af9-375">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="f8af9-375">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="f8af9-376">**target**</span><span class="sxs-lookup"><span data-stu-id="f8af9-376">**target**</span></span> | <span data-ttu-id="f8af9-377">La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-377">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="f8af9-378">Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones).</span><span class="sxs-lookup"><span data-stu-id="f8af9-378">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="f8af9-379">**exclude**</span><span class="sxs-lookup"><span data-stu-id="f8af9-379">**exclude**</span></span> | <span data-ttu-id="f8af9-380">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-380">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="f8af9-381">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="f8af9-381">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="f8af9-382">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f8af9-382">Examples</span></span>

<span data-ttu-id="f8af9-383">**Ensamblado único**</span><span class="sxs-lookup"><span data-stu-id="f8af9-383">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="f8af9-384">**Ensamblado único específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="f8af9-384">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="f8af9-385">**Conjunto de archivos DLL que usan un carácter comodín**</span><span class="sxs-lookup"><span data-stu-id="f8af9-385">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="f8af9-386">**Archivos DLL para distintas plataformas**</span><span class="sxs-lookup"><span data-stu-id="f8af9-386">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="f8af9-387">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="f8af9-387">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="f8af9-388">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="f8af9-388">Including content files</span></span>

<span data-ttu-id="f8af9-389">Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8af9-389">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="f8af9-390">Como son inmutables, no se prevé que el proyecto de consumo los modifique.</span><span class="sxs-lookup"><span data-stu-id="f8af9-390">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="f8af9-391">Entre los archivos de contenido se encuentran los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8af9-391">Example content files include:</span></span>

- <span data-ttu-id="f8af9-392">Imágenes que se insertan como recursos</span><span class="sxs-lookup"><span data-stu-id="f8af9-392">Images that are embedded as resources</span></span>
- <span data-ttu-id="f8af9-393">Archivos de código fuente que ya están compilados</span><span class="sxs-lookup"><span data-stu-id="f8af9-393">Source files that are already compiled</span></span>
- <span data-ttu-id="f8af9-394">Scripts que se deben incluir con la salida de la compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="f8af9-394">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="f8af9-395">Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto</span><span class="sxs-lookup"><span data-stu-id="f8af9-395">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="f8af9-396">Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-396">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="f8af9-397">Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f8af9-397">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="f8af9-398">Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.</span><span class="sxs-lookup"><span data-stu-id="f8af9-398">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="f8af9-399">Usar el elemento files para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="f8af9-399">Using the files element for content files</span></span>

<span data-ttu-id="f8af9-400">En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="f8af9-400">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="f8af9-401">**Archivos de contenido básicos**</span><span class="sxs-lookup"><span data-stu-id="f8af9-401">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="f8af9-402">**Archivos de contenido con estructura de directorios**</span><span class="sxs-lookup"><span data-stu-id="f8af9-402">**Content files with directory structure**</span></span>

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

<span data-ttu-id="f8af9-403">**Archivo de contenido específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="f8af9-403">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="f8af9-404">**Archivo de contenido copiado en una carpeta con un punto en el nombre**</span><span class="sxs-lookup"><span data-stu-id="f8af9-404">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="f8af9-405">En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:</span><span class="sxs-lookup"><span data-stu-id="f8af9-405">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="f8af9-406">**Archivos de contenido sin extensión**</span><span class="sxs-lookup"><span data-stu-id="f8af9-406">**Content files without extensions**</span></span>

<span data-ttu-id="f8af9-407">Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="f8af9-407">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="f8af9-408">**Archivos de contenido con una ruta de acceso y un destino profundos**</span><span class="sxs-lookup"><span data-stu-id="f8af9-408">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="f8af9-409">En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:</span><span class="sxs-lookup"><span data-stu-id="f8af9-409">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="f8af9-410">**Cambiar el nombre de un archivo de contenido del paquete**</span><span class="sxs-lookup"><span data-stu-id="f8af9-410">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="f8af9-411">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="f8af9-411">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="f8af9-412">Usar el elemento contentFiles para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="f8af9-412">Using the contentFiles element for content files</span></span>

<span data-ttu-id="f8af9-413">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="f8af9-413">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="f8af9-414">De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados.</span><span class="sxs-lookup"><span data-stu-id="f8af9-414">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="f8af9-415">En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-415">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="f8af9-416">Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.</span><span class="sxs-lookup"><span data-stu-id="f8af9-416">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="f8af9-417">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:</span><span class="sxs-lookup"><span data-stu-id="f8af9-417">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="f8af9-418">Atributo</span><span class="sxs-lookup"><span data-stu-id="f8af9-418">Attribute</span></span> | <span data-ttu-id="f8af9-419">Descripción</span><span class="sxs-lookup"><span data-stu-id="f8af9-419">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8af9-420">**include**</span><span class="sxs-lookup"><span data-stu-id="f8af9-420">**include**</span></span> | <span data-ttu-id="f8af9-421">(Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-421">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="f8af9-422">La ruta de acceso es relativa a la carpeta `contentFiles` a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="f8af9-422">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="f8af9-423">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="f8af9-423">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="f8af9-424">**exclude**</span><span class="sxs-lookup"><span data-stu-id="f8af9-424">**exclude**</span></span> | <span data-ttu-id="f8af9-425">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-425">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="f8af9-426">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="f8af9-426">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="f8af9-427">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="f8af9-427">**buildAction**</span></span> | <span data-ttu-id="f8af9-428">Acción de compilación que se va a asignar al elemento de contenido de MSBuild, como `Content`, `None`, `Embedded Resource`, `Compile`, etc. El valor predeterminado es `Compile`.</span><span class="sxs-lookup"><span data-stu-id="f8af9-428">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="f8af9-429">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="f8af9-429">**copyToOutput**</span></span> | <span data-ttu-id="f8af9-430">Un valor booleano que indica si se deben copiar los elementos de contenido en la carpeta de salida de compilación (o publicación).</span><span class="sxs-lookup"><span data-stu-id="f8af9-430">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="f8af9-431">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="f8af9-431">The default is false.</span></span> |
| <span data-ttu-id="f8af9-432">**flatten**</span><span class="sxs-lookup"><span data-stu-id="f8af9-432">**flatten**</span></span> | <span data-ttu-id="f8af9-433">Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false).</span><span class="sxs-lookup"><span data-stu-id="f8af9-433">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="f8af9-434">Esta marca solo funciona cuando la marca copyToOutput está establecida en true.</span><span class="sxs-lookup"><span data-stu-id="f8af9-434">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="f8af9-435">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="f8af9-435">The default is false.</span></span> |

<span data-ttu-id="f8af9-436">Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo.</span><span class="sxs-lookup"><span data-stu-id="f8af9-436">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="f8af9-437">Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas.</span><span class="sxs-lookup"><span data-stu-id="f8af9-437">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="f8af9-438">La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.</span><span class="sxs-lookup"><span data-stu-id="f8af9-438">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="f8af9-439">Estructura de carpetas de los paquetes</span><span class="sxs-lookup"><span data-stu-id="f8af9-439">Package folder structure</span></span>

<span data-ttu-id="f8af9-440">El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="f8af9-440">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="f8af9-441">`codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.</span><span class="sxs-lookup"><span data-stu-id="f8af9-441">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="f8af9-442">`TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="f8af9-442">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="f8af9-443">Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.</span><span class="sxs-lookup"><span data-stu-id="f8af9-443">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="f8af9-444">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8af9-444">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="f8af9-445">Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8af9-445">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="f8af9-446">Sección contentFiles de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f8af9-446">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="f8af9-447">Archivos nuspec de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f8af9-447">Example nuspec files</span></span>

<span data-ttu-id="f8af9-448">**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**</span><span class="sxs-lookup"><span data-stu-id="f8af9-448">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="f8af9-449">**Un archivo `.nuspec` con dependencias**</span><span class="sxs-lookup"><span data-stu-id="f8af9-449">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="f8af9-450">**Un archivo `.nuspec` con archivos**</span><span class="sxs-lookup"><span data-stu-id="f8af9-450">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="f8af9-451">**Un archivo `.nuspec` con ensamblados de plataforma**</span><span class="sxs-lookup"><span data-stu-id="f8af9-451">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="f8af9-452">En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:</span><span class="sxs-lookup"><span data-stu-id="f8af9-452">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="f8af9-453">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="f8af9-453">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="f8af9-454">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="f8af9-454">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="f8af9-455">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="f8af9-455">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="f8af9-456">Windows Phone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="f8af9-456">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
