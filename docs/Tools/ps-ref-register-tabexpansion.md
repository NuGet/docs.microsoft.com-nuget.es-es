---
title: Referencia de PowerShell de NuGet Register-TabExpansion | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia de comandos de PowerShell de Register-TabExpansion en la consola de administrador de paquetes de NuGet en Visual Studio.
keywords: Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, Register-TabExpansion de paquete de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e363b8a7fa7e25d24331eb3e4eb87141e6a3b97
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="a89d0-104">Register-TabExpansion (consola de administrador de paquetes en Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a89d0-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a89d0-105">*Disponible solo en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*</span><span class="sxs-lookup"><span data-stu-id="a89d0-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a89d0-106">Registra una expansión de pestañas para los parámetros del comando especificado, de forma que cuando se usa la ficha al escribir un comando, los valores expandidos aparecen como opciones disponibles para el parámetro en cuestión.</span><span class="sxs-lookup"><span data-stu-id="a89d0-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="a89d0-107">Se sobrescriben las expansiones anteriores para el comando.</span><span class="sxs-lookup"><span data-stu-id="a89d0-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="a89d0-108">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="a89d0-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a89d0-109">Parámetros</span><span class="sxs-lookup"><span data-stu-id="a89d0-109">Parameters</span></span>

| <span data-ttu-id="a89d0-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="a89d0-110">Parameter</span></span> | <span data-ttu-id="a89d0-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="a89d0-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a89d0-112">nombre</span><span class="sxs-lookup"><span data-stu-id="a89d0-112">Name</span></span> | <span data-ttu-id="a89d0-113">(Obligatorio) El comando que se va a registrar las expansiones.</span><span class="sxs-lookup"><span data-stu-id="a89d0-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="a89d0-114">-Nombre propio modificador es opcional.</span><span class="sxs-lookup"><span data-stu-id="a89d0-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="a89d0-115">Definición</span><span class="sxs-lookup"><span data-stu-id="a89d0-115">Definition</span></span> | <span data-ttu-id="a89d0-116">(Obligatorio) Un objeto que describe el argumento en la sintaxis `@{'<parameter>' = {'<value1>', '<value2>', ...}}` donde `<parameter>` es el nombre del parámetro para modificar y cada uno de ellos `<value>` proporciona una expansión específica.</span><span class="sxs-lookup"><span data-stu-id="a89d0-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="a89d0-117">Se aceptan las comillas simples y dobles.</span><span class="sxs-lookup"><span data-stu-id="a89d0-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="a89d0-118">Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.</span><span class="sxs-lookup"><span data-stu-id="a89d0-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a89d0-119">Parámetros comunes</span><span class="sxs-lookup"><span data-stu-id="a89d0-119">Common Parameters</span></span>

<span data-ttu-id="a89d0-120">`Register-TabExpansion` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a89d0-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a89d0-121">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a89d0-121">Examples</span></span>

<span data-ttu-id="a89d0-122">Considere la posibilidad de una solución que contiene los nombres de tres proyectos EventManager, utilidades y SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="a89d0-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="a89d0-123">El programador usa con frecuencia el `Update-Package` comando en momentos diferentes a cada uno de esos proyectos.</span><span class="sxs-lookup"><span data-stu-id="a89d0-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="a89d0-124">Busca conveniente tener la `Update-Package` comandos proporcionan expansiones de finalización automática para el `-ProjectName` argumento, por lo que no necesita escribir un nombre de proyecto cada vez.</span><span class="sxs-lookup"><span data-stu-id="a89d0-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="a89d0-125">El siguiente comando, a continuación, registra los nombres de tres proyectos como una expansión de la `-ProjectName` parámetro:</span><span class="sxs-lookup"><span data-stu-id="a89d0-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="a89d0-126">A continuación, puede escribir el programador `Update-Package -ProjectName `, presione la tecla Tab y vea las expansiones ofrecidas como opciones de finalización automática:</span><span class="sxs-lookup"><span data-stu-id="a89d0-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Ejemplo del uso de registro TabExpansion](media/Register-TabExpansion-Example.png)
