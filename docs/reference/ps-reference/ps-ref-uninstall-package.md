---
title: 'Desinstalación de NuGet: referencia de PowerShell de paquetes'
description: Referencia para el comando de PowerShell Uninstall-Package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384420"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Consola del Administrador de paquetes en Visual Studio)

*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando Generic PowerShell Uninstall-package, consulte la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Quita un paquete de un proyecto y, opcionalmente, quita sus dependencias. Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.

## <a name="syntax"></a>Sintaxis

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.

## <a name="parameters"></a>Parameters

| Parámetro | Descripción |
| --- | --- |
| Id. | Desee Identificador del paquete que se va a desinstalar. El propio modificador-ID es opcional. |
| Version | Versión del paquete que se va a desinstalar, que tiene como valor predeterminado la versión instalada actualmente. |
| RemoveDependencies | Desinstale el paquete y sus dependencias no usadas. Es decir, si alguna dependencia tiene otro paquete que depende de ella, se omite. |
| NombreDelProyecto | Proyecto desde el que se va a desinstalar el paquete. el valor predeterminado es el proyecto predeterminado. |
| Force | Fuerza la desinstalación de un paquete, aunque otros paquetes dependan de él. |
| WhatIf | Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la desinstalación. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Uninstall-Package` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
