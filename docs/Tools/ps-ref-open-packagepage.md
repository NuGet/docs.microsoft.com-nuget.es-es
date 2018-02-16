---
title: "Referencia de página del paquete NuGet abrir PowerShell | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referencia de comandos de PowerShell de página del paquete abierto en la consola de administrador de paquetes de NuGet en Visual Studio."
keywords: "Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, Abrir página del paquete del paquete NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cc645d9a2779fd6b1b329e9aac4777d50f75d16
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="f409f-104">Abrir página del paquete (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f409f-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f409f-105">*En desuso en 3.0 +; disponible solo en el [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="f409f-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f409f-106">Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso de informes para el paquete especificado.</span><span class="sxs-lookup"><span data-stu-id="f409f-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="f409f-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="f409f-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f409f-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="f409f-108">Parameters</span></span>

| <span data-ttu-id="f409f-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="f409f-109">Parameter</span></span> | <span data-ttu-id="f409f-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="f409f-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f409f-111">Id.</span><span class="sxs-lookup"><span data-stu-id="f409f-111">Id</span></span> | <span data-ttu-id="f409f-112">El identificador del paquete del paquete adecuado.</span><span class="sxs-lookup"><span data-stu-id="f409f-112">The package ID of the desired package.</span></span> <span data-ttu-id="f409f-113">-Identificador propio modificador es opcional.</span><span class="sxs-lookup"><span data-stu-id="f409f-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f409f-114">Versión</span><span class="sxs-lookup"><span data-stu-id="f409f-114">Version</span></span> | <span data-ttu-id="f409f-115">La versión del paquete, la versión más reciente de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f409f-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="f409f-116">Origen</span><span class="sxs-lookup"><span data-stu-id="f409f-116">Source</span></span> | <span data-ttu-id="f409f-117">El origen del paquete, el valor predeterminado para el origen seleccionado en el origen de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="f409f-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="f409f-118">Licencia</span><span class="sxs-lookup"><span data-stu-id="f409f-118">License</span></span> | <span data-ttu-id="f409f-119">Se abre el explorador a la dirección URL de licencia del paquete.</span><span class="sxs-lookup"><span data-stu-id="f409f-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="f409f-120">Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="f409f-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f409f-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="f409f-121">ReportAbuse</span></span> | <span data-ttu-id="f409f-122">Se abre el explorador para la dirección URL de abuso de informes del paquete.</span><span class="sxs-lookup"><span data-stu-id="f409f-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="f409f-123">Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="f409f-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f409f-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="f409f-124">PassThru</span></span> | <span data-ttu-id="f409f-125">Muestra la dirección URL; Utilícelo con - WhatIf para suprimir abrir el explorador.</span><span class="sxs-lookup"><span data-stu-id="f409f-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="f409f-126">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="f409f-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f409f-127">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="f409f-127">Common Parameters</span></span>

<span data-ttu-id="f409f-128">`Open-PackagePage` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f409f-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f409f-129">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f409f-129">Examples</span></span>

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