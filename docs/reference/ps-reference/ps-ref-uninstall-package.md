---
title: Referencia de PowerShell de Uninstall-Package de NuGet
description: Referencia de Uninstall-Package comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237132"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="78661-103">Uninstall-Package (consola del administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="78661-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="78661-104">*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando genérico de Uninstall-Package de PowerShell, consulte la [referencia de PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="78661-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="78661-105">Quita un paquete de un proyecto y, opcionalmente, quita sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="78661-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="78661-106">Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.</span><span class="sxs-lookup"><span data-stu-id="78661-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="78661-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="78661-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="78661-108">Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.</span><span class="sxs-lookup"><span data-stu-id="78661-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="78661-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="78661-109">Parameters</span></span>

| <span data-ttu-id="78661-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="78661-110">Parameter</span></span> | <span data-ttu-id="78661-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="78661-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="78661-112">Identificador</span><span class="sxs-lookup"><span data-stu-id="78661-112">Id</span></span> | <span data-ttu-id="78661-113">Desee Identificador del paquete que se va a desinstalar.</span><span class="sxs-lookup"><span data-stu-id="78661-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="78661-114">El propio modificador-ID es opcional.</span><span class="sxs-lookup"><span data-stu-id="78661-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="78661-115">Versión</span><span class="sxs-lookup"><span data-stu-id="78661-115">Version</span></span> | <span data-ttu-id="78661-116">Versión del paquete que se va a desinstalar, que tiene como valor predeterminado la versión instalada actualmente.</span><span class="sxs-lookup"><span data-stu-id="78661-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="78661-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="78661-117">RemoveDependencies</span></span> | <span data-ttu-id="78661-118">Desinstale el paquete y sus dependencias no usadas.</span><span class="sxs-lookup"><span data-stu-id="78661-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="78661-119">Es decir, si alguna dependencia tiene otro paquete que depende de ella, se omite.</span><span class="sxs-lookup"><span data-stu-id="78661-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="78661-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="78661-120">ProjectName</span></span> | <span data-ttu-id="78661-121">Proyecto desde el que se va a desinstalar el paquete. el valor predeterminado es el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="78661-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="78661-122">Force</span><span class="sxs-lookup"><span data-stu-id="78661-122">Force</span></span> | <span data-ttu-id="78661-123">Fuerza la desinstalación de un paquete, aunque otros paquetes dependan de él.</span><span class="sxs-lookup"><span data-stu-id="78661-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="78661-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="78661-124">WhatIf</span></span> | <span data-ttu-id="78661-125">Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la desinstalación.</span><span class="sxs-lookup"><span data-stu-id="78661-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="78661-126">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="78661-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="78661-127">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="78661-127">Common Parameters</span></span>

<span data-ttu-id="78661-128">`Uninstall-Package` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="78661-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="78661-129">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="78661-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```