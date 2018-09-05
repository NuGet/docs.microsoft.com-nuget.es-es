---
title: Referencia de PowerShell Get-paquete de NuGet
description: Referencia de comandos de PowerShell Get-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a28b29614dfe5abdeb24438b3451d96634a120db
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551447"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ced54-103">Get-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ced54-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ced54-104">*Este tema describe el comando dentro de la [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows. El comando de PowerShell Get-Package genérico, vea el [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="ced54-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="ced54-105">Recupera la lista de los paquetes instalados en el repositorio local, se enumeran los paquetes disponibles desde un origen del paquete cuando se usa con el modificador - ListAvailable o listas de actualizaciones disponibles cuando se usa con-conmutador de actualización.</span><span class="sxs-lookup"><span data-stu-id="ced54-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="ced54-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="ced54-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="ced54-107">Sin parámetros, `Get-Package` muestra la lista de los paquetes instalados en el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ced54-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="ced54-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="ced54-108">Parameters</span></span>

| <span data-ttu-id="ced54-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ced54-109">Parameter</span></span> | <span data-ttu-id="ced54-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="ced54-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ced54-111">Origen</span><span class="sxs-lookup"><span data-stu-id="ced54-111">Source</span></span> | <span data-ttu-id="ced54-112">La ruta de acceso URL o carpeta para el paquete.</span><span class="sxs-lookup"><span data-stu-id="ced54-112">The URL or folder path for the package .</span></span> <span data-ttu-id="ced54-113">Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="ced54-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="ced54-114">Si se omite, `Get-Package` busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="ced54-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="ced54-115">Cuando se usa con - ListAvailable, valor predeterminado es en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ced54-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="ced54-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="ced54-116">ListAvailable</span></span> | <span data-ttu-id="ced54-117">Enumera los paquetes disponibles desde un origen del paquete, de forma predeterminada en nuget.org. Muestra el valor predeterminado es 50 paquetes a menos que se especifica PageSize - o - primero.</span><span class="sxs-lookup"><span data-stu-id="ced54-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="ced54-118">Actualizaciones</span><span class="sxs-lookup"><span data-stu-id="ced54-118">Updates</span></span> | <span data-ttu-id="ced54-119">Enumera los paquetes que tienen una actualización disponible desde el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="ced54-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="ced54-120">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="ced54-120">ProjectName</span></span> | <span data-ttu-id="ced54-121">El proyecto desde el que se va a obtener los paquetes instalados.</span><span class="sxs-lookup"><span data-stu-id="ced54-121">The project from which to get installed packages.</span></span> <span data-ttu-id="ced54-122">Si se omite, devuelve instala los proyectos de toda la solución.</span><span class="sxs-lookup"><span data-stu-id="ced54-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="ced54-123">Filtro</span><span class="sxs-lookup"><span data-stu-id="ced54-123">Filter</span></span> | <span data-ttu-id="ced54-124">Una cadena de filtro utilizada para restringir la lista de paquetes aplicando el Id. de paquete, descripción y etiquetas.</span><span class="sxs-lookup"><span data-stu-id="ced54-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="ced54-125">First</span><span class="sxs-lookup"><span data-stu-id="ced54-125">First</span></span> | <span data-ttu-id="ced54-126">El número de paquetes que se devolverán desde el principio de la lista.</span><span class="sxs-lookup"><span data-stu-id="ced54-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="ced54-127">Si no se especifica, valor predeterminado es 50.</span><span class="sxs-lookup"><span data-stu-id="ced54-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="ced54-128">Skip</span><span class="sxs-lookup"><span data-stu-id="ced54-128">Skip</span></span> | <span data-ttu-id="ced54-129">Omite la primera &lt;int&gt; paquetes en la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="ced54-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="ced54-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="ced54-130">AllVersions</span></span> | <span data-ttu-id="ced54-131">Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="ced54-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="ced54-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="ced54-132">IncludePrerelease</span></span> | <span data-ttu-id="ced54-133">Incluye paquetes de versión preliminar en los resultados.</span><span class="sxs-lookup"><span data-stu-id="ced54-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="ced54-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="ced54-134">PageSize</span></span> | <span data-ttu-id="ced54-135">*(3.0 +)*  Cuando se usa con - ListAvailable (obligatorio), el número de paquetes para mostrar antes de dar un símbolo del sistema para continuar.</span><span class="sxs-lookup"><span data-stu-id="ced54-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="ced54-136">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="ced54-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ced54-137">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="ced54-137">Common Parameters</span></span>

<span data-ttu-id="ced54-138">`Get-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ced54-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ced54-139">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ced54-139">Examples</span></span>

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
