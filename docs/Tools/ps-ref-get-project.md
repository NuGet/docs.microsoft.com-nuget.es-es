---
title: Referencia de PowerShell de NuGet Get-proyecto | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 09c10ea3-ba26-4bfa-999e-de5350e6e920
description: Referencia de comandos de GetProject PowerShell en la consola de administrador de paquetes de NuGet en Visual Studio.
keywords: Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, Get-proyecto de paquete de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 40c986164c3f6bd6a02877e15827541aae77d8ad
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="a49f3-104">Get-proyecto (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a49f3-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a49f3-105">*Disponible solo en el [consola del Administrador de paquetes de NuGet](Package-Manager-Console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="a49f3-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a49f3-106">Muestra información sobre el valor predeterminado o el proyecto especificado.</span><span class="sxs-lookup"><span data-stu-id="a49f3-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="a49f3-107">`Get-Project`en concreto, devuelve un referente al objeto DTE (entorno de herramientas de desarrollo) de Visual Studio para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a49f3-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="a49f3-108">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="a49f3-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a49f3-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="a49f3-109">Parameters</span></span>

| <span data-ttu-id="a49f3-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="a49f3-110">Parameter</span></span> | <span data-ttu-id="a49f3-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="a49f3-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a49f3-112">Name</span><span class="sxs-lookup"><span data-stu-id="a49f3-112">Name</span></span> | <span data-ttu-id="a49f3-113">Especifica el proyecto para mostrar, el valor predeterminado para el proyecto predeterminado seleccionado en la consola de administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="a49f3-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="a49f3-114">-Nombre de conmutador es opcional.</span><span class="sxs-lookup"><span data-stu-id="a49f3-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="a49f3-115">Todas</span><span class="sxs-lookup"><span data-stu-id="a49f3-115">All</span></span> | <span data-ttu-id="a49f3-116">Muestra información acerca de todos los proyectos de la solución; el orden de los proyectos no es determinista.</span><span class="sxs-lookup"><span data-stu-id="a49f3-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="a49f3-117">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="a49f3-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a49f3-118">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="a49f3-118">Common Parameters</span></span>

<span data-ttu-id="a49f3-119">`Get-Project`admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a49f3-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a49f3-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a49f3-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```