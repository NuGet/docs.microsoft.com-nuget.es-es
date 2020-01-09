---
title: 'Actualización de NuGet: referencia de PowerShell de paquetes'
description: Referencia del comando de PowerShell Update-package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e1bff9d4b7391d8be87afa4b8f2fbd51ae922140
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384861"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c2113-103">Update-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c2113-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c2113-104">*Solo está disponible en la [consola del administrador de paquetes NuGet](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="c2113-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c2113-105">Actualiza un paquete y sus dependencias, o todos los paquetes de un proyecto, a una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="c2113-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="c2113-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="c2113-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="c2113-107">En NuGet 2.8 +, `Update-Package` se puede usar para degradar un paquete existente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="c2113-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="c2113-108">Por ejemplo, si tiene instalado Microsoft. AspNet. MVC 5.1.0-RC1, el siguiente comando lo degradará a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="c2113-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="c2113-109">Parameters</span><span class="sxs-lookup"><span data-stu-id="c2113-109">Parameters</span></span>

|  <span data-ttu-id="c2113-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="c2113-110">Parameter</span></span> | <span data-ttu-id="c2113-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="c2113-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2113-112">Id.</span><span class="sxs-lookup"><span data-stu-id="c2113-112">Id</span></span> | <span data-ttu-id="c2113-113">Identificador del paquete que se va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="c2113-113">The identifier of the package to update.</span></span> <span data-ttu-id="c2113-114">Si se omite, actualiza todos los paquetes.</span><span class="sxs-lookup"><span data-stu-id="c2113-114">If omitted, updates all packages.</span></span> <span data-ttu-id="c2113-115">El propio modificador-ID es opcional.</span><span class="sxs-lookup"><span data-stu-id="c2113-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="c2113-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="c2113-116">IgnoreDependencies</span></span> | <span data-ttu-id="c2113-117">Omite la actualización de las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="c2113-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="c2113-118">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="c2113-118">ProjectName</span></span> | <span data-ttu-id="c2113-119">Nombre del proyecto que contiene los paquetes que se van a actualizar; el valor predeterminado es todos los proyectos.</span><span class="sxs-lookup"><span data-stu-id="c2113-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="c2113-120">Version</span><span class="sxs-lookup"><span data-stu-id="c2113-120">Version</span></span> | <span data-ttu-id="c2113-121">Versión que se va a usar para la actualización, que tiene como valor predeterminado la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="c2113-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="c2113-122">En NuGet 3.0 y versiones posteriores, el valor de la versión debe ser uno de los más *bajos, HighestMinor*o *HighestPatch* (equivalente a Safe).</span><span class="sxs-lookup"><span data-stu-id="c2113-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="c2113-123">Caja fuerte</span><span class="sxs-lookup"><span data-stu-id="c2113-123">Safe</span></span> | <span data-ttu-id="c2113-124">Restringe las actualizaciones solo a las versiones con la misma versión principal y secundaria que el paquete instalado actualmente.</span><span class="sxs-lookup"><span data-stu-id="c2113-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="c2113-125">Origen</span><span class="sxs-lookup"><span data-stu-id="c2113-125">Source</span></span> | <span data-ttu-id="c2113-126">La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="c2113-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="c2113-127">Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="c2113-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="c2113-128">Si se omite, `Update-Package` busca en el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="c2113-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="c2113-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="c2113-129">IncludePrerelease</span></span> | <span data-ttu-id="c2113-130">Incluye paquetes de versión preliminar para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="c2113-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="c2113-131">Reinstalación</span><span class="sxs-lookup"><span data-stu-id="c2113-131">Reinstall</span></span> | <span data-ttu-id="c2113-132">Resintalls paquetes con sus versiones instaladas actualmente.</span><span class="sxs-lookup"><span data-stu-id="c2113-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="c2113-133">Vea [Reinstalación y actualización de paquetes](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c2113-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="c2113-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="c2113-134">FileConflictAction</span></span> | <span data-ttu-id="c2113-135">Acción que se realizará cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="c2113-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="c2113-136">Los valores posibles son *overwrite, ignore, None, OverwriteAll*y *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="c2113-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="c2113-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="c2113-137">DependencyVersion</span></span> | <span data-ttu-id="c2113-138">La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:</span><span class="sxs-lookup"><span data-stu-id="c2113-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="c2113-139">*Más bajo* (valor predeterminado): la versión más baja</span><span class="sxs-lookup"><span data-stu-id="c2113-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="c2113-140">*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</span><span class="sxs-lookup"><span data-stu-id="c2113-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="c2113-141">*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</span><span class="sxs-lookup"><span data-stu-id="c2113-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="c2113-142">*Más alto* (valor predeterminado para Update-package sin parámetros): la versión más alta</span><span class="sxs-lookup"><span data-stu-id="c2113-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="c2113-143">Puede establecer el valor predeterminado mediante la opción [`dependencyVersion`](../nuget-config-file.md#config-section) del archivo de `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="c2113-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="c2113-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="c2113-144">ToHighestPatch</span></span> | <span data-ttu-id="c2113-145">equivalente a Safe.</span><span class="sxs-lookup"><span data-stu-id="c2113-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="c2113-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="c2113-146">ToHighestMinor</span></span> | <span data-ttu-id="c2113-147">Restringe las actualizaciones a solo las versiones con la misma versión principal que el paquete instalado actualmente.</span><span class="sxs-lookup"><span data-stu-id="c2113-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="c2113-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="c2113-148">WhatIf</span></span> | <span data-ttu-id="c2113-149">Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la actualización.</span><span class="sxs-lookup"><span data-stu-id="c2113-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="c2113-150">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="c2113-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="c2113-151">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="c2113-151">Common Parameters</span></span>

<span data-ttu-id="c2113-152">`Update-Package` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c2113-152">`Update-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="c2113-153">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c2113-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
