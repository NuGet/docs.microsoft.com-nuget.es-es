---
title: Referencia de PowerShell de Get-Project de NuGet
description: Referencia del comando de PowerShell de GetProject en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6d9e1d48c8e1838f193878cab3483b1bfba7d7f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238080"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="ff77b-103">Get-Project (consola del administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ff77b-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ff77b-104">*Solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="ff77b-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ff77b-105">Muestra información sobre el proyecto predeterminado o el especificado.</span><span class="sxs-lookup"><span data-stu-id="ff77b-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="ff77b-106">`Get-Project` en concreto, devuelve un objeto referente al objeto DTE de Visual Studio (entorno de herramientas de desarrollo) del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ff77b-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="ff77b-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="ff77b-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ff77b-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="ff77b-108">Parameters</span></span>

| <span data-ttu-id="ff77b-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ff77b-109">Parameter</span></span> | <span data-ttu-id="ff77b-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="ff77b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff77b-111">Nombre</span><span class="sxs-lookup"><span data-stu-id="ff77b-111">Name</span></span> | <span data-ttu-id="ff77b-112">Especifica el proyecto que se va a mostrar, que tiene como valor predeterminado el proyecto predeterminado seleccionado en la consola del administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="ff77b-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="ff77b-113">El modificador-name es opcional.</span><span class="sxs-lookup"><span data-stu-id="ff77b-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="ff77b-114">Todo</span><span class="sxs-lookup"><span data-stu-id="ff77b-114">All</span></span> | <span data-ttu-id="ff77b-115">Muestra información de todos los proyectos de la solución; el orden de los proyectos no es determinista.</span><span class="sxs-lookup"><span data-stu-id="ff77b-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="ff77b-116">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="ff77b-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ff77b-117">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="ff77b-117">Common Parameters</span></span>

<span data-ttu-id="ff77b-118">`Get-Project` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ff77b-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ff77b-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ff77b-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```