---
title: Referencia de .nuspec para NuGet
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6d190d9fdb26d76fa8e46b7d283c1857cfab26e9
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508041"
---
# <a name="nuspec-reference"></a><span data-ttu-id="2b7bb-103">Referencia de .nuspec</span><span class="sxs-lookup"><span data-stu-id="2b7bb-103">.nuspec reference</span></span>

<span data-ttu-id="2b7bb-104">Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="2b7bb-105">Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="2b7bb-106">El manifiesto siempre se incluye en un paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="2b7bb-107">En este tema:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-107">In this topic:</span></span>

- [<span data-ttu-id="2b7bb-108">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="2b7bb-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="2b7bb-109">[Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="2b7bb-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="2b7bb-110">Dependencias</span><span class="sxs-lookup"><span data-stu-id="2b7bb-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="2b7bb-111">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="2b7bb-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="2b7bb-112">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="2b7bb-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="2b7bb-113">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="2b7bb-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="2b7bb-114">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="2b7bb-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="2b7bb-115">Archivos de ejemplo de nuspec</span><span class="sxs-lookup"><span data-stu-id="2b7bb-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="2b7bb-116">Esquema y forma general</span><span class="sxs-lookup"><span data-stu-id="2b7bb-116">General form and schema</span></span>

<span data-ttu-id="2b7bb-117">El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="2b7bb-118">En este esquema, los archivos `.nuspec` tienen el siguiente formato general:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="2b7bb-119">Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="2b7bb-120">Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="2b7bb-121">En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):</span><span class="sxs-lookup"><span data-stu-id="2b7bb-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="2b7bb-123">Atributos de metadatos</span><span class="sxs-lookup"><span data-stu-id="2b7bb-123">Metadata attributes</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="2b7bb-124">Elementos de metadatos necesarios</span><span class="sxs-lookup"><span data-stu-id="2b7bb-124">Required metadata elements</span></span>

<span data-ttu-id="2b7bb-125">Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-125">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="2b7bb-126">Estos elementos deben aparecer dentro de un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-126">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="2b7bb-127">Elemento</span><span class="sxs-lookup"><span data-stu-id="2b7bb-127">Element</span></span> | <span data-ttu-id="2b7bb-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="2b7bb-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b7bb-129">**identificador**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-129">**id**</span></span> | <span data-ttu-id="2b7bb-130">El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-130">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="2b7bb-131">Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-131">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="2b7bb-132">Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-132">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="2b7bb-133">**version**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-133">**version**</span></span> | <span data-ttu-id="2b7bb-134">La versión del paquete, siguiendo el patrón *mayor.menor.revisión*.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-134">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="2b7bb-135">Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-135">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="2b7bb-136">**description**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-136">**description**</span></span> | <span data-ttu-id="2b7bb-137">Una descripción larga del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-137">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="2b7bb-138">**authors**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-138">**authors**</span></span> | <span data-ttu-id="2b7bb-139">Una lista separada por comas de los autores de los paquetes, que coinciden con los nombres de perfil de nuget.org. Estos se muestran en la galería de NuGet, en nuget.org, y se usan para hacer referencias cruzadas a paquetes de los mismos autores.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-139">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="2b7bb-140">Elementos de metadatos opcionales</span><span class="sxs-lookup"><span data-stu-id="2b7bb-140">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="2b7bb-141">título</span><span class="sxs-lookup"><span data-stu-id="2b7bb-141">title</span></span>
<span data-ttu-id="2b7bb-142">Un título fácil de usar del paquete, que se usa normalmente en las visualizaciones de la interfaz de usuario, como en nuget.org, y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-142">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="2b7bb-143">Si no se especifica, se usa el identificador del paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-143">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="2b7bb-144">owners</span><span class="sxs-lookup"><span data-stu-id="2b7bb-144">owners</span></span>
<span data-ttu-id="2b7bb-145">Lista separada por comas de los creadores del paquete usando nombres de perfil en nuget.org. Suele ser la misma lista que en `authors` y se ignora al cargar el paquete en nuget.org. Vea [Administrar los propietarios de paquetes en nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-145">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="2b7bb-146">projectUrl</span><span class="sxs-lookup"><span data-stu-id="2b7bb-146">projectUrl</span></span>
<span data-ttu-id="2b7bb-147">Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-147">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="2b7bb-148">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="2b7bb-148">licenseUrl</span></span>
<span data-ttu-id="2b7bb-149">Dirección URL de la licencia del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-149">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="iconurl"></a><span data-ttu-id="2b7bb-150">iconUrl</span><span class="sxs-lookup"><span data-stu-id="2b7bb-150">iconUrl</span></span>
<span data-ttu-id="2b7bb-151">Dirección URL para una imagen de 64 x 64 con fondo transparente para usarla como icono para el paquete en la visualización de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-151">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="2b7bb-152">Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-152">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="2b7bb-153">Por ejemplo, para utilizar una imagen desde GitHub, use el archivo sin formato, como la dirección URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-153">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="2b7bb-154">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="2b7bb-154">requireLicenseAcceptance</span></span>
<span data-ttu-id="2b7bb-155">Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-155">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="2b7bb-156">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="2b7bb-156">developmentDependency</span></span>
<span data-ttu-id="2b7bb-157">*(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-157">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span>
#### <a name="summary"></a><span data-ttu-id="2b7bb-158">resumen</span><span class="sxs-lookup"><span data-stu-id="2b7bb-158">summary</span></span>
<span data-ttu-id="2b7bb-159">Descripción breve del paquete para su visualización en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-159">A short description of the package for UI display.</span></span> <span data-ttu-id="2b7bb-160">Si se omite, se usará una versión truncada de `description`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-160">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="2b7bb-161">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="2b7bb-161">releaseNotes</span></span>
<span data-ttu-id="2b7bb-162">*(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-162">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="2b7bb-163">copyright</span><span class="sxs-lookup"><span data-stu-id="2b7bb-163">copyright</span></span>
<span data-ttu-id="2b7bb-164">*(1.5+)* Información de copyright del paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-164">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="2b7bb-165">lenguaje</span><span class="sxs-lookup"><span data-stu-id="2b7bb-165">language</span></span>
<span data-ttu-id="2b7bb-166">Identificador de configuración regional del paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-166">The locale ID for the package.</span></span> <span data-ttu-id="2b7bb-167">Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-167">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="2b7bb-168">etiquetas</span><span class="sxs-lookup"><span data-stu-id="2b7bb-168">tags</span></span>
<span data-ttu-id="2b7bb-169">Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-169">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="2b7bb-170">posibilidad de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="2b7bb-170">serviceable</span></span> 
<span data-ttu-id="2b7bb-171">*(3.3+)* Solo para uso interno de NuGet.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-171">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="2b7bb-172">repositorio</span><span class="sxs-lookup"><span data-stu-id="2b7bb-172">repository</span></span>
<span data-ttu-id="2b7bb-173">Repositorio de metadatos, que consta de cuatro atributos opcionales: *tipo* y *url* *(4.0 y versiones posteriores)*, y *rama* y  *confirmación* *(4.6 y versiones posteriores)*.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-173">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="2b7bb-174">Estos atributos permiten asignar los archivos .nupkg en el repositorio que se crearon, con la posibilidad de obtener tal como se detalla como la rama individual o la confirmación de que se creó el paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-174">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="2b7bb-175">Debe ser una dirección url disponible públicamente que se puede invocar directamente mediante un software de control de versión.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-175">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="2b7bb-176">No debe ser una página html tal como está pensado para el equipo.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-176">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="2b7bb-177">Para vincular a la página del proyecto, use el `projectUrl` campo, en su lugar. |</span><span class="sxs-lookup"><span data-stu-id="2b7bb-177">For linking to project page, use the `projectUrl` field, instead.|</span></span>
#### <a name="minclientversion"></a><span data-ttu-id="2b7bb-178">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="2b7bb-178">minClientVersion</span></span>
<span data-ttu-id="2b7bb-179">Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-179">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="2b7bb-180">Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-180">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="2b7bb-181">Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-181">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="2b7bb-182">Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3".</span><span class="sxs-lookup"><span data-stu-id="2b7bb-182">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="2b7bb-183">Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-183">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="2b7bb-184">Elementos de colección</span><span class="sxs-lookup"><span data-stu-id="2b7bb-184">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="2b7bb-185">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="2b7bb-185">packageTypes</span></span>
<span data-ttu-id="2b7bb-186">*(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-186">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="2b7bb-187">Cada tipo de paquete tiene atributos de *name* y *version*.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-187">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="2b7bb-188">Vea [Establecimiento de un tipo de paquete](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-188">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="2b7bb-189">dependencias</span><span class="sxs-lookup"><span data-stu-id="2b7bb-189">dependencies</span></span>
<span data-ttu-id="2b7bb-190">Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-190">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="2b7bb-191">Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-191">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="2b7bb-192">Vea [Dependencias](#dependencies-element) a continuación.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-192">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="2b7bb-193">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="2b7bb-193">frameworkAssemblies</span></span>
<span data-ttu-id="2b7bb-194">*(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-194">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="2b7bb-195">Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-195">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="2b7bb-196">Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-196">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="2b7bb-197">referencias</span><span class="sxs-lookup"><span data-stu-id="2b7bb-197">references</span></span>
<span data-ttu-id="2b7bb-198">*(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-198">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="2b7bb-199">Cada referencia tiene un atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-199">Each reference has a *file* attribute.</span></span> <span data-ttu-id="2b7bb-200">`<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-200">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="2b7bb-201">Si se omite, se incluyen todas las referencias de `lib`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-201">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="2b7bb-202">Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-202">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="2b7bb-203">contentFiles</span><span class="sxs-lookup"><span data-stu-id="2b7bb-203">contentFiles</span></span>
<span data-ttu-id="2b7bb-204">*(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-204">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="2b7bb-205">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-205">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="2b7bb-206">Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-206">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="2b7bb-207">archivos</span><span class="sxs-lookup"><span data-stu-id="2b7bb-207">files</span></span> 
<span data-ttu-id="2b7bb-208">El nodo `<package>` puede contener un nodo `<files>` como un elemento del mismo nivel de `<metadata>`, o un elemento secundario `<contentFiles>` en `<metadata>`, para especificar los archivos de contenido y de ensamblado que se deben incluir en el paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-208">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="2b7bb-209">Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-209">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="2b7bb-210">Tokens de reemplazo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-210">Replacement tokens</span></span>

<span data-ttu-id="2b7bb-211">Al crear un paquete, el [comando `nuget pack`](../tools/cli-ref-pack.md) reemplaza los tokens delimitados por $ en el nodo `<metadata>` del archivo `.nuspec` por valores procedentes de un archivo de proyecto o del conmutador `-properties` del comando `pack`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-211">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="2b7bb-212">En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-212">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="2b7bb-213">Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-213">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="2b7bb-214">Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-214">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="2b7bb-215">Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-215">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="2b7bb-216">Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-216">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="2b7bb-217">Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-217">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="2b7bb-218">Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-218">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="2b7bb-219">Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-219">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="2b7bb-220">Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-220">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="2b7bb-221">Token</span><span class="sxs-lookup"><span data-stu-id="2b7bb-221">Token</span></span> | <span data-ttu-id="2b7bb-222">Origen del valor</span><span class="sxs-lookup"><span data-stu-id="2b7bb-222">Value source</span></span> | <span data-ttu-id="2b7bb-223">Valor</span><span class="sxs-lookup"><span data-stu-id="2b7bb-223">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="2b7bb-224">**$id$**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-224">**$id$**</span></span> | <span data-ttu-id="2b7bb-225">Archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="2b7bb-225">Project file</span></span> | <span data-ttu-id="2b7bb-226">AssemblyName (título) del archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="2b7bb-226">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="2b7bb-227">**$version$**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-227">**$version$**</span></span> | <span data-ttu-id="2b7bb-228">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-228">AssemblyInfo</span></span> | <span data-ttu-id="2b7bb-229">AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="2b7bb-229">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="2b7bb-230">**$author$**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-230">**$author$**</span></span> | <span data-ttu-id="2b7bb-231">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-231">AssemblyInfo</span></span> | <span data-ttu-id="2b7bb-232">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="2b7bb-232">AssemblyCompany</span></span> |
| <span data-ttu-id="2b7bb-233">**$title$**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-233">**$title$**</span></span> | <span data-ttu-id="2b7bb-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-234">AssemblyInfo</span></span> | <span data-ttu-id="2b7bb-235">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="2b7bb-235">AssemblyTitle</span></span> |
| <span data-ttu-id="2b7bb-236">**$description$**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-236">**$description$**</span></span> | <span data-ttu-id="2b7bb-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-237">AssemblyInfo</span></span> | <span data-ttu-id="2b7bb-238">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="2b7bb-238">AssemblyDescription</span></span> |
| <span data-ttu-id="2b7bb-239">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-239">**$copyright$**</span></span> | <span data-ttu-id="2b7bb-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-240">AssemblyInfo</span></span> | <span data-ttu-id="2b7bb-241">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="2b7bb-241">AssemblyCopyright</span></span> |
| <span data-ttu-id="2b7bb-242">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-242">**$configuration$**</span></span> | <span data-ttu-id="2b7bb-243">Archivo DLL del ensamblado</span><span class="sxs-lookup"><span data-stu-id="2b7bb-243">Assembly DLL</span></span> | <span data-ttu-id="2b7bb-244">Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-244">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="2b7bb-245">Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-245">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="2b7bb-246">Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-246">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="2b7bb-247">Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-247">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="2b7bb-248">Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-248">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="2b7bb-249">Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-249">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="2b7bb-250">Elemento de dependencias</span><span class="sxs-lookup"><span data-stu-id="2b7bb-250">Dependencies element</span></span>

<span data-ttu-id="2b7bb-251">El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-251">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="2b7bb-252">Los atributos de cada `<dependency>` son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-252">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="2b7bb-253">Atributo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-253">Attribute</span></span> | <span data-ttu-id="2b7bb-254">Descripción</span><span class="sxs-lookup"><span data-stu-id="2b7bb-254">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="2b7bb-255">(Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-255">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="2b7bb-256">(Obligatorio) Intervalo de versiones aceptable como dependencia.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-256">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="2b7bb-257">Vea [Control de versiones de paquetes](../reference/package-versioning.md#version-ranges-and-wildcards) para consultar la sintaxis exacta.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-257">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="2b7bb-258">include</span><span class="sxs-lookup"><span data-stu-id="2b7bb-258">include</span></span> | <span data-ttu-id="2b7bb-259">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-259">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="2b7bb-260">El valor predeterminado es `none`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-260">The default value is `none`.</span></span> |
| <span data-ttu-id="2b7bb-261">exclude</span><span class="sxs-lookup"><span data-stu-id="2b7bb-261">exclude</span></span> | <span data-ttu-id="2b7bb-262">Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="2b7bb-263">El valor predeterminado es `all`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-263">The  default value is `all`.</span></span> <span data-ttu-id="2b7bb-264">Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-264">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="2b7bb-265">Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-265">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="2b7bb-266">Etiqueta Include o Exclude</span><span class="sxs-lookup"><span data-stu-id="2b7bb-266">Include/Exclude tag</span></span> | <span data-ttu-id="2b7bb-267">Carpetas afectadas del destino</span><span class="sxs-lookup"><span data-stu-id="2b7bb-267">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="2b7bb-268">contentFiles</span><span class="sxs-lookup"><span data-stu-id="2b7bb-268">contentFiles</span></span> | <span data-ttu-id="2b7bb-269">Contenido</span><span class="sxs-lookup"><span data-stu-id="2b7bb-269">Content</span></span> |
| <span data-ttu-id="2b7bb-270">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="2b7bb-270">runtime</span></span> | <span data-ttu-id="2b7bb-271">Runtime, Resources y FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="2b7bb-271">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="2b7bb-272">compile</span><span class="sxs-lookup"><span data-stu-id="2b7bb-272">compile</span></span> | <span data-ttu-id="2b7bb-273">lib</span><span class="sxs-lookup"><span data-stu-id="2b7bb-273">lib</span></span> |
| <span data-ttu-id="2b7bb-274">compilación</span><span class="sxs-lookup"><span data-stu-id="2b7bb-274">build</span></span> | <span data-ttu-id="2b7bb-275">build (propiedades y destinos de MSBuild)</span><span class="sxs-lookup"><span data-stu-id="2b7bb-275">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="2b7bb-276">nativas</span><span class="sxs-lookup"><span data-stu-id="2b7bb-276">native</span></span> | <span data-ttu-id="2b7bb-277">nativas</span><span class="sxs-lookup"><span data-stu-id="2b7bb-277">native</span></span> |
| <span data-ttu-id="2b7bb-278">ninguna</span><span class="sxs-lookup"><span data-stu-id="2b7bb-278">none</span></span> | <span data-ttu-id="2b7bb-279">Sin carpetas</span><span class="sxs-lookup"><span data-stu-id="2b7bb-279">No folders</span></span> |
| <span data-ttu-id="2b7bb-280">todo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-280">all</span></span> | <span data-ttu-id="2b7bb-281">Todas las carpetas</span><span class="sxs-lookup"><span data-stu-id="2b7bb-281">All folders</span></span> |

<span data-ttu-id="2b7bb-282">Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-282">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="2b7bb-283">Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-283">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="2b7bb-284">Nota: al crear un archivo `.nuspec` a partir de un proyecto mediante `nuget spec`, las dependencias que existen en ese proyecto se incluyen automáticamente en el archivo `.nuspec` resultante.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-284">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="2b7bb-285">Grupos de dependencia</span><span class="sxs-lookup"><span data-stu-id="2b7bb-285">Dependency groups</span></span>

<span data-ttu-id="2b7bb-286">*Versión 2.0+*</span><span class="sxs-lookup"><span data-stu-id="2b7bb-286">*Version 2.0+*</span></span>

<span data-ttu-id="2b7bb-287">Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-287">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="2b7bb-288">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-288">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="2b7bb-289">Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-289">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="2b7bb-290">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-290">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="2b7bb-291">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-291">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="2b7bb-292">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-292">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="2b7bb-293">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-293">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="2b7bb-294">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="2b7bb-294">Explicit assembly references</span></span>

<span data-ttu-id="2b7bb-295">El elemento `<references>` especifica explícitamente los ensamblados a los que debe hacer referencia el proyecto de destino al usar el paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-295">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="2b7bb-296">Cuando este elemento está presente, NuGet agrega referencias únicamente a los ensamblados enumerados. No agrega referencias a otros ensamblados en la carpeta `lib` del paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-296">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="2b7bb-297">Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-297">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="2b7bb-298">Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-298">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="2b7bb-299">Al usar [contratos de código](/dotnet/framework/debug-trace-profile/code-contracts), por ejemplo, los ensamblados de contrato deben estar junto a los ensamblados en tiempo de ejecución que alimentan de manera que Visual Studio los pueda encontrar, pero no es necesario que el proyecto haga referencia a los ensamblados de contrato ni que se copien en la carpeta `bin` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-299">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="2b7bb-300">De forma parecida, las referencias explícitas se pueden usar para los marcos de pruebas unitarias, como XUnit, que necesita que sus ensamblados de herramientas estén situados junto a los ensamblados en tiempo de ejecución, pero no necesita que se incluyan como referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-300">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="2b7bb-301">Grupos de referencias</span><span class="sxs-lookup"><span data-stu-id="2b7bb-301">Reference groups</span></span>

<span data-ttu-id="2b7bb-302">Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-302">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="2b7bb-303">Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-303">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="2b7bb-304">Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-304">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="2b7bb-305">El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-305">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="2b7bb-306">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-306">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="2b7bb-307">El formato del grupo no se puede combinar con una lista plana.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-307">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="2b7bb-308">En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-308">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="2b7bb-309">Referencias de ensamblado de plataforma</span><span class="sxs-lookup"><span data-stu-id="2b7bb-309">Framework assembly references</span></span>

<span data-ttu-id="2b7bb-310">Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-310">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="2b7bb-311">Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-311">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="2b7bb-312">Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-312">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="2b7bb-313">El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-313">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="2b7bb-314">Atributo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-314">Attribute</span></span> | <span data-ttu-id="2b7bb-315">Descripción</span><span class="sxs-lookup"><span data-stu-id="2b7bb-315">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b7bb-316">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-316">**assemblyName**</span></span> | <span data-ttu-id="2b7bb-317">(Obligatorio) Nombre completo del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-317">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="2b7bb-318">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-318">**targetFramework**</span></span> | <span data-ttu-id="2b7bb-319">(Opcional) Especifica la plataforma de destino a la que se aplica esta referencia.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-319">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="2b7bb-320">Si se omite, indica que la referencia se aplica a todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-320">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="2b7bb-321">Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-321">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="2b7bb-322">En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-322">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="2b7bb-323">Incluir archivos de ensamblado</span><span class="sxs-lookup"><span data-stu-id="2b7bb-323">Including assembly files</span></span>

<span data-ttu-id="2b7bb-324">Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-324">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="2b7bb-325">El comando `nuget pack` selecciona automáticamente los archivos necesarios.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-325">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="2b7bb-326">Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-326">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="2b7bb-327">Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-327">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="2b7bb-328">Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-328">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="2b7bb-329">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-329">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="2b7bb-330">Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-330">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="2b7bb-331">Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-331">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="2b7bb-332">Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-332">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="2b7bb-333">Atributos del elemento File</span><span class="sxs-lookup"><span data-stu-id="2b7bb-333">File element attributes</span></span>

<span data-ttu-id="2b7bb-334">Cada elemento `<file>` especifica los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-334">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="2b7bb-335">Atributo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-335">Attribute</span></span> | <span data-ttu-id="2b7bb-336">Descripción</span><span class="sxs-lookup"><span data-stu-id="2b7bb-336">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b7bb-337">**src**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-337">**src**</span></span> | <span data-ttu-id="2b7bb-338">Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-338">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="2b7bb-339">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-339">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="2b7bb-340">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-340">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="2b7bb-341">**target**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-341">**target**</span></span> | <span data-ttu-id="2b7bb-342">La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-342">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="2b7bb-343">Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-343">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="2b7bb-344">**exclude**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-344">**exclude**</span></span> | <span data-ttu-id="2b7bb-345">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-345">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="2b7bb-346">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-346">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="2b7bb-347">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2b7bb-347">Examples</span></span>

<span data-ttu-id="2b7bb-348">**Ensamblado único**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-348">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="2b7bb-349">**Ensamblado único específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-349">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="2b7bb-350">**Conjunto de archivos DLL que usan un carácter comodín**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-350">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="2b7bb-351">**Archivos DLL para distintas plataformas**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-351">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="2b7bb-352">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-352">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="2b7bb-353">Incluir archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="2b7bb-353">Including content files</span></span>

<span data-ttu-id="2b7bb-354">Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-354">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="2b7bb-355">Como son inmutables, no se prevé que el proyecto de consumo los modifique.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-355">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="2b7bb-356">Entre los archivos de contenido se encuentran los siguientes:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-356">Example content files include:</span></span>

- <span data-ttu-id="2b7bb-357">Imágenes que se insertan como recursos</span><span class="sxs-lookup"><span data-stu-id="2b7bb-357">Images that are embedded as resources</span></span>
- <span data-ttu-id="2b7bb-358">Archivos de código fuente que ya están compilados</span><span class="sxs-lookup"><span data-stu-id="2b7bb-358">Source files that are already compiled</span></span>
- <span data-ttu-id="2b7bb-359">Scripts que se deben incluir con la salida de la compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="2b7bb-359">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="2b7bb-360">Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto</span><span class="sxs-lookup"><span data-stu-id="2b7bb-360">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="2b7bb-361">Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-361">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="2b7bb-362">Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-362">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="2b7bb-363">Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-363">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="2b7bb-364">Usar el elemento files para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="2b7bb-364">Using the files element for content files</span></span>

<span data-ttu-id="2b7bb-365">En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-365">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="2b7bb-366">**Archivos de contenido básicos**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-366">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="2b7bb-367">**Archivos de contenido con estructura de directorios**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-367">**Content files with directory structure**</span></span>

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

<span data-ttu-id="2b7bb-368">**Archivo de contenido específico para una plataforma de destino**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-368">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="2b7bb-369">**Archivo de contenido copiado en una carpeta con un punto en el nombre**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-369">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="2b7bb-370">En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-370">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="2b7bb-371">**Archivos de contenido sin extensión**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-371">**Content files without extensions**</span></span>

<span data-ttu-id="2b7bb-372">Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-372">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="2b7bb-373">**Archivos de contenido con una ruta de acceso y un destino profundos**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-373">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="2b7bb-374">En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-374">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="2b7bb-375">**Cambiar el nombre de un archivo de contenido del paquete**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-375">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="2b7bb-376">**Archivos de exclusión**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-376">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="2b7bb-377">Usar el elemento contentFiles para los archivos de contenido</span><span class="sxs-lookup"><span data-stu-id="2b7bb-377">Using the contentFiles element for content files</span></span>

<span data-ttu-id="2b7bb-378">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="2b7bb-378">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="2b7bb-379">De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-379">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="2b7bb-380">En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-380">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="2b7bb-381">Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-381">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="2b7bb-382">Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-382">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="2b7bb-383">Atributo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-383">Attribute</span></span> | <span data-ttu-id="2b7bb-384">Descripción</span><span class="sxs-lookup"><span data-stu-id="2b7bb-384">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b7bb-385">**include**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-385">**include**</span></span> | <span data-ttu-id="2b7bb-386">(Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-386">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="2b7bb-387">La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-387">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="2b7bb-388">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-388">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="2b7bb-389">**exclude**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-389">**exclude**</span></span> | <span data-ttu-id="2b7bb-390">Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-390">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="2b7bb-391">El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="2b7bb-392">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-392">**buildAction**</span></span> | <span data-ttu-id="2b7bb-393">Acción de compilación que se debe asignar al elemento de contenido para MSBuild, como `Content`, `None`, `Embedded Resource`, `Compile`, etc. El valor predeterminado es `Compile`.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-393">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="2b7bb-394">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-394">**copyToOutput**</span></span> | <span data-ttu-id="2b7bb-395">Un valor booleano que indica si se va a copiar los elementos de contenido a la compilación de carpeta de salida (o publicar).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-395">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="2b7bb-396">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-396">The default is false.</span></span> |
| <span data-ttu-id="2b7bb-397">**flatten**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-397">**flatten**</span></span> | <span data-ttu-id="2b7bb-398">Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-398">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="2b7bb-399">Esta marca solo funciona cuando la marca copyToOutput está establecida en true.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-399">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="2b7bb-400">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-400">The default is false.</span></span> |

<span data-ttu-id="2b7bb-401">Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-401">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="2b7bb-402">Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-402">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="2b7bb-403">La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-403">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="2b7bb-404">Estructura de carpetas de los paquetes</span><span class="sxs-lookup"><span data-stu-id="2b7bb-404">Package folder structure</span></span>

<span data-ttu-id="2b7bb-405">El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-405">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="2b7bb-406">`codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-406">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="2b7bb-407">`TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="2b7bb-407">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="2b7bb-408">Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.</span><span class="sxs-lookup"><span data-stu-id="2b7bb-408">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="2b7bb-409">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-409">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="2b7bb-410">Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-410">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="2b7bb-411">Sección contentFiles de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2b7bb-411">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="2b7bb-412">Archivos de ejemplo de nuspec</span><span class="sxs-lookup"><span data-stu-id="2b7bb-412">Example nuspec files</span></span>

<span data-ttu-id="2b7bb-413">**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-413">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="2b7bb-414">**Un archivo `.nuspec` con dependencias**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-414">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="2b7bb-415">**Un archivo `.nuspec` con archivos**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-415">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="2b7bb-416">**Un archivo `.nuspec` con ensamblados de plataforma**</span><span class="sxs-lookup"><span data-stu-id="2b7bb-416">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="2b7bb-417">En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:</span><span class="sxs-lookup"><span data-stu-id="2b7bb-417">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="2b7bb-418">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="2b7bb-418">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="2b7bb-419">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="2b7bb-419">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="2b7bb-420">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="2b7bb-420">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="2b7bb-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="2b7bb-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="2b7bb-422">Windows Phone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="2b7bb-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
