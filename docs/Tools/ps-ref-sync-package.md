---
title: "Referencia de PowerShell de sincronización-paquete de NuGet | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1b980b93-fa58-430c-b663-78ce069b1603
description: "Referencia de comandos de PowerShell de paquete de sincronización en la consola de administrador de paquetes de NuGet en Visual Studio."
keywords: "Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, paquete de sincronización del paquete NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dc542714f14f0e6d3e827292f8fce06561fe270
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="86c32-104">Paquete de sincronización (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="86c32-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="86c32-105">*Versión 3.0 +; disponible solo en el [NuGet Package Manager Console](Package-Manager-Console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="86c32-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="86c32-106">Obtiene la versión del paquete instalado desde especificado (o predeterminado) del proyecto y sincroniza la versión para el resto de proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="86c32-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="86c32-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="86c32-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="86c32-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="86c32-108">Parameters</span></span>

| <span data-ttu-id="86c32-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="86c32-109">Parameter</span></span> | <span data-ttu-id="86c32-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="86c32-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86c32-111">Id.</span><span class="sxs-lookup"><span data-stu-id="86c32-111">Id</span></span> | <span data-ttu-id="86c32-112">(Obligatorio) El identificador del paquete que se va a sincronizar. -Identificador propio modificador es opcional.</span><span class="sxs-lookup"><span data-stu-id="86c32-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="86c32-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="86c32-113">IgnoreDependencies</span></span> | <span data-ttu-id="86c32-114">Instalar solo este paquete pero no sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="86c32-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="86c32-115">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="86c32-115">ProjectName</span></span> | <span data-ttu-id="86c32-116">El proyecto para sincronizar el paquete, el valor predeterminado para el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="86c32-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="86c32-117">Versión</span><span class="sxs-lookup"><span data-stu-id="86c32-117">Version</span></span> | <span data-ttu-id="86c32-118">La versión del paquete para la sincronización, la versión instalada actualmente de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="86c32-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="86c32-119">Origen</span><span class="sxs-lookup"><span data-stu-id="86c32-119">Source</span></span> | <span data-ttu-id="86c32-120">La ruta de acceso URL o una carpeta de origen del paquete para buscar.</span><span class="sxs-lookup"><span data-stu-id="86c32-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="86c32-121">Las rutas de acceso de la carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="86c32-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="86c32-122">Si se omite, `Sync-Package` busca en el origen del paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="86c32-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="86c32-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="86c32-123">IncludePrerelease</span></span> | <span data-ttu-id="86c32-124">Incluye paquetes de versión preliminar de la sincronización.</span><span class="sxs-lookup"><span data-stu-id="86c32-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="86c32-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="86c32-125">FileConflictAction</span></span> | <span data-ttu-id="86c32-126">La acción que se realizará cuando se le pregunte para sobrescribir u omitir los archivos existentes al que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="86c32-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="86c32-127">Los valores posibles son *sobrescribir, omitir, None, OverwriteAll*, y *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="86c32-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="86c32-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="86c32-128">DependencyVersion</span></span> | <span data-ttu-id="86c32-129">La versión de los paquetes de dependencia que se va a usar, que puede ser uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="86c32-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="86c32-130">*Menor* (valor predeterminado): la versión más antigua</span><span class="sxs-lookup"><span data-stu-id="86c32-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="86c32-131">*HighestPatch*: la versión con la revisión mínimo mayor, menor menor, más alto</span><span class="sxs-lookup"><span data-stu-id="86c32-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="86c32-132">*HighestMinor*: la versión con el menor principales, mayor revisión secundaria, más alto</span><span class="sxs-lookup"><span data-stu-id="86c32-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="86c32-133">*Mayor* (predeterminado para el paquete de actualización sin parámetros): la versión más reciente</span><span class="sxs-lookup"><span data-stu-id="86c32-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="86c32-134">Puede establecer el valor predeterminado mediante la [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) en el `Nuget.Config` archivo.</span><span class="sxs-lookup"><span data-stu-id="86c32-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="86c32-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="86c32-135">WhatIf</span></span> | <span data-ttu-id="86c32-136">Muestra qué ocurre cuando se ejecuta el comando sin realmente realizar la sincronización.</span><span class="sxs-lookup"><span data-stu-id="86c32-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="86c32-137">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="86c32-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="86c32-138">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="86c32-138">Common Parameters</span></span>

<span data-ttu-id="86c32-139">`Sync-Package`admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="86c32-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="86c32-140">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="86c32-140">Examples</span></span>

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
