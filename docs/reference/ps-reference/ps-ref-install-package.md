---
title: Referencia de PowerShell de Install-Package de NuGet
description: Referencia de Install-Package comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5bda888e0fb526faca79e88da93b0ceb9aff5348
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237210"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ef43f-103">Install-Package (consola del administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ef43f-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ef43f-104">*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando genérico de Install-Package de PowerShell, consulte la [referencia de PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="ef43f-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="ef43f-105">Instala un paquete y sus dependencias en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="ef43f-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="ef43f-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="ef43f-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="ef43f-107">En NuGet 2.8 +, `Install-Package` puede degradar un paquete existente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ef43f-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="ef43f-108">Por ejemplo, si tiene instalado Microsoft. AspNet. MVC 5.1.0-RC1, el siguiente comando lo degradará a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="ef43f-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="ef43f-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="ef43f-109">Parameters</span></span>

| <span data-ttu-id="ef43f-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ef43f-110">Parameter</span></span> | <span data-ttu-id="ef43f-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef43f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef43f-112">Identificador</span><span class="sxs-lookup"><span data-stu-id="ef43f-112">Id</span></span> | <span data-ttu-id="ef43f-113">Desee Identificador del paquete que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="ef43f-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="ef43f-114">( *3.0 +* ) El identificador puede ser una ruta de acceso o dirección URL de un `packages.config` archivo o un `.nupkg` archivo.</span><span class="sxs-lookup"><span data-stu-id="ef43f-114">( *3.0+* ) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="ef43f-115">El propio modificador-ID es opcional.</span><span class="sxs-lookup"><span data-stu-id="ef43f-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ef43f-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="ef43f-116">IgnoreDependencies</span></span> | <span data-ttu-id="ef43f-117">Instale solo este paquete y no sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="ef43f-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="ef43f-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="ef43f-118">ProjectName</span></span> | <span data-ttu-id="ef43f-119">El proyecto en el que se va a instalar el paquete, que tiene como valor predeterminado el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ef43f-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="ef43f-120">Source</span><span class="sxs-lookup"><span data-stu-id="ef43f-120">Source</span></span> | <span data-ttu-id="ef43f-121">La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="ef43f-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="ef43f-122">Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="ef43f-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="ef43f-123">Si se omite, `Install-Package` busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="ef43f-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="ef43f-124">Versión</span><span class="sxs-lookup"><span data-stu-id="ef43f-124">Version</span></span> | <span data-ttu-id="ef43f-125">Versión del paquete que se va a instalar. el valor predeterminado es la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="ef43f-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="ef43f-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="ef43f-126">IncludePrerelease</span></span> | <span data-ttu-id="ef43f-127">Tiene en cuenta los paquetes de versión preliminar para la instalación.</span><span class="sxs-lookup"><span data-stu-id="ef43f-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="ef43f-128">Si se omite, solo se considerarán los paquetes estables.</span><span class="sxs-lookup"><span data-stu-id="ef43f-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="ef43f-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="ef43f-129">FileConflictAction</span></span> | <span data-ttu-id="ef43f-130">Acción que se realizará cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ef43f-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="ef43f-131">Los valores posibles son *overwrite, ignore, None, OverwriteAll* y *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="ef43f-131">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="ef43f-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="ef43f-132">DependencyVersion</span></span> | <span data-ttu-id="ef43f-133">La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:</span><span class="sxs-lookup"><span data-stu-id="ef43f-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="ef43f-134">*Más bajo* (valor predeterminado): la versión más baja</span><span class="sxs-lookup"><span data-stu-id="ef43f-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="ef43f-135">*HighestPatch* : la versión con la revisión principal más baja, menor menor y más alta.</span><span class="sxs-lookup"><span data-stu-id="ef43f-135">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="ef43f-136">*HighestMinor* : la versión con el reenvío más bajo principal, más alto, más alto</span><span class="sxs-lookup"><span data-stu-id="ef43f-136">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="ef43f-137">*Mayor* (valor predeterminado para Update-Package sin parámetros): la versión más alta</span><span class="sxs-lookup"><span data-stu-id="ef43f-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="ef43f-138">Puede establecer el valor predeterminado mediante la [`dependencyVersion`](../nuget-config-file.md#config-section) configuración del `Nuget.Config` archivo.</span><span class="sxs-lookup"><span data-stu-id="ef43f-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="ef43f-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="ef43f-139">WhatIf</span></span> | <span data-ttu-id="ef43f-140">Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la instalación.</span><span class="sxs-lookup"><span data-stu-id="ef43f-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="ef43f-141">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="ef43f-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ef43f-142">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="ef43f-142">Common Parameters</span></span>

<span data-ttu-id="ef43f-143">`Install-Package` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ef43f-143">`Install-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ef43f-144">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ef43f-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```