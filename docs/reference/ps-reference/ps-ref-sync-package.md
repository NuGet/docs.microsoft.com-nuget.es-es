---
title: 'Sincronización de NuGet: referencia de PowerShell de paquetes'
description: Referencia del comando PowerShell de paquete de sincronización en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a48a09a27b6db9b774e59b9a10652067179e2c27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327312"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f6d9c-103">Sync-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f6d9c-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f6d9c-104">*Versión 3.0 +; solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="f6d9c-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f6d9c-105">Obtiene la versión del paquete instalado del proyecto especificado (o predeterminado) y sincroniza la versión con el resto de proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="f6d9c-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="f6d9c-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f6d9c-107">Parámetros</span><span class="sxs-lookup"><span data-stu-id="f6d9c-107">Parameters</span></span>

| <span data-ttu-id="f6d9c-108">Parámetro</span><span class="sxs-lookup"><span data-stu-id="f6d9c-108">Parameter</span></span> | <span data-ttu-id="f6d9c-109">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="f6d9c-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6d9c-110">Id</span><span class="sxs-lookup"><span data-stu-id="f6d9c-110">Id</span></span> | <span data-ttu-id="f6d9c-111">Desee Identificador del paquete que se va a sincronizar. El propio modificador-ID es opcional.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f6d9c-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="f6d9c-112">IgnoreDependencies</span></span> | <span data-ttu-id="f6d9c-113">Instale solo este paquete y no sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="f6d9c-114">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="f6d9c-114">ProjectName</span></span> | <span data-ttu-id="f6d9c-115">Proyecto del que se va a sincronizar el paquete, que tiene como valor predeterminado el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="f6d9c-116">`Version`</span><span class="sxs-lookup"><span data-stu-id="f6d9c-116">Version</span></span> | <span data-ttu-id="f6d9c-117">Versión del paquete que se va a sincronizar, que tiene como valor predeterminado la versión instalada actualmente.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="f6d9c-118">source</span><span class="sxs-lookup"><span data-stu-id="f6d9c-118">Source</span></span> | <span data-ttu-id="f6d9c-119">La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f6d9c-120">Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f6d9c-121">Si se omite `Sync-Package` , busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f6d9c-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f6d9c-122">IncludePrerelease</span></span> | <span data-ttu-id="f6d9c-123">Incluye paquetes de versión preliminar en la sincronización.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="f6d9c-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f6d9c-124">FileConflictAction</span></span> | <span data-ttu-id="f6d9c-125">Acción que se realizará cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f6d9c-126">Los valores posibles son *overwrite, ignore, None, OverwriteAll*y *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="f6d9c-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f6d9c-127">DependencyVersion</span></span> | <span data-ttu-id="f6d9c-128">La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:</span><span class="sxs-lookup"><span data-stu-id="f6d9c-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f6d9c-129">*Más bajo* (valor predeterminado): la versión más baja</span><span class="sxs-lookup"><span data-stu-id="f6d9c-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f6d9c-130">*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f6d9c-131">*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</span><span class="sxs-lookup"><span data-stu-id="f6d9c-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f6d9c-132">*Más alto* (valor predeterminado para Update-package sin parámetros): la versión más alta</span><span class="sxs-lookup"><span data-stu-id="f6d9c-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="f6d9c-133">Puede establecer el valor predeterminado mediante la [`dependencyVersion`](../nuget-config-file.md#config-section) configuración `Nuget.Config` del archivo.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="f6d9c-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f6d9c-134">WhatIf</span></span> | <span data-ttu-id="f6d9c-135">Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la sincronización.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="f6d9c-136">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f6d9c-137">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="f6d9c-137">Common Parameters</span></span>

<span data-ttu-id="f6d9c-138">`Sync-Package`admite los siguientes [parámetros de PowerShell comunes](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f6d9c-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f6d9c-139">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f6d9c-139">Examples</span></span>

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
