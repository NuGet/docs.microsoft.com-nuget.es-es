---
title: Referencia de versión del paquete NuGet
description: Detalles exactos sobre cómo especificar números de versión e intervalos de otros paquetes de los que depende un paquete NuGet y cómo se instalan las dependencias.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520355"
---
# <a name="package-versioning"></a><span data-ttu-id="586f7-103">Control de versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="586f7-103">Package versioning</span></span>

<span data-ttu-id="586f7-104">Siempre se hace referencia a un paquete específico mediante su identificador de paquete y un número de versión exacto.</span><span class="sxs-lookup"><span data-stu-id="586f7-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="586f7-105">Por ejemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) en nuget.org tiene varias docenas de paquetes específicos disponibles, que van desde la versión *4.1.10311* a la versión *6.1.3* (la versión estable más reciente) y una variedad de versiones preliminares como *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="586f7-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="586f7-106">Al crear un paquete, se asigna un número de versión específico con un sufijo de texto de versión preliminar opcional.</span><span class="sxs-lookup"><span data-stu-id="586f7-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="586f7-107">Por otra parte, al consumir paquetes puede especificar un número de versión exacto o un intervalo de versiones admisibles.</span><span class="sxs-lookup"><span data-stu-id="586f7-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="586f7-108">En este tema:</span><span class="sxs-lookup"><span data-stu-id="586f7-108">In this topic:</span></span>

- <span data-ttu-id="586f7-109">[Aspectos básicos de la versión](#version-basics), incluidos los sufijos de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="586f7-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="586f7-110">Intervalos de versiones y caracteres comodín</span><span class="sxs-lookup"><span data-stu-id="586f7-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="586f7-111">Números de versión normalizados</span><span class="sxs-lookup"><span data-stu-id="586f7-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="586f7-112">Aspectos básicos de la versión</span><span class="sxs-lookup"><span data-stu-id="586f7-112">Version basics</span></span>

<span data-ttu-id="586f7-113">Un número de versión específico tiene el formato *.Revisión[-Sufijo]* , donde los componentes tienen los significados siguientes:</span><span class="sxs-lookup"><span data-stu-id="586f7-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="586f7-114">*VersiónPrincipal*: Cambios importantes</span><span class="sxs-lookup"><span data-stu-id="586f7-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="586f7-115">*VersiónSecundaria*: nuevas características, compatibles con versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="586f7-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="586f7-116">*Revisión*: solo correcciones de errores compatibles con versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="586f7-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="586f7-117">*-Sufijo* (opcional): un guión seguido de una cadena que denota una versión preliminar (según la [convención de Versionamiento Semántico o SemVer 1.0](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="586f7-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="586f7-118">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="586f7-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="586f7-119">nuget.org rechaza cualquier carga de paquetes que carezca de un número de versión exacto.</span><span class="sxs-lookup"><span data-stu-id="586f7-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="586f7-120">La versión debe especificarse en el archivo `.nuspec` o de proyecto que se usa para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="586f7-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="586f7-121">Versiones preliminares</span><span class="sxs-lookup"><span data-stu-id="586f7-121">Pre-release versions</span></span>

<span data-ttu-id="586f7-122">Técnicamente hablando, los creadores de paquetes pueden usar cualquier cadena como sufijo para denotar una versión preliminar, ya que NuGet trata cualquier versión como versión preliminar y no realiza ninguna otra interpretación.</span><span class="sxs-lookup"><span data-stu-id="586f7-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="586f7-123">Es decir, NuGet muestra la cadena de versión completa en cualquier interfaz de usuario que esté implicada, dejando cualquier interpretación del significado del sufijo para el consumidor.</span><span class="sxs-lookup"><span data-stu-id="586f7-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="586f7-124">Dicho esto, los desarrolladores de paquetes generalmente siguen las convenciones de nomenclatura reconocidas:</span><span class="sxs-lookup"><span data-stu-id="586f7-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="586f7-125">`-alpha`: versión alfa, que se suele usar para el trabajo en curso y la experimentación.</span><span class="sxs-lookup"><span data-stu-id="586f7-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="586f7-126">`-beta`: versión beta, que suele contar con todas las características de la próxima versión planificada, pero puede contener errores conocidos.</span><span class="sxs-lookup"><span data-stu-id="586f7-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="586f7-127">`-rc`: versión candidata para lanzamiento. Suele ser una versión potencialmente definitiva (estable) a menos que surjan errores importantes.</span><span class="sxs-lookup"><span data-stu-id="586f7-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="586f7-128">NuGet 4.3.0+ admite [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que es compatible con números de versión preliminar con notación de puntos, como en *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="586f7-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="586f7-129">La notación de puntos no es compatible con versiones de NuGet anteriores a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="586f7-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="586f7-130">Puede usar un formato como *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="586f7-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="586f7-131">Cuando resuelva referencias de paquete y varias versiones de paquete solo se diferencien en el sufijo, NuGet elegirá primero una versión sin sufijo y luego aplicará la prioridad a las versiones preliminares en orden alfabético inverso.</span><span class="sxs-lookup"><span data-stu-id="586f7-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="586f7-132">Por ejemplo, se elegirían las siguientes versiones en el orden exacto mostrado:</span><span class="sxs-lookup"><span data-stu-id="586f7-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="586f7-133">Versionamiento Semántico 2.0.0</span><span class="sxs-lookup"><span data-stu-id="586f7-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="586f7-134">Con Nuget 4.3.0+ y Visual Studio 2017 versión 15.3+, NuGet admite [Versionamiento Semántico 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="586f7-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="586f7-135">Ciertas semánticas de SemVer v2.0.0 no se admiten en los clientes más antiguos.</span><span class="sxs-lookup"><span data-stu-id="586f7-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="586f7-136">NuGet considera que una versión de paquete es específica de SemVer v2.0.0 si alguna de las siguientes afirmaciones es verdadera:</span><span class="sxs-lookup"><span data-stu-id="586f7-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="586f7-137">La etiqueta de versión preliminar está separada por puntos, por ejemplo, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="586f7-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="586f7-138">La versión tiene metadatos de compilación, por ejemplo, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="586f7-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="586f7-139">En el caso de nuget.org, se define un paquete como un paquete de SemVer v2.0.0 si se cumple alguna de las siguientes instrucciones:</span><span class="sxs-lookup"><span data-stu-id="586f7-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="586f7-140">La versión propia del paquete es compatible con SemVer v2.0.0, pero no con SemVer v1.0.0, tal y como se definió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="586f7-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="586f7-141">Cualquiera de los intervalos de versiones de dependencia del paquete tiene una versión mínima o máxima que es compatible con SemVer v2.0.0 pero no con SemVer v1.0.0, definida anteriormente; por ejemplo, *[1.0.0-alpha.1, )* .</span><span class="sxs-lookup"><span data-stu-id="586f7-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="586f7-142">Si carga un paquete específico de SemVer v2.0.0 en nuget.org, dicho paquete no es visible para los clientes más antiguos y solo está disponible para los siguientes clientes de NuGet:</span><span class="sxs-lookup"><span data-stu-id="586f7-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="586f7-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="586f7-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="586f7-144">Versión de Visual Studio 2017 15.3+</span><span class="sxs-lookup"><span data-stu-id="586f7-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="586f7-145">Visual Studio 2015 con [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="586f7-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="586f7-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="586f7-146">dotnet</span></span>
  - <span data-ttu-id="586f7-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="586f7-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="586f7-148">Clientes de terceros:</span><span class="sxs-lookup"><span data-stu-id="586f7-148">Third-party clients:</span></span>

- <span data-ttu-id="586f7-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="586f7-149">JetBrains Rider</span></span>
- <span data-ttu-id="586f7-150">Versión de Paket 5.0+</span><span class="sxs-lookup"><span data-stu-id="586f7-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="586f7-151">Intervalos de versiones y caracteres comodín</span><span class="sxs-lookup"><span data-stu-id="586f7-151">Version ranges and wildcards</span></span>

<span data-ttu-id="586f7-152">Cuando se hace referencia a las dependencias de paquete, NuGet admite el uso de la notación de intervalo para especificar intervalos de versión, que se resumen de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="586f7-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="586f7-153">Notation</span><span class="sxs-lookup"><span data-stu-id="586f7-153">Notation</span></span> | <span data-ttu-id="586f7-154">Regla aplicada</span><span class="sxs-lookup"><span data-stu-id="586f7-154">Applied rule</span></span> | <span data-ttu-id="586f7-155">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="586f7-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="586f7-156">1.0</span><span class="sxs-lookup"><span data-stu-id="586f7-156">1.0</span></span> | <span data-ttu-id="586f7-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="586f7-157">x ≥ 1.0</span></span> | <span data-ttu-id="586f7-158">Versión mínima, incluida</span><span class="sxs-lookup"><span data-stu-id="586f7-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="586f7-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="586f7-159">(1.0,)</span></span> | <span data-ttu-id="586f7-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="586f7-160">x > 1.0</span></span> | <span data-ttu-id="586f7-161">Versión mínima, excluida</span><span class="sxs-lookup"><span data-stu-id="586f7-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="586f7-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="586f7-162">[1.0]</span></span> | <span data-ttu-id="586f7-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="586f7-163">x == 1.0</span></span> | <span data-ttu-id="586f7-164">Coincidencia de versión exacta</span><span class="sxs-lookup"><span data-stu-id="586f7-164">Exact version match</span></span> |
| <span data-ttu-id="586f7-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="586f7-165">(,1.0]</span></span> | <span data-ttu-id="586f7-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="586f7-166">x ≤ 1.0</span></span> | <span data-ttu-id="586f7-167">Versión máxima, incluida</span><span class="sxs-lookup"><span data-stu-id="586f7-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="586f7-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="586f7-168">(,1.0)</span></span> | <span data-ttu-id="586f7-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="586f7-169">x < 1.0</span></span> | <span data-ttu-id="586f7-170">Versión máxima, excluida</span><span class="sxs-lookup"><span data-stu-id="586f7-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="586f7-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="586f7-171">[1.0,2.0]</span></span> | <span data-ttu-id="586f7-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="586f7-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="586f7-173">Intervalo exacto, ambos incluidos</span><span class="sxs-lookup"><span data-stu-id="586f7-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="586f7-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="586f7-174">(1.0,2.0)</span></span> | <span data-ttu-id="586f7-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="586f7-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="586f7-176">Intervalo exacto, ambos excluidos</span><span class="sxs-lookup"><span data-stu-id="586f7-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="586f7-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="586f7-177">[1.0,2.0)</span></span> | <span data-ttu-id="586f7-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="586f7-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="586f7-179">Versión mínima incluida y versión máxima excluida mezcladas</span><span class="sxs-lookup"><span data-stu-id="586f7-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="586f7-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="586f7-180">(1.0)</span></span>    | <span data-ttu-id="586f7-181">no válidos</span><span class="sxs-lookup"><span data-stu-id="586f7-181">invalid</span></span> | <span data-ttu-id="586f7-182">no válidos</span><span class="sxs-lookup"><span data-stu-id="586f7-182">invalid</span></span> |

<span data-ttu-id="586f7-183">Cuando se usa el formato PackageReference, NuGet admite también el uso de una notación de caracteres comodín, \*, en las partes del número de versión principal, versión secundaria, revisión y sufijo de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="586f7-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="586f7-184">Los caracteres comodín no se admiten con el formato `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="586f7-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="586f7-185">Los intervalos de versiones de PackageReference incluyen las versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="586f7-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="586f7-186">Por diseño, las versiones flotantes no resuelven las versiones preliminares, a menos que se opte por ellas.</span><span class="sxs-lookup"><span data-stu-id="586f7-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="586f7-187">Para ver el estado de la solicitud de características relacionadas, consulte el [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="586f7-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="586f7-188">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="586f7-188">Examples</span></span>

<span data-ttu-id="586f7-189">Especifique siempre una versión o un intervalo de versiones para las dependencias de paquete en archivos de proyecto, archivos `packages.config` y archivos `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="586f7-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="586f7-190">Sin una versión o un intervalo de versiones, NuGet 2.8.x y las versiones anteriores eligen la versión del paquete más reciente disponible al resolver una dependencia, mientras que NuGet 3.x y las versiones posteriores eligen la versión de paquete más baja.</span><span class="sxs-lookup"><span data-stu-id="586f7-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="586f7-191">La especificación de una versión o un intervalo de versiones evita esta incertidumbre.</span><span class="sxs-lookup"><span data-stu-id="586f7-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="586f7-192">Referencias en los archivos de proyecto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="586f7-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="586f7-193">**Referencias en `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="586f7-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="586f7-194">En `packages.config`, todas las dependencias se muestran con un atributo `version` exacto que se usa al restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="586f7-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="586f7-195">El atributo `allowedVersions` solo se usa durante las operaciones de actualización para restringir las versiones en las que se puede actualizar el paquete.</span><span class="sxs-lookup"><span data-stu-id="586f7-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="586f7-196">**Referencias en archivos `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="586f7-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="586f7-197">El atributo `version` de un elemento `<dependency>` describe las versiones de intervalo que son aceptables para una dependencia.</span><span class="sxs-lookup"><span data-stu-id="586f7-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="586f7-198">Números de versión normalizados</span><span class="sxs-lookup"><span data-stu-id="586f7-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="586f7-199">Se trata de un cambio importante en NuGet 3.4 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="586f7-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="586f7-200">Al obtener paquetes de un repositorio durante las operaciones de instalación, reinstalación o restauración, NuGet 3.4+ trata los números de versión de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="586f7-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="586f7-201">Los ceros a la izquierda se quitan de los números de versión:</span><span class="sxs-lookup"><span data-stu-id="586f7-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="586f7-202">Un cero en la cuarta parte del número de versión se omitirá</span><span class="sxs-lookup"><span data-stu-id="586f7-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="586f7-203">Las operaciones `pack` y `restore` normalizan las versiones siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="586f7-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="586f7-204">En el caso de los paquetes ya creados, esta normalización no afecta a los números de versión de los propios paquetes; solo afecta al modo en que NuGet coincide con las versiones cuando se resuelven las dependencias.</span><span class="sxs-lookup"><span data-stu-id="586f7-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="586f7-205">Sin embargo, los repositorios de paquetes NuGet deben tratar estos valores de la misma manera que NuGet para evitar la duplicación de la versión del paquete.</span><span class="sxs-lookup"><span data-stu-id="586f7-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="586f7-206">Por lo tanto, un repositorio que contiene la versión *1.0* de un paquete no debe hospedar también la versión *1.0.0* como un paquete independiente y diferente.</span><span class="sxs-lookup"><span data-stu-id="586f7-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
