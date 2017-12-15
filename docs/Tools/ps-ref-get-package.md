---
title: Referencia de PowerShell Get-paquete de NuGet | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 42476008-64b3-480e-a966-98b2fa38b681
description: Referencia de comandos de PowerShell Get-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
keywords: Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, Get-Package de paquete de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3f93ab82e9fb769ee20070aa39ba8e3e05953839
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4e921-104">Get-Package (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4e921-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4e921-105">*Este tema describe el comando dentro de la [NuGet Package Manager Console](Package-Manager-Console.md) en Visual Studio en Windows. Para el comando de PowerShell Get-Package genérico, vea la [referencia de PowerShell PackageManagement](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="4e921-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="4e921-106">Recupera la lista de paquetes instalados en el repositorio local, enumera los paquetes disponibles en un origen del paquete cuando se usa con el modificador - ListAvailable o listas de actualizaciones disponibles cuando se usa con-conmutador de actualización.</span><span class="sxs-lookup"><span data-stu-id="4e921-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="4e921-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="4e921-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="4e921-108">Sin parámetros, `Get-Package` muestra la lista de paquetes instalados en el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="4e921-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="4e921-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="4e921-109">Parameters</span></span>

| <span data-ttu-id="4e921-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="4e921-110">Parameter</span></span> | <span data-ttu-id="4e921-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="4e921-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e921-112">Origen</span><span class="sxs-lookup"><span data-stu-id="4e921-112">Source</span></span> | <span data-ttu-id="4e921-113">La ruta de acceso URL o una carpeta para el paquete.</span><span class="sxs-lookup"><span data-stu-id="4e921-113">The URL or folder path for the package .</span></span> <span data-ttu-id="4e921-114">Las rutas de acceso de la carpeta local pueden ser absoluta o relativa a la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="4e921-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="4e921-115">Si se omite, `Get-Package` busca en el origen del paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="4e921-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="4e921-116">Cuando se usa con - ListAvailable, el valor predeterminado es nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4e921-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="4e921-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="4e921-117">ListAvailable</span></span> | <span data-ttu-id="4e921-118">Enumera los paquetes disponibles en un origen del paquete, nuget.org de forma predeterminada. Muestra el valor predeterminado es 50 paquetes a menos que se especifique PageSize - o - primero.</span><span class="sxs-lookup"><span data-stu-id="4e921-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="4e921-119">Actualizaciones</span><span class="sxs-lookup"><span data-stu-id="4e921-119">Updates</span></span> | <span data-ttu-id="4e921-120">Enumera los paquetes que tienen una actualización disponible en el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="4e921-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="4e921-121">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="4e921-121">ProjectName</span></span> | <span data-ttu-id="4e921-122">El proyecto desde el que se obtendrán los paquetes instalados.</span><span class="sxs-lookup"><span data-stu-id="4e921-122">The project from which to get installed packages.</span></span> <span data-ttu-id="4e921-123">Si se omite, devuelve instaladas proyectos para toda la solución.</span><span class="sxs-lookup"><span data-stu-id="4e921-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="4e921-124">Filtro</span><span class="sxs-lookup"><span data-stu-id="4e921-124">Filter</span></span> | <span data-ttu-id="4e921-125">Una cadena de filtro que se usa para reducir la lista de paquetes mediante la aplicación para el Id. de paquete, la descripción y etiquetas.</span><span class="sxs-lookup"><span data-stu-id="4e921-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="4e921-126">First</span><span class="sxs-lookup"><span data-stu-id="4e921-126">First</span></span> | <span data-ttu-id="4e921-127">El número de paquetes que se va a devolver desde el principio de la lista.</span><span class="sxs-lookup"><span data-stu-id="4e921-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="4e921-128">Si no se especifica, valor predeterminado es 50.</span><span class="sxs-lookup"><span data-stu-id="4e921-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="4e921-129">Skip</span><span class="sxs-lookup"><span data-stu-id="4e921-129">Skip</span></span> | <span data-ttu-id="4e921-130">Omite la primera &lt;int&gt; paquetes en la lista mostrada.</span><span class="sxs-lookup"><span data-stu-id="4e921-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="4e921-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="4e921-131">AllVersions</span></span> | <span data-ttu-id="4e921-132">Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="4e921-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="4e921-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="4e921-133">IncludePrerelease</span></span> | <span data-ttu-id="4e921-134">Incluye paquetes de versión preliminar en los resultados.</span><span class="sxs-lookup"><span data-stu-id="4e921-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="4e921-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="4e921-135">PageSize</span></span> | <span data-ttu-id="4e921-136">*(3.0 +)*  Cuando se usa con - ListAvailable (obligatorio), el número de paquetes para mostrar antes de entregar un mensaje para continuar.</span><span class="sxs-lookup"><span data-stu-id="4e921-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="4e921-137">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="4e921-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4e921-138">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="4e921-138">Common Parameters</span></span>

<span data-ttu-id="4e921-139">`Get-Package`admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4e921-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4e921-140">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="4e921-140">Examples</span></span>

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

