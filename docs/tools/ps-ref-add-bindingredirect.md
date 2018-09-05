---
title: NuGet BindingRedirect-Agregar referencia de PowerShell
description: Referencia de comandos de PowerShell Add-BindingRedirect en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551662"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="2c093-103">Add-BindingRedirect (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="2c093-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2c093-104">*Solo está disponible en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="2c093-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="2c093-105">Examina todos los ensamblados en la ruta de acceso de salida para un proyecto y agregar redirecciones de enlaces al archivo de configuración de aplicación o web donde sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2c093-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="2c093-106">Este comando se ejecuta automáticamente al instalar un paquete.</span><span class="sxs-lookup"><span data-stu-id="2c093-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="2c093-107">Para obtener más información sobre cómo enlazar redirecciones y por qué se usan, vea [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación. NET.</span><span class="sxs-lookup"><span data-stu-id="2c093-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="2c093-108">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="2c093-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2c093-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="2c093-109">Parameters</span></span>

| <span data-ttu-id="2c093-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2c093-110">Parameter</span></span> | <span data-ttu-id="2c093-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="2c093-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c093-112">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="2c093-112">ProjectName</span></span> | <span data-ttu-id="2c093-113">(Obligatorio) El proyecto que se va a agregar redirecciones de enlace.</span><span class="sxs-lookup"><span data-stu-id="2c093-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="2c093-114">El propio conmutador - nombreproyecto es opcional.</span><span class="sxs-lookup"><span data-stu-id="2c093-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="2c093-115">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="2c093-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2c093-116">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="2c093-116">Common Parameters</span></span>

<span data-ttu-id="2c093-117">`Add-BindingRedirect` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="2c093-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2c093-118">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2c093-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```