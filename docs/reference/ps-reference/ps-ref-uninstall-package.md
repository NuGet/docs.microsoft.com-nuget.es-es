---
title: Referencia de NuGet Uninstall-Package PowerShell
description: Referencia de Uninstall-Package comando de PowerShell en la consola de Administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901790"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="38944-103">Uninstall-Package (Administrador de paquetes consola en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="38944-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="38944-104">*En este tema se describe el comando dentro de [Administrador de paquetes Console](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para obtener el comando genérico de Uninstall-Package PowerShell, consulte la referencia [de PackageManagement de PowerShell.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="38944-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="38944-105">Quita un paquete de un proyecto y, opcionalmente, quita sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="38944-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="38944-106">Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.</span><span class="sxs-lookup"><span data-stu-id="38944-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="38944-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="38944-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="38944-108">Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.</span><span class="sxs-lookup"><span data-stu-id="38944-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="38944-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="38944-109">Parameters</span></span>

| <span data-ttu-id="38944-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="38944-110">Parameter</span></span> | <span data-ttu-id="38944-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="38944-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38944-112">Identificador</span><span class="sxs-lookup"><span data-stu-id="38944-112">Id</span></span> | <span data-ttu-id="38944-113">(Obligatorio) Identificador del paquete que se desinstalará.</span><span class="sxs-lookup"><span data-stu-id="38944-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="38944-114">El propio modificador -Id es opcional.</span><span class="sxs-lookup"><span data-stu-id="38944-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="38944-115">Versión</span><span class="sxs-lookup"><span data-stu-id="38944-115">Version</span></span> | <span data-ttu-id="38944-116">La versión del paquete que se desinstalará, con el valor predeterminado de la versión instalada actualmente.</span><span class="sxs-lookup"><span data-stu-id="38944-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="38944-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="38944-117">RemoveDependencies</span></span> | <span data-ttu-id="38944-118">Desinstale el paquete y sus dependencias no utilizadas.</span><span class="sxs-lookup"><span data-stu-id="38944-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="38944-119">Es decir, si alguna dependencia tiene otro paquete que depende de él, se omite.</span><span class="sxs-lookup"><span data-stu-id="38944-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="38944-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="38944-120">ProjectName</span></span> | <span data-ttu-id="38944-121">Proyecto del que se va a desinstalar el paquete, cuyo valor predeterminado es el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="38944-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="38944-122">Force</span><span class="sxs-lookup"><span data-stu-id="38944-122">Force</span></span> | <span data-ttu-id="38944-123">Fuerza la desinstalación de un paquete, incluso si otros paquetes dependen de él.</span><span class="sxs-lookup"><span data-stu-id="38944-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="38944-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="38944-124">WhatIf</span></span> | <span data-ttu-id="38944-125">Muestra lo que sucedería al ejecutar el comando sin realizar realmente la desinstalación.</span><span class="sxs-lookup"><span data-stu-id="38944-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="38944-126">Ninguno de estos parámetros acepta caracteres comodín o entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="38944-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="38944-127">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="38944-127">Common Parameters</span></span>

<span data-ttu-id="38944-128">`Uninstall-Package` admite los siguientes parámetros comunes de [PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="38944-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="38944-129">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="38944-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```