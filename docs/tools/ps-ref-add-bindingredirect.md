---
title: Referencia de PowerShell de NuGet agregar redirección de enlace
description: Referencia de comandos de PowerShell agregar redirección de enlace en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817628"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="6e999-103">Add-BindingRedirect (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6e999-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6e999-104">*Disponible solo en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="6e999-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6e999-105">Examina todos los ensamblados de la ruta de acceso de salida para un proyecto y agrega redirecciones de enlace al archivo de configuración de aplicación o web cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6e999-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="6e999-106">Este comando se ejecuta automáticamente al instalar un paquete.</span><span class="sxs-lookup"><span data-stu-id="6e999-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="6e999-107">Para obtener más información sobre cómo enlazar redirecciones y por qué se usan, vea [redirigir versiones de ensamblado](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación. NET.</span><span class="sxs-lookup"><span data-stu-id="6e999-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="6e999-108">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="6e999-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6e999-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="6e999-109">Parameters</span></span>

| <span data-ttu-id="6e999-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6e999-110">Parameter</span></span> | <span data-ttu-id="6e999-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="6e999-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6e999-112">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="6e999-112">ProjectName</span></span> | <span data-ttu-id="6e999-113">(Obligatorio) El proyecto que se va a agregar redirecciones de enlace.</span><span class="sxs-lookup"><span data-stu-id="6e999-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="6e999-114">El propio modificador - NombreDeProyecto es opcional.</span><span class="sxs-lookup"><span data-stu-id="6e999-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="6e999-115">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="6e999-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6e999-116">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="6e999-116">Common Parameters</span></span>

<span data-ttu-id="6e999-117">`Add-BindingRedirect` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6e999-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6e999-118">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6e999-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```