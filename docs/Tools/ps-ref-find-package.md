---
title: Referencia de PowerShell de NuGet Find-Package | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia de comandos de PowerShell de Find-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
keywords: Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, Find-Package de paquete de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 47b8420cc49d0a76709cf3268af69fcff310d165
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="bc896-104">Find-Package (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="bc896-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="bc896-105">*Versión 3.0 +; Este tema describe el comando dentro de la [NuGet Package Manager Console](Package-Manager-Console.md) en Visual Studio en Windows. Para el comando de PowerShell Find-Package genérico, vea la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="bc896-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="bc896-106">Obtiene el conjunto de paquetes remotos con especificado Id. o palabras clave del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="bc896-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="bc896-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="bc896-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="bc896-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="bc896-108">Parameters</span></span>

| <span data-ttu-id="bc896-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="bc896-109">Parameter</span></span> | <span data-ttu-id="bc896-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="bc896-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bc896-111">Id. de &lt;palabras clave&gt;</span><span class="sxs-lookup"><span data-stu-id="bc896-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="bc896-112">(Obligatorio) Palabras clave que se usará al buscar el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="bc896-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="bc896-113">Utilice - ExactMatch para devolver solo los paquetes cuyo Id. de paquete coincide con las palabras clave.</span><span class="sxs-lookup"><span data-stu-id="bc896-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="bc896-114">Si no se especifica ninguna palabra clave, `Find-Package` devuelve una lista de los primeros 20 paquetes descargas o el número especificada por - primero.</span><span class="sxs-lookup"><span data-stu-id="bc896-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="bc896-115">Tenga en cuenta que - Id. es opcional y una operación inefectiva.</span><span class="sxs-lookup"><span data-stu-id="bc896-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="bc896-116">Origen</span><span class="sxs-lookup"><span data-stu-id="bc896-116">Source</span></span> | <span data-ttu-id="bc896-117">La ruta de acceso URL o una carpeta de origen del paquete para buscar.</span><span class="sxs-lookup"><span data-stu-id="bc896-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="bc896-118">Las rutas de acceso de la carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="bc896-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="bc896-119">Si se omite, `Find-Package` busca en el origen del paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="bc896-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="bc896-120">AllVersions</span><span class="sxs-lookup"><span data-stu-id="bc896-120">AllVersions</span></span> | <span data-ttu-id="bc896-121">Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="bc896-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="bc896-122">First</span><span class="sxs-lookup"><span data-stu-id="bc896-122">First</span></span> | <span data-ttu-id="bc896-123">El número de paquetes que se va a devolver desde el principio de la lista; el valor predeterminado es 20.</span><span class="sxs-lookup"><span data-stu-id="bc896-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="bc896-124">Skip</span><span class="sxs-lookup"><span data-stu-id="bc896-124">Skip</span></span> | <span data-ttu-id="bc896-125">Omite la primera &lt;int&gt; paquetes en la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="bc896-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="bc896-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="bc896-126">IncludePrerelease</span></span> | <span data-ttu-id="bc896-127">Incluye paquetes de versión preliminar en los resultados.</span><span class="sxs-lookup"><span data-stu-id="bc896-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="bc896-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="bc896-128">ExactMatch</span></span> | <span data-ttu-id="bc896-129">Especificado para usar &lt;palabras clave&gt; como un identificador del paquete distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="bc896-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="bc896-130">StartWith</span><span class="sxs-lookup"><span data-stu-id="bc896-130">StartWith</span></span> | <span data-ttu-id="bc896-131">Devuelve paquetes cuyo paquete identificador comienza con &lt;palabras clave&gt;.</span><span class="sxs-lookup"><span data-stu-id="bc896-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="bc896-132">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="bc896-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="bc896-133">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="bc896-133">Common Parameters</span></span>

<span data-ttu-id="bc896-134">`Find-Package`admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="bc896-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="bc896-135">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="bc896-135">Examples</span></span>

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
