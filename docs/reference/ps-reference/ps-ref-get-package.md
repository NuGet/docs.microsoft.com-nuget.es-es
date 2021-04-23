---
title: Referencia de NuGet Get-Package PowerShell
description: Referencia de Get-Package comando de PowerShell en la consola de Administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901738"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="9eafc-103">Get-Package (Administrador de paquetes console en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9eafc-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9eafc-104">*En este tema se describe el comando dentro de Administrador de paquetes [Console](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para obtener el comando Get-Package de PowerShell genérico, vea la referencia [de PackageManagement de PowerShell.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="9eafc-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="9eafc-105">Recupera la lista de paquetes instalados en el repositorio local, enumera los paquetes disponibles desde un origen de paquete cuando se usan con el modificador -ListAvailable o enumera las actualizaciones disponibles cuando se usan con el modificador -Update.</span><span class="sxs-lookup"><span data-stu-id="9eafc-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="9eafc-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="9eafc-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="9eafc-107">Sin parámetros, `Get-Package` muestra la lista de paquetes instalados en el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9eafc-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="9eafc-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="9eafc-108">Parameters</span></span>

| <span data-ttu-id="9eafc-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="9eafc-109">Parameter</span></span> | <span data-ttu-id="9eafc-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="9eafc-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9eafc-111">Source</span><span class="sxs-lookup"><span data-stu-id="9eafc-111">Source</span></span> | <span data-ttu-id="9eafc-112">Dirección URL o ruta de acceso de carpeta para el paquete .</span><span class="sxs-lookup"><span data-stu-id="9eafc-112">The URL or folder path for the package .</span></span> <span data-ttu-id="9eafc-113">Las rutas de acceso de carpeta local pueden ser absolutas o relativas a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="9eafc-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="9eafc-114">Si se omite, `Get-Package` busca en el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="9eafc-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="9eafc-115">Cuando se usa con -ListAvailable, el valor predeterminado es nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9eafc-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="9eafc-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="9eafc-116">ListAvailable</span></span> | <span data-ttu-id="9eafc-117">Enumera los paquetes disponibles desde un origen de paquete, con el valor predeterminado nuget.org. Muestra un valor predeterminado de 50 paquetes a menos que se especifique -PageSize o -First.</span><span class="sxs-lookup"><span data-stu-id="9eafc-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="9eafc-118">Actualizaciones</span><span class="sxs-lookup"><span data-stu-id="9eafc-118">Updates</span></span> | <span data-ttu-id="9eafc-119">Enumera los paquetes que tienen una actualización disponible desde el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="9eafc-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="9eafc-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="9eafc-120">ProjectName</span></span> | <span data-ttu-id="9eafc-121">Proyecto desde el que se obtienen los paquetes instalados.</span><span class="sxs-lookup"><span data-stu-id="9eafc-121">The project from which to get installed packages.</span></span> <span data-ttu-id="9eafc-122">Si se omite, devuelve los proyectos instalados para toda la solución.</span><span class="sxs-lookup"><span data-stu-id="9eafc-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="9eafc-123">Filtrar</span><span class="sxs-lookup"><span data-stu-id="9eafc-123">Filter</span></span> | <span data-ttu-id="9eafc-124">Cadena de filtro que se usa para restringir la lista de paquetes al aplicarla al identificador, la descripción y las etiquetas del paquete.</span><span class="sxs-lookup"><span data-stu-id="9eafc-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="9eafc-125">First</span><span class="sxs-lookup"><span data-stu-id="9eafc-125">First</span></span> | <span data-ttu-id="9eafc-126">Número de paquetes que se devolverán desde el principio de la lista.</span><span class="sxs-lookup"><span data-stu-id="9eafc-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="9eafc-127">Si no se especifica, el valor predeterminado es 50.</span><span class="sxs-lookup"><span data-stu-id="9eafc-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="9eafc-128">Omitir</span><span class="sxs-lookup"><span data-stu-id="9eafc-128">Skip</span></span> | <span data-ttu-id="9eafc-129">Omite los primeros paquetes &lt; int de la lista &gt; mostrada.</span><span class="sxs-lookup"><span data-stu-id="9eafc-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="9eafc-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="9eafc-130">AllVersions</span></span> | <span data-ttu-id="9eafc-131">Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="9eafc-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="9eafc-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="9eafc-132">IncludePrerelease</span></span> | <span data-ttu-id="9eafc-133">Incluye paquetes de versión preliminar en los resultados.</span><span class="sxs-lookup"><span data-stu-id="9eafc-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="9eafc-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="9eafc-134">PageSize</span></span> | <span data-ttu-id="9eafc-135">*(3.0+)* Cuando se usa con -ListAvailable (obligatorio), el número de paquetes que se enumerarán antes de dar una solicitud para continuar.</span><span class="sxs-lookup"><span data-stu-id="9eafc-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="9eafc-136">Ninguno de estos parámetros acepta caracteres comodín o entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="9eafc-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9eafc-137">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="9eafc-137">Common Parameters</span></span>

<span data-ttu-id="9eafc-138">`Get-Package` admite los siguientes parámetros comunes de [PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9eafc-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9eafc-139">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9eafc-139">Examples</span></span>

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