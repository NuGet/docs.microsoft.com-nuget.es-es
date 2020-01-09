---
title: Referencia de PowerShell para buscar paquetes de NuGet
description: Referencia del comando de PowerShell Find-Package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384638"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="77431-103">Find-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="77431-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="77431-104">*Versión 3.0 +; en este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando de búsqueda-paquete de PowerShell genérico, vea la [referencia de PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="77431-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="77431-105">Obtiene el conjunto de paquetes remotos con el identificador o las palabras clave especificados del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="77431-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="77431-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="77431-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="77431-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="77431-107">Parameters</span></span>

| <span data-ttu-id="77431-108">Parámetro</span><span class="sxs-lookup"><span data-stu-id="77431-108">Parameter</span></span> | <span data-ttu-id="77431-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="77431-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77431-110">ID &lt;palabras clave&gt;</span><span class="sxs-lookup"><span data-stu-id="77431-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="77431-111">Desee Palabras clave que se deben usar al buscar en el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="77431-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="77431-112">Use-ExactMatch para devolver solo los paquetes cuyo identificador de paquete coincida con las palabras clave.</span><span class="sxs-lookup"><span data-stu-id="77431-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="77431-113">Si no se proporcionan palabras clave, `Find-Package` devuelve una lista de los 20 primeros paquetes por descargas o el número especificado por-First.</span><span class="sxs-lookup"><span data-stu-id="77431-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="77431-114">Tenga en cuenta que-ID es opcional y no es operativo.</span><span class="sxs-lookup"><span data-stu-id="77431-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="77431-115">Origen</span><span class="sxs-lookup"><span data-stu-id="77431-115">Source</span></span> | <span data-ttu-id="77431-116">La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="77431-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="77431-117">Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="77431-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="77431-118">Si se omite, `Find-Package` busca en el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="77431-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="77431-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="77431-119">AllVersions</span></span> | <span data-ttu-id="77431-120">Muestra todas las versiones disponibles de cada paquete en lugar de la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="77431-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="77431-121">First</span><span class="sxs-lookup"><span data-stu-id="77431-121">First</span></span> | <span data-ttu-id="77431-122">Número de paquetes que se van a devolver desde el principio de la lista; el valor predeterminado es 20.</span><span class="sxs-lookup"><span data-stu-id="77431-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="77431-123">Skip</span><span class="sxs-lookup"><span data-stu-id="77431-123">Skip</span></span> | <span data-ttu-id="77431-124">Omite la primera &lt;int&gt; paquetes de la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="77431-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="77431-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="77431-125">IncludePrerelease</span></span> | <span data-ttu-id="77431-126">Incluye paquetes de versiones preliminares en los resultados.</span><span class="sxs-lookup"><span data-stu-id="77431-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="77431-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="77431-127">ExactMatch</span></span> | <span data-ttu-id="77431-128">Se especifica para usar &lt;palabras clave&gt; como un identificador de paquete que distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="77431-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="77431-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="77431-129">StartWith</span></span> | <span data-ttu-id="77431-130">Devuelve los paquetes cuyo identificador de paquete comienza con &lt;palabras clave&gt;.</span><span class="sxs-lookup"><span data-stu-id="77431-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="77431-131">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="77431-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="77431-132">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="77431-132">Common Parameters</span></span>

<span data-ttu-id="77431-133">`Find-Package` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="77431-133">`Find-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="77431-134">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="77431-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
