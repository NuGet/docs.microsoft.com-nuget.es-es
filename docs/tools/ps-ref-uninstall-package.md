---
title: Referencia de PowerShell de NuGet Uninstall-Package
description: Referencia de comandos de PowerShell Uninstall-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551648"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="cc771-103">Uninstall-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cc771-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="cc771-104">*Este tema describe el comando dentro de la [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows. El comando de PowerShell Uninstall-Package genérico, vea el [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="cc771-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="cc771-105">Quita un paquete desde un proyecto, quitar, opcionalmente, sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="cc771-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="cc771-106">Si otros paquetes dependen de este paquete, el comando fallará a menos que – Force se especifica la opción.</span><span class="sxs-lookup"><span data-stu-id="cc771-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="cc771-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="cc771-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="cc771-108">Si otros paquetes dependen de este paquete, el comando fallará a menos que – Force se especifica la opción.</span><span class="sxs-lookup"><span data-stu-id="cc771-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="cc771-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="cc771-109">Parameters</span></span>

| <span data-ttu-id="cc771-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="cc771-110">Parameter</span></span> | <span data-ttu-id="cc771-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="cc771-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc771-112">Id.</span><span class="sxs-lookup"><span data-stu-id="cc771-112">Id</span></span> | <span data-ttu-id="cc771-113">(Obligatorio) El identificador del paquete para desinstalar.</span><span class="sxs-lookup"><span data-stu-id="cc771-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="cc771-114">-Identificador propio conmutador es opcional.</span><span class="sxs-lookup"><span data-stu-id="cc771-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="cc771-115">Versión</span><span class="sxs-lookup"><span data-stu-id="cc771-115">Version</span></span> | <span data-ttu-id="cc771-116">La versión del paquete para desinstalar, la versión actualmente instalada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cc771-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="cc771-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="cc771-117">RemoveDependencies</span></span> | <span data-ttu-id="cc771-118">Desinstale el paquete y sus dependencias no usadas.</span><span class="sxs-lookup"><span data-stu-id="cc771-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="cc771-119">Es decir, si una dependencia tiene otro paquete que depende de él, se omitirá.</span><span class="sxs-lookup"><span data-stu-id="cc771-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="cc771-120">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="cc771-120">ProjectName</span></span> | <span data-ttu-id="cc771-121">El proyecto desde el que se va a desinstalar el paquete, de forma predeterminada el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="cc771-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="cc771-122">Force</span><span class="sxs-lookup"><span data-stu-id="cc771-122">Force</span></span> | <span data-ttu-id="cc771-123">Fuerza un paquete que se desinstalara, incluso si otros paquetes dependen de él.</span><span class="sxs-lookup"><span data-stu-id="cc771-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="cc771-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="cc771-124">WhatIf</span></span> | <span data-ttu-id="cc771-125">Muestra lo que sucedería cuando ejecute el comando sin tener que realizar la desinstalación.</span><span class="sxs-lookup"><span data-stu-id="cc771-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="cc771-126">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="cc771-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="cc771-127">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="cc771-127">Common Parameters</span></span>

<span data-ttu-id="cc771-128">`Uninstall-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cc771-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="cc771-129">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="cc771-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
