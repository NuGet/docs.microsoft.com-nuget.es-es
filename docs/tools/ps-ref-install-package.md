---
title: Referencia de PowerShell de NuGet Install-Package
description: Referencia de comandos de PowerShell de Install-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842498"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="44782-103">Install-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="44782-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="44782-104">*Este tema describe el comando dentro de la [Package Manager Console](package-manager-console.md) en Visual Studio en Windows. El comando de PowerShell, Install-Package genérico, vea el [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="44782-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="44782-105">Instala un paquete y sus dependencias en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="44782-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="44782-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="44782-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="44782-107">En NuGet 2.8 y versiones posteriores, `Install-Package` puede degradar un paquete existente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="44782-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="44782-108">Por ejemplo, si tiene 5.1.0-rc1 Microsoft.AspNet.MVC instalado, el siguiente comando de la degradación a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="44782-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="44782-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="44782-109">Parameters</span></span>

| <span data-ttu-id="44782-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="44782-110">Parameter</span></span> | <span data-ttu-id="44782-111">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="44782-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44782-112">Id</span><span class="sxs-lookup"><span data-stu-id="44782-112">Id</span></span> | <span data-ttu-id="44782-113">(Obligatorio) El identificador del paquete para instalar.</span><span class="sxs-lookup"><span data-stu-id="44782-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="44782-114">(*3.0 +* ) el identificador puede ser una ruta de acceso o dirección URL de un `packages.config` archivo o un `.nupkg` archivo.</span><span class="sxs-lookup"><span data-stu-id="44782-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="44782-115">-Identificador propio conmutador es opcional.</span><span class="sxs-lookup"><span data-stu-id="44782-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="44782-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="44782-116">IgnoreDependencies</span></span> | <span data-ttu-id="44782-117">Instalar solo este paquete y no a sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="44782-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="44782-118">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="44782-118">ProjectName</span></span> | <span data-ttu-id="44782-119">El proyecto en el que se va a instalar el paquete, de forma predeterminada el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="44782-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="44782-120">source</span><span class="sxs-lookup"><span data-stu-id="44782-120">Source</span></span> | <span data-ttu-id="44782-121">La ruta de acceso URL o carpeta para buscar el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="44782-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="44782-122">Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="44782-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="44782-123">Si se omite, `Install-Package` busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="44782-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="44782-124">`Version`</span><span class="sxs-lookup"><span data-stu-id="44782-124">Version</span></span> | <span data-ttu-id="44782-125">La versión del paquete para instalar, la versión más reciente de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="44782-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="44782-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="44782-126">IncludePrerelease</span></span> | <span data-ttu-id="44782-127">Considera que los paquetes de versión preliminar para la instalación.</span><span class="sxs-lookup"><span data-stu-id="44782-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="44782-128">Si se omite, se consideran solo los paquetes estables.</span><span class="sxs-lookup"><span data-stu-id="44782-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="44782-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="44782-129">FileConflictAction</span></span> | <span data-ttu-id="44782-130">La acción que se realizará cuando se le pida sobrescribir u omitir los archivos existentes que se hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="44782-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="44782-131">Los valores posibles son *sobrescribir, omitir, None, OverwriteAll*, y *(3.0 y versiones posteriores)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="44782-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="44782-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="44782-132">DependencyVersion</span></span> | <span data-ttu-id="44782-133">La versión de los paquetes de dependencia para usar, que puede ser uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="44782-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="44782-134">*Menor* (valor predeterminado): la versión más antigua</span><span class="sxs-lookup"><span data-stu-id="44782-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="44782-135">*HighestPatch*: la versión con la revisión menor principal, secundaria menor, más alta</span><span class="sxs-lookup"><span data-stu-id="44782-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="44782-136">*HighestMinor*: la versión con el menor principales, revisiones secundarias y de mayor más alto</span><span class="sxs-lookup"><span data-stu-id="44782-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="44782-137">*Mayor* (predeterminado para el paquete de actualización sin parámetros): la versión más alta</span><span class="sxs-lookup"><span data-stu-id="44782-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="44782-138">Puede establecer el valor predeterminado con el [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) en el `Nuget.Config` archivo.</span><span class="sxs-lookup"><span data-stu-id="44782-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="44782-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="44782-139">WhatIf</span></span> | <span data-ttu-id="44782-140">Muestra lo que sucedería cuando ejecute el comando sin tener que realizar la instalación.</span><span class="sxs-lookup"><span data-stu-id="44782-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="44782-141">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="44782-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="44782-142">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="44782-142">Common Parameters</span></span>

<span data-ttu-id="44782-143">`Install-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="44782-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="44782-144">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="44782-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
