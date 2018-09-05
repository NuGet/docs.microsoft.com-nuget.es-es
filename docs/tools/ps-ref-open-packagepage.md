---
title: Referencia de PowerShell de NuGet abierto-PackagePage
description: Referencia de comandos de PowerShell abierto PackagePage en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547173"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="a35d3-103">Open-PackagePage (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a35d3-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a35d3-104">*En desuso en 3.0 + solo está disponible en el [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="a35d3-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a35d3-105">Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso de informes para el paquete especificado.</span><span class="sxs-lookup"><span data-stu-id="a35d3-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="a35d3-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="a35d3-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a35d3-107">Parámetros</span><span class="sxs-lookup"><span data-stu-id="a35d3-107">Parameters</span></span>

| <span data-ttu-id="a35d3-108">Parámetro</span><span class="sxs-lookup"><span data-stu-id="a35d3-108">Parameter</span></span> | <span data-ttu-id="a35d3-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="a35d3-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a35d3-110">Id.</span><span class="sxs-lookup"><span data-stu-id="a35d3-110">Id</span></span> | <span data-ttu-id="a35d3-111">El identificador del paquete del paquete deseado.</span><span class="sxs-lookup"><span data-stu-id="a35d3-111">The package ID of the desired package.</span></span> <span data-ttu-id="a35d3-112">-Identificador propio conmutador es opcional.</span><span class="sxs-lookup"><span data-stu-id="a35d3-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="a35d3-113">Versión</span><span class="sxs-lookup"><span data-stu-id="a35d3-113">Version</span></span> | <span data-ttu-id="a35d3-114">La versión del paquete, la versión más reciente de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a35d3-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="a35d3-115">Origen</span><span class="sxs-lookup"><span data-stu-id="a35d3-115">Source</span></span> | <span data-ttu-id="a35d3-116">El origen del paquete, el valor predeterminado el origen seleccionado en el origen de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="a35d3-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="a35d3-117">Licencia</span><span class="sxs-lookup"><span data-stu-id="a35d3-117">License</span></span> | <span data-ttu-id="a35d3-118">Se abre el explorador a la dirección URL de licencia del paquete.</span><span class="sxs-lookup"><span data-stu-id="a35d3-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="a35d3-119">Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="a35d3-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="a35d3-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="a35d3-120">ReportAbuse</span></span> | <span data-ttu-id="a35d3-121">Se abre el explorador para la dirección URL de abuso de informes del paquete.</span><span class="sxs-lookup"><span data-stu-id="a35d3-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="a35d3-122">Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="a35d3-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="a35d3-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="a35d3-123">PassThru</span></span> | <span data-ttu-id="a35d3-124">Muestra la dirección URL; Utilícelo con - WhatIf para suprimir la apertura del explorador.</span><span class="sxs-lookup"><span data-stu-id="a35d3-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="a35d3-125">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="a35d3-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a35d3-126">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="a35d3-126">Common Parameters</span></span>

<span data-ttu-id="a35d3-127">`Open-PackagePage` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a35d3-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a35d3-128">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a35d3-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```