---
title: Referencia de PowerShell Get-proyecto de NuGet
description: Referencia de comandos de GetProject PowerShell en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842280"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="7ffa0-103">Get-Project (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7ffa0-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7ffa0-104">*Solo está disponible en el [Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="7ffa0-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7ffa0-105">Muestra información sobre el valor predeterminado o el proyecto especificado.</span><span class="sxs-lookup"><span data-stu-id="7ffa0-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="7ffa0-106">`Get-Project` en concreto, devuelve un referente al objeto DTE (entorno de herramientas de desarrollo) de Visual Studio para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7ffa0-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="7ffa0-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="7ffa0-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7ffa0-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="7ffa0-108">Parameters</span></span>

| <span data-ttu-id="7ffa0-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="7ffa0-109">Parameter</span></span> | <span data-ttu-id="7ffa0-110">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="7ffa0-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7ffa0-111">NOMBRE</span><span class="sxs-lookup"><span data-stu-id="7ffa0-111">Name</span></span> | <span data-ttu-id="7ffa0-112">Especifica el proyecto para mostrar, el proyecto predeterminado seleccionado en la consola de administrador de paquetes de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7ffa0-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="7ffa0-113">-Nombre de conmutador es opcional.</span><span class="sxs-lookup"><span data-stu-id="7ffa0-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="7ffa0-114">Todo</span><span class="sxs-lookup"><span data-stu-id="7ffa0-114">All</span></span> | <span data-ttu-id="7ffa0-115">Muestra información de todos los proyectos de la solución; el orden de los proyectos no es determinista.</span><span class="sxs-lookup"><span data-stu-id="7ffa0-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="7ffa0-116">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="7ffa0-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7ffa0-117">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="7ffa0-117">Common Parameters</span></span>

<span data-ttu-id="7ffa0-118">`Get-Project` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7ffa0-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7ffa0-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7ffa0-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```