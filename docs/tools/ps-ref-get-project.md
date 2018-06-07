---
title: Referencia de PowerShell de NuGet Get-proyecto
description: Referencia de comandos de GetProject PowerShell en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: afdf9f762bbd34531f9d9093238a2fed27e3f4d3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817761"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="d06a6-103">Get-Project (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d06a6-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d06a6-104">*Disponible solo en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="d06a6-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d06a6-105">Muestra información sobre el valor predeterminado o el proyecto especificado.</span><span class="sxs-lookup"><span data-stu-id="d06a6-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="d06a6-106">`Get-Project` en concreto, devuelve un referente al objeto DTE (entorno de herramientas de desarrollo) de Visual Studio para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d06a6-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="d06a6-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="d06a6-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d06a6-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="d06a6-108">Parameters</span></span>

| <span data-ttu-id="d06a6-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d06a6-109">Parameter</span></span> | <span data-ttu-id="d06a6-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="d06a6-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d06a6-111">nombre</span><span class="sxs-lookup"><span data-stu-id="d06a6-111">Name</span></span> | <span data-ttu-id="d06a6-112">Especifica el proyecto para mostrar, el valor predeterminado para el proyecto predeterminado seleccionado en la consola de administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="d06a6-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="d06a6-113">-Nombre de conmutador es opcional.</span><span class="sxs-lookup"><span data-stu-id="d06a6-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="d06a6-114">Todas</span><span class="sxs-lookup"><span data-stu-id="d06a6-114">All</span></span> | <span data-ttu-id="d06a6-115">Muestra información acerca de todos los proyectos de la solución; el orden de los proyectos no es determinista.</span><span class="sxs-lookup"><span data-stu-id="d06a6-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="d06a6-116">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="d06a6-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d06a6-117">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="d06a6-117">Common Parameters</span></span>

<span data-ttu-id="d06a6-118">`Get-Project` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d06a6-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d06a6-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d06a6-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```