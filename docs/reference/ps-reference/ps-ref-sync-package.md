---
title: Referencia de PowerShell de Sync-Package de NuGet
description: Referencia de Sync-Package comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 4261b0a20a4fd4183f7b08096c3477e6f9d0a02d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777404"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="1e11d-103">Sync-Package (consola del administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1e11d-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1e11d-104">*Versión 3.0 +; solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="1e11d-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1e11d-105">Obtiene la versión del paquete instalado del proyecto especificado (o predeterminado) y sincroniza la versión con el resto de proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="1e11d-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="1e11d-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="1e11d-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1e11d-107">Parámetros</span><span class="sxs-lookup"><span data-stu-id="1e11d-107">Parameters</span></span>

| <span data-ttu-id="1e11d-108">Parámetro</span><span class="sxs-lookup"><span data-stu-id="1e11d-108">Parameter</span></span> | <span data-ttu-id="1e11d-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e11d-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e11d-110">Identificador</span><span class="sxs-lookup"><span data-stu-id="1e11d-110">Id</span></span> | <span data-ttu-id="1e11d-111">Desee Identificador del paquete que se va a sincronizar. El propio modificador-ID es opcional.</span><span class="sxs-lookup"><span data-stu-id="1e11d-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="1e11d-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="1e11d-112">IgnoreDependencies</span></span> | <span data-ttu-id="1e11d-113">Instale solo este paquete y no sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="1e11d-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="1e11d-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="1e11d-114">ProjectName</span></span> | <span data-ttu-id="1e11d-115">Proyecto del que se va a sincronizar el paquete, que tiene como valor predeterminado el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="1e11d-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="1e11d-116">Versión</span><span class="sxs-lookup"><span data-stu-id="1e11d-116">Version</span></span> | <span data-ttu-id="1e11d-117">Versión del paquete que se va a sincronizar, que tiene como valor predeterminado la versión instalada actualmente.</span><span class="sxs-lookup"><span data-stu-id="1e11d-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="1e11d-118">Source</span><span class="sxs-lookup"><span data-stu-id="1e11d-118">Source</span></span> | <span data-ttu-id="1e11d-119">La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="1e11d-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="1e11d-120">Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="1e11d-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="1e11d-121">Si se omite, `Sync-Package` busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="1e11d-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="1e11d-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="1e11d-122">IncludePrerelease</span></span> | <span data-ttu-id="1e11d-123">Incluye paquetes de versión preliminar en la sincronización.</span><span class="sxs-lookup"><span data-stu-id="1e11d-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="1e11d-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="1e11d-124">FileConflictAction</span></span> | <span data-ttu-id="1e11d-125">Acción que se realizará cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e11d-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="1e11d-126">Los valores posibles son *overwrite, ignore, None, OverwriteAll* y *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="1e11d-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="1e11d-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="1e11d-127">DependencyVersion</span></span> | <span data-ttu-id="1e11d-128">La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e11d-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="1e11d-129">*Más bajo* (valor predeterminado): la versión más baja</span><span class="sxs-lookup"><span data-stu-id="1e11d-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="1e11d-130">*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</span><span class="sxs-lookup"><span data-stu-id="1e11d-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="1e11d-131">*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</span><span class="sxs-lookup"><span data-stu-id="1e11d-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="1e11d-132">*Mayor* (valor predeterminado para Update-Package sin parámetros): la versión más alta</span><span class="sxs-lookup"><span data-stu-id="1e11d-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="1e11d-133">Puede establecer el valor predeterminado mediante la [`dependencyVersion`](../nuget-config-file.md#config-section) configuración del `Nuget.Config` archivo.</span><span class="sxs-lookup"><span data-stu-id="1e11d-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="1e11d-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="1e11d-134">WhatIf</span></span> | <span data-ttu-id="1e11d-135">Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la sincronización.</span><span class="sxs-lookup"><span data-stu-id="1e11d-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="1e11d-136">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="1e11d-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1e11d-137">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="1e11d-137">Common Parameters</span></span>

<span data-ttu-id="1e11d-138">`Sync-Package` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1e11d-138">`Sync-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1e11d-139">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="1e11d-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```