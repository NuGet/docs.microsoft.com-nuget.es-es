---
title: 'Instalación de NuGet: referencia de PowerShell de paquetes'
description: Referencia del comando de PowerShell Install-Package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327342"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3c64a-103">Install-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3c64a-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3c64a-104">*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando genérico Install-Package de PowerShell, consulte la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="3c64a-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3c64a-105">Instala un paquete y sus dependencias en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="3c64a-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="3c64a-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3c64a-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="3c64a-107">En NuGet 2.8 +, `Install-Package` puede degradar un paquete existente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3c64a-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="3c64a-108">Por ejemplo, si tiene instalado Microsoft. AspNet. MVC 5.1.0-RC1, el siguiente comando lo degradará a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="3c64a-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="3c64a-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3c64a-109">Parameters</span></span>

| <span data-ttu-id="3c64a-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="3c64a-110">Parameter</span></span> | <span data-ttu-id="3c64a-111">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="3c64a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c64a-112">Id</span><span class="sxs-lookup"><span data-stu-id="3c64a-112">Id</span></span> | <span data-ttu-id="3c64a-113">Desee Identificador del paquete que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="3c64a-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="3c64a-114">(*3.0 +* ) El identificador puede ser una ruta de acceso o dirección URL `packages.config` de un archivo `.nupkg` o un archivo.</span><span class="sxs-lookup"><span data-stu-id="3c64a-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="3c64a-115">El propio modificador-ID es opcional.</span><span class="sxs-lookup"><span data-stu-id="3c64a-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="3c64a-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="3c64a-116">IgnoreDependencies</span></span> | <span data-ttu-id="3c64a-117">Instale solo este paquete y no sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="3c64a-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="3c64a-118">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="3c64a-118">ProjectName</span></span> | <span data-ttu-id="3c64a-119">El proyecto en el que se va a instalar el paquete, que tiene como valor predeterminado el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="3c64a-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="3c64a-120">source</span><span class="sxs-lookup"><span data-stu-id="3c64a-120">Source</span></span> | <span data-ttu-id="3c64a-121">La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="3c64a-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="3c64a-122">Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="3c64a-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="3c64a-123">Si se omite `Install-Package` , busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="3c64a-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="3c64a-124">`Version`</span><span class="sxs-lookup"><span data-stu-id="3c64a-124">Version</span></span> | <span data-ttu-id="3c64a-125">Versión del paquete que se va a instalar. el valor predeterminado es la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="3c64a-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="3c64a-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="3c64a-126">IncludePrerelease</span></span> | <span data-ttu-id="3c64a-127">Tiene en cuenta los paquetes de versión preliminar para la instalación.</span><span class="sxs-lookup"><span data-stu-id="3c64a-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="3c64a-128">Si se omite, solo se tienen en cuenta los paquetes estables.</span><span class="sxs-lookup"><span data-stu-id="3c64a-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="3c64a-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="3c64a-129">FileConflictAction</span></span> | <span data-ttu-id="3c64a-130">Acción que se realizará cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3c64a-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="3c64a-131">Los valores posibles son *overwrite, ignore, None, OverwriteAll*y *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="3c64a-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="3c64a-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="3c64a-132">DependencyVersion</span></span> | <span data-ttu-id="3c64a-133">La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:</span><span class="sxs-lookup"><span data-stu-id="3c64a-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="3c64a-134">*Más bajo* (valor predeterminado): la versión más baja</span><span class="sxs-lookup"><span data-stu-id="3c64a-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="3c64a-135">*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</span><span class="sxs-lookup"><span data-stu-id="3c64a-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="3c64a-136">*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</span><span class="sxs-lookup"><span data-stu-id="3c64a-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="3c64a-137">*Más alto* (valor predeterminado para Update-package sin parámetros): la versión más alta</span><span class="sxs-lookup"><span data-stu-id="3c64a-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="3c64a-138">Puede establecer el valor predeterminado mediante la [`dependencyVersion`](../nuget-config-file.md#config-section) configuración `Nuget.Config` del archivo.</span><span class="sxs-lookup"><span data-stu-id="3c64a-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="3c64a-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="3c64a-139">WhatIf</span></span> | <span data-ttu-id="3c64a-140">Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la instalación.</span><span class="sxs-lookup"><span data-stu-id="3c64a-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="3c64a-141">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="3c64a-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3c64a-142">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="3c64a-142">Common Parameters</span></span>

<span data-ttu-id="3c64a-143">`Install-Package`admite los siguientes [parámetros de PowerShell comunes](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3c64a-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3c64a-144">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="3c64a-144">Examples</span></span>

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
