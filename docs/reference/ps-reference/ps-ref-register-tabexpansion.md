---
title: Referencia de PowerShell de Register-TabExpansion de NuGet
description: Referencia de Register-TabExpansion comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6ad0da0e84fc2e31499c06bde013d2a256987d9a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777458"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="d4cc0-103">Register-TabExpansion (consola del administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d4cc0-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d4cc0-104">*Solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="d4cc0-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d4cc0-105">Registra una expansión de pestaña para los parámetros del comando especificado, de modo que cuando se usa la pestaña al escribir un comando, los valores expandidos aparecen como opciones disponibles para el parámetro en cuestión.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="d4cc0-106">Se sobrescriben las expansiones anteriores para el comando.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="d4cc0-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="d4cc0-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d4cc0-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="d4cc0-108">Parameters</span></span>

| <span data-ttu-id="d4cc0-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d4cc0-109">Parameter</span></span> | <span data-ttu-id="d4cc0-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="d4cc0-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4cc0-111">Nombre</span><span class="sxs-lookup"><span data-stu-id="d4cc0-111">Name</span></span> | <span data-ttu-id="d4cc0-112">Desee Comando en el que se van a registrar las expansiones.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="d4cc0-113">El propio modificador-name es opcional.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="d4cc0-114">Definición</span><span class="sxs-lookup"><span data-stu-id="d4cc0-114">Definition</span></span> | <span data-ttu-id="d4cc0-115">Desee Un objeto que describe el argumento en la sintaxis `@{'<parameter>' = {'<value1>', '<value2>', ...}}` donde `<parameter>` es el nombre del parámetro que se va a modificar y cada uno `<value>` proporciona una expansión específica.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="d4cc0-116">Se aceptan comillas simples y dobles.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="d4cc0-117">Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d4cc0-118">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="d4cc0-118">Common Parameters</span></span>

<span data-ttu-id="d4cc0-119">`Register-TabExpansion` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-119">`Register-TabExpansion` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d4cc0-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d4cc0-120">Examples</span></span>

<span data-ttu-id="d4cc0-121">Considere una solución que contenga tres nombres de proyecto EventManager, Utilities y SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="d4cc0-122">Con frecuencia, el desarrollador usa el `Update-Package` comando en momentos diferentes con cada uno de estos proyectos.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="d4cc0-123">Es conveniente que el `Update-Package` comando proporcione expansiones de finalización automática para el `-ProjectName` argumento, por lo que no es necesario escribir un nombre de proyecto cada vez.</span><span class="sxs-lookup"><span data-stu-id="d4cc0-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="d4cc0-124">El siguiente comando registra los tres nombres de proyecto como una expansión para el `-ProjectName` parámetro:</span><span class="sxs-lookup"><span data-stu-id="d4cc0-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="d4cc0-125">A continuación, el desarrollador puede escribir `Update-Package -ProjectName ` , presionar Tab y ver las expansiones que se ofrecen como opciones de finalización automática:</span><span class="sxs-lookup"><span data-stu-id="d4cc0-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Ejemplo de uso de Register-TabExpansion](media/Register-TabExpansion-Example.png)