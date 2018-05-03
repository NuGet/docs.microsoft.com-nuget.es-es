---
title: Referencia de PowerShell de página del paquete NuGet abierto
description: Referencia de comandos de PowerShell de página del paquete abierto en la consola de administrador de paquetes de NuGet en Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="cbb0c-103">Abrir página del paquete (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cbb0c-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="cbb0c-104">*En desuso en 3.0 +; disponible solo en el [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="cbb0c-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="cbb0c-105">Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso de informes para el paquete especificado.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="cbb0c-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="cbb0c-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="cbb0c-107">Parámetros</span><span class="sxs-lookup"><span data-stu-id="cbb0c-107">Parameters</span></span>

| <span data-ttu-id="cbb0c-108">Parámetro</span><span class="sxs-lookup"><span data-stu-id="cbb0c-108">Parameter</span></span> | <span data-ttu-id="cbb0c-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="cbb0c-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cbb0c-110">Id.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-110">Id</span></span> | <span data-ttu-id="cbb0c-111">El identificador del paquete del paquete adecuado.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-111">The package ID of the desired package.</span></span> <span data-ttu-id="cbb0c-112">-Identificador propio modificador es opcional.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="cbb0c-113">Versión</span><span class="sxs-lookup"><span data-stu-id="cbb0c-113">Version</span></span> | <span data-ttu-id="cbb0c-114">La versión del paquete, la versión más reciente de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="cbb0c-115">Origen</span><span class="sxs-lookup"><span data-stu-id="cbb0c-115">Source</span></span> | <span data-ttu-id="cbb0c-116">El origen del paquete, el valor predeterminado para el origen seleccionado en el origen de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="cbb0c-117">Licencia</span><span class="sxs-lookup"><span data-stu-id="cbb0c-117">License</span></span> | <span data-ttu-id="cbb0c-118">Se abre el explorador a la dirección URL de licencia del paquete.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="cbb0c-119">Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="cbb0c-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="cbb0c-120">ReportAbuse</span></span> | <span data-ttu-id="cbb0c-121">Se abre el explorador para la dirección URL de abuso de informes del paquete.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="cbb0c-122">Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="cbb0c-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="cbb0c-123">PassThru</span></span> | <span data-ttu-id="cbb0c-124">Muestra la dirección URL; Utilícelo con - WhatIf para suprimir abrir el explorador.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="cbb0c-125">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="cbb0c-126">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="cbb0c-126">Common Parameters</span></span>

<span data-ttu-id="cbb0c-127">`Open-PackagePage` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cbb0c-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="cbb0c-128">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="cbb0c-128">Examples</span></span>

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