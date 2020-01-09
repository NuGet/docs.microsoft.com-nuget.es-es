---
title: Referencia de PowerShell de obtención-proyecto de NuGet
description: Referencia del comando de PowerShell de GetProject en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384625"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Consola del Administrador de paquetes en Visual Studio)

*Solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*

Muestra información sobre el proyecto predeterminado o el especificado. `Get-Project` devuelve específicamente un objeto referente al objeto DTE de Visual Studio (entorno de herramientas de desarrollo) del proyecto.

## <a name="syntax"></a>Sintaxis

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Parámetro | Descripción |
| --- | --- |
| Name | Especifica el proyecto que se va a mostrar, que tiene como valor predeterminado el proyecto predeterminado seleccionado en la consola del administrador de paquetes. El modificador-name es opcional. |
| Todos | Muestra información de todos los proyectos de la solución; el orden de los proyectos no es determinista. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Get-Project` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```