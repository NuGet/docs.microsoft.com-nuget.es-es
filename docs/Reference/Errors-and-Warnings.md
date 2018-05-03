---
title: NuGet referencia de errores y advertencias
description: Referencia completa para las advertencias y errores emitidos de NuGet durante varias operaciones de NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: anangaur
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
ms.openlocfilehash: dcff20e35adc0a3dbcc7bef482f81a937cf059c5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="4a2fe-103">Errores y advertencias</span><span class="sxs-lookup"><span data-stu-id="4a2fe-103">Errors and warnings</span></span>

<span data-ttu-id="4a2fe-104">En 4.3.0+ de NuGet, errores y advertencias se numeran como se describe en este tema y proporcionan información detallada para ayudarle a solucionar los problemas que conlleva.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="4a2fe-105">Los errores y advertencias que se indican aquí sólo están disponibles con [PackageReference-based](../consume-packages/package-references-in-project-files.md) 4.3.0+ de NuGet y proyectos.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="4a2fe-106">NuGet también respeta las propiedades de MSBuild para suprimir las advertencias o elevar los privilegios a errores.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="4a2fe-107">Para obtener más información, consulte [Cómo: Suprimir advertencias del compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) en la documentación de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="4a2fe-108">**errores**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-108">**Errors**</span></span>

| <span data-ttu-id="4a2fe-109">Agrupar</span><span class="sxs-lookup"><span data-stu-id="4a2fe-109">Group</span></span> | <span data-ttu-id="4a2fe-110">Números de error</span><span class="sxs-lookup"><span data-stu-id="4a2fe-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="4a2fe-111">Errores de entrada no válidos</span><span class="sxs-lookup"><span data-stu-id="4a2fe-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="4a2fe-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="4a2fe-113">Errores de paquete y proyecto ausente</span><span class="sxs-lookup"><span data-stu-id="4a2fe-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="4a2fe-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (anteriormente NU1607), [NU1108](#nu1108) (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="4a2fe-115">Errores de compatibilidad</span><span class="sxs-lookup"><span data-stu-id="4a2fe-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="4a2fe-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="4a2fe-117">**Advertencias**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-117">**Warnings**</span></span>

| <span data-ttu-id="4a2fe-118">Agrupar</span><span class="sxs-lookup"><span data-stu-id="4a2fe-118">Group</span></span> | <span data-ttu-id="4a2fe-119">Números de advertencia</span><span class="sxs-lookup"><span data-stu-id="4a2fe-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="4a2fe-120">Advertencias de entrada no válidas</span><span class="sxs-lookup"><span data-stu-id="4a2fe-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="4a2fe-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="4a2fe-122">Advertencias de la versión de paquete inesperado</span><span class="sxs-lookup"><span data-stu-id="4a2fe-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="4a2fe-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="4a2fe-124">Advertencias de conflicto de resolución</span><span class="sxs-lookup"><span data-stu-id="4a2fe-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="4a2fe-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="4a2fe-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="4a2fe-126">Advertencias de reserva de paquete</span><span class="sxs-lookup"><span data-stu-id="4a2fe-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="4a2fe-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="4a2fe-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="4a2fe-128">Advertencias de fuentes</span><span class="sxs-lookup"><span data-stu-id="4a2fe-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="4a2fe-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="4a2fe-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="4a2fe-130">Las advertencias y errores internos de NuGet</span><span class="sxs-lookup"><span data-stu-id="4a2fe-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="4a2fe-131">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="4a2fe-132">Paquetes firmados (creación y verificación)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="4a2fe-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="4a2fe-134">Errores de entrada no válidos</span><span class="sxs-lookup"><span data-stu-id="4a2fe-134">Invalid input errors</span></span>

<span data-ttu-id="4a2fe-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="4a2fe-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="4a2fe-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-137">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-137">**Issue**</span></span> | <span data-ttu-id="4a2fe-138">El proyecto no contiene uno o varios marcos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="4a2fe-139">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-139">**Example message**</span></span> | <span data-ttu-id="4a2fe-140">*El proyecto projA no especifica ningún marco de destino en c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="4a2fe-141">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-141">**Solution**</span></span> | <span data-ttu-id="4a2fe-142">Agregar un `TargetFramework` o `TargetFrameworks` propiedad al archivo del proyecto especificado.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="4a2fe-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="4a2fe-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-144">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-144">**Issue**</span></span> | <span data-ttu-id="4a2fe-145">Combinación no válida de entradas junto con una palabra clave clara.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="4a2fe-146">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-146">**Example message**</span></span> | <span data-ttu-id="4a2fe-147">*'CLEAR' no se puede usar junto con otros valores*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="4a2fe-148">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-148">**Solution**</span></span> | <span data-ttu-id="4a2fe-149">Usar claro por sí mismo y omitir todas las demás entradas.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="4a2fe-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="4a2fe-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-151">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-151">**Issue**</span></span> | <span data-ttu-id="4a2fe-152">`PackageTargetFallback` y `AssetTargetFallback` proporcionar un comportamiento diferente para la selección de activos y no pueden usarse juntos.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="4a2fe-153">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-153">**Example message**</span></span> | <span data-ttu-id="4a2fe-154">*PackageTargetFallback y AssetTargetFallback no pueden usarse juntos. Quite las referencias de PackageTargetFallback(deprecated) desde el entorno del proyecto.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="4a2fe-155">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-155">**Solution**</span></span> | <span data-ttu-id="4a2fe-156">Quitar las regiones `PackageTargetFallback` elemento desde el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="4a2fe-157">Errores de paquete y proyecto ausente</span><span class="sxs-lookup"><span data-stu-id="4a2fe-157">Missing package and project errors</span></span>

<span data-ttu-id="4a2fe-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="4a2fe-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="4a2fe-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-160">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-160">**Issue**</span></span> | <span data-ttu-id="4a2fe-161">Un grupo de dependencia no puede resolver.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-161">A dependency group not be resolved.</span></span> <span data-ttu-id="4a2fe-162">Se trata de un problema genérico para los tipos que no son paquetes o proyectos.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="4a2fe-163">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-163">**Example message**</span></span> | <span data-ttu-id="4a2fe-164">*No se puede resolver System.Missing para net45*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="4a2fe-165">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-165">**Solution**</span></span> | <span data-ttu-id="4a2fe-166">Abra el archivo de proyecto y examine la lista de sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="4a2fe-167">Compruebe que cada dependencia existe en los orígenes del paquete que está usando y que el paquete es compatible con .NET framework de destino del proyecto.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="4a2fe-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="4a2fe-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-169">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-169">**Issue**</span></span> | <span data-ttu-id="4a2fe-170">El paquete no se encuentra en los orígenes.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="4a2fe-171">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-171">**Example message**</span></span> | <span data-ttu-id="4a2fe-172">*No se puede encontrar el paquete System.Missing. Ningún paquete existe con este identificador en orígenes: core dotnet, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="4a2fe-173">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-173">**Solution**</span></span> | <span data-ttu-id="4a2fe-174">Examinar las dependencias del proyecto en Visual Studio para asegurarse de que está usando el número de identificador y la versión de paquete correcto.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="4a2fe-175">Compruebe también que la [configuración NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica los orígenes del paquete la espera que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="4a2fe-176">Si usa los paquetes que tienen [control de versiones semántico 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), asegúrese de que está usando el [V3 fuente](https://api.nuget.org/v3/index.json) en el [configuración NuGet](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-176">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="4a2fe-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="4a2fe-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-178">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-178">**Issue**</span></span> | <span data-ttu-id="4a2fe-179">Se encontró el identificador de paquete pero no se encuentra una versión dentro del intervalo de dependencia especificado en cualquiera de los orígenes.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="4a2fe-180">El intervalo puede especificarse mediante un paquete y no el usuario.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="4a2fe-181">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-181">**Example message**</span></span> | <span data-ttu-id="4a2fe-182">*No se puede encontrar el paquete NuGet.Versioning con la versión (> = 9.0.1)<br/> -30 encontrar versiones en nuget.org [más cercano de la versión: 4.0.0]<br/> -10 encuentra versiones en dotnet buildtools [más cercano de la versión: 4.0.0-rc-2129]<br/> -encuentra 9 versiones en NuGetVolatile [más cercano de la versión: 3.0.0-beta-00032]<br/> -encontrar versiones 0 en dotnet core<br/> -encontrar versiones 0 en roslyn de dotnet.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="4a2fe-183">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-183">**Solution**</span></span> | <span data-ttu-id="4a2fe-184">Edite el archivo de proyecto para corregir la versión del paquete.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="4a2fe-185">Compruebe también que la [configuración NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica los orígenes del paquete la espera que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="4a2fe-186">Debe cambiar la versión de requeted si este paquete hace referencia directamente al proyecto.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="4a2fe-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="4a2fe-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-188">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-188">**Issue**</span></span> | <span data-ttu-id="4a2fe-189">El proyecto había especificado una versión estable para el intervalo de dependencia, pero no se encontraron ninguna versión estable en ese intervalo.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="4a2fe-190">Se encontraron versiones preliminares, pero no se permiten.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="4a2fe-191">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-191">**Example message**</span></span> | <span data-ttu-id="4a2fe-192">*No se puede encontrar un paquete estable NuGet.Versioning con la versión (> = 3.0.0)<br/> -10 encuentra versiones en dotnet buildtools [más cercano de versión: 4.0.0-rc-2129]<br/> -versiones 9 se encuentra en NuGetVolatile [más cercano de versión: 3.0.0-beta-00032] <br/> -Encontrar versiones 0 en dotnet core<br/> -encontrar versiones 0 en roslyn de dotnet.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="4a2fe-193">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-193">**Solution**</span></span> |  <span data-ttu-id="4a2fe-194">Editar el intervalo de versiones en el archivo de proyecto para incluir versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="4a2fe-195">Vea [control de versiones del paquete](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="4a2fe-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="4a2fe-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-197">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-197">**Issue**</span></span> | <span data-ttu-id="4a2fe-198">Un ProjectReference apunta a un archivo que no existe.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="4a2fe-199">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-199">**Example message**</span></span> | <span data-ttu-id="4a2fe-200">*Referencia de proyecto no existe 'c:\a.csproj'. Compruebe que la referencia al proyecto es válida y que existe el archivo de proyecto.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="4a2fe-201">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-201">**Solution**</span></span> | <span data-ttu-id="4a2fe-202">Edite el archivo de proyecto para corregir la ruta de acceso al proyecto que se hace referencia o para quitar la referencia completamente si ya no es necesario.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="4a2fe-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="4a2fe-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-204">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-204">**Issue**</span></span> | <span data-ttu-id="4a2fe-205">El archivo de proyecto existe pero no se proporcionó ninguna información de restauración para él.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="4a2fe-206">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-206">**Example message**</span></span> | <span data-ttu-id="4a2fe-207">*No se puede leer la información de proyecto de 'c:\a.csproj'. El archivo de proyecto puede ser destinos no válidos o que faltan necesarios para la restauración.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="4a2fe-208">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-208">**Solution**</span></span> | <span data-ttu-id="4a2fe-209">En Visual Studio, el error puede deberse a que el proyecto está cargado, en cuyo caso recargar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="4a2fe-210">Desde la línea de comandos, esto podría significar que el archivo está dañado o que no contiene la opción de instalación "después de importaciones" necesita para que la restauración leer el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="4a2fe-211">Compruebe que el archivo de proyecto es válido y que contiene un destino de "una vez que importe".</span><span class="sxs-lookup"><span data-stu-id="4a2fe-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="4a2fe-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="4a2fe-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-213">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-213">**Issue**</span></span> | <span data-ttu-id="4a2fe-214">Las restricciones de dependencia no se pueden resolver.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="4a2fe-215">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-215">**Example message**</span></span> | <span data-ttu-id="4a2fe-216">*No se pueden satisfacer las solicitudes en conflicto para {id}: {ruta de acceso de conflicto} Framework: {gráfico de destino}*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="4a2fe-217">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-217">**Solution**</span></span> | <span data-ttu-id="4a2fe-218">Edite el archivo de proyecto para especificar intervalos más abiertos para la dependencia en lugar de una versión exacta.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="4a2fe-219">NU1107 (anteriormente NU1607)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-220">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-220">**Issue**</span></span> | <span data-ttu-id="4a2fe-221">No se puede resolver las restricciones de dependencia entre paquetes.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="4a2fe-222">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-222">**Example message**</span></span> | <span data-ttu-id="4a2fe-223">*Ha detectado para NuGet.Versioning un conflicto de versión. Hacen referencia al paquete directamente desde el proyecto para resolver este problema.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="4a2fe-224">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-224">**Solution**</span></span> | <span data-ttu-id="4a2fe-225">Paquetes con las restricciones de dependencia en versiones exactas no permitir que los otros paquetes aumentar la versión, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="4a2fe-226">Agregue una referencia al proyecto directamente (en el archivo de proyecto) con la versión exacta requerida.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="4a2fe-227">NU1108 (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-228">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-228">**Issue**</span></span> | <span data-ttu-id="4a2fe-229">Se detectó una dependencia circular.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="4a2fe-230">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-230">**Example message**</span></span> | <span data-ttu-id="4a2fe-231">*Se detectó un ciclo: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="4a2fe-232">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-232">**Solution**</span></span> | <span data-ttu-id="4a2fe-233">El paquete se creó incorrectamente; Póngase en contacto con el propietario del paquete para corregir el error.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="4a2fe-234">Errores de compatibilidad</span><span class="sxs-lookup"><span data-stu-id="4a2fe-234">Compatibility errors</span></span>

<span data-ttu-id="4a2fe-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="4a2fe-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="4a2fe-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-237">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-237">**Issue**</span></span> | <span data-ttu-id="4a2fe-238">Un proyecto de dependencia no contiene un marco de trabajo compatible con el proyecto actual.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="4a2fe-239">Por lo general, .NET framework de destino del proyecto es una versión posterior a del proyecto usada.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="4a2fe-240">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-240">**Example message**</span></span> | <span data-ttu-id="4a2fe-241">*WAN de proyecto no es compatible con netstandard1.3 (. NETStandard, Version = v1.3). Project admite de WAN:<br/> -netstandard1.6 (. NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="4a2fe-242">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-242">**Solution**</span></span> | <span data-ttu-id="4a2fe-243">Cambiar la plataforma de destino del proyecto a una versión igual o menor que el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="4a2fe-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="4a2fe-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-245">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-245">**Issue**</span></span> | <span data-ttu-id="4a2fe-246">Un paquete de dependencia no contiene ningún activos compatibles con el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="4a2fe-247">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-247">**Example message**</span></span> | <span data-ttu-id="4a2fe-248">*Paquete System.ComponentModel.EventBasedAsync 4.0.11 no es compatible con netstandard1.3 (. NETStandard, Version = v1.3). Paquete admite System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (. NETFramework, Version = v4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. NETStandard, Version = v1.0)<br/> -portable net45 + win8 + wp8 + wpa81 (. NETPortable, Version = v0.0, perfil = Profile259)<br/> -win8 (Windows, versión = v8.0)<br/> -wp8 (WindowsPhone, Version = v8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="4a2fe-249">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-249">**Solution**</span></span> | <span data-ttu-id="4a2fe-250">Cambiar plataforma de destino del proyecto a uno que admite el paquete.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="4a2fe-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="4a2fe-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-252">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-252">**Issue**</span></span> | <span data-ttu-id="4a2fe-253">El paquete no es compatible con el proyecto `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="4a2fe-254">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-254">**Example message**</span></span> | <span data-ttu-id="4a2fe-255">*System.Example 1.0.0 proporciona un ensamblado de referencia en tiempo de compilación para.dll en net461, pero no hay ningún ensamblado en tiempo de ejecución compatible.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="4a2fe-256">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-256">**Solution**</span></span> | <span data-ttu-id="4a2fe-257">Cambiar el `RuntimeIdentifier` valores utilizados en el proyecto según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="4a2fe-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="4a2fe-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-259">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-259">**Issue**</span></span> | <span data-ttu-id="4a2fe-260">El paquete requiere características o marcos de trabajo no admitidas actualmente por la versión instalada de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="4a2fe-261">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-261">**Example message**</span></span> | <span data-ttu-id="4a2fe-262">*El paquete 'NuGet.Versioning' requiere NuGet versión de cliente '5.0.0' o superior, pero la versión de NuGet actual es '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="4a2fe-263">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-263">**Solution**</span></span> | <span data-ttu-id="4a2fe-264">Instale una versión más reciente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="4a2fe-265">Vea [herramientas de cliente de instalación de NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="4a2fe-266">Advertencias de entrada no válidas</span><span class="sxs-lookup"><span data-stu-id="4a2fe-266">Invalid input warnings</span></span>

<span data-ttu-id="4a2fe-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="4a2fe-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="4a2fe-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-269">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-269">**Issue**</span></span> | <span data-ttu-id="4a2fe-270">La restauración de proyecto está intentando operar en no se encontró.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="4a2fe-271">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-271">**Example message**</span></span> | <span data-ttu-id="4a2fe-272">*La carpeta 'c:\projects\a' no contiene ningún proyecto para restaurar.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="4a2fe-273">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-273">**Solution**</span></span> | <span data-ttu-id="4a2fe-274">Ejecutar la restauración de nuget en una carpeta que contiene un proyecto.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="4a2fe-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="4a2fe-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-276">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-276">**Issue**</span></span> | <span data-ttu-id="4a2fe-277">`RuntimeSupports` contiene un perfil no válido.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="4a2fe-278">Por lo general, no se encontró el perfil admite en un `runtime.json` archivos de los paquetes de dependencia actual.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="4a2fe-279">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-279">**Example message**</span></span> | <span data-ttu-id="4a2fe-280">*Perfil de compatibilidad desconocido: aaa*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="4a2fe-281">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-281">**Solution**</span></span> | <span data-ttu-id="4a2fe-282">Compruebe el `RuntimeSupports` valor en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="4a2fe-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="4a2fe-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-284">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-284">**Issue**</span></span> | <span data-ttu-id="4a2fe-285">Un proyecto de dependencia no importa los destinos de restauración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="4a2fe-286">Esto es similar a NU1105, pero aquí se omite el proyecto y pasa por alto en lugar de producir todos de restauración a un error.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="4a2fe-287">En soluciones complejas a menudo hay otros tipos de proyectos que pueden no admitir la restauración.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="4a2fe-288">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-288">**Example message**</span></span> | <span data-ttu-id="4a2fe-289">*Se omitirá la restauración para el proyecto 'c:\a.csproj'. El archivo de proyecto puede ser destinos no válidos o que faltan necesarios para la restauración.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="4a2fe-290">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-290">**Solution**</span></span> | <span data-ttu-id="4a2fe-291">Esto puede ocurrir por proyectos que importen props/destinos comunes que se importan automáticamente la restauración.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="4a2fe-292">Si el proyecto no tiene que restaurarse Esto puede hacer caso omiso.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="4a2fe-293">En caso contrario, edite el proyecto afectado para agregar destinos de restauración.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="4a2fe-294">Advertencias de la versión de paquete inesperado</span><span class="sxs-lookup"><span data-stu-id="4a2fe-294">Unexpected package version warnings</span></span>

<span data-ttu-id="4a2fe-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="4a2fe-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="4a2fe-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-297">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-297">**Issue**</span></span> | <span data-ttu-id="4a2fe-298">Se incrementará en una dependencia de proyecto directa a una versión más reciente que el proyecto especificado.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="4a2fe-299">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-299">**Example message**</span></span> | <span data-ttu-id="4a2fe-300">*Dependencia especificada era NuGet.Versioning (> = 3.5.0) pero terminaba con NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="4a2fe-301">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-301">**Solution**</span></span> | <span data-ttu-id="4a2fe-302">Actualice la dependencia en el proyecto con una versión adecuada.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="4a2fe-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="4a2fe-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-304">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-304">**Issue**</span></span> | <span data-ttu-id="4a2fe-305">Una dependencia del paquete falta un límite inferior.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="4a2fe-306">Esto no permite la restauración buscar el *mejor coincidencia*.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="4a2fe-307">Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="4a2fe-308">Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="4a2fe-309">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-309">**Example message**</span></span> | <span data-ttu-id="4a2fe-310">*NuGet.Packaging 4.0.0 no proporciona un límite inferior inclusivo de dependencia NuGet.Versioning (3.5.0 >). Una mejor coincidencia aproximada de 3.6.0 se resolvió.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="4a2fe-311">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-311">**Solution**</span></span> | <span data-ttu-id="4a2fe-312">Esto suele ser un error de creación de paquete.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-312">This is usually a package authoring error.</span></span> <span data-ttu-id="4a2fe-313">Póngase en contacto con el autor del paquete para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="4a2fe-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="4a2fe-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-315">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-315">**Issue**</span></span> | <span data-ttu-id="4a2fe-316">Una dependencia del paquete especifica una versión que no se pudo encontrar.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="4a2fe-317">Normalmente, los orígenes del paquete no contienen la versión de límite inferior esperado.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="4a2fe-318">Una versión posterior se usó en su lugar, que es distinto de lo que se creó el paquete en.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="4a2fe-319">Esto significa que la restauración no se encontró el *mejor coincidencia*.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="4a2fe-320">Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="4a2fe-321">Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="4a2fe-322">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-322">**Example message**</span></span> | <span data-ttu-id="4a2fe-323">NuGet.Packaging 4.0.0 depende NuGet.Versioning (> = 4.0.0) pero no se encontró 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="4a2fe-324">Una mejor coincidencia aproximada de 5.0.0 se resolvió.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="4a2fe-325">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-325">**Solution**</span></span> | <span data-ttu-id="4a2fe-326">Si no se ha liberado el paquete que esperaba, a continuación, puede tratarse de un error de creación de paquete.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="4a2fe-327">Póngase en contacto con el autor del paquete para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="4a2fe-328">Si se ha liberado el paquete, compruebe que está disponible en los orígenes del paquete que está usando.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="4a2fe-329">Si usa una fuente privada, debe actualizar el paquete en esa fuente.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="4a2fe-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="4a2fe-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-331">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-331">**Issue**</span></span> | <span data-ttu-id="4a2fe-332">Una dependencia de proyecto no define un límite inferior.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="4a2fe-333">Esto significa que la restauración no se encontró el *mejor coincidencia*.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="4a2fe-334">Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="4a2fe-335">Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="4a2fe-336">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-336">**Example message**</span></span> | <span data-ttu-id="4a2fe-337">*Proyecto dependencia NuGet.Versioning (< = 9.0.0) doe no contiene un límite inferior inclusivo. Incluir un límite inferior en la versión de dependencia para garantizar que los resultados de restauración coherentes.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="4a2fe-338">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-338">**Solution**</span></span> | <span data-ttu-id="4a2fe-339">Actualice el proyecto `PackageReference` `Version` atributo para incluir un límite inferior.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="4a2fe-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="4a2fe-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-341">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-341">**Issue**</span></span> | <span data-ttu-id="4a2fe-342">Un paquete de dependencia especificó una restricción de versión en una versión posterior de un paquete que la restauración que se resuelven en última instancia.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="4a2fe-343">Es decir, debido a la "más cercano de wins" regla al resolver paquetes, un paquete cuanto más cerca en el gráfico de puede invalidar un paquete está lejos.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="4a2fe-344">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-344">**Example message**</span></span> | <span data-ttu-id="4a2fe-345">*Detecta la degradación de paquete: NuGet.Versioning de 4.0.0 3.5.0. Hacen referencia al paquete directamente desde el proyecto para seleccionar una versión diferente.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="4a2fe-346">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-346">**Solution**</span></span> | <span data-ttu-id="4a2fe-347">Agregue una referencia directa al proyecto para la versión más reciente del paquete que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="4a2fe-348">Advertencias de conflicto de resolución</span><span class="sxs-lookup"><span data-stu-id="4a2fe-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="4a2fe-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="4a2fe-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-350">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-350">**Issue**</span></span> | <span data-ttu-id="4a2fe-351">Un paquete resuelto es mayor que permite que una restricción de dependencia.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="4a2fe-352">Esto significa que un paquete al que hace referencia directamente un proyecto invalida las restricciones de dependencia de otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="4a2fe-353">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-353">**Example message**</span></span> | <span data-ttu-id="4a2fe-354">*Versión del paquete detectado fuera de restricción de dependencia: x 1.0.0 requiere y (= 1.0.0) pero la versión y 2.0.0 se resolvió.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="4a2fe-355">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-355">**Solution**</span></span> | <span data-ttu-id="4a2fe-356">En algunos casos esto tiene su porqué y se puede suprimir la advertencia.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="4a2fe-357">En caso contrario, cambie la referencia del proyecto al paquete para ampliar sus restricciones de versión.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="4a2fe-358">Advertencias de reserva de paquete</span><span class="sxs-lookup"><span data-stu-id="4a2fe-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="4a2fe-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="4a2fe-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-360">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-360">**Issue**</span></span> | <span data-ttu-id="4a2fe-361">`PackageTargetFallback` / `AssetTargetFallback` se usa para seleccionar los activos de un paquete.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="4a2fe-362">La advertencia que los usuarios sepan que los activos pueden no ser compatible al 100%.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="4a2fe-363">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-363">**Example message**</span></span> | <span data-ttu-id="4a2fe-364">*Paquete 'NuGet.Versioning' se restauró usando 'portable net45 + win8' en su lugar, la plataforma de destino del proyecto 'netstandard1.5'. Este paquete no puede ser totalmente compatible con el proyecto.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="4a2fe-365">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-365">**Solution**</span></span> | <span data-ttu-id="4a2fe-366">Cambiar plataforma de destino del proyecto a uno que admite el paquete.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="4a2fe-367">Advertencias de fuentes</span><span class="sxs-lookup"><span data-stu-id="4a2fe-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="4a2fe-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="4a2fe-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-369">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-369">**Issue**</span></span> | <span data-ttu-id="4a2fe-370">Se produjo un error al leer la fuente cuando `IgnoreFailedSources` se establece en true, se convierte en una advertencia no es grave.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="4a2fe-371">Esto podría contener todos los mensajes y es genérico.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="4a2fe-372">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-372">**Example message**</span></span> | <span data-ttu-id="4a2fe-373">N/D</span><span class="sxs-lookup"><span data-stu-id="4a2fe-373">n/a</span></span> |
| <span data-ttu-id="4a2fe-374">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-374">**Solution**</span></span> | <span data-ttu-id="4a2fe-375">Editar la configuración para especificar los orígenes de válido.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="4a2fe-376">Las advertencias y errores internos de NuGet</span><span class="sxs-lookup"><span data-stu-id="4a2fe-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="4a2fe-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="4a2fe-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="4a2fe-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-379">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-379">**Issue**</span></span> | <span data-ttu-id="4a2fe-380">Un error interno no es específico de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="4a2fe-381">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-381">**Solution**</span></span> | <span data-ttu-id="4a2fe-382">Compruebe los registros para obtener más información</span><span class="sxs-lookup"><span data-stu-id="4a2fe-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="4a2fe-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="4a2fe-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-384">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-384">**Issue**</span></span> | <span data-ttu-id="4a2fe-385">Advertencias interno no es específico de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="4a2fe-386">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-386">**Solution**</span></span> | <span data-ttu-id="4a2fe-387">Compruebe los registros para obtener más información</span><span class="sxs-lookup"><span data-stu-id="4a2fe-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="4a2fe-388">Paquetes firmados (creación y verificación)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="4a2fe-389">*4.6.0+ de NuGet*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="4a2fe-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="4a2fe-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="4a2fe-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-392">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-392">**Issue**</span></span> | <span data-ttu-id="4a2fe-393">Un error específico del no relacionados con la firma del paquete y había firmado de comprobación del paquete.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="4a2fe-394">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-394">**Solution**</span></span> | <span data-ttu-id="4a2fe-395">Compruebe los registros para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="4a2fe-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="4a2fe-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-397">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-397">**Issue**</span></span> | <span data-ttu-id="4a2fe-398">Argumentos no válidos a cualquiera la [firmar comando](../tools/cli-ref-sign.md) o [comprobar comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="4a2fe-399">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-399">**Solution**</span></span> | <span data-ttu-id="4a2fe-400">Compruebe y corrija los argumentos proporcionados.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="4a2fe-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="4a2fe-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-402">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-402">**Issue**</span></span> | <span data-ttu-id="4a2fe-403">El `-Timestamper` no se especificó la opción con la [comando de inicio de sesión de nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="4a2fe-404">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-404">**Example message**</span></span> | <span data-ttu-id="4a2fe-405">*El '-Timestamper' no se ha proporcionado la opción. El paquete firmado no estará con marca de tiempo.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="4a2fe-406">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-406">**Solution**</span></span> | <span data-ttu-id="4a2fe-407">Especifique el `-Timestamper` opción con `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="4a2fe-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="4a2fe-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-409">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-409">**Issue**</span></span> | <span data-ttu-id="4a2fe-410">Se proporcionó un paquete sin firmar para los [nuget Compruebe comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="4a2fe-411">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-411">**Solution**</span></span> | <span data-ttu-id="4a2fe-412">Ejecute `nuget verify` con un paquete firmado.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="4a2fe-413">Vea [firmar un paquete](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="4a2fe-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="4a2fe-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-415">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-415">**Issue**</span></span> | <span data-ttu-id="4a2fe-416">Error en la comprobación de integridad de paquete, lo que significa que un paquete firmado se ha alterado desde que se está firmando.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="4a2fe-417">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-417">**Solution**</span></span> | <span data-ttu-id="4a2fe-418">Analice el equipo con el software antivirus.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="4a2fe-419">A continuación, quite el paquete desde el equipo, vuelva a instalarlo y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="4a2fe-420">Si el problema continúa, póngase en contacto con el propietario del origen del paquete y el paquete.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="4a2fe-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="4a2fe-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-422">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-422">**Issue**</span></span> | <span data-ttu-id="4a2fe-423">No se pudo crear la cadena de certificados para la firma primaria.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="4a2fe-424">El certificado de firma principal no es de confianza, revocado, o información de revocación del certificado no está disponible.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="4a2fe-425">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-425">**Example message**</span></span> | <span data-ttu-id="4a2fe-426">*Advertencia: NU3018: la función de revocación no pudo comprobar la revocación del certificado.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="4a2fe-427">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-427">**Solution**</span></span> | <span data-ttu-id="4a2fe-428">Usar un certificado de confianza y es válido.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="4a2fe-429">Compruebe la conectividad de internet.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="4a2fe-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="4a2fe-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4a2fe-431">**Problema**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-431">**Issue**</span></span> | <span data-ttu-id="4a2fe-432">No se pudo crear la cadena de certificados para la firma de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="4a2fe-433">El certificado de firma de marca de tiempo no es de confianza, revocado, o información de revocación del certificado no está disponible.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="4a2fe-434">**Mensaje de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-434">**Example message**</span></span> | <span data-ttu-id="4a2fe-435">*Advertencia: NU3028: la función de revocación no pudo comprobar la revocación del certificado.*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="4a2fe-436">**Solución**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-436">**Solution**</span></span> | <span data-ttu-id="4a2fe-437">Usar un certificado de confianza y es válido.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="4a2fe-438">Compruebe la conectividad de internet.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-438">Check internet connectivity.</span></span> |
