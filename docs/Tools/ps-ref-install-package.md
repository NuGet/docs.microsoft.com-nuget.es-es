---
title: Referencia de PowerShell de paquete de instalación de NuGet | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia de comandos de PowerShell de paquete de instalación en la consola de administrador de paquetes de NuGet en Visual Studio.
keywords: Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, Install-Package de paquete de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99c965c2f8c12c7a59ee48e270172b719c1482ea
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="455c6-104">Paquete de instalación (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="455c6-104">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="455c6-105">*Este tema describe el comando dentro de la [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows. Para el comando de PowerShell Install-Package genérico, vea la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="455c6-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="455c6-106">Instala un paquete y sus dependencias en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="455c6-106">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="455c6-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="455c6-107">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="455c6-108">En NuGet 2.8 + `Install-Package` puede degradar un paquete existente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="455c6-108">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="455c6-109">Por ejemplo, si tiene 5.1.0-rc1 Microsoft.AspNet.MVC instalado, el siguiente comando de la degradación a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="455c6-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="455c6-110">Parámetros</span><span class="sxs-lookup"><span data-stu-id="455c6-110">Parameters</span></span>

| <span data-ttu-id="455c6-111">Parámetro</span><span class="sxs-lookup"><span data-stu-id="455c6-111">Parameter</span></span> | <span data-ttu-id="455c6-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="455c6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="455c6-113">Id.</span><span class="sxs-lookup"><span data-stu-id="455c6-113">Id</span></span> | <span data-ttu-id="455c6-114">(Obligatorio) El identificador de paquete que desea instalar.</span><span class="sxs-lookup"><span data-stu-id="455c6-114">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="455c6-115">(*3.0 +*) el identificador puede ser una ruta de acceso o dirección URL de un `packages.config` archivo o un `.nupkg` archivo.</span><span class="sxs-lookup"><span data-stu-id="455c6-115">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="455c6-116">-Identificador propio modificador es opcional.</span><span class="sxs-lookup"><span data-stu-id="455c6-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="455c6-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="455c6-117">IgnoreDependencies</span></span> | <span data-ttu-id="455c6-118">Instalar solo este paquete pero no sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="455c6-118">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="455c6-119">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="455c6-119">ProjectName</span></span> | <span data-ttu-id="455c6-120">El proyecto en el que se va a instalar el paquete, el valor predeterminado para el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="455c6-120">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="455c6-121">Origen</span><span class="sxs-lookup"><span data-stu-id="455c6-121">Source</span></span> | <span data-ttu-id="455c6-122">La ruta de acceso URL o una carpeta de origen del paquete para buscar.</span><span class="sxs-lookup"><span data-stu-id="455c6-122">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="455c6-123">Las rutas de acceso de la carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="455c6-123">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="455c6-124">Si se omite, `Install-Package` busca en el origen del paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="455c6-124">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="455c6-125">Versión</span><span class="sxs-lookup"><span data-stu-id="455c6-125">Version</span></span> | <span data-ttu-id="455c6-126">La versión del paquete para instalar, toma como valor predeterminado para la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="455c6-126">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="455c6-127">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="455c6-127">IncludePrerelease</span></span> | <span data-ttu-id="455c6-128">Considera los paquetes de versión preliminar para la instalación.</span><span class="sxs-lookup"><span data-stu-id="455c6-128">Considers prerelease packages for the install.</span></span> <span data-ttu-id="455c6-129">Si se omite, se consideran solo los paquetes estables.</span><span class="sxs-lookup"><span data-stu-id="455c6-129">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="455c6-130">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="455c6-130">FileConflictAction</span></span> | <span data-ttu-id="455c6-131">La acción que se realizará cuando se le pregunte para sobrescribir u omitir los archivos existentes al que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="455c6-131">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="455c6-132">Los valores posibles son *sobrescribir, omitir, None, OverwriteAll*, y *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="455c6-132">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="455c6-133">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="455c6-133">DependencyVersion</span></span> | <span data-ttu-id="455c6-134">La versión de los paquetes de dependencia que se va a usar, que puede ser uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="455c6-134">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="455c6-135">*Menor* (valor predeterminado): la versión más antigua</span><span class="sxs-lookup"><span data-stu-id="455c6-135">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="455c6-136">*HighestPatch*: la versión con la revisión mínimo mayor, menor menor, más alto</span><span class="sxs-lookup"><span data-stu-id="455c6-136">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="455c6-137">*HighestMinor*: la versión con el menor principales, mayor revisión secundaria, más alto</span><span class="sxs-lookup"><span data-stu-id="455c6-137">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="455c6-138">*Mayor* (predeterminado para el paquete de actualización sin parámetros): la versión más reciente</span><span class="sxs-lookup"><span data-stu-id="455c6-138">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="455c6-139">Puede establecer el valor predeterminado mediante la [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) en el `Nuget.Config` archivo.</span><span class="sxs-lookup"><span data-stu-id="455c6-139">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="455c6-140">WhatIf</span><span class="sxs-lookup"><span data-stu-id="455c6-140">WhatIf</span></span> | <span data-ttu-id="455c6-141">Muestra qué ocurre cuando se ejecuta el comando sin realmente realizar la instalación.</span><span class="sxs-lookup"><span data-stu-id="455c6-141">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="455c6-142">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="455c6-142">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="455c6-143">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="455c6-143">Common Parameters</span></span>

<span data-ttu-id="455c6-144">`Install-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="455c6-144">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="455c6-145">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="455c6-145">Examples</span></span>

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
