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
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (consola de administrador de paquetes en Visual Studio)

*Este tema describe el comando dentro de la [NuGet Package Manager Console](Package-Manager-Console.md) en Visual Studio en Windows. Para el comando de PowerShell Uninstall-Package genérico, vea la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

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

`Uninstall-Package`admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
