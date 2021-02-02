---
title: Referencia de versión del paquete NuGet
description: Detalles exactos sobre cómo especificar números de versión e intervalos de otros paquetes de los que depende un paquete NuGet y cómo se instalan las dependencias.
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 5ba7860fae1037c0c0eb4c55d2df12d98b1d77cf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775114"
---
# <a name="package-versioning"></a><span data-ttu-id="b7800-103">Control de versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="b7800-103">Package versioning</span></span>

<span data-ttu-id="b7800-104">Siempre se hace referencia a un paquete específico mediante su identificador de paquete y un número de versión exacto.</span><span class="sxs-lookup"><span data-stu-id="b7800-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="b7800-105">Por ejemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) en nuget.org tiene varias docenas de paquetes específicos disponibles, que van desde la versión *4.1.10311* a la versión *6.1.3* (la versión estable más reciente) y una variedad de versiones preliminares como *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="b7800-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="b7800-106">Al crear un paquete, se asigna un número de versión específico con un sufijo de texto de versión preliminar opcional.</span><span class="sxs-lookup"><span data-stu-id="b7800-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="b7800-107">Por otra parte, al consumir paquetes puede especificar un número de versión exacto o un intervalo de versiones admisibles.</span><span class="sxs-lookup"><span data-stu-id="b7800-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="b7800-108">En este tema:</span><span class="sxs-lookup"><span data-stu-id="b7800-108">In this topic:</span></span>

- <span data-ttu-id="b7800-109">[Aspectos básicos de la versión](#version-basics), incluidos los sufijos de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="b7800-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="b7800-110">Rangos de versiones</span><span class="sxs-lookup"><span data-stu-id="b7800-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="b7800-111">Números de versión normalizados</span><span class="sxs-lookup"><span data-stu-id="b7800-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="b7800-112">Aspectos básicos de la versión</span><span class="sxs-lookup"><span data-stu-id="b7800-112">Version basics</span></span>

<span data-ttu-id="b7800-113">Un número de versión específico tiene el formato *.Revisión[-Sufijo]* , donde los componentes tienen los significados siguientes:</span><span class="sxs-lookup"><span data-stu-id="b7800-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="b7800-114">*VersiónPrincipal*: Cambios importantes</span><span class="sxs-lookup"><span data-stu-id="b7800-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="b7800-115">*VersiónSecundaria*: nuevas características, compatibles con versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="b7800-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="b7800-116">*Revisión*: solo correcciones de errores compatibles con versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="b7800-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="b7800-117">*-Sufijo* (opcional): un guión seguido de una cadena que denota una versión preliminar (según la [convención de Versionamiento Semántico o SemVer 1.0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="b7800-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="b7800-118">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="b7800-118">**Examples:**</span></span>

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="b7800-119">nuget.org rechaza cualquier carga de paquetes que carezca de un número de versión exacto.</span><span class="sxs-lookup"><span data-stu-id="b7800-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="b7800-120">La versión debe especificarse en el archivo `.nuspec` o de proyecto que se usa para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="b7800-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="b7800-121">Versiones preliminares</span><span class="sxs-lookup"><span data-stu-id="b7800-121">Pre-release versions</span></span>

<span data-ttu-id="b7800-122">Técnicamente hablando, los creadores de paquetes pueden usar cualquier cadena como sufijo para denotar una versión preliminar, ya que NuGet trata cualquier versión como versión preliminar y no realiza ninguna otra interpretación.</span><span class="sxs-lookup"><span data-stu-id="b7800-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="b7800-123">Es decir, NuGet muestra la cadena de versión completa en cualquier interfaz de usuario que esté implicada, dejando cualquier interpretación del significado del sufijo para el consumidor.</span><span class="sxs-lookup"><span data-stu-id="b7800-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="b7800-124">Dicho esto, los desarrolladores de paquetes generalmente siguen las convenciones de nomenclatura reconocidas:</span><span class="sxs-lookup"><span data-stu-id="b7800-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="b7800-125">`-alpha`: versión alfa, que se suele usar para el trabajo en curso y la experimentación.</span><span class="sxs-lookup"><span data-stu-id="b7800-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="b7800-126">`-beta`: versión beta, que suele contar con todas las características de la próxima versión planificada, pero puede contener errores conocidos.</span><span class="sxs-lookup"><span data-stu-id="b7800-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="b7800-127">`-rc`: versión candidata para lanzamiento. Suele ser una versión potencialmente definitiva (estable) a menos que surjan errores importantes.</span><span class="sxs-lookup"><span data-stu-id="b7800-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="b7800-128">NuGet 4.3.0+ admite [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), que es compatible con números de versión preliminar con notación de puntos, como en *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="b7800-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="b7800-129">La notación de puntos no es compatible con versiones de NuGet anteriores a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="b7800-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="b7800-130">Puede usar un formato como *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="b7800-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="b7800-131">Cuando resuelva referencias de paquete y varias versiones de paquete solo se diferencien en el sufijo, NuGet elegirá primero una versión sin sufijo y luego aplicará la prioridad a las versiones preliminares en orden alfabético inverso.</span><span class="sxs-lookup"><span data-stu-id="b7800-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="b7800-132">Por ejemplo, se elegirían las siguientes versiones en el orden exacto mostrado:</span><span class="sxs-lookup"><span data-stu-id="b7800-132">For example, the following versions would be chosen in the exact order shown:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a><span data-ttu-id="b7800-133">Versionamiento Semántico 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b7800-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="b7800-134">Con Nuget 4.3.0+ y Visual Studio 2017 versión 15.3+, NuGet admite [Versionamiento Semántico 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="b7800-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="b7800-135">Ciertas semánticas de SemVer v2.0.0 no se admiten en los clientes más antiguos.</span><span class="sxs-lookup"><span data-stu-id="b7800-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="b7800-136">NuGet considera que una versión de paquete es específica de SemVer v2.0.0 si alguna de las siguientes afirmaciones es verdadera:</span><span class="sxs-lookup"><span data-stu-id="b7800-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="b7800-137">La etiqueta de versión preliminar está separada por puntos, por ejemplo, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="b7800-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="b7800-138">La versión tiene metadatos de compilación, por ejemplo, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="b7800-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="b7800-139">En el caso de nuget.org, se define un paquete como un paquete de SemVer v2.0.0 si se cumple alguna de las siguientes instrucciones:</span><span class="sxs-lookup"><span data-stu-id="b7800-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="b7800-140">La versión propia del paquete es compatible con SemVer v2.0.0, pero no con SemVer v1.0.0, tal y como se definió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b7800-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="b7800-141">Cualquiera de los intervalos de versiones de dependencia del paquete tiene una versión mínima o máxima que es compatible con SemVer v2.0.0 pero no con SemVer v1.0.0, definida anteriormente; por ejemplo, *[1.0.0-alpha.1, )* .</span><span class="sxs-lookup"><span data-stu-id="b7800-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="b7800-142">Si carga un paquete específico de SemVer v2.0.0 en nuget.org, dicho paquete no es visible para los clientes más antiguos y solo está disponible para los siguientes clientes de NuGet:</span><span class="sxs-lookup"><span data-stu-id="b7800-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="b7800-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="b7800-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="b7800-144">Versión de Visual Studio 2017 15.3+</span><span class="sxs-lookup"><span data-stu-id="b7800-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="b7800-145">Visual Studio 2015 con [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="b7800-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="b7800-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="b7800-146">dotnet</span></span>
  - <span data-ttu-id="b7800-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="b7800-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="b7800-148">Clientes de terceros:</span><span class="sxs-lookup"><span data-stu-id="b7800-148">Third-party clients:</span></span>

- <span data-ttu-id="b7800-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="b7800-149">JetBrains Rider</span></span>
- <span data-ttu-id="b7800-150">Versión de Paket 5.0+</span><span class="sxs-lookup"><span data-stu-id="b7800-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="b7800-151">Rangos de versiones</span><span class="sxs-lookup"><span data-stu-id="b7800-151">Version ranges</span></span>

<span data-ttu-id="b7800-152">Cuando se hace referencia a las dependencias de paquete, NuGet admite el uso de la notación de intervalo para especificar intervalos de versión, que se resumen de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="b7800-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="b7800-153">Notation</span><span class="sxs-lookup"><span data-stu-id="b7800-153">Notation</span></span> | <span data-ttu-id="b7800-154">Regla aplicada</span><span class="sxs-lookup"><span data-stu-id="b7800-154">Applied rule</span></span> | <span data-ttu-id="b7800-155">Descripción</span><span class="sxs-lookup"><span data-stu-id="b7800-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="b7800-156">1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-156">1.0</span></span> | <span data-ttu-id="b7800-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-157">x ≥ 1.0</span></span> | <span data-ttu-id="b7800-158">Versión mínima, incluida</span><span class="sxs-lookup"><span data-stu-id="b7800-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="b7800-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="b7800-159">(1.0,)</span></span> | <span data-ttu-id="b7800-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-160">x > 1.0</span></span> | <span data-ttu-id="b7800-161">Versión mínima, excluida</span><span class="sxs-lookup"><span data-stu-id="b7800-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="b7800-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="b7800-162">[1.0]</span></span> | <span data-ttu-id="b7800-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-163">x == 1.0</span></span> | <span data-ttu-id="b7800-164">Coincidencia de versión exacta</span><span class="sxs-lookup"><span data-stu-id="b7800-164">Exact version match</span></span> |
| <span data-ttu-id="b7800-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="b7800-165">(,1.0]</span></span> | <span data-ttu-id="b7800-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-166">x ≤ 1.0</span></span> | <span data-ttu-id="b7800-167">Versión máxima, incluida</span><span class="sxs-lookup"><span data-stu-id="b7800-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="b7800-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="b7800-168">(,1.0)</span></span> | <span data-ttu-id="b7800-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-169">x < 1.0</span></span> | <span data-ttu-id="b7800-170">Versión máxima, excluida</span><span class="sxs-lookup"><span data-stu-id="b7800-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="b7800-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="b7800-171">[1.0,2.0]</span></span> | <span data-ttu-id="b7800-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="b7800-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="b7800-173">Intervalo exacto, ambos incluidos</span><span class="sxs-lookup"><span data-stu-id="b7800-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="b7800-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b7800-174">(1.0,2.0)</span></span> | <span data-ttu-id="b7800-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b7800-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="b7800-176">Intervalo exacto, ambos excluidos</span><span class="sxs-lookup"><span data-stu-id="b7800-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="b7800-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b7800-177">[1.0,2.0)</span></span> | <span data-ttu-id="b7800-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b7800-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="b7800-179">Versión mínima incluida y versión máxima excluida mezcladas</span><span class="sxs-lookup"><span data-stu-id="b7800-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="b7800-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="b7800-180">(1.0)</span></span>    | <span data-ttu-id="b7800-181">no válidos</span><span class="sxs-lookup"><span data-stu-id="b7800-181">invalid</span></span> | <span data-ttu-id="b7800-182">no válidos</span><span class="sxs-lookup"><span data-stu-id="b7800-182">invalid</span></span> |

<span data-ttu-id="b7800-183">Cuando se usa el formato PackageReference, NuGet admite también el uso de una notación flotante, \*, en las partes del número de versión principal, versión secundaria, revisión y sufijo de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="b7800-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="b7800-184">Las versiones flotantes no se admiten con el formato `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="b7800-184">Floating versions are not supported with the `packages.config` format.</span></span> <span data-ttu-id="b7800-185">Cuando se especifica una versión flotante, la regla se resuelve como la versión más alta existente que coincide con la descripción de la versión.</span><span class="sxs-lookup"><span data-stu-id="b7800-185">When a floating version is specified, the rule is to resolve to the highest existent version that matches the version description.</span></span> <span data-ttu-id="b7800-186">A continuación se muestran ejemplos de versiones flotantes y las resoluciones.</span><span class="sxs-lookup"><span data-stu-id="b7800-186">Examples of floating versions and the resolutions are below.</span></span>

> [!Note]
> <span data-ttu-id="b7800-187">Los intervalos de versiones de PackageReference incluyen las versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="b7800-187">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="b7800-188">Por diseño, las versiones flotantes no resuelven las versiones preliminares, a menos que se opte por ellas.</span><span class="sxs-lookup"><span data-stu-id="b7800-188">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="b7800-189">Para ver el estado de la solicitud de características relacionadas, consulte el [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="b7800-189">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="b7800-190">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="b7800-190">Examples</span></span>

<span data-ttu-id="b7800-191">Especifique siempre una versión o un intervalo de versiones para las dependencias de paquete en archivos de proyecto, archivos `packages.config` y archivos `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b7800-191">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="b7800-192">Sin una versión o un intervalo de versiones, NuGet 2.8.x y las versiones anteriores eligen la versión del paquete más reciente disponible al resolver una dependencia, mientras que NuGet 3.x y las versiones posteriores eligen la versión de paquete más baja.</span><span class="sxs-lookup"><span data-stu-id="b7800-192">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="b7800-193">La especificación de una versión o un intervalo de versiones evita esta incertidumbre.</span><span class="sxs-lookup"><span data-stu-id="b7800-193">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="b7800-194">Referencias en los archivos de proyecto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="b7800-194">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a><span data-ttu-id="b7800-195">Resoluciones de versiones flotantes</span><span class="sxs-lookup"><span data-stu-id="b7800-195">Floating version resolutions</span></span> 

| <span data-ttu-id="b7800-196">Versión</span><span class="sxs-lookup"><span data-stu-id="b7800-196">Version</span></span> | <span data-ttu-id="b7800-197">Versiones presentes en el servidor</span><span class="sxs-lookup"><span data-stu-id="b7800-197">Versions present on server</span></span> | <span data-ttu-id="b7800-198">Solución</span><span class="sxs-lookup"><span data-stu-id="b7800-198">Resolution</span></span> | <span data-ttu-id="b7800-199">Motivo</span><span class="sxs-lookup"><span data-stu-id="b7800-199">Reason</span></span> | <span data-ttu-id="b7800-200">Notas</span><span class="sxs-lookup"><span data-stu-id="b7800-200">Notes</span></span> |
|----------|--------------|-------------|-------------|-------------|
| * | <span data-ttu-id="b7800-201">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-201">1.1.0</span></span> <br> <span data-ttu-id="b7800-202">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b7800-202">1.1.1</span></span> <br> <span data-ttu-id="b7800-203">1.2.0</span><span class="sxs-lookup"><span data-stu-id="b7800-203">1.2.0</span></span> <br> <span data-ttu-id="b7800-204">1.3.0-alpha</span><span class="sxs-lookup"><span data-stu-id="b7800-204">1.3.0-alpha</span></span>  | <span data-ttu-id="b7800-205">1.2.0</span><span class="sxs-lookup"><span data-stu-id="b7800-205">1.2.0</span></span> | <span data-ttu-id="b7800-206">Versión estable más alta.</span><span class="sxs-lookup"><span data-stu-id="b7800-206">The highest stable version.</span></span> |
| <span data-ttu-id="b7800-207">1.1.\*</span><span class="sxs-lookup"><span data-stu-id="b7800-207">1.1.\*</span></span> | <span data-ttu-id="b7800-208">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-208">1.1.0</span></span> <br> <span data-ttu-id="b7800-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b7800-209">1.1.1</span></span> <br> <span data-ttu-id="b7800-210">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="b7800-210">1.1.2-alpha</span></span> <br> <span data-ttu-id="b7800-211">1.2.0-alpha</span><span class="sxs-lookup"><span data-stu-id="b7800-211">1.2.0-alpha</span></span> | <span data-ttu-id="b7800-212">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b7800-212">1.1.1</span></span> | <span data-ttu-id="b7800-213">Versión estable más alta que respeta el patrón especificado.</span><span class="sxs-lookup"><span data-stu-id="b7800-213">The highest stable version that respects the specified pattern.</span></span>|
| <span data-ttu-id="b7800-214">\* - \*</span><span class="sxs-lookup"><span data-stu-id="b7800-214">\* - \*</span></span> | <span data-ttu-id="b7800-215">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-215">1.1.0</span></span> <br> <span data-ttu-id="b7800-216">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b7800-216">1.1.1</span></span> <br> <span data-ttu-id="b7800-217">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="b7800-217">1.1.2-alpha</span></span> <br> <span data-ttu-id="b7800-218">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="b7800-218">1.3.0-beta</span></span>  | <span data-ttu-id="b7800-219">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="b7800-219">1.3.0-beta</span></span> | <span data-ttu-id="b7800-220">Versión más alta, incluidas las versiones no estables.</span><span class="sxs-lookup"><span data-stu-id="b7800-220">The highest version including the not stable versions.</span></span> | <span data-ttu-id="b7800-221">Disponible en la versión 16.6 de Visual Studio, versión 5.6 de NuGet, SDK de .NET Core de la versión 3.1.300</span><span class="sxs-lookup"><span data-stu-id="b7800-221">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |
| <span data-ttu-id="b7800-222">1.1.\* - \*</span><span class="sxs-lookup"><span data-stu-id="b7800-222">1.1.\* - \*</span></span> | <span data-ttu-id="b7800-223">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b7800-223">1.1.0</span></span> <br> <span data-ttu-id="b7800-224">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b7800-224">1.1.1</span></span> <br> <span data-ttu-id="b7800-225">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="b7800-225">1.1.2-alpha</span></span> <br> <span data-ttu-id="b7800-226">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="b7800-226">1.1.2-beta</span></span> <br> <span data-ttu-id="b7800-227">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="b7800-227">1.3.0-beta</span></span>  | <span data-ttu-id="b7800-228">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="b7800-228">1.1.2-beta</span></span> | <span data-ttu-id="b7800-229">Versión más alta que respeta el patrón e incluye las versiones no estables.</span><span class="sxs-lookup"><span data-stu-id="b7800-229">The highest version respecting the pattern and including the not stable versions.</span></span> | <span data-ttu-id="b7800-230">Disponible en la versión 16.6 de Visual Studio, versión 5.6 de NuGet, SDK de .NET Core de la versión 3.1.300</span><span class="sxs-lookup"><span data-stu-id="b7800-230">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |

<span data-ttu-id="b7800-231">**Referencias en `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="b7800-231">**References in `packages.config`:**</span></span>

<span data-ttu-id="b7800-232">En `packages.config`, todas las dependencias se muestran con un atributo `version` exacto que se usa al restaurar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="b7800-232">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="b7800-233">El atributo `allowedVersions` solo se usa durante las operaciones de actualización para restringir las versiones en las que se puede actualizar el paquete.</span><span class="sxs-lookup"><span data-stu-id="b7800-233">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="b7800-234">**Referencias en archivos `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="b7800-234">**References in `.nuspec` files**</span></span>

<span data-ttu-id="b7800-235">El atributo `version` de un elemento `<dependency>` describe las versiones de intervalo que son aceptables para una dependencia.</span><span class="sxs-lookup"><span data-stu-id="b7800-235">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="b7800-236">Números de versión normalizados</span><span class="sxs-lookup"><span data-stu-id="b7800-236">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="b7800-237">Se trata de un cambio importante en NuGet 3.4 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="b7800-237">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="b7800-238">Al obtener paquetes de un repositorio durante las operaciones de instalación, reinstalación o restauración, NuGet 3.4+ trata los números de versión de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="b7800-238">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="b7800-239">Los ceros a la izquierda se quitan de los números de versión:</span><span class="sxs-lookup"><span data-stu-id="b7800-239">Leading zeroes are removed from version numbers:</span></span>

  <span data-ttu-id="b7800-240">1.00 se trata como 1.0 1.01.1 se trata como 1.1.1 1.00.0.1 se trata como 1.0.0.1</span><span class="sxs-lookup"><span data-stu-id="b7800-240">1.00 is treated as 1.0 1.01.1 is treated as 1.1.1 1.00.0.1 is treated as 1.0.0.1</span></span>

- <span data-ttu-id="b7800-241">Un cero en la cuarta parte del número de versión se omitirá</span><span class="sxs-lookup"><span data-stu-id="b7800-241">A zero in the fourth part of the version number will be omitted</span></span>

  <span data-ttu-id="b7800-242">1.0.0.0 se trata como 1.0.0 1.0.01.0 se trata como 1.0.1</span><span class="sxs-lookup"><span data-stu-id="b7800-242">1.0.0.0 is treated as 1.0.0 1.0.01.0 is treated as 1.0.1</span></span>

- <span data-ttu-id="b7800-243">Se eliminarán los metadatos de la compilación 2.0.0 de SemVer.</span><span class="sxs-lookup"><span data-stu-id="b7800-243">SemVer 2.0.0 build metadata is removed</span></span>

  <span data-ttu-id="b7800-244">1.0.7+r3456 se trata como 1.0.7</span><span class="sxs-lookup"><span data-stu-id="b7800-244">1.0.7+r3456 is treated as 1.0.7</span></span>

<span data-ttu-id="b7800-245">Las operaciones `pack` y `restore` normalizan las versiones siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="b7800-245">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="b7800-246">En el caso de los paquetes ya creados, esta normalización no afecta a los números de versión de los propios paquetes; solo afecta al modo en que NuGet coincide con las versiones cuando se resuelven las dependencias.</span><span class="sxs-lookup"><span data-stu-id="b7800-246">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="b7800-247">Sin embargo, los repositorios de paquetes NuGet deben tratar estos valores de la misma manera que NuGet para evitar la duplicación de la versión del paquete.</span><span class="sxs-lookup"><span data-stu-id="b7800-247">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="b7800-248">Por lo tanto, un repositorio que contiene la versión *1.0* de un paquete no debe hospedar también la versión *1.0.0* como un paquete independiente y diferente.</span><span class="sxs-lookup"><span data-stu-id="b7800-248">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
