---
title: Referencia de PowerShell de NuGet agregar redirección de enlace
description: Referencia de comandos de PowerShell agregar redirección de enlace en la consola de administrador de paquetes de NuGet en Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="048b9-103">Add-BindingRedirect (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="048b9-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="048b9-104">*Disponible solo en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="048b9-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="048b9-105">Examina todos los ensamblados de la ruta de acceso de salida para un proyecto y agrega redirecciones de enlace al archivo de configuración de aplicación o web cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="048b9-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="048b9-106">Este comando se ejecuta automáticamente al instalar un paquete.</span><span class="sxs-lookup"><span data-stu-id="048b9-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="048b9-107">Para obtener más información sobre cómo enlazar redirecciones y por qué se usan, vea [redirigir versiones de ensamblado](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación. NET.</span><span class="sxs-lookup"><span data-stu-id="048b9-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="048b9-108">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="048b9-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="048b9-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="048b9-109">Parameters</span></span>

| <span data-ttu-id="048b9-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="048b9-110">Parameter</span></span> | <span data-ttu-id="048b9-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="048b9-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="048b9-112">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="048b9-112">ProjectName</span></span> | <span data-ttu-id="048b9-113">(Obligatorio) El proyecto que se va a agregar redirecciones de enlace.</span><span class="sxs-lookup"><span data-stu-id="048b9-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="048b9-114">El propio modificador - NombreDeProyecto es opcional.</span><span class="sxs-lookup"><span data-stu-id="048b9-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="048b9-115">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="048b9-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="048b9-116">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="048b9-116">Common Parameters</span></span>

<span data-ttu-id="048b9-117">`Add-BindingRedirect` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="048b9-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="048b9-118">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="048b9-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```