---
title: NuGet referencia de errores y advertencias | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia completa para las advertencias y errores emitidos de NuGet durante varias operaciones de NuGet.
keywords: NuGet errores y advertencias de NuGet, diagnóstico
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 020e31dc8646c43b86bcee555f1772e8b1db7761
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="dd9bb-104">Errores y advertencias</span><span class="sxs-lookup"><span data-stu-id="dd9bb-104">Errors and warnings</span></span>

<span data-ttu-id="dd9bb-105">En 4.3.0+ de NuGet, errores y advertencias se numeran como se describe en este tema y proporcionan información detallada para ayudarle a solucionar los problemas que conlleva.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="dd9bb-106">Los errores y advertencias que se indican aquí sólo están disponibles con [PackageReference-based](../consume-packages/package-references-in-project-files.md) 4.3.0+ de NuGet y proyectos.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="dd9bb-107">NuGet también respeta las propiedades de MSBuild para suprimir las advertencias o elevar los privilegios a errores.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="dd9bb-108">Para obtener más información, consulte [Cómo: Suprimir advertencias del compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) en la documentación de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="dd9bb-109">**Errors**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-109">**Errors**</span></span>

| <span data-ttu-id="dd9bb-110">Agrupar</span><span class="sxs-lookup"><span data-stu-id="dd9bb-110">Group</span></span> | <span data-ttu-id="dd9bb-111">Números de error</span><span class="sxs-lookup"><span data-stu-id="dd9bb-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="dd9bb-112">Errores de entrada no válidos</span><span class="sxs-lookup"><span data-stu-id="dd9bb-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="dd9bb-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="dd9bb-114">Errores de paquete y proyecto ausente</span><span class="sxs-lookup"><span data-stu-id="dd9bb-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="dd9bb-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (anteriormente NU1607), [NU1108](#nu1108) (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="dd9bb-116">Errores de compatibilidad</span><span class="sxs-lookup"><span data-stu-id="dd9bb-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="dd9bb-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="dd9bb-118">**Advertencias**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-118">**Warnings**</span></span>

| <span data-ttu-id="dd9bb-119">Agrupar</span><span class="sxs-lookup"><span data-stu-id="dd9bb-119">Group</span></span> | <span data-ttu-id="dd9bb-120">Números de advertencia</span><span class="sxs-lookup"><span data-stu-id="dd9bb-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="dd9bb-121">Advertencias de entrada no válidas</span><span class="sxs-lookup"><span data-stu-id="dd9bb-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="dd9bb-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="dd9bb-123">Advertencias de la versión de paquete inesperado</span><span class="sxs-lookup"><span data-stu-id="dd9bb-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="dd9bb-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="dd9bb-125">Advertencias de conflicto de resolución</span><span class="sxs-lookup"><span data-stu-id="dd9bb-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="dd9bb-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="dd9bb-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="dd9bb-127">Advertencias de reserva de paquete</span><span class="sxs-lookup"><span data-stu-id="dd9bb-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="dd9bb-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="dd9bb-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="dd9bb-129">Advertencias de fuentes</span><span class="sxs-lookup"><span data-stu-id="dd9bb-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="dd9bb-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="dd9bb-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="dd9bb-131">Las advertencias y errores internos de NuGet</span><span class="sxs-lookup"><span data-stu-id="dd9bb-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="dd9bb-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="dd9bb-133">Paquetes firmados (creación y verificación)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="dd9bb-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="dd9bb-135">Errores de entrada no válidos</span><span class="sxs-lookup"><span data-stu-id="dd9bb-135">Invalid input errors</span></span>

<span data-ttu-id="dd9bb-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="dd9bb-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="dd9bb-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-138">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-138">**Issue**</span></span> | <span data-ttu-id="dd9bb-139">El proyecto no contiene uno o varios marcos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="dd9bb-140">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-140">**Example message**</span></span> | <span data-ttu-id="dd9bb-141">*El proyecto projA no especifica ningún marco de destino en c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="dd9bb-142">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-142">**Solution**</span></span> | <span data-ttu-id="dd9bb-143">Agregar un `TargetFramework` o `TargetFrameworks` propiedad al archivo del proyecto especificado.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="dd9bb-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="dd9bb-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-145">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-145">**Issue**</span></span> | <span data-ttu-id="dd9bb-146">Combinación no válida de entradas junto con una palabra clave clara.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="dd9bb-147">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-147">**Example message**</span></span> | <span data-ttu-id="dd9bb-148">*'CLEAR' no se puede usar junto con otros valores*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="dd9bb-149">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-149">**Solution**</span></span> | <span data-ttu-id="dd9bb-150">Usar claro por sí mismo y omitir todas las demás entradas.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="dd9bb-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="dd9bb-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-152">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-152">**Issue**</span></span> | <span data-ttu-id="dd9bb-153">`PackageTargetFallback` y `AssetTargetFallback` proporcionar un comportamiento diferente para la selección de activos y no pueden usarse juntos.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="dd9bb-154">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-154">**Example message**</span></span> | <span data-ttu-id="dd9bb-155">*PackageTargetFallback y AssetTargetFallback no pueden usarse juntos. Quite las referencias de PackageTargetFallback(deprecated) desde el entorno del proyecto.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="dd9bb-156">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-156">**Solution**</span></span> | <span data-ttu-id="dd9bb-157">Quitar las regiones `PackageTargetFallback` elemento desde el proyecto.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="dd9bb-158">Errores de paquete y proyecto ausente</span><span class="sxs-lookup"><span data-stu-id="dd9bb-158">Missing package and project errors</span></span>

<span data-ttu-id="dd9bb-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="dd9bb-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="dd9bb-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-161">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-161">**Issue**</span></span> | <span data-ttu-id="dd9bb-162">Un grupo de dependencia no puede resolver.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-162">A dependency group not be resolved.</span></span> <span data-ttu-id="dd9bb-163">Se trata de un problema genérico para los tipos que no son paquetes o proyectos.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="dd9bb-164">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-164">**Example message**</span></span> | <span data-ttu-id="dd9bb-165">*No se puede resolver System.Missing para net45*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="dd9bb-166">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-166">**Solution**</span></span> | <span data-ttu-id="dd9bb-167">Abra el archivo de proyecto y examine la lista de sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="dd9bb-168">Compruebe que cada dependencia existe en los orígenes del paquete que está usando y que el paquete es compatible con .NET framework de destino del proyecto.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="dd9bb-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="dd9bb-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-170">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-170">**Issue**</span></span> | <span data-ttu-id="dd9bb-171">El paquete no se encuentra en los orígenes.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="dd9bb-172">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-172">**Example message**</span></span> | <span data-ttu-id="dd9bb-173">*No se puede encontrar el paquete System.Missing. Ningún paquete existe con este identificador en orígenes: core dotnet, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="dd9bb-174">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-174">**Solution**</span></span> | <span data-ttu-id="dd9bb-175">Examinar las dependencias del proyecto en Visual Studio para asegurarse de que está usando el número de identificador y la versión de paquete correcto.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="dd9bb-176">Compruebe también que la [configuración NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica los orígenes del paquete la espera que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="dd9bb-177">Si usa los paquetes que tienen [control de versiones semántico 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), asegúrese de que está usando el [V3 fuente](https://api.nuget.org/v3/index.json) en el [configuración NuGet](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="dd9bb-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="dd9bb-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="dd9bb-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-179">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-179">**Issue**</span></span> | <span data-ttu-id="dd9bb-180">Se encontró el identificador de paquete pero no se encuentra una versión dentro del intervalo de dependencia especificado en cualquiera de los orígenes.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="dd9bb-181">El intervalo puede especificarse mediante un paquete y no el usuario.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="dd9bb-182">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-182">**Example message**</span></span> | <span data-ttu-id="dd9bb-183">*No se puede encontrar el paquete NuGet.Versioning con la versión (> = 9.0.1)<br/> -30 encontrar versiones en nuget.org [más cercano de la versión: 4.0.0]<br/> -10 encuentra versiones en dotnet buildtools [más cercano de la versión: 4.0.0-rc-2129]<br/> -encuentra 9 versiones en NuGetVolatile [más cercano de la versión: 3.0.0-beta-00032]<br/> -encontrar versiones 0 en dotnet core<br/> -encontrar versiones 0 en roslyn de dotnet.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="dd9bb-184">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-184">**Solution**</span></span> | <span data-ttu-id="dd9bb-185">Edite el archivo de proyecto para corregir la versión del paquete.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-185">Edit the project file to correct the package version.</span></span> <span data-ttu-id="dd9bb-186">Compruebe también que la [configuración NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica los orígenes del paquete la espera que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="dd9bb-187">Debe cambiar la versión de requeted si este paquete hace referencia directamente al proyecto.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="dd9bb-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="dd9bb-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-189">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-189">**Issue**</span></span> | <span data-ttu-id="dd9bb-190">El proyecto había especificado una versión estable para el intervalo de dependencia, pero no se encontraron ninguna versión estable en ese intervalo.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="dd9bb-191">Se encontraron versiones preliminares, pero no se permiten.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="dd9bb-192">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-192">**Example message**</span></span> | <span data-ttu-id="dd9bb-193">*No se puede encontrar un paquete estable NuGet.Versioning con la versión (> = 3.0.0)<br/> -10 encuentra versiones en dotnet buildtools [más cercano de versión: 4.0.0-rc-2129]<br/> -versiones 9 se encuentra en NuGetVolatile [más cercano de versión: 3.0.0-beta-00032] <br/> -Encontrar versiones 0 en dotnet core<br/> -encontrar versiones 0 en roslyn de dotnet.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="dd9bb-194">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-194">**Solution**</span></span> |  <span data-ttu-id="dd9bb-195">Editar el intervalo de versiones en el archivo de proyecto para incluir versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-195">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="dd9bb-196">Vea [control de versiones del paquete](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="dd9bb-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="dd9bb-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="dd9bb-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-198">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-198">**Issue**</span></span> | <span data-ttu-id="dd9bb-199">Un ProjectReference apunta a un archivo que no existe.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="dd9bb-200">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-200">**Example message**</span></span> | <span data-ttu-id="dd9bb-201">*Referencia de proyecto no existe 'c:\a.csproj'. Compruebe que la referencia al proyecto es válida y que existe el archivo de proyecto.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="dd9bb-202">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-202">**Solution**</span></span> | <span data-ttu-id="dd9bb-203">Edite el archivo de proyecto para corregir la ruta de acceso al proyecto que se hace referencia o para quitar la referencia completamente si ya no es necesario.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="dd9bb-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="dd9bb-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-205">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-205">**Issue**</span></span> | <span data-ttu-id="dd9bb-206">El archivo de proyecto existe pero no se proporcionó ninguna información de restauración para él.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="dd9bb-207">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-207">**Example message**</span></span> | <span data-ttu-id="dd9bb-208">*No se puede leer la información de proyecto de 'c:\a.csproj'. El archivo de proyecto puede ser destinos no válidos o que faltan necesarios para la restauración.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="dd9bb-209">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-209">**Solution**</span></span> | <span data-ttu-id="dd9bb-210">En Visual Studio, el error puede deberse a que el proyecto está cargado, en cuyo caso recargar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="dd9bb-211">Desde la línea de comandos, esto podría significar que el archivo está dañado o que no contiene la opción de instalación "después de importaciones" necesita para que la restauración leer el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="dd9bb-212">Compruebe que el archivo de proyecto es válido y que contiene un destino de "una vez que importe".</span><span class="sxs-lookup"><span data-stu-id="dd9bb-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="dd9bb-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="dd9bb-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-214">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-214">**Issue**</span></span> | <span data-ttu-id="dd9bb-215">Las restricciones de dependencia no se pueden resolver.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="dd9bb-216">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-216">**Example message**</span></span> | <span data-ttu-id="dd9bb-217">*No se pueden satisfacer las solicitudes en conflicto para {id}: {ruta de acceso de conflicto} Framework: {gráfico de destino}*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="dd9bb-218">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-218">**Solution**</span></span> | <span data-ttu-id="dd9bb-219">Edite el archivo de proyecto para especificar intervalos más abiertos para la dependencia en lugar de una versión exacta.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-219">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="dd9bb-220">NU1107 (anteriormente NU1607)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-221">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-221">**Issue**</span></span> | <span data-ttu-id="dd9bb-222">No se puede resolver las restricciones de dependencia entre paquetes.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="dd9bb-223">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-223">**Example message**</span></span> | <span data-ttu-id="dd9bb-224">*Ha detectado para NuGet.Versioning un conflicto de versión. Hacen referencia al paquete directamente desde el proyecto para resolver este problema.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="dd9bb-225">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-225">**Solution**</span></span> | <span data-ttu-id="dd9bb-226">Paquetes con las restricciones de dependencia en versiones exactas no permitir que los otros paquetes aumentar la versión, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="dd9bb-227">Agregue una referencia al proyecto directamente (en el archivo de proyecto) con la versión exacta requerida.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-227">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="dd9bb-228">NU1108 (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-229">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-229">**Issue**</span></span> | <span data-ttu-id="dd9bb-230">Se detectó una dependencia circular.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="dd9bb-231">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-231">**Example message**</span></span> | <span data-ttu-id="dd9bb-232">*Se detectó un ciclo: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="dd9bb-233">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-233">**Solution**</span></span> | <span data-ttu-id="dd9bb-234">El paquete se creó incorrectamente; Póngase en contacto con el propietario del paquete para corregir el error.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="dd9bb-235">Errores de compatibilidad</span><span class="sxs-lookup"><span data-stu-id="dd9bb-235">Compatibility errors</span></span>

<span data-ttu-id="dd9bb-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="dd9bb-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="dd9bb-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-238">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-238">**Issue**</span></span> | <span data-ttu-id="dd9bb-239">Un proyecto de dependencia no contiene un marco de trabajo compatible con el proyecto actual.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="dd9bb-240">Por lo general, .NET framework de destino del proyecto es una versión posterior a del proyecto usada.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="dd9bb-241">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-241">**Example message**</span></span> | <span data-ttu-id="dd9bb-242">*WAN de proyecto no es compatible con netstandard1.3 (. NETStandard, Version = v1.3). Project admite de WAN:<br/> -netstandard1.6 (. NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="dd9bb-243">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-243">**Solution**</span></span> | <span data-ttu-id="dd9bb-244">Cambiar la plataforma de destino del proyecto a una versión igual o menor que el proyecto.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="dd9bb-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="dd9bb-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-246">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-246">**Issue**</span></span> | <span data-ttu-id="dd9bb-247">Un paquete de dependencia no contiene ningún activos compatibles con el proyecto.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="dd9bb-248">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-248">**Example message**</span></span> | <span data-ttu-id="dd9bb-249">*Paquete System.ComponentModel.EventBasedAsync 4.0.11 no es compatible con netstandard1.3 (. NETStandard, Version = v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="dd9bb-250">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-250">**Solution**</span></span> | <span data-ttu-id="dd9bb-251">Cambiar plataforma de destino del proyecto a uno que admite el paquete.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="dd9bb-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="dd9bb-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-253">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-253">**Issue**</span></span> | <span data-ttu-id="dd9bb-254">El paquete no es compatible con el proyecto `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="dd9bb-255">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-255">**Example message**</span></span> | <span data-ttu-id="dd9bb-256">*System.Example 1.0.0 proporciona un ensamblado de referencia en tiempo de compilación para.dll en net461, pero no hay ningún ensamblado en tiempo de ejecución compatible.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="dd9bb-257">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-257">**Solution**</span></span> | <span data-ttu-id="dd9bb-258">Cambiar el `RuntimeIdentifier` valores utilizados en el proyecto según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="dd9bb-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="dd9bb-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-260">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-260">**Issue**</span></span> | <span data-ttu-id="dd9bb-261">El paquete requiere características o marcos de trabajo no admitidas actualmente por la versión instalada de NuGet.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="dd9bb-262">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-262">**Example message**</span></span> | <span data-ttu-id="dd9bb-263">*El paquete 'NuGet.Versioning' requiere NuGet versión de cliente '5.0.0' o superior, pero la versión de NuGet actual es '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="dd9bb-264">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-264">**Solution**</span></span> | <span data-ttu-id="dd9bb-265">Instale una versión más reciente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="dd9bb-266">Vea [herramientas de cliente de instalación de NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="dd9bb-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="dd9bb-267">Advertencias de entrada no válidas</span><span class="sxs-lookup"><span data-stu-id="dd9bb-267">Invalid input warnings</span></span>

<span data-ttu-id="dd9bb-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="dd9bb-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="dd9bb-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-270">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-270">**Issue**</span></span> | <span data-ttu-id="dd9bb-271">La restauración de proyecto está intentando operar en no se encontró.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="dd9bb-272">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-272">**Example message**</span></span> | <span data-ttu-id="dd9bb-273">*La carpeta 'c:\projects\a' no contiene ningún proyecto para restaurar.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="dd9bb-274">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-274">**Solution**</span></span> | <span data-ttu-id="dd9bb-275">Ejecutar la restauración de nuget en una carpeta que contiene un proyecto.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="dd9bb-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="dd9bb-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-277">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-277">**Issue**</span></span> | <span data-ttu-id="dd9bb-278">`RuntimeSupports` contiene un perfil no válido.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="dd9bb-279">Por lo general, no se encontró el perfil admite en un `runtime.json` archivos de los paquetes de dependencia actual.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="dd9bb-280">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-280">**Example message**</span></span> | <span data-ttu-id="dd9bb-281">*Perfil de compatibilidad desconocido: aaa*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="dd9bb-282">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-282">**Solution**</span></span> | <span data-ttu-id="dd9bb-283">Compruebe el `RuntimeSupports` valor en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="dd9bb-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="dd9bb-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-285">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-285">**Issue**</span></span> | <span data-ttu-id="dd9bb-286">Un proyecto de dependencia no importa los destinos de restauración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="dd9bb-287">Esto es similar a NU1105, pero aquí se omite el proyecto y pasa por alto en lugar de producir todos de restauración a un error.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="dd9bb-288">En soluciones complejas a menudo hay otros tipos de proyectos que pueden no admitir la restauración.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="dd9bb-289">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-289">**Example message**</span></span> | <span data-ttu-id="dd9bb-290">*Se omitirá la restauración para el proyecto 'c:\a.csproj'. El archivo de proyecto puede ser destinos no válidos o que faltan necesarios para la restauración.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="dd9bb-291">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-291">**Solution**</span></span> | <span data-ttu-id="dd9bb-292">Esto puede ocurrir por proyectos que importen props/destinos comunes que se importan automáticamente la restauración.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="dd9bb-293">Si el proyecto no tiene que restaurarse Esto puede hacer caso omiso.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="dd9bb-294">En caso contrario, edite el proyecto afectado para agregar destinos de restauración.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="dd9bb-295">Advertencias de la versión de paquete inesperado</span><span class="sxs-lookup"><span data-stu-id="dd9bb-295">Unexpected package version warnings</span></span>

<span data-ttu-id="dd9bb-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="dd9bb-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="dd9bb-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-298">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-298">**Issue**</span></span> | <span data-ttu-id="dd9bb-299">Se incrementará en una dependencia de proyecto directa a una versión más reciente que el proyecto especificado.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="dd9bb-300">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-300">**Example message**</span></span> | <span data-ttu-id="dd9bb-301">*Dependencia especificada era NuGet.Versioning (> = 3.5.0) pero terminaba con NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="dd9bb-302">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-302">**Solution**</span></span> | <span data-ttu-id="dd9bb-303">Actualice la dependencia en el proyecto con una versión adecuada.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="dd9bb-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="dd9bb-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-305">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-305">**Issue**</span></span> | <span data-ttu-id="dd9bb-306">Una dependencia del paquete falta un límite inferior.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="dd9bb-307">Esto no permite la restauración buscar el *mejor coincidencia*.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="dd9bb-308">Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="dd9bb-309">Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="dd9bb-310">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-310">**Example message**</span></span> | <span data-ttu-id="dd9bb-311">*NuGet.Packaging 4.0.0 no proporciona un límite inferior inclusivo de dependencia NuGet.Versioning (3.5.0 >). Una mejor coincidencia aproximada de 3.6.0 se resolvió.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="dd9bb-312">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-312">**Solution**</span></span> | <span data-ttu-id="dd9bb-313">Esto suele ser un error de creación de paquete.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-313">This is usually a package authoring error.</span></span> <span data-ttu-id="dd9bb-314">Póngase en contacto con el autor del paquete para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="dd9bb-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="dd9bb-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-316">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-316">**Issue**</span></span> | <span data-ttu-id="dd9bb-317">Una dependencia del paquete especifica una versión que no se pudo encontrar.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="dd9bb-318">Normalmente, los orígenes del paquete no contienen la versión de límite inferior esperado.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="dd9bb-319">Una versión posterior se usó en su lugar, que es distinto de lo que se creó el paquete en.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="dd9bb-320">Esto significa que la restauración no se encontró el *mejor coincidencia*.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="dd9bb-321">Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="dd9bb-322">Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="dd9bb-323">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-323">**Example message**</span></span> | <span data-ttu-id="dd9bb-324">NuGet.Packaging 4.0.0 depende NuGet.Versioning (> = 4.0.0) pero no se encontró 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="dd9bb-325">Una mejor coincidencia aproximada de 5.0.0 se resolvió.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="dd9bb-326">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-326">**Solution**</span></span> | <span data-ttu-id="dd9bb-327">Si no se ha liberado el paquete que esperaba, a continuación, puede tratarse de un error de creación de paquete.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="dd9bb-328">Póngase en contacto con el autor del paquete para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="dd9bb-329">Si se ha liberado el paquete, compruebe que está disponible en los orígenes del paquete que está usando.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="dd9bb-330">Si usa una fuente privada, debe actualizar el paquete en esa fuente.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="dd9bb-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="dd9bb-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-332">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-332">**Issue**</span></span> | <span data-ttu-id="dd9bb-333">Una dependencia de proyecto no define un límite inferior.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="dd9bb-334">Esto significa que la restauración no se encontró el *mejor coincidencia*.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="dd9bb-335">Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="dd9bb-336">Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="dd9bb-337">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-337">**Example message**</span></span> | <span data-ttu-id="dd9bb-338">*Proyecto dependencia NuGet.Versioning (< = 9.0.0) doe no contiene un límite inferior inclusivo. Incluir un límite inferior en la versión de dependencia para garantizar que los resultados de restauración coherentes.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="dd9bb-339">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-339">**Solution**</span></span> | <span data-ttu-id="dd9bb-340">Actualice el proyecto `PackageReference` `Version` atributo para incluir un límite inferior.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="dd9bb-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="dd9bb-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-342">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-342">**Issue**</span></span> | <span data-ttu-id="dd9bb-343">Un paquete de dependencia especificó una restricción de versión en una versión posterior de un paquete que la restauración que se resuelven en última instancia.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="dd9bb-344">Es decir, debido a la "más cercano de wins" regla al resolver paquetes, un paquete cuanto más cerca en el gráfico de puede invalidar un paquete está lejos.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="dd9bb-345">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-345">**Example message**</span></span> | <span data-ttu-id="dd9bb-346">*Detecta la degradación de paquete: NuGet.Versioning de 4.0.0 3.5.0. Hacen referencia al paquete directamente desde el proyecto para seleccionar una versión diferente.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="dd9bb-347">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-347">**Solution**</span></span> | <span data-ttu-id="dd9bb-348">Agregue una referencia directa al proyecto para la versión más reciente del paquete que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="dd9bb-349">Advertencias de conflicto de resolución</span><span class="sxs-lookup"><span data-stu-id="dd9bb-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="dd9bb-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="dd9bb-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-351">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-351">**Issue**</span></span> | <span data-ttu-id="dd9bb-352">Un paquete resuelto es mayor que permite que una restricción de dependencia.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="dd9bb-353">Esto significa que un paquete al que hace referencia directamente un proyecto invalida las restricciones de dependencia de otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="dd9bb-354">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-354">**Example message**</span></span> | <span data-ttu-id="dd9bb-355">*Versión del paquete detectado fuera de restricción de dependencia: x 1.0.0 requiere y (= 1.0.0) pero la versión y 2.0.0 se resolvió.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="dd9bb-356">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-356">**Solution**</span></span> | <span data-ttu-id="dd9bb-357">En algunos casos esto tiene su porqué y se puede suprimir la advertencia.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="dd9bb-358">En caso contrario, cambie la referencia del proyecto al paquete para ampliar sus restricciones de versión.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="dd9bb-359">Advertencias de reserva de paquete</span><span class="sxs-lookup"><span data-stu-id="dd9bb-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="dd9bb-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="dd9bb-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-361">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-361">**Issue**</span></span> | <span data-ttu-id="dd9bb-362">`PackageTargetFallback` / `AssetTargetFallback` se usa para seleccionar los activos de un paquete.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="dd9bb-363">La advertencia que los usuarios sepan que los activos pueden no ser compatible al 100%.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="dd9bb-364">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-364">**Example message**</span></span> | <span data-ttu-id="dd9bb-365">*Paquete 'NuGet.Versioning' se restauró usando 'portable net45 + win8' en su lugar, la plataforma de destino del proyecto 'netstandard1.5'. Este paquete no puede ser totalmente compatible con el proyecto.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="dd9bb-366">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-366">**Solution**</span></span> | <span data-ttu-id="dd9bb-367">Cambiar plataforma de destino del proyecto a uno que admite el paquete.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="dd9bb-368">Advertencias de fuentes</span><span class="sxs-lookup"><span data-stu-id="dd9bb-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="dd9bb-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="dd9bb-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-370">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-370">**Issue**</span></span> | <span data-ttu-id="dd9bb-371">Se produjo un error al leer la fuente cuando `IgnoreFailedSources` se establece en true, se convierte en una advertencia no es grave.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="dd9bb-372">Esto podría contener todos los mensajes y es genérico.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="dd9bb-373">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-373">**Example message**</span></span> | <span data-ttu-id="dd9bb-374">N/D</span><span class="sxs-lookup"><span data-stu-id="dd9bb-374">n/a</span></span> |
| <span data-ttu-id="dd9bb-375">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-375">**Solution**</span></span> | <span data-ttu-id="dd9bb-376">Editar la configuración para especificar los orígenes de válido.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="dd9bb-377">Las advertencias y errores internos de NuGet</span><span class="sxs-lookup"><span data-stu-id="dd9bb-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="dd9bb-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="dd9bb-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="dd9bb-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-380">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-380">**Issue**</span></span> | <span data-ttu-id="dd9bb-381">Un error interno no es específico de NuGet.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="dd9bb-382">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-382">**Solution**</span></span> | <span data-ttu-id="dd9bb-383">Compruebe los registros para obtener más información</span><span class="sxs-lookup"><span data-stu-id="dd9bb-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="dd9bb-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="dd9bb-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-385">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-385">**Issue**</span></span> | <span data-ttu-id="dd9bb-386">Advertencias interno no es específico de NuGet.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="dd9bb-387">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-387">**Solution**</span></span> | <span data-ttu-id="dd9bb-388">Compruebe los registros para obtener más información</span><span class="sxs-lookup"><span data-stu-id="dd9bb-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="dd9bb-389">Paquetes firmados (creación y verificación)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="dd9bb-390">*4.6.0+ de NuGet*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="dd9bb-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="dd9bb-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="dd9bb-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="dd9bb-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-393">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-393">**Issue**</span></span> | <span data-ttu-id="dd9bb-394">Un error específico del no relacionados con la firma del paquete y había firmado de comprobación del paquete.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="dd9bb-395">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-395">**Solution**</span></span> | <span data-ttu-id="dd9bb-396">Compruebe los registros para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="dd9bb-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="dd9bb-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-398">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-398">**Issue**</span></span> | <span data-ttu-id="dd9bb-399">Argumentos no válidos a cualquiera la [firmar comando](../tools/cli-ref-sign.md) o [comprobar comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="dd9bb-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="dd9bb-400">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-400">**Solution**</span></span> | <span data-ttu-id="dd9bb-401">Compruebe y corrija los argumentos proporcionados.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="dd9bb-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="dd9bb-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-403">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-403">**Issue**</span></span> | <span data-ttu-id="dd9bb-404">El `-Timestamper` no se especificó la opción con la [comando de inicio de sesión de nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="dd9bb-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="dd9bb-405">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-405">**Example message**</span></span> | <span data-ttu-id="dd9bb-406">*El '-Timestamper' no se ha proporcionado la opción. El paquete firmado no estará con marca de tiempo.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="dd9bb-407">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-407">**Solution**</span></span> | <span data-ttu-id="dd9bb-408">Especifique el `-Timestamper` opción con `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="dd9bb-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="dd9bb-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-410">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-410">**Issue**</span></span> | <span data-ttu-id="dd9bb-411">Se proporcionó un paquete sin firmar para los [nuget Compruebe comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="dd9bb-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="dd9bb-412">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-412">**Solution**</span></span> | <span data-ttu-id="dd9bb-413">Ejecute `nuget verify` con un paquete firmado.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="dd9bb-414">Vea [firmar un paquete](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="dd9bb-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="dd9bb-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="dd9bb-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-416">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-416">**Issue**</span></span> | <span data-ttu-id="dd9bb-417">Error en la comprobación de integridad de paquete, lo que significa que un paquete firmado se ha alterado desde que se está firmando.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="dd9bb-418">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-418">**Solution**</span></span> | <span data-ttu-id="dd9bb-419">Analice el equipo con el software antivirus.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="dd9bb-420">A continuación, quite el paquete desde el equipo, vuelva a instalarlo y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="dd9bb-421">Si el problema continúa, póngase en contacto con el propietario del origen del paquete y el paquete.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="dd9bb-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="dd9bb-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-423">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-423">**Issue**</span></span> | <span data-ttu-id="dd9bb-424">No se pudo crear la cadena de certificados para la firma primaria.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="dd9bb-425">El certificado de firma principal no es de confianza, revocado, o información de revocación del certificado no está disponible.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="dd9bb-426">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-426">**Example message**</span></span> | <span data-ttu-id="dd9bb-427">*Advertencia: NU3018: la función de revocación no pudo comprobar la revocación del certificado.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="dd9bb-428">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-428">**Solution**</span></span> | <span data-ttu-id="dd9bb-429">Usar un certificado de confianza y es válido.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="dd9bb-430">Compruebe la conectividad de internet.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="dd9bb-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="dd9bb-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dd9bb-432">**Problema**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-432">**Issue**</span></span> | <span data-ttu-id="dd9bb-433">No se pudo crear la cadena de certificados para la firma de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="dd9bb-434">El certificado de firma de marca de tiempo no es de confianza, revocado, o información de revocación del certificado no está disponible.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="dd9bb-435">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-435">**Example message**</span></span> | <span data-ttu-id="dd9bb-436">*Advertencia: NU3028: la función de revocación no pudo comprobar la revocación del certificado.*</span><span class="sxs-lookup"><span data-stu-id="dd9bb-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="dd9bb-437">**Solución**</span><span class="sxs-lookup"><span data-stu-id="dd9bb-437">**Solution**</span></span> | <span data-ttu-id="dd9bb-438">Usar un certificado de confianza y es válido.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="dd9bb-439">Compruebe la conectividad de internet.</span><span class="sxs-lookup"><span data-stu-id="dd9bb-439">Check internet connectivity.</span></span> |
