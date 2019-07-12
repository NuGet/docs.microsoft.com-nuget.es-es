---
title: Referencia de PowerShell de NuGet Uninstall-Package
description: Referencia de comandos de PowerShell Uninstall-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842475"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Consola del Administrador de paquetes en Visual Studio)

*Este tema describe el comando dentro de la [Package Manager Console](package-manager-console.md) en Visual Studio en Windows. El comando de PowerShell Uninstall-Package genérico, vea el [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Quita un paquete desde un proyecto, quitar, opcionalmente, sus dependencias. Si otros paquetes dependen de este paquete, el comando fallará a menos que – Force se especifica la opción.

## <a name="syntax"></a>Sintaxis

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si otros paquetes dependen de este paquete, el comando fallará a menos que – Force se especifica la opción.

## <a name="parameters"></a>Parámetros

| Parámetro | DESCRIPCIÓN |
| --- | --- |
| Id | (Obligatorio) El identificador del paquete para desinstalar. -Identificador propio conmutador es opcional. |
| `Version` | La versión del paquete para desinstalar, la versión actualmente instalada de forma predeterminada. |
| RemoveDependencies | Desinstale el paquete y sus dependencias no usadas. Es decir, si una dependencia tiene otro paquete que depende de él, se omitirá. |
| NombreDelProyecto | El proyecto desde el que se va a desinstalar el paquete, de forma predeterminada el proyecto predeterminado. |
| Force | Fuerza un paquete que se desinstalara, incluso si otros paquetes dependen de él. |
| WhatIf | Muestra lo que sucedería cuando ejecute el comando sin tener que realizar la desinstalación. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Uninstall-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
