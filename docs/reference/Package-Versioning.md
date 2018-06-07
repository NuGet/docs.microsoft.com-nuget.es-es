---
title: Referencia de la versión de paquete de NuGet
description: Detalles exactos en la especificación de números de versión y las duraciones de otros paquetes en la que depende de un paquete de NuGet y cómo se instalan las dependencias.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: db529a4aa92f0f0bce0b52b21d2a01bf973d01f2
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817602"
---
# <a name="package-versioning"></a><span data-ttu-id="631a1-103">Control de versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="631a1-103">Package versioning</span></span>

<span data-ttu-id="631a1-104">Siempre se conoce que un paquete específico mediante su identificador de paquete y un número de versión exacta.</span><span class="sxs-lookup"><span data-stu-id="631a1-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="631a1-105">Por ejemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) en nuget.org tiene varios paquetes específicos de doce disponibles, que van desde la versión *4.1.10311* versión *6.1.3* (el estable de más reciente lanzamiento) y una variedad de versiones preliminares como *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="631a1-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="631a1-106">Al crear un paquete, asigne a un número de versión específico con un sufijo de texto opcional de una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="631a1-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="631a1-107">Por otro lado, al consumir paquetes, puede especificar un número de versión exacta o un intervalo de versiones aceptables.</span><span class="sxs-lookup"><span data-stu-id="631a1-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="631a1-108">En este tema:</span><span class="sxs-lookup"><span data-stu-id="631a1-108">In this topic:</span></span>

- <span data-ttu-id="631a1-109">[Conceptos básicos de la versión](#version-basics) incluidos los sufijos de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="631a1-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="631a1-110">Caracteres comodín ni intervalos de versiones</span><span class="sxs-lookup"><span data-stu-id="631a1-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="631a1-111">Números de versión normalizada</span><span class="sxs-lookup"><span data-stu-id="631a1-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="631a1-112">Conceptos básicos de versión</span><span class="sxs-lookup"><span data-stu-id="631a1-112">Version basics</span></span>

<span data-ttu-id="631a1-113">Es un número de versión específico en el formulario *Major.Minor.Patch [-sufijo]*, donde los componentes tienen los significados siguientes:</span><span class="sxs-lookup"><span data-stu-id="631a1-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="631a1-114">*Principales*: cambios importantes</span><span class="sxs-lookup"><span data-stu-id="631a1-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="631a1-115">*Secundaria*: nuevas características, pero compatible con versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="631a1-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="631a1-116">*Revisión*: solo compatible con versiones anteriores correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="631a1-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="631a1-117">*-Sufijo* (opcional): un guión seguido de una cadena que indica una versión preliminar (siguientes el [convención de control de versiones semántico o 1.0 SemVer](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="631a1-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="631a1-118">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="631a1-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="631a1-119">NuGet.org rechaza cualquier carga de paquete que no tiene un número de versión exacta.</span><span class="sxs-lookup"><span data-stu-id="631a1-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="631a1-120">La versión debe especificarse en el `.nuspec` o archivo de proyecto utilizado para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="631a1-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="631a1-121">Versiones preliminares</span><span class="sxs-lookup"><span data-stu-id="631a1-121">Pre-release versions</span></span>

<span data-ttu-id="631a1-122">Técnicamente hablando, creadores del paquete pueden utilizar cualquier cadena como un sufijo para denotar una versión preliminar, como NuGet trata cualquier dicha versión como versión preliminar y convierte en ninguna otra interpretación.</span><span class="sxs-lookup"><span data-stu-id="631a1-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="631a1-123">Es decir, la versión completa de cadena en la interfaz de usuario de muestra de NuGet está implicada, dejando cualquier interpretación de significado del sufijo para el consumidor.</span><span class="sxs-lookup"><span data-stu-id="631a1-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="631a1-124">Es decir, los desarrolladores de paquetes suelen seguir las convenciones de nomenclatura reconocidas:</span><span class="sxs-lookup"><span data-stu-id="631a1-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="631a1-125">`-alpha`: Versión alfa, se utiliza normalmente para experimentación y de trabajo en curso.</span><span class="sxs-lookup"><span data-stu-id="631a1-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="631a1-126">`-beta`: versión beta, que suele contar con todas las características de la próxima versión planificada, pero puede contener errores conocidos.</span><span class="sxs-lookup"><span data-stu-id="631a1-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="631a1-127">`-rc`: versión candidata para lanzamiento. Suele ser una versión potencialmente definitiva (estable) a menos que surjan errores importantes.</span><span class="sxs-lookup"><span data-stu-id="631a1-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="631a1-128">Es compatible con NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que es compatible con números de versión preliminar con la notación de puntos, como en *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="631a1-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="631a1-129">La notación de puntos no es compatible con versiones de NuGet anteriores a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="631a1-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="631a1-130">Puede utilizar un formulario como *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="631a1-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="631a1-131">Al resolver las referencias del paquete y varias versiones de paquete distinguirse sólo por sufijo, NuGet elige una versión sin un sufijo en primer lugar, a continuación, aplica la prioridad para la versión preliminar en orden alfabético inverso.</span><span class="sxs-lookup"><span data-stu-id="631a1-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="631a1-132">Por ejemplo, las siguientes versiones se elegiría en el orden mostrado:</span><span class="sxs-lookup"><span data-stu-id="631a1-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="631a1-133">Control de versiones semántico 2.0.0</span><span class="sxs-lookup"><span data-stu-id="631a1-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="631a1-134">Con NuGet 4.3.0+ y Visual Studio 2017 versión 15.3 +, NuGet es compatible con [control de versiones semántico 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="631a1-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="631a1-135">No se admite determinada semántica de SemVer v2.0.0 en clientes más antiguos.</span><span class="sxs-lookup"><span data-stu-id="631a1-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="631a1-136">NuGet se considera que una versión de paquete como SemVer v2.0.0 específico si se cumple alguna de las instrucciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="631a1-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="631a1-137">La etiqueta de versión preliminar es separados por puntos, por ejemplo, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="631a1-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="631a1-138">La versión tiene metadatos de la compilación, por ejemplo, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="631a1-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="631a1-139">Para nuget.org, un paquete se define como un paquete de v2.0.0 SemVer si se cumple alguna de las instrucciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="631a1-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="631a1-140">La versión del paquete es SemVer v2.0.0 compatible pero no SemVer v1.0.0 compatible, como se definió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="631a1-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="631a1-141">Cualquiera de los intervalos de versiones de dependencia del paquete tiene una versión mínima o máxima que es SemVer v2.0.0 compatible pero no SemVer v1.0.0 compatible, definidos anteriormente; Por ejemplo, *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="631a1-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="631a1-142">Si carga un paquete de v2.0.0 específica SemVer en nuget.org, el paquete es invisible para los clientes más antiguos y están disponibles para los siguientes clientes de NuGet:</span><span class="sxs-lookup"><span data-stu-id="631a1-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="631a1-143">4.3.0+ de NuGet</span><span class="sxs-lookup"><span data-stu-id="631a1-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="631a1-144">Visual Studio 2017 versión 15.3 +</span><span class="sxs-lookup"><span data-stu-id="631a1-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="631a1-145">Visual Studio 2015 con [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="631a1-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="631a1-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="631a1-146">dotnet</span></span>
  - <span data-ttu-id="631a1-147">dotnetcore.exe (2.0.0+ del SDK. NET)</span><span class="sxs-lookup"><span data-stu-id="631a1-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="631a1-148">Clientes de otro fabricante:</span><span class="sxs-lookup"><span data-stu-id="631a1-148">Third-party clients:</span></span>

- <span data-ttu-id="631a1-149">JetBrains piloto</span><span class="sxs-lookup"><span data-stu-id="631a1-149">JetBrains Rider</span></span>
- <span data-ttu-id="631a1-150">Paket versión 5.0 +</span><span class="sxs-lookup"><span data-stu-id="631a1-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="631a1-151">Caracteres comodín ni intervalos de versiones</span><span class="sxs-lookup"><span data-stu-id="631a1-151">Version ranges and wildcards</span></span>

<span data-ttu-id="631a1-152">Cuando se hace referencia a las dependencias de paquete, NuGet admite el uso de la notación de intervalo para especificar intervalos de versiones, resumidos del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="631a1-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="631a1-153">Notation</span><span class="sxs-lookup"><span data-stu-id="631a1-153">Notation</span></span> | <span data-ttu-id="631a1-154">Regla aplicada</span><span class="sxs-lookup"><span data-stu-id="631a1-154">Applied rule</span></span> | <span data-ttu-id="631a1-155">Descripción</span><span class="sxs-lookup"><span data-stu-id="631a1-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="631a1-156">1.0</span><span class="sxs-lookup"><span data-stu-id="631a1-156">1.0</span></span> | <span data-ttu-id="631a1-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="631a1-157">x ≥ 1.0</span></span> | <span data-ttu-id="631a1-158">Versión mínima, ambos inclusive</span><span class="sxs-lookup"><span data-stu-id="631a1-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="631a1-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="631a1-159">(1.0,)</span></span> | <span data-ttu-id="631a1-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="631a1-160">x > 1.0</span></span> | <span data-ttu-id="631a1-161">Versión mínima, exclusivo</span><span class="sxs-lookup"><span data-stu-id="631a1-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="631a1-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="631a1-162">[1.0]</span></span> | <span data-ttu-id="631a1-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="631a1-163">x == 1.0</span></span> | <span data-ttu-id="631a1-164">Coincidencia de versión exacta</span><span class="sxs-lookup"><span data-stu-id="631a1-164">Exact version match</span></span> |
| <span data-ttu-id="631a1-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="631a1-165">(,1.0]</span></span> | <span data-ttu-id="631a1-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="631a1-166">x ≤ 1.0</span></span> | <span data-ttu-id="631a1-167">Versión máxima, ambos inclusive</span><span class="sxs-lookup"><span data-stu-id="631a1-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="631a1-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="631a1-168">(,1.0)</span></span> | <span data-ttu-id="631a1-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="631a1-169">x < 1.0</span></span> | <span data-ttu-id="631a1-170">Versión máxima, exclusivo</span><span class="sxs-lookup"><span data-stu-id="631a1-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="631a1-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="631a1-171">[1.0,2.0]</span></span> | <span data-ttu-id="631a1-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="631a1-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="631a1-173">Intervalo exacto, ambos inclusive</span><span class="sxs-lookup"><span data-stu-id="631a1-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="631a1-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="631a1-174">(1.0,2.0)</span></span> | <span data-ttu-id="631a1-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="631a1-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="631a1-176">Intervalo exacto, exclusivo</span><span class="sxs-lookup"><span data-stu-id="631a1-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="631a1-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="631a1-177">[1.0,2.0)</span></span> | <span data-ttu-id="631a1-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="631a1-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="631a1-179">Inclusivo mínimo y exclusivo máximo versión mixta</span><span class="sxs-lookup"><span data-stu-id="631a1-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="631a1-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="631a1-180">(1.0)</span></span>    | <span data-ttu-id="631a1-181">no válidos</span><span class="sxs-lookup"><span data-stu-id="631a1-181">invalid</span></span> | <span data-ttu-id="631a1-182">no válidos</span><span class="sxs-lookup"><span data-stu-id="631a1-182">invalid</span></span> |

<span data-ttu-id="631a1-183">Cuando se utiliza el formato PackageReference, NuGet también admite la notación de un carácter comodín, \*, para principal, secundaria, revisión y partes de sufijo de versión preliminar del número.</span><span class="sxs-lookup"><span data-stu-id="631a1-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="631a1-184">No se admite caracteres comodín con el `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="631a1-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="631a1-185">No se incluyen las versiones preliminares al resolver los intervalos de versiones.</span><span class="sxs-lookup"><span data-stu-id="631a1-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="631a1-186">Versiones preliminares *son* incluido cuando se usa un carácter comodín (\*).</span><span class="sxs-lookup"><span data-stu-id="631a1-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="631a1-187">El intervalo de versiones *[1.0,2.0]*, por ejemplo, no incluye la versión beta 2.0, pero la notación de comodín _2.0-\*_ does.</span><span class="sxs-lookup"><span data-stu-id="631a1-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="631a1-188">Vea [emitir 912](https://github.com/NuGet/Home/issues/912) para obtener más información sobre los caracteres comodín de la versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="631a1-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="631a1-189">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="631a1-189">Examples</span></span>

<span data-ttu-id="631a1-190">Especifique siempre una versión o un intervalo de versiones para las dependencias de paquete en los archivos de proyecto, `packages.config` archivos, y `.nuspec` archivos.</span><span class="sxs-lookup"><span data-stu-id="631a1-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="631a1-191">Sin una versión o un intervalo de versiones, NuGet 2.8.x y elige anteriormente la versión más reciente de paquetes disponibles al resolver una dependencia, mientras que NuGet 3.x y versiones posteriores elige la versión más antigua del paquete.</span><span class="sxs-lookup"><span data-stu-id="631a1-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="631a1-192">Especificar una versión o intervalo evita esta incertidumbre.</span><span class="sxs-lookup"><span data-stu-id="631a1-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="631a1-193">Referencias en los archivos de proyecto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="631a1-193">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="631a1-194">**Hace referencia en `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="631a1-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="631a1-195">En `packages.config`, todas las dependencias se muestran con un exacta `version` atributo que se utiliza al restaurar paquetes.</span><span class="sxs-lookup"><span data-stu-id="631a1-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="631a1-196">El `allowedVersions` atributo se utiliza solo durante las operaciones de actualización para restringir las versiones a la que el paquete que se actualicen.</span><span class="sxs-lookup"><span data-stu-id="631a1-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="631a1-197">**Hace referencia en `.nuspec` archivos**</span><span class="sxs-lookup"><span data-stu-id="631a1-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="631a1-198">El `version` de atributo en un `<dependency>` elemento describe las versiones de intervalo que son aceptables para una dependencia.</span><span class="sxs-lookup"><span data-stu-id="631a1-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="631a1-199">Números de versión normalizada</span><span class="sxs-lookup"><span data-stu-id="631a1-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="631a1-200">Se trata de una novedad para NuGet 3.4 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="631a1-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="631a1-201">Al obtener los paquetes de un repositorio durante la instalación, vuelva a instalar o restaurar las operaciones, NuGet 3.4 + trata los números de versión como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="631a1-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="631a1-202">Se quitan los ceros iniciales de números de versión:</span><span class="sxs-lookup"><span data-stu-id="631a1-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="631a1-203">Se omitirá un cero en la cuarta parte del número de versión</span><span class="sxs-lookup"><span data-stu-id="631a1-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="631a1-204">Esta normalización no afecta a los números de versión de los paquetes a sí mismos; afecta a cómo NuGet coincide solo versiones al resolver las dependencias.</span><span class="sxs-lookup"><span data-stu-id="631a1-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="631a1-205">Sin embargo, los repositorios de paquete de NuGet deben tratar estos valores en la misma manera que NuGet para evitar la duplicación de la versión de paquete.</span><span class="sxs-lookup"><span data-stu-id="631a1-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="631a1-206">Por lo tanto un repositorio que contiene la versión *1.0* de un paquete no deben también hospedar versión *1.0.0* como un paquete distinto e independiente.</span><span class="sxs-lookup"><span data-stu-id="631a1-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
