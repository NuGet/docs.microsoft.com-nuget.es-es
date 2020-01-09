---
title: Referencia de PowerShell Open-PackagePage de NuGet
description: Referencia del comando de PowerShell Open-PackagePage en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384433"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="8e42e-103">Open-PackagePage (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="8e42e-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="8e42e-104">*En desuso en 3.0 +; solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="8e42e-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="8e42e-105">Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso del informe para el paquete especificado.</span><span class="sxs-lookup"><span data-stu-id="8e42e-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="8e42e-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="8e42e-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="8e42e-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="8e42e-107">Parameters</span></span>

| <span data-ttu-id="8e42e-108">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8e42e-108">Parameter</span></span> | <span data-ttu-id="8e42e-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="8e42e-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e42e-110">Id.</span><span class="sxs-lookup"><span data-stu-id="8e42e-110">Id</span></span> | <span data-ttu-id="8e42e-111">IDENTIFICADOR del paquete deseado.</span><span class="sxs-lookup"><span data-stu-id="8e42e-111">The package ID of the desired package.</span></span> <span data-ttu-id="8e42e-112">El propio modificador-ID es opcional.</span><span class="sxs-lookup"><span data-stu-id="8e42e-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="8e42e-113">Version</span><span class="sxs-lookup"><span data-stu-id="8e42e-113">Version</span></span> | <span data-ttu-id="8e42e-114">La versión del paquete, que tiene como valor predeterminado la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="8e42e-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="8e42e-115">Origen</span><span class="sxs-lookup"><span data-stu-id="8e42e-115">Source</span></span> | <span data-ttu-id="8e42e-116">El origen del paquete, que tiene como valor predeterminado el origen seleccionado en la lista desplegable origen.</span><span class="sxs-lookup"><span data-stu-id="8e42e-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="8e42e-117">Licencia</span><span class="sxs-lookup"><span data-stu-id="8e42e-117">License</span></span> | <span data-ttu-id="8e42e-118">Abre el explorador en la dirección URL de la licencia del paquete.</span><span class="sxs-lookup"><span data-stu-id="8e42e-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="8e42e-119">Si no se especifica ninguna licencia ni-ReportAbuse, el explorador abrirá la dirección URL del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="8e42e-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="8e42e-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="8e42e-120">ReportAbuse</span></span> | <span data-ttu-id="8e42e-121">Abre el explorador en la dirección URL del informe de abuso de informes.</span><span class="sxs-lookup"><span data-stu-id="8e42e-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="8e42e-122">Si no se especifica ninguna licencia ni-ReportAbuse, el explorador abrirá la dirección URL del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="8e42e-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="8e42e-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="8e42e-123">PassThru</span></span> | <span data-ttu-id="8e42e-124">Muestra la dirección URL; Use con-WhatIf para suprimir la apertura del explorador.</span><span class="sxs-lookup"><span data-stu-id="8e42e-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="8e42e-125">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="8e42e-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="8e42e-126">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="8e42e-126">Common Parameters</span></span>

<span data-ttu-id="8e42e-127">`Open-PackagePage` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="8e42e-127">`Open-PackagePage` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="8e42e-128">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="8e42e-128">Examples</span></span>

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