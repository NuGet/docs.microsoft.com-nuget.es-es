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
ms.openlocfilehash: 41f27d7a1b6b363a562f26590b220d9e11e944f1
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="3ca3a-104">Agregar redirección de enlace (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3ca3a-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3ca3a-105">*Disponible solo en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="3ca3a-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3ca3a-106">Examina todos los ensamblados de la ruta de acceso de salida para un proyecto y agrega redirecciones de enlace al archivo de configuración de aplicación o web cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3ca3a-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="3ca3a-107">Este comando se ejecuta automáticamente al instalar un paquete.</span><span class="sxs-lookup"><span data-stu-id="3ca3a-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="3ca3a-108">Para obtener más información sobre cómo enlazar redirecciones y por qué se usan, vea [redirigir versiones de ensamblado](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación. NET.</span><span class="sxs-lookup"><span data-stu-id="3ca3a-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="3ca3a-109">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3ca3a-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3ca3a-110">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3ca3a-110">Parameters</span></span>

| <span data-ttu-id="3ca3a-111">Parámetro</span><span class="sxs-lookup"><span data-stu-id="3ca3a-111">Parameter</span></span> | <span data-ttu-id="3ca3a-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="3ca3a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3ca3a-113">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="3ca3a-113">ProjectName</span></span> | <span data-ttu-id="3ca3a-114">(Obligatorio) El proyecto que se va a agregar redirecciones de enlace.</span><span class="sxs-lookup"><span data-stu-id="3ca3a-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="3ca3a-115">El propio modificador - NombreDeProyecto es opcional.</span><span class="sxs-lookup"><span data-stu-id="3ca3a-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="3ca3a-116">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="3ca3a-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3ca3a-117">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="3ca3a-117">Common Parameters</span></span>

<span data-ttu-id="3ca3a-118">`Add-BindingRedirect` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3ca3a-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3ca3a-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="3ca3a-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```