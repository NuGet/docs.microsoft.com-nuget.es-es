---
title: Referencia de PowerShell de Find-paquete de NuGet
description: Referencia de comandos de PowerShell de Find-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842522"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5aa8d-103">Find-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5aa8d-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5aa8d-104">*Versión 3.0 o superior; Este tema describe el comando dentro de la [Package Manager Console](package-manager-console.md) en Visual Studio en Windows. El comando de PowerShell Find-Package genérico, vea el [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="5aa8d-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="5aa8d-105">Obtiene el conjunto de paquetes remotos con el identificador especificado o palabras clave del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="5aa8d-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="5aa8d-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5aa8d-107">Parámetros</span><span class="sxs-lookup"><span data-stu-id="5aa8d-107">Parameters</span></span>

| <span data-ttu-id="5aa8d-108">Parámetro</span><span class="sxs-lookup"><span data-stu-id="5aa8d-108">Parameter</span></span> | <span data-ttu-id="5aa8d-109">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="5aa8d-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5aa8d-110">Id. de &lt;palabras clave&gt;</span><span class="sxs-lookup"><span data-stu-id="5aa8d-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="5aa8d-111">(Obligatorio) Palabras clave pueden usarse al buscar el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="5aa8d-112">Utilice - ExactMatch para devolver solo los paquetes cuyo identificador de paquete coincide con las palabras clave.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="5aa8d-113">Si no se especifica ninguna palabra clave, `Find-Package` devuelve una lista de los primeros 20 paquetes por descarga o el número especificada por - primero.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="5aa8d-114">Tenga en cuenta que - Id. es opcional y una operación inefectiva.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="5aa8d-115">source</span><span class="sxs-lookup"><span data-stu-id="5aa8d-115">Source</span></span> | <span data-ttu-id="5aa8d-116">La ruta de acceso URL o carpeta para buscar el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5aa8d-117">Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5aa8d-118">Si se omite, `Find-Package` busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5aa8d-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="5aa8d-119">AllVersions</span></span> | <span data-ttu-id="5aa8d-120">Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="5aa8d-121">Primero</span><span class="sxs-lookup"><span data-stu-id="5aa8d-121">First</span></span> | <span data-ttu-id="5aa8d-122">El número de paquetes que se devolverán desde el principio de la lista. el valor predeterminado es 20.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="5aa8d-123">Skip</span><span class="sxs-lookup"><span data-stu-id="5aa8d-123">Skip</span></span> | <span data-ttu-id="5aa8d-124">Omite la primera &lt;int&gt; paquetes en la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="5aa8d-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5aa8d-125">IncludePrerelease</span></span> | <span data-ttu-id="5aa8d-126">Incluye paquetes de versión preliminar en los resultados.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="5aa8d-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="5aa8d-127">ExactMatch</span></span> | <span data-ttu-id="5aa8d-128">Especificado para usar &lt;palabras clave&gt; como un identificador del paquete distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="5aa8d-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="5aa8d-129">StartWith</span></span> | <span data-ttu-id="5aa8d-130">Devuelve los paquetes cuyo paquete ID comienza con &lt;palabras clave&gt;.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="5aa8d-131">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5aa8d-132">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="5aa8d-132">Common Parameters</span></span>

<span data-ttu-id="5aa8d-133">`Find-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5aa8d-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5aa8d-134">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5aa8d-134">Examples</span></span>

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
