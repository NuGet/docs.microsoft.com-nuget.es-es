---
title: Referencia de PowerShell para obtener paquetes de NuGet
description: Referencia del comando de PowerShell Get-Package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 431e5f292f069ad5eb0c9f7f511d6b06810c8760
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327352"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="444b4-103">Get-Package (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="444b4-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="444b4-104">*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando genérico Get-Package de PowerShell, consulte la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="444b4-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="444b4-105">Recupera la lista de paquetes instalados en el repositorio local, enumera los paquetes disponibles en un origen del paquete cuando se usa con el modificador-ListAvailable o enumera las actualizaciones disponibles cuando se usa con el modificador-Update.</span><span class="sxs-lookup"><span data-stu-id="444b4-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="444b4-106">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="444b4-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="444b4-107">Sin parámetros, `Get-Package` muestra la lista de paquetes instalados en el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="444b4-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="444b4-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="444b4-108">Parameters</span></span>

| <span data-ttu-id="444b4-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="444b4-109">Parameter</span></span> | <span data-ttu-id="444b4-110">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="444b4-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="444b4-111">source</span><span class="sxs-lookup"><span data-stu-id="444b4-111">Source</span></span> | <span data-ttu-id="444b4-112">La dirección URL o la ruta de acceso de la carpeta para el paquete.</span><span class="sxs-lookup"><span data-stu-id="444b4-112">The URL or folder path for the package .</span></span> <span data-ttu-id="444b4-113">Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="444b4-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="444b4-114">Si se omite `Get-Package` , busca el origen del paquete seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="444b4-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="444b4-115">Cuando se usa con-ListAvailable, el valor predeterminado es nuget.org.</span><span class="sxs-lookup"><span data-stu-id="444b4-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="444b4-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="444b4-116">ListAvailable</span></span> | <span data-ttu-id="444b4-117">Enumera los paquetes disponibles en el origen de un paquete, con el valor predeterminado nuget.org. Muestra un valor predeterminado de 50 paquetes, a menos que se especifiquen-PageSize y/o-First.</span><span class="sxs-lookup"><span data-stu-id="444b4-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="444b4-118">Actualizaciones</span><span class="sxs-lookup"><span data-stu-id="444b4-118">Updates</span></span> | <span data-ttu-id="444b4-119">Enumera los paquetes que tienen una actualización disponible desde el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="444b4-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="444b4-120">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="444b4-120">ProjectName</span></span> | <span data-ttu-id="444b4-121">Proyecto desde el que se van a obtener los paquetes instalados.</span><span class="sxs-lookup"><span data-stu-id="444b4-121">The project from which to get installed packages.</span></span> <span data-ttu-id="444b4-122">Si se omite, devuelve los proyectos instalados para toda la solución.</span><span class="sxs-lookup"><span data-stu-id="444b4-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="444b4-123">Filtro</span><span class="sxs-lookup"><span data-stu-id="444b4-123">Filter</span></span> | <span data-ttu-id="444b4-124">Cadena de filtro que se usa para restringir la lista de paquetes aplicándolos al identificador, la descripción y las etiquetas del paquete.</span><span class="sxs-lookup"><span data-stu-id="444b4-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="444b4-125">Primero</span><span class="sxs-lookup"><span data-stu-id="444b4-125">First</span></span> | <span data-ttu-id="444b4-126">Número de paquetes que se van a devolver desde el principio de la lista.</span><span class="sxs-lookup"><span data-stu-id="444b4-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="444b4-127">Si no se especifica, el valor predeterminado es 50.</span><span class="sxs-lookup"><span data-stu-id="444b4-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="444b4-128">Skip</span><span class="sxs-lookup"><span data-stu-id="444b4-128">Skip</span></span> | <span data-ttu-id="444b4-129">Omite los primeros &lt;paquetes int&gt; de la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="444b4-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="444b4-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="444b4-130">AllVersions</span></span> | <span data-ttu-id="444b4-131">Muestra todas las versiones disponibles de cada paquete en lugar de la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="444b4-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="444b4-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="444b4-132">IncludePrerelease</span></span> | <span data-ttu-id="444b4-133">Incluye paquetes de versiones preliminares en los resultados.</span><span class="sxs-lookup"><span data-stu-id="444b4-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="444b4-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="444b4-134">PageSize</span></span> | <span data-ttu-id="444b4-135">*(3.0 +)* Cuando se usa con-ListAvailable (obligatorio), el número de paquetes que se deben enumerar antes de dar un mensaje para continuar.</span><span class="sxs-lookup"><span data-stu-id="444b4-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="444b4-136">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="444b4-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="444b4-137">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="444b4-137">Common Parameters</span></span>

<span data-ttu-id="444b4-138">`Get-Package`admite los siguientes [parámetros de PowerShell comunes](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="444b4-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="444b4-139">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="444b4-139">Examples</span></span>

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
