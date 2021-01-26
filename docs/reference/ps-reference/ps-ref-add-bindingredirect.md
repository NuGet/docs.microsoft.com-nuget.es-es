---
title: Referencia de PowerShell de Add-BindingRedirect de NuGet
description: Referencia de Add-BindingRedirect comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777610"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="6a3be-103">Add-BindingRedirect (consola del administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6a3be-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6a3be-104">*Solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="6a3be-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6a3be-105">Examina todos los ensamblados de la ruta de acceso de salida de un proyecto y agrega redirecciones de enlace al archivo de configuración web o de aplicación cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6a3be-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="6a3be-106">Este comando se ejecuta automáticamente al instalar un paquete.</span><span class="sxs-lookup"><span data-stu-id="6a3be-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="6a3be-107">Esto solo se aplica a los escenarios que usan un archivo de packages.config.</span><span class="sxs-lookup"><span data-stu-id="6a3be-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="6a3be-108">Para obtener más información, vea [referencia de archivos de packages.config NuGet](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="6a3be-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="6a3be-109">Para obtener más información sobre las redirecciones de enlace y por qué se usan, consulte [redirección de versiones de ensamblado](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación de .net.</span><span class="sxs-lookup"><span data-stu-id="6a3be-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="6a3be-110">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="6a3be-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6a3be-111">Parámetros</span><span class="sxs-lookup"><span data-stu-id="6a3be-111">Parameters</span></span>

| <span data-ttu-id="6a3be-112">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6a3be-112">Parameter</span></span> | <span data-ttu-id="6a3be-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="6a3be-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6a3be-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="6a3be-114">ProjectName</span></span> | <span data-ttu-id="6a3be-115">Desee Proyecto al que se van a agregar redirecciones de enlace.</span><span class="sxs-lookup"><span data-stu-id="6a3be-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="6a3be-116">El propio modificador-ProjectName es opcional.</span><span class="sxs-lookup"><span data-stu-id="6a3be-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="6a3be-117">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="6a3be-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6a3be-118">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="6a3be-118">Common Parameters</span></span>

<span data-ttu-id="6a3be-119">`Add-BindingRedirect` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6a3be-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6a3be-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6a3be-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```