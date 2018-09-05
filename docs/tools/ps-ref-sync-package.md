---
title: Referencia de PowerShell de sincronización-paquete de NuGet
description: Referencia de comandos de PowerShell de sincronización de paquete en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547999"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f71d0-103">Sync-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f71d0-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f71d0-104">*Versión 3.0 o superior; solo está disponible en el [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="f71d0-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f71d0-105">Obtiene la versión del paquete instalado desde especificado (o predeterminada) del proyecto y sincroniza la versión para el resto de los proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="f71d0-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="f71d0-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="f71d0-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f71d0-107">Parámetros</span><span class="sxs-lookup"><span data-stu-id="f71d0-107">Parameters</span></span>

| <span data-ttu-id="f71d0-108">Parámetro</span><span class="sxs-lookup"><span data-stu-id="f71d0-108">Parameter</span></span> | <span data-ttu-id="f71d0-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="f71d0-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f71d0-110">Id.</span><span class="sxs-lookup"><span data-stu-id="f71d0-110">Id</span></span> | <span data-ttu-id="f71d0-111">(Obligatorio) El identificador del paquete para sincronizar. -Identificador propio conmutador es opcional.</span><span class="sxs-lookup"><span data-stu-id="f71d0-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f71d0-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="f71d0-112">IgnoreDependencies</span></span> | <span data-ttu-id="f71d0-113">Instalar solo este paquete y no a sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="f71d0-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="f71d0-114">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="f71d0-114">ProjectName</span></span> | <span data-ttu-id="f71d0-115">El proyecto para sincronizar el paquete, de forma predeterminada el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f71d0-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="f71d0-116">Versión</span><span class="sxs-lookup"><span data-stu-id="f71d0-116">Version</span></span> | <span data-ttu-id="f71d0-117">La versión del paquete para la sincronización, la versión actualmente instalada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f71d0-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="f71d0-118">Origen</span><span class="sxs-lookup"><span data-stu-id="f71d0-118">Source</span></span> | <span data-ttu-id="f71d0-119">La ruta de acceso URL o carpeta para buscar el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="f71d0-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f71d0-120">Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="f71d0-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f71d0-121">Si se omite, `Sync-Package` busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="f71d0-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f71d0-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f71d0-122">IncludePrerelease</span></span> | <span data-ttu-id="f71d0-123">Incluye paquetes de versión preliminar de la sincronización.</span><span class="sxs-lookup"><span data-stu-id="f71d0-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="f71d0-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f71d0-124">FileConflictAction</span></span> | <span data-ttu-id="f71d0-125">La acción que se realizará cuando se le pida sobrescribir u omitir los archivos existentes que se hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f71d0-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f71d0-126">Los valores posibles son *sobrescribir, omitir, None, OverwriteAll*, y *(3.0 y versiones posteriores)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="f71d0-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="f71d0-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f71d0-127">DependencyVersion</span></span> | <span data-ttu-id="f71d0-128">La versión de los paquetes de dependencia para usar, que puede ser uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f71d0-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f71d0-129">*Menor* (valor predeterminado): la versión más antigua</span><span class="sxs-lookup"><span data-stu-id="f71d0-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f71d0-130">*HighestPatch*: la versión con la revisión menor principal, secundaria menor, más alta</span><span class="sxs-lookup"><span data-stu-id="f71d0-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f71d0-131">*HighestMinor*: la versión con el menor principales, revisiones secundarias y de mayor más alto</span><span class="sxs-lookup"><span data-stu-id="f71d0-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f71d0-132">*Mayor* (predeterminado para el paquete de actualización sin parámetros): la versión más alta</span><span class="sxs-lookup"><span data-stu-id="f71d0-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="f71d0-133">Puede establecer el valor predeterminado con el [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) en el `Nuget.Config` archivo.</span><span class="sxs-lookup"><span data-stu-id="f71d0-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="f71d0-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f71d0-134">WhatIf</span></span> | <span data-ttu-id="f71d0-135">Muestra lo que sucedería cuando ejecute el comando sin tener que realizar la sincronización.</span><span class="sxs-lookup"><span data-stu-id="f71d0-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="f71d0-136">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="f71d0-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f71d0-137">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="f71d0-137">Common Parameters</span></span>

<span data-ttu-id="f71d0-138">`Sync-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f71d0-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f71d0-139">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f71d0-139">Examples</span></span>

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
