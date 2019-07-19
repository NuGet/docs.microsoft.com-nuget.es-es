---
title: 'Desinstalación de NuGet: referencia de PowerShell de paquetes'
description: Referencia para el comando de PowerShell Uninstall-Package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327282"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Consola del Administrador de paquetes en Visual Studio)

*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando Generic PowerShell Uninstall-package, consulte la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Quita un paquete de un proyecto y, opcionalmente, quita sus dependencias. Si otros paquetes dependen de este paquete, el comando producirá un error a menos que se especifique la opción – Force.

## <a name="syntax"></a>Sintaxis

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si otros paquetes dependen de este paquete, el comando producirá un error a menos que se especifique la opción – Force.

## <a name="parameters"></a>Parámetros

| Parámetro | DESCRIPCIÓN |
| --- | --- |
| Id | Desee Identificador del paquete que se va a desinstalar. El propio modificador-ID es opcional. |
| `Version` | Versión del paquete que se va a desinstalar, que tiene como valor predeterminado la versión instalada actualmente. |
| RemoveDependencies | Desinstale el paquete y sus dependencias no usadas. Es decir, si alguna dependencia tiene otro paquete que depende de ella, se omite. |
| NombreDelProyecto | Proyecto desde el que se va a desinstalar el paquete. el valor predeterminado es el proyecto predeterminado. |
| Aplica | Fuerza la desinstalación de un paquete, aunque otros paquetes dependan de él. |
| WhatIf | Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la desinstalación. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Uninstall-Package`admite los siguientes [parámetros de PowerShell comunes](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
