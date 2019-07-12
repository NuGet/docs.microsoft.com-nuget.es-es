---
title: Referencia de PowerShell Register-TabExpansion de NuGet
description: Referencia de comandos de PowerShell Register-TabExpansion en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842481"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="6b66e-103">Register-TabExpansion (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6b66e-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6b66e-104">*Solo está disponible en el [Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="6b66e-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6b66e-105">Registra una expansión de pestañas para los parámetros del comando especificado, de modo que cuando se usa la pestaña al escribir un comando, los valores expandidos aparecen como opciones disponibles para el parámetro en cuestión.</span><span class="sxs-lookup"><span data-stu-id="6b66e-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="6b66e-106">Se sobrescriben cualquier expansiones del comando anteriores.</span><span class="sxs-lookup"><span data-stu-id="6b66e-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="6b66e-107">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="6b66e-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6b66e-108">Parámetros</span><span class="sxs-lookup"><span data-stu-id="6b66e-108">Parameters</span></span>

| <span data-ttu-id="6b66e-109">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6b66e-109">Parameter</span></span> | <span data-ttu-id="6b66e-110">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="6b66e-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b66e-111">NOMBRE</span><span class="sxs-lookup"><span data-stu-id="6b66e-111">Name</span></span> | <span data-ttu-id="6b66e-112">(Obligatorio) El comando que se va a registrar las expansiones.</span><span class="sxs-lookup"><span data-stu-id="6b66e-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="6b66e-113">-Nombre propio conmutador es opcional.</span><span class="sxs-lookup"><span data-stu-id="6b66e-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="6b66e-114">Definición</span><span class="sxs-lookup"><span data-stu-id="6b66e-114">Definition</span></span> | <span data-ttu-id="6b66e-115">(Obligatorio) Un objeto que describe el argumento en la sintaxis `@{'<parameter>' = {'<value1>', '<value2>', ...}}` donde `<parameter>` es el nombre del parámetro para modificar y cada `<value>` proporciona una expansión específica.</span><span class="sxs-lookup"><span data-stu-id="6b66e-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="6b66e-116">Se aceptan las comillas simples y dobles.</span><span class="sxs-lookup"><span data-stu-id="6b66e-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="6b66e-117">Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.</span><span class="sxs-lookup"><span data-stu-id="6b66e-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6b66e-118">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="6b66e-118">Common Parameters</span></span>

<span data-ttu-id="6b66e-119">`Register-TabExpansion` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6b66e-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6b66e-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6b66e-120">Examples</span></span>

<span data-ttu-id="6b66e-121">Considere la posibilidad de una solución que contiene tres nombres de los proyectos EventManager, utilidades y SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="6b66e-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="6b66e-122">El programador usa con frecuencia el `Update-Package` comando en momentos diferentes con cada uno de esos proyectos.</span><span class="sxs-lookup"><span data-stu-id="6b66e-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="6b66e-123">Busca conveniente tener el `Update-Package` comandos proporcionan las expansiones de finalización automática para el `-ProjectName` argumento, así que no necesita escribir un nombre de proyecto cada vez.</span><span class="sxs-lookup"><span data-stu-id="6b66e-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="6b66e-124">El siguiente comando y, a continuación, registra esos nombres de tres proyectos como una expansión para el `-ProjectName` parámetro:</span><span class="sxs-lookup"><span data-stu-id="6b66e-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="6b66e-125">A continuación, puede escribir el desarrollador `Update-Package -ProjectName `, presione la tecla Tab y vea las expansiones ofrecidas como opciones de Autocompletar:</span><span class="sxs-lookup"><span data-stu-id="6b66e-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Ejemplo del uso de Register-TabExpansion](media/Register-TabExpansion-Example.png)
