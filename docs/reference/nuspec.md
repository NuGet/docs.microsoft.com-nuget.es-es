---
title: Referencia de .nuspec para NuGet
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 142f82386395b8ab2ed1d57218db9bc1d2e98638
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843451"
---
# <a name="nuspec-reference"></a><span data-ttu-id="d1f92-103">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="d1f92-103">.nuspec reference</span></span>

<span data-ttu-id="d1f92-104">Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="d1f92-105">Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores.</span><span class="sxs-lookup"><span data-stu-id="d1f92-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="d1f92-106">El manifiesto siempre se incluye en un paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="d1f92-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="d1f92-107">In this topic:</span></span>

- [<span data-ttu-id="d1f92-108">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="d1f92-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="d1f92-109">[Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d1f92-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="d1f92-110">Dependencias</span><span class="sxs-lookup"><span data-stu-id="d1f92-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="d1f92-111">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="d1f92-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="d1f92-112">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="d1f92-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="d1f92-113">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="d1f92-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="d1f92-114">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="d1f92-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="d1f92-115">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1f92-115">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="d1f92-116">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="d1f92-116">General form and schema</span></span>

<span data-ttu-id="d1f92-117">El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="d1f92-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="d1f92-118">En este esquema, los archivos `.nuspec` tienen el siguiente formato general:</span><span class="sxs-lookup"><span data-stu-id="d1f92-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="d1f92-119">Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="d1f92-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="d1f92-120">Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="d1f92-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="d1f92-121">En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):</span><span class="sxs-lookup"><span data-stu-id="d1f92-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="d1f92-123">Atributos de metadatos</span><span class="sxs-lookup"><span data-stu-id="d1f92-123">Metadata attributes</span></span>

<span data-ttu-id="d1f92-124">El elemento `<metadata>` admite los atributos descritos en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="d1f92-124">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="d1f92-125">Atributo</span><span class="sxs-lookup"><span data-stu-id="d1f92-125">Attribute</span></span> | <span data-ttu-id="d1f92-126">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1f92-126">Required</span></span> | <span data-ttu-id="d1f92-127">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1f92-127">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="d1f92-128">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="d1f92-128">**minClientVersion**</span></span> | <span data-ttu-id="d1f92-129">No</span><span class="sxs-lookup"><span data-stu-id="d1f92-129">No</span></span> | <span data-ttu-id="d1f92-130">Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1f92-130">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="d1f92-131">Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d1f92-131">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="d1f92-132">Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-132">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="d1f92-133">Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3".</span><span class="sxs-lookup"><span data-stu-id="d1f92-133">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="d1f92-134">Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-134">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="d1f92-135">Elementos de metadatos necesarios</span><span class="sxs-lookup"><span data-stu-id="d1f92-135">Required metadata elements</span></span>

<span data-ttu-id="d1f92-136">Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-136">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="d1f92-137">Estos elementos deben aparecer dentro de un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-137">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="d1f92-138">Elemento</span><span class="sxs-lookup"><span data-stu-id="d1f92-138">Element</span></span> | <span data-ttu-id="d1f92-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1f92-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1f92-140">**identificador**</span><span class="sxs-lookup"><span data-stu-id="d1f92-140">**id**</span></span> | <span data-ttu-id="d1f92-141">El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-141">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="d1f92-142">Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET.</span><span class="sxs-lookup"><span data-stu-id="d1f92-142">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="d1f92-143">Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="d1f92-143">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="d1f92-144">**version**</span><span class="sxs-lookup"><span data-stu-id="d1f92-144">**version**</span></span> | <span data-ttu-id="d1f92-145">La versión del paquete, siguiendo el patrón *mayor.menor.revisión*.</span><span class="sxs-lookup"><span data-stu-id="d1f92-145">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="d1f92-146">Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="d1f92-146">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="d1f92-147">**description**</span><span class="sxs-lookup"><span data-stu-id="d1f92-147">**description**</span></span> | <span data-ttu-id="d1f92-148">Una descripción larga del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="d1f92-148">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="d1f92-149">**authors**</span><span class="sxs-lookup"><span data-stu-id="d1f92-149">**authors**</span></span> | <span data-ttu-id="d1f92-150">Una lista separada por comas de los autores de los paquetes, que coinciden con los nombres de perfil de nuget.org. Estos se muestran en la galería de NuGet, en nuget.org, y se usan para hacer referencias cruzadas a paquetes de los mismos autores.</span><span class="sxs-lookup"><span data-stu-id="d1f92-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="d1f92-151">Elementos de metadatos opcionales</span><span class="sxs-lookup"><span data-stu-id="d1f92-151">Optional metadata elements</span></span>

<span data-ttu-id="d1f92-152">Estos elementos pueden aparecer dentro de un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-152">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="d1f92-153">Elementos únicos</span><span class="sxs-lookup"><span data-stu-id="d1f92-153">Single elements</span></span>

| <span data-ttu-id="d1f92-154">Elemento</span><span class="sxs-lookup"><span data-stu-id="d1f92-154">Element</span></span> | <span data-ttu-id="d1f92-155">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1f92-155">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1f92-156">**title**</span><span class="sxs-lookup"><span data-stu-id="d1f92-156">**title**</span></span> | <span data-ttu-id="d1f92-157">Un título fácil de usar del paquete, que se usa normalmente en las visualizaciones de la interfaz de usuario, como en nuget.org, y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1f92-157">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="d1f92-158">Si no se especifica, se usa el identificador del paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-158">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="d1f92-159">**owners**</span><span class="sxs-lookup"><span data-stu-id="d1f92-159">**owners**</span></span> | <span data-ttu-id="d1f92-160">Lista separada por comas de los creadores del paquete usando nombres de perfil en nuget.org. Suele ser la misma lista que en `authors` y se ignora al cargar el paquete en nuget.org. Vea [Administrar los propietarios de paquetes en nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="d1f92-160">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="d1f92-161">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="d1f92-161">**projectUrl**</span></span> | <span data-ttu-id="d1f92-162">Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d1f92-162">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="d1f92-163">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="d1f92-163">**licenseUrl**</span></span> | <span data-ttu-id="d1f92-164">Dirección URL de la licencia del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d1f92-164">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="d1f92-165">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="d1f92-165">**iconUrl**</span></span> | <span data-ttu-id="d1f92-166">Dirección URL para una imagen de 64 x 64 con fondo transparente para usarla como icono para el paquete en la visualización de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="d1f92-166">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="d1f92-167">Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen.</span><span class="sxs-lookup"><span data-stu-id="d1f92-167">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="d1f92-168">Por ejemplo, para utilizar una imagen desde GitHub, use el archivo sin formato, como la dirección URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="d1f92-168">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> |
| <span data-ttu-id="d1f92-169">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="d1f92-169">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="d1f92-170">Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="d1f92-170">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="d1f92-171">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="d1f92-171">**developmentDependency**</span></span> | <span data-ttu-id="d1f92-172">*(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="d1f92-172">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="d1f92-173">**summary**</span><span class="sxs-lookup"><span data-stu-id="d1f92-173">**summary**</span></span> | <span data-ttu-id="d1f92-174">Descripción breve del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="d1f92-174">A short description of the package for UI display.</span></span> <span data-ttu-id="d1f92-175">Si se omite, se usará una versión truncada de `description`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-175">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="d1f92-176">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="d1f92-176">**releaseNotes**</span></span> | <span data-ttu-id="d1f92-177">*(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-177">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="d1f92-178">**copyright**</span><span class="sxs-lookup"><span data-stu-id="d1f92-178">**copyright**</span></span> | <span data-ttu-id="d1f92-179">*(1.5+)* Información de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-179">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="d1f92-180">**language**</span><span class="sxs-lookup"><span data-stu-id="d1f92-180">**language**</span></span> | <span data-ttu-id="d1f92-181">Identificador de configuración regional del paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-181">The locale ID for the package.</span></span> <span data-ttu-id="d1f92-182">Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d1f92-182">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="d1f92-183">**tags**</span><span class="sxs-lookup"><span data-stu-id="d1f92-183">**tags**</span></span>  | <span data-ttu-id="d1f92-184">Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados.</span><span class="sxs-lookup"><span data-stu-id="d1f92-184">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="d1f92-185">**serviceable**</span><span class="sxs-lookup"><span data-stu-id="d1f92-185">**serviceable**</span></span> | <span data-ttu-id="d1f92-186">*(3.3+)* Solo para uso interno de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d1f92-186">*(3.3+)* For internal NuGet use only.</span></span> |
| <span data-ttu-id="d1f92-187">**repositorio**</span><span class="sxs-lookup"><span data-stu-id="d1f92-187">**repository**</span></span> | <span data-ttu-id="d1f92-188">Repositorio de metadatos, que consta de cuatro atributos opcionales: *tipo* y *url* *(4.0 y versiones posteriores)*, y *rama* y  *confirmación* *(4.6 y versiones posteriores)*.</span><span class="sxs-lookup"><span data-stu-id="d1f92-188">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="d1f92-189">Estos atributos permiten asignar los archivos .nupkg en el repositorio que se crearon, con la posibilidad de obtener tal como se detalla como la rama individual o la confirmación de que se creó el paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-189">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="d1f92-190">Elementos de colección</span><span class="sxs-lookup"><span data-stu-id="d1f92-190">Collection elements</span></span>

| <span data-ttu-id="d1f92-191">Elemento</span><span class="sxs-lookup"><span data-stu-id="d1f92-191">Element</span></span> | <span data-ttu-id="d1f92-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1f92-192">Description</span></span> |
| --- | --- |
<span data-ttu-id="d1f92-193">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="d1f92-193">**packageTypes**</span></span> | <span data-ttu-id="d1f92-194">*(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional.</span><span class="sxs-lookup"><span data-stu-id="d1f92-194">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="d1f92-195">Cada tipo de paquete tiene atributos de *name* y *version*.</span><span class="sxs-lookup"><span data-stu-id="d1f92-195">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="d1f92-196">Vea [Establecimiento de un tipo de paquete](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="d1f92-196">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="d1f92-197">**dependencies**</span><span class="sxs-lookup"><span data-stu-id="d1f92-197">**dependencies**</span></span> | <span data-ttu-id="d1f92-198">Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-198">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="d1f92-199">Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="d1f92-199">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="d1f92-200">Vea [Dependencias](#dependencies) a continuación.</span><span class="sxs-lookup"><span data-stu-id="d1f92-200">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="d1f92-201">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="d1f92-201">**frameworkAssemblies**</span></span> | <span data-ttu-id="d1f92-202">*(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-202">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="d1f92-203">Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="d1f92-203">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="d1f92-204">Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación.</span><span class="sxs-lookup"><span data-stu-id="d1f92-204">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="d1f92-205">**references**</span><span class="sxs-lookup"><span data-stu-id="d1f92-205">**references**</span></span> | <span data-ttu-id="d1f92-206">*(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="d1f92-206">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="d1f92-207">Cada referencia tiene un atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="d1f92-207">Each reference has a *file* attribute.</span></span> <span data-ttu-id="d1f92-208">`<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-208">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="d1f92-209">Si se omite, se incluyen todas las referencias de `lib`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-209">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="d1f92-210">Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación.</span><span class="sxs-lookup"><span data-stu-id="d1f92-210">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="d1f92-211">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="d1f92-211">**contentFiles**</span></span> | <span data-ttu-id="d1f92-212">*(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="d1f92-212">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="d1f92-213">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d1f92-213">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="d1f92-214">Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación.</span><span class="sxs-lookup"><span data-stu-id="d1f92-214">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="d1f92-215">Files (elemento)</span><span class="sxs-lookup"><span data-stu-id="d1f92-215">Files element</span></span>

<span data-ttu-id="d1f92-216">El nodo `<package>` puede contener un nodo `<files>` como un elemento del mismo nivel de `<metadata>`, o un elemento secundario `<contentFiles>` en `<metadata>`, para especificar los archivos de contenido y de ensamblado que se deben incluir en el paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-216">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="d1f92-217">Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.</span><span class="sxs-lookup"><span data-stu-id="d1f92-217">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="d1f92-218">Tokens de reemplazo</span><span class="sxs-lookup"><span data-stu-id="d1f92-218">Replacement tokens</span></span>

<span data-ttu-id="d1f92-219">Al crear un paquete, el [comando `nuget pack`](../tools/cli-ref-pack.md) reemplaza los tokens delimitados por $ en el nodo `<metadata>` del archivo `.nuspec` por valores procedentes de un archivo de proyecto o del conmutador `-properties` del comando `pack`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-219">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="d1f92-220">En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-220">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="d1f92-221">Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="d1f92-221">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="d1f92-222">Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="d1f92-222">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="d1f92-223">Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-223">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="d1f92-224">Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="d1f92-224">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="d1f92-225">Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares.</span><span class="sxs-lookup"><span data-stu-id="d1f92-225">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="d1f92-226">Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-226">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="d1f92-227">Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="d1f92-227">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="d1f92-228">Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d1f92-228">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="d1f92-229">Token</span><span class="sxs-lookup"><span data-stu-id="d1f92-229">Token</span></span> | <span data-ttu-id="d1f92-230">Origen del valor</span><span class="sxs-lookup"><span data-stu-id="d1f92-230">Value source</span></span> | <span data-ttu-id="d1f92-231">Valor</span><span class="sxs-lookup"><span data-stu-id="d1f92-231">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="d1f92-232">**$id$**</span><span class="sxs-lookup"><span data-stu-id="d1f92-232">**$id$**</span></span> | <span data-ttu-id="d1f92-233">Archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="d1f92-233">Project file</span></span> | <span data-ttu-id="d1f92-234">AssemblyName (título) del archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="d1f92-234">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="d1f92-235">**$version$**</span><span class="sxs-lookup"><span data-stu-id="d1f92-235">**$version$**</span></span> | <span data-ttu-id="d1f92-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d1f92-236">AssemblyInfo</span></span> | <span data-ttu-id="d1f92-237">AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="d1f92-237">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="d1f92-238">**$author$**</span><span class="sxs-lookup"><span data-stu-id="d1f92-238">**$author$**</span></span> | <span data-ttu-id="d1f92-239">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d1f92-239">AssemblyInfo</span></span> | <span data-ttu-id="d1f92-240">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="d1f92-240">AssemblyCompany</span></span> |
| <span data-ttu-id="d1f92-241">**$title$**</span><span class="sxs-lookup"><span data-stu-id="d1f92-241">**$title$**</span></span> | <span data-ttu-id="d1f92-242">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d1f92-242">AssemblyInfo</span></span> | <span data-ttu-id="d1f92-243">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="d1f92-243">AssemblyTitle</span></span> |
| <span data-ttu-id="d1f92-244">**$description$**</span><span class="sxs-lookup"><span data-stu-id="d1f92-244">**$description$**</span></span> | <span data-ttu-id="d1f92-245">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d1f92-245">AssemblyInfo</span></span> | <span data-ttu-id="d1f92-246">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="d1f92-246">AssemblyDescription</span></span> |
| <span data-ttu-id="d1f92-247">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="d1f92-247">**$copyright$**</span></span> | <span data-ttu-id="d1f92-248">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d1f92-248">AssemblyInfo</span></span> | <span data-ttu-id="d1f92-249">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="d1f92-249">AssemblyCopyright</span></span> |
| <span data-ttu-id="d1f92-250">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="d1f92-250">**$configuration$**</span></span> | <span data-ttu-id="d1f92-251">Archivo DLL del ensamblado</span><span class="sxs-lookup"><span data-stu-id="d1f92-251">Assembly DLL</span></span> | <span data-ttu-id="d1f92-252">Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar.</span><span class="sxs-lookup"><span data-stu-id="d1f92-252">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="d1f92-253">Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d1f92-253">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="d1f92-254">Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="d1f92-254">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="d1f92-255">Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual.</span><span class="sxs-lookup"><span data-stu-id="d1f92-255">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="d1f92-256">Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="d1f92-256">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="d1f92-257">Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:</span><span class="sxs-lookup"><span data-stu-id="d1f92-257">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="d1f92-258">Dependencias</span><span class="sxs-lookup"><span data-stu-id="d1f92-258">Dependencies</span></span>

<span data-ttu-id="d1f92-259">El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="d1f92-259">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="d1f92-260">Los atributos de cada `<dependency>` son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d1f92-260">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="d1f92-261">Atributo</span><span class="sxs-lookup"><span data-stu-id="d1f92-261">Attribute</span></span> | <span data-ttu-id="d1f92-262">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1f92-262">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="d1f92-263">(Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-263">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="d1f92-264">(Obligatorio) Intervalo de versiones aceptable como dependencia.</span><span class="sxs-lookup"><span data-stu-id="d1f92-264">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="d1f92-265">Vea [Control de versiones de paquetes](../reference/package-versioning.md#version-ranges-and-wildcards) para consultar la sintaxis exacta.</span><span class="sxs-lookup"><span data-stu-id="d1f92-265">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="d1f92-266">include</span><span class="sxs-lookup"><span data-stu-id="d1f92-266">include</span></span> | <span data-ttu-id="d1f92-267">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="d1f92-267">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="d1f92-268">El valor predeterminado es `none`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-268">The default value is `none`.</span></span> |
| <span data-ttu-id="d1f92-269">exclude</span><span class="sxs-lookup"><span data-stu-id="d1f92-269">exclude</span></span> | <span data-ttu-id="d1f92-270">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="d1f92-270">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="d1f92-271">El valor predeterminado es `all`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-271">The  default value is `all`.</span></span> <span data-ttu-id="d1f92-272">Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-272">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="d1f92-273">Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-273">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="d1f92-274">Etiqueta Include o Exclude</span><span class="sxs-lookup"><span data-stu-id="d1f92-274">Include/Exclude tag</span></span> | <span data-ttu-id="d1f92-275">Carpetas afectadas del destino</span><span class="sxs-lookup"><span data-stu-id="d1f92-275">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="d1f92-276">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d1f92-276">contentFiles</span></span> | <span data-ttu-id="d1f92-277">Contenido</span><span class="sxs-lookup"><span data-stu-id="d1f92-277">Content</span></span> |
| <span data-ttu-id="d1f92-278">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="d1f92-278">runtime</span></span> | <span data-ttu-id="d1f92-279">Runtime, Resources y FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d1f92-279">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="d1f92-280">compile</span><span class="sxs-lookup"><span data-stu-id="d1f92-280">compile</span></span> | <span data-ttu-id="d1f92-281">lib</span><span class="sxs-lookup"><span data-stu-id="d1f92-281">lib</span></span> |
| <span data-ttu-id="d1f92-282">compilación</span><span class="sxs-lookup"><span data-stu-id="d1f92-282">build</span></span> | <span data-ttu-id="d1f92-283">build (propiedades y destinos de MSBuild)</span><span class="sxs-lookup"><span data-stu-id="d1f92-283">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="d1f92-284">nativas</span><span class="sxs-lookup"><span data-stu-id="d1f92-284">native</span></span> | <span data-ttu-id="d1f92-285">nativas</span><span class="sxs-lookup"><span data-stu-id="d1f92-285">native</span></span> |
| <span data-ttu-id="d1f92-286">ninguna</span><span class="sxs-lookup"><span data-stu-id="d1f92-286">none</span></span> | <span data-ttu-id="d1f92-287">Sin carpetas</span><span class="sxs-lookup"><span data-stu-id="d1f92-287">No folders</span></span> |
| <span data-ttu-id="d1f92-288">todo</span><span class="sxs-lookup"><span data-stu-id="d1f92-288">all</span></span> | <span data-ttu-id="d1f92-289">Todas las carpetas</span><span class="sxs-lookup"><span data-stu-id="d1f92-289">All folders</span></span> |

<span data-ttu-id="d1f92-290">Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="d1f92-290">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="d1f92-291">Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-291">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="d1f92-292">Nota: al crear un archivo `.nuspec` a partir de un proyecto mediante `nuget spec`, las dependencias que existen en ese proyecto se incluyen automáticamente en el archivo `.nuspec` resultante.</span><span class="sxs-lookup"><span data-stu-id="d1f92-292">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="d1f92-293">Grupos de dependencia</span><span class="sxs-lookup"><span data-stu-id="d1f92-293">Dependency groups</span></span>

<span data-ttu-id="d1f92-294">*Versión 2.0+*</span><span class="sxs-lookup"><span data-stu-id="d1f92-294">*Version 2.0+*</span></span>

<span data-ttu-id="d1f92-295">Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-295">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="d1f92-296">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-296">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="d1f92-297">Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d1f92-297">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d1f92-298">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias.</span><span class="sxs-lookup"><span data-stu-id="d1f92-298">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="d1f92-299">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="d1f92-299">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d1f92-300">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="d1f92-300">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d1f92-301">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="d1f92-301">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="d1f92-302">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="d1f92-302">Explicit assembly references</span></span>

<span data-ttu-id="d1f92-303">El elemento `<references>` especifica explícitamente los ensamblados a los que debe hacer referencia el proyecto de destino al usar el paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-303">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="d1f92-304">Cuando este elemento está presente, NuGet agrega referencias únicamente a los ensamblados enumerados. No agrega referencias a otros ensamblados en la carpeta `lib` del paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-304">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="d1f92-305">Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:</span><span class="sxs-lookup"><span data-stu-id="d1f92-305">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="d1f92-306">Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="d1f92-306">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="d1f92-307">Al usar [contratos de código](/dotnet/framework/debug-trace-profile/code-contracts), por ejemplo, los ensamblados de contrato deben estar junto a los ensamblados en tiempo de ejecución que alimentan de manera que Visual Studio los pueda encontrar, pero no es necesario que el proyecto haga referencia a los ensamblados de contrato ni que se copien en la carpeta `bin` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d1f92-307">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="d1f92-308">De forma parecida, las referencias explícitas se pueden usar para los marcos de pruebas unitarias, como XUnit, que necesita que sus ensamblados de herramientas estén situados junto a los ensamblados en tiempo de ejecución, pero no necesita que se incluyan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="d1f92-308">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="d1f92-309">Grupos de referencias</span><span class="sxs-lookup"><span data-stu-id="d1f92-309">Reference groups</span></span>

<span data-ttu-id="d1f92-310">Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-310">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="d1f92-311">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-311">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="d1f92-312">Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d1f92-312">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d1f92-313">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias.</span><span class="sxs-lookup"><span data-stu-id="d1f92-313">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="d1f92-314">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="d1f92-314">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d1f92-315">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="d1f92-315">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d1f92-316">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="d1f92-316">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="d1f92-317">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="d1f92-317">Framework assembly references</span></span>

<span data-ttu-id="d1f92-318">Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo.</span><span class="sxs-lookup"><span data-stu-id="d1f92-318">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="d1f92-319">Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias.</span><span class="sxs-lookup"><span data-stu-id="d1f92-319">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="d1f92-320">Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-320">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="d1f92-321">El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="d1f92-321">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="d1f92-322">Atributo</span><span class="sxs-lookup"><span data-stu-id="d1f92-322">Attribute</span></span> | <span data-ttu-id="d1f92-323">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1f92-323">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1f92-324">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="d1f92-324">**assemblyName**</span></span> | <span data-ttu-id="d1f92-325">(Obligatorio) Nombre completo del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="d1f92-325">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="d1f92-326">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="d1f92-326">**targetFramework**</span></span> | <span data-ttu-id="d1f92-327">(Opcional) Especifica la plataforma de destino a la que se aplica esta referencia.</span><span class="sxs-lookup"><span data-stu-id="d1f92-327">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="d1f92-328">Si se omite, indica que la referencia se aplica a todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="d1f92-328">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="d1f92-329">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="d1f92-329">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="d1f92-330">En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="d1f92-330">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="d1f92-331">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="d1f92-331">Including assembly files</span></span>

<span data-ttu-id="d1f92-332">Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-332">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="d1f92-333">El comando `nuget pack` selecciona automáticamente los archivos necesarios.</span><span class="sxs-lookup"><span data-stu-id="d1f92-333">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="d1f92-334">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados.</span><span class="sxs-lookup"><span data-stu-id="d1f92-334">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="d1f92-335">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-335">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="d1f92-336">Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente.</span><span class="sxs-lookup"><span data-stu-id="d1f92-336">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="d1f92-337">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d1f92-337">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="d1f92-338">Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="d1f92-338">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="d1f92-339">Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d1f92-339">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="d1f92-340">Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="d1f92-340">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="d1f92-341">Atributos del elemento File</span><span class="sxs-lookup"><span data-stu-id="d1f92-341">File element attributes</span></span>

<span data-ttu-id="d1f92-342">Cada elemento `<file>` especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="d1f92-342">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="d1f92-343">Atributo</span><span class="sxs-lookup"><span data-stu-id="d1f92-343">Attribute</span></span> | <span data-ttu-id="d1f92-344">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1f92-344">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1f92-345">**src**</span><span class="sxs-lookup"><span data-stu-id="d1f92-345">**src**</span></span> | <span data-ttu-id="d1f92-346">Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-346">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d1f92-347">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="d1f92-347">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d1f92-348">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="d1f92-348">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d1f92-349">**target**</span><span class="sxs-lookup"><span data-stu-id="d1f92-349">**target**</span></span> | <span data-ttu-id="d1f92-350">La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-350">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="d1f92-351">Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones).</span><span class="sxs-lookup"><span data-stu-id="d1f92-351">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="d1f92-352">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d1f92-352">**exclude**</span></span> | <span data-ttu-id="d1f92-353">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-353">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d1f92-354">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="d1f92-354">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="d1f92-355">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1f92-355">Examples</span></span>

<span data-ttu-id="d1f92-356">**Ensamblado único**</span><span class="sxs-lookup"><span data-stu-id="d1f92-356">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="d1f92-357">**Ensamblado único específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="d1f92-357">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="d1f92-358">**Conjunto de archivos DLL que usan un carácter comodín**</span><span class="sxs-lookup"><span data-stu-id="d1f92-358">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="d1f92-359">**Archivos DLL para distintas plataformas**</span><span class="sxs-lookup"><span data-stu-id="d1f92-359">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="d1f92-360">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="d1f92-360">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="d1f92-361">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="d1f92-361">Including content files</span></span>

<span data-ttu-id="d1f92-362">Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="d1f92-362">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="d1f92-363">Como son inmutables, no se prevé que el proyecto de consumo los modifique.</span><span class="sxs-lookup"><span data-stu-id="d1f92-363">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="d1f92-364">Entre los archivos de contenido se encuentran los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d1f92-364">Example content files include:</span></span>

- <span data-ttu-id="d1f92-365">Imágenes que se insertan como recursos</span><span class="sxs-lookup"><span data-stu-id="d1f92-365">Images that are embedded as resources</span></span>
- <span data-ttu-id="d1f92-366">Archivos de código fuente que ya están compilados</span><span class="sxs-lookup"><span data-stu-id="d1f92-366">Source files that are already compiled</span></span>
- <span data-ttu-id="d1f92-367">Scripts que se deben incluir con la salida de la compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="d1f92-367">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="d1f92-368">Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto</span><span class="sxs-lookup"><span data-stu-id="d1f92-368">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="d1f92-369">Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-369">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="d1f92-370">Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d1f92-370">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="d1f92-371">Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.</span><span class="sxs-lookup"><span data-stu-id="d1f92-371">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="d1f92-372">Usar el elemento files para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="d1f92-372">Using the files element for content files</span></span>

<span data-ttu-id="d1f92-373">En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="d1f92-373">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="d1f92-374">**Archivos de contenido básicos**</span><span class="sxs-lookup"><span data-stu-id="d1f92-374">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="d1f92-375">**Archivos de contenido con estructura de directorios**</span><span class="sxs-lookup"><span data-stu-id="d1f92-375">**Content files with directory structure**</span></span>

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

<span data-ttu-id="d1f92-376">**Archivo de contenido específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="d1f92-376">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="d1f92-377">**Archivo de contenido copiado en una carpeta con un punto en el nombre**</span><span class="sxs-lookup"><span data-stu-id="d1f92-377">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="d1f92-378">En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:</span><span class="sxs-lookup"><span data-stu-id="d1f92-378">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="d1f92-379">**Archivos de contenido sin extensión**</span><span class="sxs-lookup"><span data-stu-id="d1f92-379">**Content files without extensions**</span></span>

<span data-ttu-id="d1f92-380">Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="d1f92-380">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="d1f92-381">**Archivos de contenido con una ruta de acceso y un destino profundos**</span><span class="sxs-lookup"><span data-stu-id="d1f92-381">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="d1f92-382">En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:</span><span class="sxs-lookup"><span data-stu-id="d1f92-382">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="d1f92-383">**Cambiar el nombre de un archivo de contenido del paquete**</span><span class="sxs-lookup"><span data-stu-id="d1f92-383">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="d1f92-384">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="d1f92-384">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="d1f92-385">Usar el elemento contentFiles para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="d1f92-385">Using the contentFiles element for content files</span></span>

<span data-ttu-id="d1f92-386">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="d1f92-386">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="d1f92-387">De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados.</span><span class="sxs-lookup"><span data-stu-id="d1f92-387">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="d1f92-388">En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-388">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="d1f92-389">Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.</span><span class="sxs-lookup"><span data-stu-id="d1f92-389">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="d1f92-390">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:</span><span class="sxs-lookup"><span data-stu-id="d1f92-390">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="d1f92-391">Atributo</span><span class="sxs-lookup"><span data-stu-id="d1f92-391">Attribute</span></span> | <span data-ttu-id="d1f92-392">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1f92-392">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1f92-393">**include**</span><span class="sxs-lookup"><span data-stu-id="d1f92-393">**include**</span></span> | <span data-ttu-id="d1f92-394">(Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-394">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d1f92-395">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="d1f92-395">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d1f92-396">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="d1f92-396">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d1f92-397">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d1f92-397">**exclude**</span></span> | <span data-ttu-id="d1f92-398">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-398">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d1f92-399">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="d1f92-399">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d1f92-400">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="d1f92-400">**buildAction**</span></span> | <span data-ttu-id="d1f92-401">Acción de compilación que se debe asignar al elemento de contenido para MSBuild, como `Content`, `None`, `Embedded Resource`, `Compile`, etc. El valor predeterminado es `Compile`.</span><span class="sxs-lookup"><span data-stu-id="d1f92-401">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="d1f92-402">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="d1f92-402">**copyToOutput**</span></span> | <span data-ttu-id="d1f92-403">Un valor booleano que indica si se va a copiar los elementos de contenido a la compilación de carpeta de salida (o publicar).</span><span class="sxs-lookup"><span data-stu-id="d1f92-403">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="d1f92-404">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="d1f92-404">The default is false.</span></span> |
| <span data-ttu-id="d1f92-405">**flatten**</span><span class="sxs-lookup"><span data-stu-id="d1f92-405">**flatten**</span></span> | <span data-ttu-id="d1f92-406">Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false).</span><span class="sxs-lookup"><span data-stu-id="d1f92-406">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="d1f92-407">Esta marca solo funciona cuando la marca copyToOutput está establecida en true.</span><span class="sxs-lookup"><span data-stu-id="d1f92-407">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="d1f92-408">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="d1f92-408">The default is false.</span></span> |

<span data-ttu-id="d1f92-409">Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo.</span><span class="sxs-lookup"><span data-stu-id="d1f92-409">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="d1f92-410">Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas.</span><span class="sxs-lookup"><span data-stu-id="d1f92-410">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="d1f92-411">La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.</span><span class="sxs-lookup"><span data-stu-id="d1f92-411">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="d1f92-412">Estructura de carpetas de los paquetes</span><span class="sxs-lookup"><span data-stu-id="d1f92-412">Package folder structure</span></span>

<span data-ttu-id="d1f92-413">El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="d1f92-413">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="d1f92-414">`codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.</span><span class="sxs-lookup"><span data-stu-id="d1f92-414">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="d1f92-415">`TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="d1f92-415">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="d1f92-416">Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.</span><span class="sxs-lookup"><span data-stu-id="d1f92-416">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="d1f92-417">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d1f92-417">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="d1f92-418">Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d1f92-418">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="d1f92-419">Sección contentFiles de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d1f92-419">Example contentFiles section</span></span>

```xml
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
```

## <a name="example-nuspec-files"></a><span data-ttu-id="d1f92-420">Archivos .nuspec de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d1f92-420">Example .nuspec files</span></span>

<span data-ttu-id="d1f92-421">**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**</span><span class="sxs-lookup"><span data-stu-id="d1f92-421">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="d1f92-422">**Un archivo `.nuspec` con dependencias**</span><span class="sxs-lookup"><span data-stu-id="d1f92-422">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="d1f92-423">**Un archivo `.nuspec` con archivos**</span><span class="sxs-lookup"><span data-stu-id="d1f92-423">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="d1f92-424">**Un archivo `.nuspec` con ensamblados de plataforma**</span><span class="sxs-lookup"><span data-stu-id="d1f92-424">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="d1f92-425">En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:</span><span class="sxs-lookup"><span data-stu-id="d1f92-425">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="d1f92-426">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d1f92-426">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="d1f92-427">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d1f92-427">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="d1f92-428">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="d1f92-428">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="d1f92-429">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="d1f92-429">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="d1f92-430">Windows Phone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="d1f92-430">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
