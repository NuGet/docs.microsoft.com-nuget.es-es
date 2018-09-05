---
title: Referencia de PowerShell Get-proyecto de NuGet
description: Referencia de comandos de GetProject PowerShell en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550442"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="7e3fc-103">Get-Project (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7e3fc-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7e3fc-104">*Solo está disponible en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="7e3fc-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7e3fc-105">Muestra información sobre el valor predeterminado o el proyecto especificado.</span><span class="sxs-lookup"><span data-stu-id="7e3fc-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="7e3fc-106">`Get-Project` en concreto, devuelve un referente al objeto DTE (entorno de herramientas de desarrollo) de Visual Studio para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7e3fc-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="7e3fc-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="7e3fc-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7e3fc-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="7e3fc-108">Parameters</span></span>

| <span data-ttu-id="7e3fc-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="7e3fc-109">Parameter</span></span> | <span data-ttu-id="7e3fc-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="7e3fc-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e3fc-111">nombre</span><span class="sxs-lookup"><span data-stu-id="7e3fc-111">Name</span></span> | <span data-ttu-id="7e3fc-112">Especifica el proyecto para mostrar, el proyecto predeterminado seleccionado en la consola de administrador de paquetes de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7e3fc-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="7e3fc-113">-Nombre de conmutador es opcional.</span><span class="sxs-lookup"><span data-stu-id="7e3fc-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="7e3fc-114">Todas</span><span class="sxs-lookup"><span data-stu-id="7e3fc-114">All</span></span> | <span data-ttu-id="7e3fc-115">Muestra información de todos los proyectos de la solución; el orden de los proyectos no es determinista.</span><span class="sxs-lookup"><span data-stu-id="7e3fc-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="7e3fc-116">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="7e3fc-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7e3fc-117">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="7e3fc-117">Common Parameters</span></span>

<span data-ttu-id="7e3fc-118">`Get-Project` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7e3fc-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7e3fc-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7e3fc-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```