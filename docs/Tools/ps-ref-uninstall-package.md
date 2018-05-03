---
title: Referencia de PowerShell de NuGet Uninstall-Package
description: Referencia de comandos de PowerShell de paquete de desinstalación en la consola de administrador de paquetes de NuGet en Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (consola de administrador de paquetes en Visual Studio)

*Este tema describe el comando dentro de la [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows. Para el comando de PowerShell Uninstall-Package genérico, vea la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Quita un paquete desde un proyecto, si lo desea quitar sus dependencias. Si otros paquetes dependen de este paquete, el comando fallará a menos que la – Force se especifica la opción.

## <a name="syntax"></a>Sintaxis

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si otros paquetes dependen de este paquete, el comando fallará a menos que la – Force se especifica la opción.

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Id. | (Obligatorio) El identificador del paquete para desinstalar. -Identificador propio modificador es opcional. |
| Versión | La versión del paquete para desinstalar, la versión instalada actualmente de forma predeterminada. |
| RemoveDependencies | Desinstale el paquete y sus dependencias no usadas. Es decir, si una dependencia tiene otro paquete que depende de él, se omitirá. |
| NombreDelProyecto | El proyecto desde el que se va a desinstalar el paquete, el valor predeterminado para el proyecto predeterminado. |
| Force | Fuerza un paquete que se debe desinstalar, incluso si otros paquetes dependen de él. |
| WhatIf | Muestra qué ocurre cuando se ejecuta el comando sin realmente realizar la desinstalación. |

Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Uninstall-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
