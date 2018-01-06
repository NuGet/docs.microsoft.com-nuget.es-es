---
title: Referencia de PowerShell de NuGet Uninstall-Package | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Referencia de comandos de PowerShell de paquete de desinstalación en la consola de administrador de paquetes de NuGet en Visual Studio."
keywords: "Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, paquete de desinstalación del paquete de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0899198a354a56615a48a1f7f428674a205f386b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="172ac-104">Uninstall-Package (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="172ac-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="172ac-105">*Este tema describe el comando dentro de la [NuGet Package Manager Console](Package-Manager-Console.md) en Visual Studio en Windows. Para el comando de PowerShell Uninstall-Package genérico, vea la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="172ac-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="172ac-106">Quita un paquete desde un proyecto, si lo desea quitar sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="172ac-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="172ac-107">Si otros paquetes dependen de este paquete, el comando fallará a menos que la – Force se especifica la opción.</span><span class="sxs-lookup"><span data-stu-id="172ac-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="172ac-108">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="172ac-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="172ac-109">Si otros paquetes dependen de este paquete, el comando fallará a menos que la – Force se especifica la opción.</span><span class="sxs-lookup"><span data-stu-id="172ac-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="172ac-110">Parámetros</span><span class="sxs-lookup"><span data-stu-id="172ac-110">Parameters</span></span>

| <span data-ttu-id="172ac-111">Parámetro</span><span class="sxs-lookup"><span data-stu-id="172ac-111">Parameter</span></span> | <span data-ttu-id="172ac-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="172ac-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="172ac-113">Id.</span><span class="sxs-lookup"><span data-stu-id="172ac-113">Id</span></span> | <span data-ttu-id="172ac-114">(Obligatorio) El identificador del paquete para desinstalar.</span><span class="sxs-lookup"><span data-stu-id="172ac-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="172ac-115">-Identificador propio modificador es opcional.</span><span class="sxs-lookup"><span data-stu-id="172ac-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="172ac-116">Versión</span><span class="sxs-lookup"><span data-stu-id="172ac-116">Version</span></span> | <span data-ttu-id="172ac-117">La versión del paquete para desinstalar, la versión instalada actualmente de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="172ac-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="172ac-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="172ac-118">RemoveDependencies</span></span> | <span data-ttu-id="172ac-119">Desinstale el paquete y sus dependencias no usadas.</span><span class="sxs-lookup"><span data-stu-id="172ac-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="172ac-120">Es decir, si una dependencia tiene otro paquete que depende de él, se omitirá.</span><span class="sxs-lookup"><span data-stu-id="172ac-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="172ac-121">NombreDelProyecto</span><span class="sxs-lookup"><span data-stu-id="172ac-121">ProjectName</span></span> | <span data-ttu-id="172ac-122">El proyecto desde el que se va a desinstalar el paquete, el valor predeterminado para el proyecto predeterminado.</span><span class="sxs-lookup"><span data-stu-id="172ac-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="172ac-123">Force</span><span class="sxs-lookup"><span data-stu-id="172ac-123">Force</span></span> | <span data-ttu-id="172ac-124">Fuerza un paquete que se debe desinstalar, incluso si otros paquetes dependen de él.</span><span class="sxs-lookup"><span data-stu-id="172ac-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="172ac-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="172ac-125">WhatIf</span></span> | <span data-ttu-id="172ac-126">Muestra qué ocurre cuando se ejecuta el comando sin realmente realizar la desinstalación.</span><span class="sxs-lookup"><span data-stu-id="172ac-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="172ac-127">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="172ac-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="172ac-128">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="172ac-128">Common Parameters</span></span>

<span data-ttu-id="172ac-129">`Uninstall-Package`admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="172ac-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="172ac-130">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="172ac-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
