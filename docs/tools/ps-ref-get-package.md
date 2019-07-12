---
title: Referencia de PowerShell Get-paquete de NuGet
description: Referencia de comandos de PowerShell Get-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842517"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="34751-103">Get-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="34751-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="34751-104">*Este tema describe el comando dentro de la [Package Manager Console](package-manager-console.md) en Visual Studio en Windows. El comando de PowerShell Get-Package genérico, vea el [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="34751-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="34751-105">Recupera la lista de los paquetes instalados en el repositorio local, se enumeran los paquetes disponibles desde un origen del paquete cuando se usa con el modificador - ListAvailable o listas de actualizaciones disponibles cuando se usa con-conmutador de actualización.</span><span class="sxs-lookup"><span data-stu-id="34751-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="34751-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="34751-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="34751-107">Sin parámetros, `Get-Package` muestra la lista de los paquetes instalados en el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="34751-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="34751-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="34751-108">Parameters</span></span>

| <span data-ttu-id="34751-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="34751-109">Parameter</span></span> | <span data-ttu-id="34751-110">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="34751-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="34751-111">source</span><span class="sxs-lookup"><span data-stu-id="34751-111">Source</span></span> | <span data-ttu-id="34751-112">La ruta de acceso URL o carpeta para el paquete.</span><span class="sxs-lookup"><span data-stu-id="34751-112">The URL or folder path for the package .</span></span> <span data-ttu-id="34751-113">Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="34751-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="34751-114">Si se omite, `Get-Package` busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="34751-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="34751-115">Cuando se usa con - ListAvailable, valor predeterminado es en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="34751-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="34751-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="34751-116">ListAvailable</span></span> | <span data-ttu-id="34751-117">Enumera los paquetes disponibles desde un origen del paquete, de forma predeterminada en nuget.org. Muestra el valor predeterminado es 50 paquetes a menos que se especifica PageSize - o - primero.</span><span class="sxs-lookup"><span data-stu-id="34751-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="34751-118">Actualizaciones</span><span class="sxs-lookup"><span data-stu-id="34751-118">Updates</span></span> | <span data-ttu-id="34751-119">Enumera los paquetes que tienen una actualización disponible desde el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="34751-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="34751-120">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="34751-120">ProjectName</span></span> | <span data-ttu-id="34751-121">El proyecto desde el que se va a obtener los paquetes instalados.</span><span class="sxs-lookup"><span data-stu-id="34751-121">The project from which to get installed packages.</span></span> <span data-ttu-id="34751-122">Si se omite, devuelve instala los proyectos de toda la solución.</span><span class="sxs-lookup"><span data-stu-id="34751-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="34751-123">Filtro</span><span class="sxs-lookup"><span data-stu-id="34751-123">Filter</span></span> | <span data-ttu-id="34751-124">Una cadena de filtro utilizada para restringir la lista de paquetes aplicando el Id. de paquete, descripción y etiquetas.</span><span class="sxs-lookup"><span data-stu-id="34751-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="34751-125">Primero</span><span class="sxs-lookup"><span data-stu-id="34751-125">First</span></span> | <span data-ttu-id="34751-126">El número de paquetes que se devolverán desde el principio de la lista.</span><span class="sxs-lookup"><span data-stu-id="34751-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="34751-127">Si no se especifica, valor predeterminado es 50.</span><span class="sxs-lookup"><span data-stu-id="34751-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="34751-128">Skip</span><span class="sxs-lookup"><span data-stu-id="34751-128">Skip</span></span> | <span data-ttu-id="34751-129">Omite la primera &lt;int&gt; paquetes en la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="34751-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="34751-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="34751-130">AllVersions</span></span> | <span data-ttu-id="34751-131">Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="34751-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="34751-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="34751-132">IncludePrerelease</span></span> | <span data-ttu-id="34751-133">Incluye paquetes de versión preliminar en los resultados.</span><span class="sxs-lookup"><span data-stu-id="34751-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="34751-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="34751-134">PageSize</span></span> | <span data-ttu-id="34751-135">*(3.0 +)*  Cuando se usa con - ListAvailable (obligatorio), el número de paquetes para mostrar antes de dar un símbolo del sistema para continuar.</span><span class="sxs-lookup"><span data-stu-id="34751-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="34751-136">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="34751-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="34751-137">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="34751-137">Common Parameters</span></span>

<span data-ttu-id="34751-138">`Get-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="34751-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="34751-139">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="34751-139">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
