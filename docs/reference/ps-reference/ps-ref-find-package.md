---
title: Referencia de NuGet Find-Package PowerShell
description: Referencia de Find-Package comando de PowerShell en la consola de Administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901764"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="003ba-103">Find-Package (Administrador de paquetes console en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="003ba-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="003ba-104">*Versión 3.0+; En este tema se describe el comando dentro [de Administrador de paquetes Console](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para obtener el comando Find-Package de PowerShell genérico, vea la referencia [de PackageManagement de PowerShell.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="003ba-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="003ba-105">Obtiene el conjunto de paquetes remotos con el identificador o las palabras clave especificados del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="003ba-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="003ba-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="003ba-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="003ba-107">Parámetros</span><span class="sxs-lookup"><span data-stu-id="003ba-107">Parameters</span></span>

| <span data-ttu-id="003ba-108">Parámetro</span><span class="sxs-lookup"><span data-stu-id="003ba-108">Parameter</span></span> | <span data-ttu-id="003ba-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="003ba-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="003ba-110">Palabras &lt; clave de identificador&gt;</span><span class="sxs-lookup"><span data-stu-id="003ba-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="003ba-111">(Obligatorio) Palabras clave que se usarán al buscar en el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="003ba-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="003ba-112">Use -ExactMatch para devolver solo los paquetes cuyo identificador de paquete coincida con las palabras clave.</span><span class="sxs-lookup"><span data-stu-id="003ba-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="003ba-113">Si no se especifica ninguna palabra clave, devuelve una lista de los 20 paquetes principales por descargas o el número `Find-Package` especificado por -First.</span><span class="sxs-lookup"><span data-stu-id="003ba-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="003ba-114">Tenga en cuenta que -Id es opcional y no-op.</span><span class="sxs-lookup"><span data-stu-id="003ba-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="003ba-115">Source</span><span class="sxs-lookup"><span data-stu-id="003ba-115">Source</span></span> | <span data-ttu-id="003ba-116">Dirección URL o ruta de acceso de carpeta para el origen del paquete que se buscará.</span><span class="sxs-lookup"><span data-stu-id="003ba-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="003ba-117">Las rutas de acceso de carpeta local pueden ser absolutas o relativas a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="003ba-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="003ba-118">Si se omite, `Find-Package` busca en el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="003ba-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="003ba-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="003ba-119">AllVersions</span></span> | <span data-ttu-id="003ba-120">Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="003ba-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="003ba-121">First</span><span class="sxs-lookup"><span data-stu-id="003ba-121">First</span></span> | <span data-ttu-id="003ba-122">Número de paquetes que se devolverán desde el principio de la lista. el valor predeterminado es 20.</span><span class="sxs-lookup"><span data-stu-id="003ba-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="003ba-123">Omitir</span><span class="sxs-lookup"><span data-stu-id="003ba-123">Skip</span></span> | <span data-ttu-id="003ba-124">Omite los primeros paquetes &lt; int de la lista &gt; mostrada.</span><span class="sxs-lookup"><span data-stu-id="003ba-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="003ba-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="003ba-125">IncludePrerelease</span></span> | <span data-ttu-id="003ba-126">Incluye paquetes de versión preliminar en los resultados.</span><span class="sxs-lookup"><span data-stu-id="003ba-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="003ba-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="003ba-127">ExactMatch</span></span> | <span data-ttu-id="003ba-128">Se especifica para usar palabras &lt; clave como identificador de paquete que distingue &gt; mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="003ba-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="003ba-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="003ba-129">StartWith</span></span> | <span data-ttu-id="003ba-130">Devuelve paquetes cuyo identificador de paquete comienza con &lt; palabras clave &gt; .</span><span class="sxs-lookup"><span data-stu-id="003ba-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="003ba-131">Ninguno de estos parámetros acepta caracteres comodín o entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="003ba-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="003ba-132">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="003ba-132">Common Parameters</span></span>

<span data-ttu-id="003ba-133">`Find-Package` admite los siguientes parámetros comunes de [PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="003ba-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="003ba-134">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="003ba-134">Examples</span></span>

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