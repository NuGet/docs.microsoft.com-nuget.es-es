---
title: Referencia de PowerShell de paquete de actualización de NuGet | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia de comandos de PowerShell de paquete de actualización en la consola de administrador de paquetes de NuGet en Visual Studio.
keywords: Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, paquete de actualización del paquete de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 05772159d62f73e7d25f71ad36809f5ae8ef6aae
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="012cb-104">Paquete de actualización (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="012cb-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="012cb-105">*Disponible solo en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="012cb-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="012cb-106">Actualiza un paquete y sus dependencias o todos los paquetes en un proyecto a una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="012cb-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="012cb-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="012cb-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="012cb-108">En NuGet 2.8 + `Update-Package` puede utilizarse para cambiar un paquete existente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="012cb-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="012cb-109">Por ejemplo, si tiene 5.1.0-rc1 Microsoft.AspNet.MVC instalado, el siguiente comando de la degradación a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="012cb-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="012cb-110">Parámetros</span><span class="sxs-lookup"><span data-stu-id="012cb-110">Parameters</span></span>

|  <span data-ttu-id="012cb-111">Parámetro</span><span class="sxs-lookup"><span data-stu-id="012cb-111">Parameter</span></span> | <span data-ttu-id="012cb-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="012cb-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="012cb-113">Id.</span><span class="sxs-lookup"><span data-stu-id="012cb-113">Id</span></span> | <span data-ttu-id="012cb-114">El identificador del paquete para actualizar.</span><span class="sxs-lookup"><span data-stu-id="012cb-114">The identifier of the package to update.</span></span> <span data-ttu-id="012cb-115">Si se omite, se actualiza todos los paquetes.</span><span class="sxs-lookup"><span data-stu-id="012cb-115">If omitted, updates all packages.</span></span> <span data-ttu-id="012cb-116">-Identificador propio modificador es opcional.</span><span class="sxs-lookup"><span data-stu-id="012cb-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="012cb-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="012cb-117">IgnoreDependencies</span></span> | <span data-ttu-id="012cb-118">Omite la actualización de las dependencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="012cb-118">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="012cb-119">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="012cb-119">ProjectName</span></span> | <span data-ttu-id="012cb-120">El nombre del proyecto que contiene los paquetes que se va a actualizar, el valor predeterminado para todos los proyectos.</span><span class="sxs-lookup"><span data-stu-id="012cb-120">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="012cb-121">Versión</span><span class="sxs-lookup"><span data-stu-id="012cb-121">Version</span></span> | <span data-ttu-id="012cb-122">La versión que se utilizará para la actualización, la versión más reciente de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="012cb-122">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="012cb-123">En NuGet 3.0 +, el valor de versión debe ser uno de *mínima, máxima, HighestMinor*, o *HighestPatch* (equivalente a - seguro).</span><span class="sxs-lookup"><span data-stu-id="012cb-123">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="012cb-124">Seguridad de</span><span class="sxs-lookup"><span data-stu-id="012cb-124">Safe</span></span> | <span data-ttu-id="012cb-125">Restringe las actualizaciones a solo las versiones con la misma versión de mayor y menor que el paquete instalado actualmente.</span><span class="sxs-lookup"><span data-stu-id="012cb-125">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="012cb-126">Origen</span><span class="sxs-lookup"><span data-stu-id="012cb-126">Source</span></span> | <span data-ttu-id="012cb-127">La ruta de acceso URL o una carpeta de origen del paquete para buscar.</span><span class="sxs-lookup"><span data-stu-id="012cb-127">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="012cb-128">Las rutas de acceso de la carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="012cb-128">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="012cb-129">Si se omite, `Update-Package` busca en el origen del paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="012cb-129">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="012cb-130">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="012cb-130">IncludePrerelease</span></span> | <span data-ttu-id="012cb-131">Incluye paquetes de versión preliminar para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="012cb-131">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="012cb-132">Reinstalación</span><span class="sxs-lookup"><span data-stu-id="012cb-132">Reinstall</span></span> | <span data-ttu-id="012cb-133">Paquetes de Resintalls con sus versiones instaladas actualmente.</span><span class="sxs-lookup"><span data-stu-id="012cb-133">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="012cb-134">Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="012cb-134">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="012cb-135">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="012cb-135">FileConflictAction</span></span> | <span data-ttu-id="012cb-136">La acción que se realizará cuando se le pregunte para sobrescribir u omitir los archivos existentes al que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="012cb-136">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="012cb-137">Los valores posibles son *sobrescribir, omitir, None, OverwriteAll*, y *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="012cb-137">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="012cb-138">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="012cb-138">DependencyVersion</span></span> | <span data-ttu-id="012cb-139">La versión de los paquetes de dependencia que se va a usar, que puede ser uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="012cb-139">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="012cb-140">*Menor* (valor predeterminado): la versión más antigua</span><span class="sxs-lookup"><span data-stu-id="012cb-140">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="012cb-141">*HighestPatch*: la versión con la revisión mínimo mayor, menor menor, más alto</span><span class="sxs-lookup"><span data-stu-id="012cb-141">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="012cb-142">*HighestMinor*: la versión con el menor principales, mayor revisión secundaria, más alto</span><span class="sxs-lookup"><span data-stu-id="012cb-142">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="012cb-143">*Mayor* (predeterminado para el paquete de actualización sin parámetros): la versión más reciente</span><span class="sxs-lookup"><span data-stu-id="012cb-143">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="012cb-144">Puede establecer el valor predeterminado mediante la [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) en el `Nuget.Config` archivo.</span><span class="sxs-lookup"><span data-stu-id="012cb-144">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="012cb-145">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="012cb-145">ToHighestPatch</span></span> | <span data-ttu-id="012cb-146">Restringe las actualizaciones a solo las versiones con la misma versión menor que el paquete instalado actualmente.</span><span class="sxs-lookup"><span data-stu-id="012cb-146">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="012cb-147">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="012cb-147">ToHighestMinor</span></span> | <span data-ttu-id="012cb-148">Restringe las actualizaciones a solo las versiones con la misma versión principal que el paquete instalado actualmente.</span><span class="sxs-lookup"><span data-stu-id="012cb-148">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="012cb-149">WhatIf</span><span class="sxs-lookup"><span data-stu-id="012cb-149">WhatIf</span></span> | <span data-ttu-id="012cb-150">Muestra qué ocurre cuando se ejecuta el comando sin realmente realizar la actualización.</span><span class="sxs-lookup"><span data-stu-id="012cb-150">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="012cb-151">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="012cb-151">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="012cb-152">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="012cb-152">Common Parameters</span></span>

<span data-ttu-id="012cb-153">`Update-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="012cb-153">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="012cb-154">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="012cb-154">Examples</span></span>

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
