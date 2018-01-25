---
title: "Referencia de PowerShell de NuGet agregar redirección de enlace | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referencia de comandos de PowerShell agregar redirección de enlace en la consola de administrador de paquetes de NuGet en Visual Studio."
keywords: "Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, agregar redirección de enlace de paquete de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b755970402f29a72b9a10f1a94e4a799e9cb71cf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="7ce0e-104">Agregar redirección de enlace (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7ce0e-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7ce0e-105">*Disponible solo en el [consola del Administrador de paquetes de NuGet](Package-Manager-Console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="7ce0e-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7ce0e-106">Examina todos los ensamblados de la ruta de acceso de salida para un proyecto y agrega redirecciones de enlace al archivo de configuración de aplicación o web cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7ce0e-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="7ce0e-107">Este comando se ejecuta automáticamente al instalar un paquete.</span><span class="sxs-lookup"><span data-stu-id="7ce0e-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="7ce0e-108">Para obtener más información sobre cómo enlazar redirecciones y por qué se usan, vea [redirigir versiones de ensamblado](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación. NET.</span><span class="sxs-lookup"><span data-stu-id="7ce0e-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="7ce0e-109">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="7ce0e-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7ce0e-110">Parámetros</span><span class="sxs-lookup"><span data-stu-id="7ce0e-110">Parameters</span></span>

| <span data-ttu-id="7ce0e-111">Parámetro</span><span class="sxs-lookup"><span data-stu-id="7ce0e-111">Parameter</span></span> | <span data-ttu-id="7ce0e-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="7ce0e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7ce0e-113">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="7ce0e-113">ProjectName</span></span> | <span data-ttu-id="7ce0e-114">(Obligatorio) El proyecto que se va a agregar redirecciones de enlace.</span><span class="sxs-lookup"><span data-stu-id="7ce0e-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="7ce0e-115">El propio modificador - NombreDeProyecto es opcional.</span><span class="sxs-lookup"><span data-stu-id="7ce0e-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="7ce0e-116">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="7ce0e-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7ce0e-117">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="7ce0e-117">Common Parameters</span></span>

<span data-ttu-id="7ce0e-118">`Add-BindingRedirect`admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7ce0e-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7ce0e-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7ce0e-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```