---
title: Referencia de .nuspec para NuGet
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: e4c57c0580fe9018703291c08d60e559f95183dc
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426205"
---
# <a name="nuspec-reference"></a><span data-ttu-id="e7b00-103">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="e7b00-103">.nuspec reference</span></span>

<span data-ttu-id="e7b00-104">Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="e7b00-105">Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores.</span><span class="sxs-lookup"><span data-stu-id="e7b00-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="e7b00-106">El manifiesto siempre se incluye en un paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="e7b00-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="e7b00-107">In this topic:</span></span>

- [<span data-ttu-id="e7b00-108">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="e7b00-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="e7b00-109">[Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e7b00-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="e7b00-110">Dependencias</span><span class="sxs-lookup"><span data-stu-id="e7b00-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="e7b00-111">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="e7b00-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="e7b00-112">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="e7b00-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="e7b00-113">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="e7b00-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="e7b00-114">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="e7b00-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="e7b00-115">Archivos de ejemplo de nuspec</span><span class="sxs-lookup"><span data-stu-id="e7b00-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="e7b00-116">Compatibilidad del tipo de proyecto</span><span class="sxs-lookup"><span data-stu-id="e7b00-116">Project type compatibility</span></span>

- <span data-ttu-id="e7b00-117">Usar `.nuspec` con `nuget.exe pack` para el estilo de SDK que no son proyectos que usen `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="e7b00-118">Un `.nuspec` archivo no es necesario para crear paquetes para los proyectos de SDK de estilo (.NET Core y .NET Standard, los proyectos que utilizan el [atributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="e7b00-118">A `.nuspec` file is not required to create packages for SDK-style projects (.NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="e7b00-119">(Tenga en cuenta que un `.nuspec` se genera cuando se crea el paquete.)</span><span class="sxs-lookup"><span data-stu-id="e7b00-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="e7b00-120">Si va a crear un paquete mediante `dotnet.exe pack` o `msbuild pack target`, se recomienda que se [incluyen todas las propiedades](../reference/msbuild-targets.md#pack-target) que están normalmente en el `.nuspec` de archivos en el archivo de proyecto en su lugar.</span><span class="sxs-lookup"><span data-stu-id="e7b00-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="e7b00-121">Sin embargo, en su lugar, puede elegir a [utilizar un `.nuspec` archivo empaquetar mediante `dotnet.exe` o `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="e7b00-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="e7b00-122">Para los proyectos migran desde `packages.config` a [PackageReference](../consume-packages/package-references-in-project-files.md), un `.nuspec` archivo no es necesario para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="e7b00-123">En su lugar, use [paquete msbuild](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="e7b00-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="e7b00-124">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="e7b00-124">General form and schema</span></span>

<span data-ttu-id="e7b00-125">El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="e7b00-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="e7b00-126">En este esquema, los archivos `.nuspec` tienen el siguiente formato general:</span><span class="sxs-lookup"><span data-stu-id="e7b00-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="e7b00-127">Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="e7b00-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="e7b00-128">Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="e7b00-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="e7b00-129">En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):</span><span class="sxs-lookup"><span data-stu-id="e7b00-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="e7b00-131">Elementos de metadatos necesarios</span><span class="sxs-lookup"><span data-stu-id="e7b00-131">Required metadata elements</span></span>

<span data-ttu-id="e7b00-132">Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="e7b00-133">Estos elementos deben aparecer dentro de un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="e7b00-134">id</span><span class="sxs-lookup"><span data-stu-id="e7b00-134">id</span></span> 
<span data-ttu-id="e7b00-135">El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="e7b00-136">Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET.</span><span class="sxs-lookup"><span data-stu-id="e7b00-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="e7b00-137">Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="e7b00-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="e7b00-138">version</span><span class="sxs-lookup"><span data-stu-id="e7b00-138">version</span></span>
<span data-ttu-id="e7b00-139">La versión del paquete, siguiendo el patrón *mayor.menor.revisión*.</span><span class="sxs-lookup"><span data-stu-id="e7b00-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="e7b00-140">Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="e7b00-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="e7b00-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7b00-141">description</span></span>
<span data-ttu-id="e7b00-142">Una descripción larga del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="e7b00-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="e7b00-143">authors</span><span class="sxs-lookup"><span data-stu-id="e7b00-143">authors</span></span>
<span data-ttu-id="e7b00-144">Una lista separada por comas de los autores de los paquetes, que coinciden con los nombres de perfil de nuget.org. Estos se muestran en la galería de NuGet, en nuget.org, y se usan para hacer referencias cruzadas a paquetes de los mismos autores.</span><span class="sxs-lookup"><span data-stu-id="e7b00-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="e7b00-145">Elementos de metadatos opcionales</span><span class="sxs-lookup"><span data-stu-id="e7b00-145">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="e7b00-146">título</span><span class="sxs-lookup"><span data-stu-id="e7b00-146">title</span></span>
<span data-ttu-id="e7b00-147">Un título fácil de usar del paquete, que se usa normalmente en las visualizaciones de la interfaz de usuario, como en nuget.org, y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e7b00-147">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="e7b00-148">Si no se especifica, se usa el identificador del paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-148">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="e7b00-149">owners</span><span class="sxs-lookup"><span data-stu-id="e7b00-149">owners</span></span>
<span data-ttu-id="e7b00-150">Lista separada por comas de los creadores del paquete usando nombres de perfil en nuget.org. Suele ser la misma lista que en `authors` y se ignora al cargar el paquete en nuget.org. Vea [Administrar los propietarios de paquetes en nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="e7b00-150">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="e7b00-151">projectUrl</span><span class="sxs-lookup"><span data-stu-id="e7b00-151">projectUrl</span></span>
<span data-ttu-id="e7b00-152">Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e7b00-152">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="e7b00-153">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="e7b00-153">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="e7b00-154">licenseUrl está en desuso.</span><span class="sxs-lookup"><span data-stu-id="e7b00-154">licenseUrl is being deprecated.</span></span> <span data-ttu-id="e7b00-155">Usar la licencia en su lugar.</span><span class="sxs-lookup"><span data-stu-id="e7b00-155">Use license instead.</span></span>

<span data-ttu-id="e7b00-156">Dirección URL de la licencia del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e7b00-156">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="license"></a><span data-ttu-id="e7b00-157">licencia</span><span class="sxs-lookup"><span data-stu-id="e7b00-157">license</span></span>
<span data-ttu-id="e7b00-158">Expresión de licencia SPDX o ruta de acceso a un archivo de licencia dentro del paquete, que con frecuencia también se muestra en la interfaz de usuario como nuget.org. Si obtiene la licencia del paquete bajo una licencia comunes como BSD-2-Clause o MIT, use el identificador de licencia SPDX asociado.</span><span class="sxs-lookup"><span data-stu-id="e7b00-158">An SPDX license expression or path to a license file within the package, often shown in UI displays as well as nuget.org. If you’re licensing the package under a common license such as BSD-2-Clause or MIT, use the associated SPDX license identifier.</span></span><br><span data-ttu-id="e7b00-159">Por ejemplo: `<license type="expression">MIT</license>`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-159">For example: `<license type="expression">MIT</license>`</span></span>

<span data-ttu-id="e7b00-160">Esta es la lista completa de [identificadores de licencia SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="e7b00-160">Here is the complete list of [SPDX license identifiers](https://spdx.org/licenses/).</span></span> <span data-ttu-id="e7b00-161">NuGet.org acepta solo licencias aprobadas de OSI o FSF cuando se usa la expresión de tipo de licencia.</span><span class="sxs-lookup"><span data-stu-id="e7b00-161">NuGet.org accepts only OSI or FSF approved licenses when using license type expression.</span></span>

<span data-ttu-id="e7b00-162">Si el paquete con licencia bajo varias licencias común, puede especificar una licencia compuesto utilizando el [SPDX versión 2.0 de la sintaxis de expresión](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="e7b00-162">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span><br><span data-ttu-id="e7b00-163">Por ejemplo: `<license type="expression">BSD-2-Clause OR MIT</license>`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-163">For example: `<license type="expression">BSD-2-Clause OR MIT</license>`</span></span>

<span data-ttu-id="e7b00-164">Si usa una licencia que no se ha asignado un identificador SPDX, o se trata de una licencia personalizada, puede empaquetar un archivo (solo `.txt` o `.md`) con el texto de la licencia.</span><span class="sxs-lookup"><span data-stu-id="e7b00-164">If you are using a license that hasn’t been assigned an SPDX identifier, or it is a custom license, you can package a file (only `.txt` or `.md`) with the license text.</span></span> <span data-ttu-id="e7b00-165">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e7b00-165">For example:</span></span>
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

<span data-ttu-id="e7b00-166">Para el equivalente en MSBuild, eche un vistazo a [empaquetado de una expresión de licencia o un archivo de licencia](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="e7b00-166">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="e7b00-167">Se describe en la sintaxis exacta de las expresiones de licencia de NuGet [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="e7b00-167">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="e7b00-168">iconUrl</span><span class="sxs-lookup"><span data-stu-id="e7b00-168">iconUrl</span></span>
<span data-ttu-id="e7b00-169">Dirección URL para una imagen de 64 x 64 con fondo transparente para usarla como icono para el paquete en la visualización de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="e7b00-169">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="e7b00-170">Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen.</span><span class="sxs-lookup"><span data-stu-id="e7b00-170">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="e7b00-171">Por ejemplo, para utilizar una imagen desde GitHub, use el archivo sin formato, como la dirección URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="e7b00-171">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="e7b00-172">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e7b00-172">requireLicenseAcceptance</span></span>
<span data-ttu-id="e7b00-173">Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="e7b00-173">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="e7b00-174">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="e7b00-174">developmentDependency</span></span>
<span data-ttu-id="e7b00-175">*(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="e7b00-175">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="e7b00-176">Con PackageReference (NuGet 4.8), esta marca también significa que excluirá los activos de tiempo de compilación de la compilación.</span><span class="sxs-lookup"><span data-stu-id="e7b00-176">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="e7b00-177">Consulte [DevelopmentDependency compatibilidad con PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="e7b00-177">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>
#### <a name="summary"></a><span data-ttu-id="e7b00-178">resumen</span><span class="sxs-lookup"><span data-stu-id="e7b00-178">summary</span></span>
<span data-ttu-id="e7b00-179">Descripción breve del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="e7b00-179">A short description of the package for UI display.</span></span> <span data-ttu-id="e7b00-180">Si se omite, se usará una versión truncada de `description`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-180">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="e7b00-181">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="e7b00-181">releaseNotes</span></span>
<span data-ttu-id="e7b00-182">*(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-182">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="e7b00-183">copyright</span><span class="sxs-lookup"><span data-stu-id="e7b00-183">copyright</span></span>
<span data-ttu-id="e7b00-184">*(1.5+)* Información de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-184">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="e7b00-185">lenguaje</span><span class="sxs-lookup"><span data-stu-id="e7b00-185">language</span></span>
<span data-ttu-id="e7b00-186">Identificador de configuración regional del paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-186">The locale ID for the package.</span></span> <span data-ttu-id="e7b00-187">Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e7b00-187">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="e7b00-188">etiquetas</span><span class="sxs-lookup"><span data-stu-id="e7b00-188">tags</span></span>
<span data-ttu-id="e7b00-189">Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados.</span><span class="sxs-lookup"><span data-stu-id="e7b00-189">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="e7b00-190">serviceable</span><span class="sxs-lookup"><span data-stu-id="e7b00-190">serviceable</span></span> 
<span data-ttu-id="e7b00-191">*(3.3+)* Solo para uso interno de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e7b00-191">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="e7b00-192">repositorio</span><span class="sxs-lookup"><span data-stu-id="e7b00-192">repository</span></span>
<span data-ttu-id="e7b00-193">Repositorio de metadatos, que consta de cuatro atributos opcionales: *tipo* y *url* *(4.0 y versiones posteriores)* , y *rama* y  *confirmación* *(4.6 y versiones posteriores)* .</span><span class="sxs-lookup"><span data-stu-id="e7b00-193">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="e7b00-194">Estos atributos permiten asignar los archivos .nupkg en el repositorio que se crearon, con la posibilidad de obtener tal como se detalla como la rama individual o la confirmación de que se creó el paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-194">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="e7b00-195">Debe ser una dirección url disponible públicamente que se puede invocar directamente mediante un software de control de versión.</span><span class="sxs-lookup"><span data-stu-id="e7b00-195">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="e7b00-196">No debe ser una página html tal como está pensado para el equipo.</span><span class="sxs-lookup"><span data-stu-id="e7b00-196">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="e7b00-197">Para vincular a la página del proyecto, use el `projectUrl` campo, en su lugar.</span><span class="sxs-lookup"><span data-stu-id="e7b00-197">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="e7b00-198">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="e7b00-198">minClientVersion</span></span>
<span data-ttu-id="e7b00-199">Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e7b00-199">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="e7b00-200">Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e7b00-200">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="e7b00-201">Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-201">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="e7b00-202">Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3".</span><span class="sxs-lookup"><span data-stu-id="e7b00-202">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="e7b00-203">Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-203">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="e7b00-204">Elementos de colección</span><span class="sxs-lookup"><span data-stu-id="e7b00-204">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="e7b00-205">packageTypes</span><span class="sxs-lookup"><span data-stu-id="e7b00-205">packageTypes</span></span>
<span data-ttu-id="e7b00-206">*(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional.</span><span class="sxs-lookup"><span data-stu-id="e7b00-206">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="e7b00-207">Cada tipo de paquete tiene atributos de *name* y *version*.</span><span class="sxs-lookup"><span data-stu-id="e7b00-207">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="e7b00-208">Vea [Establecimiento de un tipo de paquete](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="e7b00-208">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="e7b00-209">dependencias</span><span class="sxs-lookup"><span data-stu-id="e7b00-209">dependencies</span></span>
<span data-ttu-id="e7b00-210">Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-210">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="e7b00-211">Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="e7b00-211">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="e7b00-212">Vea [Dependencias](#dependencies-element) a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7b00-212">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="e7b00-213">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="e7b00-213">frameworkAssemblies</span></span>
<span data-ttu-id="e7b00-214">*(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-214">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="e7b00-215">Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="e7b00-215">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="e7b00-216">Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7b00-216">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="e7b00-217">referencias</span><span class="sxs-lookup"><span data-stu-id="e7b00-217">references</span></span>
<span data-ttu-id="e7b00-218">*(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="e7b00-218">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="e7b00-219">Cada referencia tiene un atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="e7b00-219">Each reference has a *file* attribute.</span></span> <span data-ttu-id="e7b00-220">`<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-220">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="e7b00-221">Si se omite, se incluyen todas las referencias de `lib`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-221">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="e7b00-222">Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7b00-222">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="e7b00-223">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e7b00-223">contentFiles</span></span>
<span data-ttu-id="e7b00-224">*(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="e7b00-224">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="e7b00-225">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto.</span><span class="sxs-lookup"><span data-stu-id="e7b00-225">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="e7b00-226">Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación.</span><span class="sxs-lookup"><span data-stu-id="e7b00-226">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="e7b00-227">archivos</span><span class="sxs-lookup"><span data-stu-id="e7b00-227">files</span></span> 
<span data-ttu-id="e7b00-228">El `<package>` nodo puede contener un `<files>` nodo como un elemento relacionado con `<metadata>`y un `<contentFiles>` elemento secundario bajo `<metadata>`, para especificar qué archivos de ensamblado y el contenido va a incluir en el paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-228">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="e7b00-229">Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.</span><span class="sxs-lookup"><span data-stu-id="e7b00-229">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="e7b00-230">Tokens de reemplazo</span><span class="sxs-lookup"><span data-stu-id="e7b00-230">Replacement tokens</span></span>

<span data-ttu-id="e7b00-231">Al crear un paquete, el [comando `nuget pack`](../tools/cli-ref-pack.md) reemplaza los tokens delimitados por $ en el nodo `<metadata>` del archivo `.nuspec` por valores procedentes de un archivo de proyecto o del conmutador `-properties` del comando `pack`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-231">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="e7b00-232">En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-232">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="e7b00-233">Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="e7b00-233">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="e7b00-234">Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="e7b00-234">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="e7b00-235">Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-235">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="e7b00-236">Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="e7b00-236">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="e7b00-237">Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares.</span><span class="sxs-lookup"><span data-stu-id="e7b00-237">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="e7b00-238">Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-238">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="e7b00-239">Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="e7b00-239">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="e7b00-240">Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e7b00-240">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="e7b00-241">Token</span><span class="sxs-lookup"><span data-stu-id="e7b00-241">Token</span></span> | <span data-ttu-id="e7b00-242">Origen del valor</span><span class="sxs-lookup"><span data-stu-id="e7b00-242">Value source</span></span> | <span data-ttu-id="e7b00-243">Valor</span><span class="sxs-lookup"><span data-stu-id="e7b00-243">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="e7b00-244">**$id$**</span><span class="sxs-lookup"><span data-stu-id="e7b00-244">**$id$**</span></span> | <span data-ttu-id="e7b00-245">Archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="e7b00-245">Project file</span></span> | <span data-ttu-id="e7b00-246">AssemblyName (título) del archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="e7b00-246">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="e7b00-247">**$version$**</span><span class="sxs-lookup"><span data-stu-id="e7b00-247">**$version$**</span></span> | <span data-ttu-id="e7b00-248">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e7b00-248">AssemblyInfo</span></span> | <span data-ttu-id="e7b00-249">AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="e7b00-249">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="e7b00-250">**$author$**</span><span class="sxs-lookup"><span data-stu-id="e7b00-250">**$author$**</span></span> | <span data-ttu-id="e7b00-251">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e7b00-251">AssemblyInfo</span></span> | <span data-ttu-id="e7b00-252">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="e7b00-252">AssemblyCompany</span></span> |
| <span data-ttu-id="e7b00-253">**$title$**</span><span class="sxs-lookup"><span data-stu-id="e7b00-253">**$title$**</span></span> | <span data-ttu-id="e7b00-254">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e7b00-254">AssemblyInfo</span></span> | <span data-ttu-id="e7b00-255">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="e7b00-255">AssemblyTitle</span></span> |
| <span data-ttu-id="e7b00-256">**$description$**</span><span class="sxs-lookup"><span data-stu-id="e7b00-256">**$description$**</span></span> | <span data-ttu-id="e7b00-257">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e7b00-257">AssemblyInfo</span></span> | <span data-ttu-id="e7b00-258">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="e7b00-258">AssemblyDescription</span></span> |
| <span data-ttu-id="e7b00-259">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="e7b00-259">**$copyright$**</span></span> | <span data-ttu-id="e7b00-260">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e7b00-260">AssemblyInfo</span></span> | <span data-ttu-id="e7b00-261">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="e7b00-261">AssemblyCopyright</span></span> |
| <span data-ttu-id="e7b00-262">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="e7b00-262">**$configuration$**</span></span> | <span data-ttu-id="e7b00-263">Archivo DLL del ensamblado</span><span class="sxs-lookup"><span data-stu-id="e7b00-263">Assembly DLL</span></span> | <span data-ttu-id="e7b00-264">Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar.</span><span class="sxs-lookup"><span data-stu-id="e7b00-264">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="e7b00-265">Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e7b00-265">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="e7b00-266">Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="e7b00-266">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="e7b00-267">Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual.</span><span class="sxs-lookup"><span data-stu-id="e7b00-267">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="e7b00-268">Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="e7b00-268">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="e7b00-269">Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:</span><span class="sxs-lookup"><span data-stu-id="e7b00-269">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="e7b00-270">Elemento de dependencias</span><span class="sxs-lookup"><span data-stu-id="e7b00-270">Dependencies element</span></span>

<span data-ttu-id="e7b00-271">El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="e7b00-271">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="e7b00-272">Los atributos de cada `<dependency>` son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e7b00-272">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="e7b00-273">Atributo</span><span class="sxs-lookup"><span data-stu-id="e7b00-273">Attribute</span></span> | <span data-ttu-id="e7b00-274">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7b00-274">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="e7b00-275">(Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-275">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="e7b00-276">(Obligatorio) Intervalo de versiones aceptable como dependencia.</span><span class="sxs-lookup"><span data-stu-id="e7b00-276">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="e7b00-277">Vea [Control de versiones de paquetes](../reference/package-versioning.md#version-ranges-and-wildcards) para consultar la sintaxis exacta.</span><span class="sxs-lookup"><span data-stu-id="e7b00-277">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="e7b00-278">include</span><span class="sxs-lookup"><span data-stu-id="e7b00-278">include</span></span> | <span data-ttu-id="e7b00-279">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="e7b00-279">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="e7b00-280">El valor predeterminado es `all`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-280">The default value is `all`.</span></span> |
| <span data-ttu-id="e7b00-281">exclude</span><span class="sxs-lookup"><span data-stu-id="e7b00-281">exclude</span></span> | <span data-ttu-id="e7b00-282">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="e7b00-282">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="e7b00-283">El valor predeterminado es `build,analyzers` que puede que se sobrescriban.</span><span class="sxs-lookup"><span data-stu-id="e7b00-283">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="e7b00-284">Pero `content/ ContentFiles` implícitamente también se excluyen en el paquete final que no se sobrescribe.</span><span class="sxs-lookup"><span data-stu-id="e7b00-284">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="e7b00-285">Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-285">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="e7b00-286">Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-286">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="e7b00-287">Etiqueta Include o Exclude</span><span class="sxs-lookup"><span data-stu-id="e7b00-287">Include/Exclude tag</span></span> | <span data-ttu-id="e7b00-288">Carpetas afectadas del destino</span><span class="sxs-lookup"><span data-stu-id="e7b00-288">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="e7b00-289">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e7b00-289">contentFiles</span></span> | <span data-ttu-id="e7b00-290">Contenido</span><span class="sxs-lookup"><span data-stu-id="e7b00-290">Content</span></span> |
| <span data-ttu-id="e7b00-291">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="e7b00-291">runtime</span></span> | <span data-ttu-id="e7b00-292">Runtime, Resources y FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="e7b00-292">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="e7b00-293">compile</span><span class="sxs-lookup"><span data-stu-id="e7b00-293">compile</span></span> | <span data-ttu-id="e7b00-294">lib</span><span class="sxs-lookup"><span data-stu-id="e7b00-294">lib</span></span> |
| <span data-ttu-id="e7b00-295">compilación</span><span class="sxs-lookup"><span data-stu-id="e7b00-295">build</span></span> | <span data-ttu-id="e7b00-296">build (propiedades y destinos de MSBuild)</span><span class="sxs-lookup"><span data-stu-id="e7b00-296">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="e7b00-297">nativas</span><span class="sxs-lookup"><span data-stu-id="e7b00-297">native</span></span> | <span data-ttu-id="e7b00-298">nativas</span><span class="sxs-lookup"><span data-stu-id="e7b00-298">native</span></span> |
| <span data-ttu-id="e7b00-299">ninguna</span><span class="sxs-lookup"><span data-stu-id="e7b00-299">none</span></span> | <span data-ttu-id="e7b00-300">Sin carpetas</span><span class="sxs-lookup"><span data-stu-id="e7b00-300">No folders</span></span> |
| <span data-ttu-id="e7b00-301">todo</span><span class="sxs-lookup"><span data-stu-id="e7b00-301">all</span></span> | <span data-ttu-id="e7b00-302">Todas las carpetas</span><span class="sxs-lookup"><span data-stu-id="e7b00-302">All folders</span></span> |

<span data-ttu-id="e7b00-303">Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="e7b00-303">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="e7b00-304">Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-304">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="e7b00-305">Nota: Al crear un `.nuspec` desde un proyecto mediante `nuget spec`, las dependencias que existen en ese proyecto se incluyen automáticamente en el cuadro `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="e7b00-305">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="e7b00-306">Grupos de dependencia</span><span class="sxs-lookup"><span data-stu-id="e7b00-306">Dependency groups</span></span>

<span data-ttu-id="e7b00-307">*Versión 2.0+*</span><span class="sxs-lookup"><span data-stu-id="e7b00-307">*Version 2.0+*</span></span>

<span data-ttu-id="e7b00-308">Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-308">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="e7b00-309">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-309">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="e7b00-310">Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="e7b00-310">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="e7b00-311">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias.</span><span class="sxs-lookup"><span data-stu-id="e7b00-311">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="e7b00-312">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="e7b00-312">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="e7b00-313">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="e7b00-313">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="e7b00-314">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="e7b00-314">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="e7b00-315">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="e7b00-315">Explicit assembly references</span></span>

<span data-ttu-id="e7b00-316">El `<references>` elemento se usa en proyectos que usen `packages.config` especificar explícitamente los ensamblados que debe hacer referencia en el proyecto de destino cuando se usa el paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-316">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="e7b00-317">Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="e7b00-317">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="e7b00-318">Para obtener más información, vea la página en [seleccionar ensamblados referenciados por proyectos](../create-packages/select-assemblies-referenced-by-projects.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e7b00-318">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="e7b00-319">Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:</span><span class="sxs-lookup"><span data-stu-id="e7b00-319">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="e7b00-320">Grupos de referencias</span><span class="sxs-lookup"><span data-stu-id="e7b00-320">Reference groups</span></span>

<span data-ttu-id="e7b00-321">Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-321">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="e7b00-322">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-322">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="e7b00-323">Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="e7b00-323">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="e7b00-324">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias.</span><span class="sxs-lookup"><span data-stu-id="e7b00-324">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="e7b00-325">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="e7b00-325">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="e7b00-326">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="e7b00-326">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="e7b00-327">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="e7b00-327">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="e7b00-328">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="e7b00-328">Framework assembly references</span></span>

<span data-ttu-id="e7b00-329">Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo.</span><span class="sxs-lookup"><span data-stu-id="e7b00-329">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="e7b00-330">Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias.</span><span class="sxs-lookup"><span data-stu-id="e7b00-330">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="e7b00-331">Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-331">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="e7b00-332">El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="e7b00-332">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="e7b00-333">Atributo</span><span class="sxs-lookup"><span data-stu-id="e7b00-333">Attribute</span></span> | <span data-ttu-id="e7b00-334">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7b00-334">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7b00-335">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="e7b00-335">**assemblyName**</span></span> | <span data-ttu-id="e7b00-336">(Obligatorio) Nombre completo del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="e7b00-336">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="e7b00-337">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="e7b00-337">**targetFramework**</span></span> | <span data-ttu-id="e7b00-338">(Opcional) Especifica la plataforma de destino a la que se aplica esta referencia.</span><span class="sxs-lookup"><span data-stu-id="e7b00-338">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="e7b00-339">Si se omite, indica que la referencia se aplica a todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="e7b00-339">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="e7b00-340">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="e7b00-340">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="e7b00-341">En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="e7b00-341">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="e7b00-342">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="e7b00-342">Including assembly files</span></span>

<span data-ttu-id="e7b00-343">Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-343">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="e7b00-344">El comando `nuget pack` selecciona automáticamente los archivos necesarios.</span><span class="sxs-lookup"><span data-stu-id="e7b00-344">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="e7b00-345">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados.</span><span class="sxs-lookup"><span data-stu-id="e7b00-345">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="e7b00-346">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-346">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="e7b00-347">Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente.</span><span class="sxs-lookup"><span data-stu-id="e7b00-347">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="e7b00-348">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e7b00-348">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="e7b00-349">Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="e7b00-349">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="e7b00-350">Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="e7b00-350">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="e7b00-351">Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="e7b00-351">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="e7b00-352">Atributos del elemento File</span><span class="sxs-lookup"><span data-stu-id="e7b00-352">File element attributes</span></span>

<span data-ttu-id="e7b00-353">Cada elemento `<file>` especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="e7b00-353">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="e7b00-354">Atributo</span><span class="sxs-lookup"><span data-stu-id="e7b00-354">Attribute</span></span> | <span data-ttu-id="e7b00-355">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7b00-355">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7b00-356">**src**</span><span class="sxs-lookup"><span data-stu-id="e7b00-356">**src**</span></span> | <span data-ttu-id="e7b00-357">Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-357">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="e7b00-358">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="e7b00-358">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="e7b00-359">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="e7b00-359">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="e7b00-360">**target**</span><span class="sxs-lookup"><span data-stu-id="e7b00-360">**target**</span></span> | <span data-ttu-id="e7b00-361">La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-361">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="e7b00-362">Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones).</span><span class="sxs-lookup"><span data-stu-id="e7b00-362">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="e7b00-363">**exclude**</span><span class="sxs-lookup"><span data-stu-id="e7b00-363">**exclude**</span></span> | <span data-ttu-id="e7b00-364">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-364">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="e7b00-365">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="e7b00-365">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="e7b00-366">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="e7b00-366">Examples</span></span>

<span data-ttu-id="e7b00-367">**Ensamblado único**</span><span class="sxs-lookup"><span data-stu-id="e7b00-367">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="e7b00-368">**Ensamblado único específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="e7b00-368">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="e7b00-369">**Conjunto de archivos DLL que usan un carácter comodín**</span><span class="sxs-lookup"><span data-stu-id="e7b00-369">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="e7b00-370">**Archivos DLL para distintas plataformas**</span><span class="sxs-lookup"><span data-stu-id="e7b00-370">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="e7b00-371">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="e7b00-371">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="e7b00-372">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="e7b00-372">Including content files</span></span>

<span data-ttu-id="e7b00-373">Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="e7b00-373">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="e7b00-374">Como son inmutables, no se prevé que el proyecto de consumo los modifique.</span><span class="sxs-lookup"><span data-stu-id="e7b00-374">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="e7b00-375">Entre los archivos de contenido se encuentran los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e7b00-375">Example content files include:</span></span>

- <span data-ttu-id="e7b00-376">Imágenes que se insertan como recursos</span><span class="sxs-lookup"><span data-stu-id="e7b00-376">Images that are embedded as resources</span></span>
- <span data-ttu-id="e7b00-377">Archivos de código fuente que ya están compilados</span><span class="sxs-lookup"><span data-stu-id="e7b00-377">Source files that are already compiled</span></span>
- <span data-ttu-id="e7b00-378">Scripts que se deben incluir con la salida de la compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="e7b00-378">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="e7b00-379">Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto</span><span class="sxs-lookup"><span data-stu-id="e7b00-379">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="e7b00-380">Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-380">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="e7b00-381">Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="e7b00-381">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="e7b00-382">Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.</span><span class="sxs-lookup"><span data-stu-id="e7b00-382">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="e7b00-383">Usar el elemento files para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="e7b00-383">Using the files element for content files</span></span>

<span data-ttu-id="e7b00-384">En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="e7b00-384">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="e7b00-385">**Archivos de contenido básicos**</span><span class="sxs-lookup"><span data-stu-id="e7b00-385">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="e7b00-386">**Archivos de contenido con estructura de directorios**</span><span class="sxs-lookup"><span data-stu-id="e7b00-386">**Content files with directory structure**</span></span>

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

<span data-ttu-id="e7b00-387">**Archivo de contenido específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="e7b00-387">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="e7b00-388">**Archivo de contenido copiado en una carpeta con un punto en el nombre**</span><span class="sxs-lookup"><span data-stu-id="e7b00-388">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="e7b00-389">En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:</span><span class="sxs-lookup"><span data-stu-id="e7b00-389">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="e7b00-390">**Archivos de contenido sin extensión**</span><span class="sxs-lookup"><span data-stu-id="e7b00-390">**Content files without extensions**</span></span>

<span data-ttu-id="e7b00-391">Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="e7b00-391">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="e7b00-392">**Archivos de contenido con una ruta de acceso y un destino profundos**</span><span class="sxs-lookup"><span data-stu-id="e7b00-392">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="e7b00-393">En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:</span><span class="sxs-lookup"><span data-stu-id="e7b00-393">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="e7b00-394">**Cambiar el nombre de un archivo de contenido del paquete**</span><span class="sxs-lookup"><span data-stu-id="e7b00-394">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="e7b00-395">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="e7b00-395">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="e7b00-396">Usar el elemento contentFiles para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="e7b00-396">Using the contentFiles element for content files</span></span>

<span data-ttu-id="e7b00-397">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="e7b00-397">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="e7b00-398">De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados.</span><span class="sxs-lookup"><span data-stu-id="e7b00-398">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="e7b00-399">En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-399">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="e7b00-400">Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.</span><span class="sxs-lookup"><span data-stu-id="e7b00-400">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="e7b00-401">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:</span><span class="sxs-lookup"><span data-stu-id="e7b00-401">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="e7b00-402">Atributo</span><span class="sxs-lookup"><span data-stu-id="e7b00-402">Attribute</span></span> | <span data-ttu-id="e7b00-403">Descripción</span><span class="sxs-lookup"><span data-stu-id="e7b00-403">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7b00-404">**include**</span><span class="sxs-lookup"><span data-stu-id="e7b00-404">**include**</span></span> | <span data-ttu-id="e7b00-405">(Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-405">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="e7b00-406">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="e7b00-406">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="e7b00-407">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="e7b00-407">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="e7b00-408">**exclude**</span><span class="sxs-lookup"><span data-stu-id="e7b00-408">**exclude**</span></span> | <span data-ttu-id="e7b00-409">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-409">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="e7b00-410">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="e7b00-410">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="e7b00-411">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="e7b00-411">**buildAction**</span></span> | <span data-ttu-id="e7b00-412">Acción de compilación que se debe asignar al elemento de contenido para MSBuild, como `Content`, `None`, `Embedded Resource`, `Compile`, etc. El valor predeterminado es `Compile`.</span><span class="sxs-lookup"><span data-stu-id="e7b00-412">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="e7b00-413">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="e7b00-413">**copyToOutput**</span></span> | <span data-ttu-id="e7b00-414">Un valor booleano que indica si se va a copiar los elementos de contenido a la compilación de carpeta de salida (o publicar).</span><span class="sxs-lookup"><span data-stu-id="e7b00-414">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="e7b00-415">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="e7b00-415">The default is false.</span></span> |
| <span data-ttu-id="e7b00-416">**flatten**</span><span class="sxs-lookup"><span data-stu-id="e7b00-416">**flatten**</span></span> | <span data-ttu-id="e7b00-417">Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false).</span><span class="sxs-lookup"><span data-stu-id="e7b00-417">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="e7b00-418">Esta marca solo funciona cuando la marca copyToOutput está establecida en true.</span><span class="sxs-lookup"><span data-stu-id="e7b00-418">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="e7b00-419">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="e7b00-419">The default is false.</span></span> |

<span data-ttu-id="e7b00-420">Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo.</span><span class="sxs-lookup"><span data-stu-id="e7b00-420">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="e7b00-421">Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas.</span><span class="sxs-lookup"><span data-stu-id="e7b00-421">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="e7b00-422">La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.</span><span class="sxs-lookup"><span data-stu-id="e7b00-422">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="e7b00-423">Estructura de carpetas de los paquetes</span><span class="sxs-lookup"><span data-stu-id="e7b00-423">Package folder structure</span></span>

<span data-ttu-id="e7b00-424">El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="e7b00-424">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="e7b00-425">`codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.</span><span class="sxs-lookup"><span data-stu-id="e7b00-425">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="e7b00-426">`TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="e7b00-426">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="e7b00-427">Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.</span><span class="sxs-lookup"><span data-stu-id="e7b00-427">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="e7b00-428">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e7b00-428">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="e7b00-429">Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e7b00-429">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="e7b00-430">Sección contentFiles de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e7b00-430">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="e7b00-431">Archivos de ejemplo de nuspec</span><span class="sxs-lookup"><span data-stu-id="e7b00-431">Example nuspec files</span></span>

<span data-ttu-id="e7b00-432">**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**</span><span class="sxs-lookup"><span data-stu-id="e7b00-432">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="e7b00-433">**Un archivo `.nuspec` con dependencias**</span><span class="sxs-lookup"><span data-stu-id="e7b00-433">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="e7b00-434">**Un archivo `.nuspec` con archivos**</span><span class="sxs-lookup"><span data-stu-id="e7b00-434">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="e7b00-435">**Un archivo `.nuspec` con ensamblados de plataforma**</span><span class="sxs-lookup"><span data-stu-id="e7b00-435">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="e7b00-436">En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:</span><span class="sxs-lookup"><span data-stu-id="e7b00-436">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="e7b00-437">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="e7b00-437">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="e7b00-438">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="e7b00-438">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="e7b00-439">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="e7b00-439">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="e7b00-440">Windows Phone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="e7b00-440">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
