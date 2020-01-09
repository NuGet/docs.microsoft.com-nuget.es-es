---
title: Referencia de PowerShell Add-BindingRedirect de NuGet
description: Referencia del comando Add-BindingRedirect de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384989"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="137dc-103">Add-BindingRedirect (Consola del Administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="137dc-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="137dc-104">*Solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="137dc-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="137dc-105">Examina todos los ensamblados de la ruta de acceso de salida de un proyecto y agrega redirecciones de enlace al archivo de configuración web o de aplicación cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="137dc-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="137dc-106">Este comando se ejecuta automáticamente al instalar un paquete.</span><span class="sxs-lookup"><span data-stu-id="137dc-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="137dc-107">Para obtener más información sobre las redirecciones de enlace y por qué se usan, consulte [redirección de versiones de ensamblado](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación de .net.</span><span class="sxs-lookup"><span data-stu-id="137dc-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="137dc-108">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="137dc-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="137dc-109">Parameters</span><span class="sxs-lookup"><span data-stu-id="137dc-109">Parameters</span></span>

| <span data-ttu-id="137dc-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="137dc-110">Parameter</span></span> | <span data-ttu-id="137dc-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="137dc-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="137dc-112">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="137dc-112">ProjectName</span></span> | <span data-ttu-id="137dc-113">Desee Proyecto al que se van a agregar redirecciones de enlace.</span><span class="sxs-lookup"><span data-stu-id="137dc-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="137dc-114">El propio modificador-ProjectName es opcional.</span><span class="sxs-lookup"><span data-stu-id="137dc-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="137dc-115">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="137dc-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="137dc-116">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="137dc-116">Common Parameters</span></span>

<span data-ttu-id="137dc-117">`Add-BindingRedirect` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="137dc-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="137dc-118">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="137dc-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```