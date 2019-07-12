---
title: Referencia de PowerShell Get-proyecto de NuGet
description: Referencia de comandos de GetProject PowerShell en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842280"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Consola del Administrador de paquetes en Visual Studio)

*Solo está disponible en el [Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*

Muestra información sobre el valor predeterminado o el proyecto especificado. `Get-Project` en concreto, devuelve un referente al objeto DTE (entorno de herramientas de desarrollo) de Visual Studio para el proyecto.

## <a name="syntax"></a>Sintaxis

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | DESCRIPCIÓN |
| --- | --- |
| NOMBRE | Especifica el proyecto para mostrar, el proyecto predeterminado seleccionado en la consola de administrador de paquetes de forma predeterminada. -Nombre de conmutador es opcional. |
| Todo | Muestra información de todos los proyectos de la solución; el orden de los proyectos no es determinista. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Get-Project` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```