---
title: Referencia de NuGet Uninstall-Package PowerShell
description: Referencia de Uninstall-Package comando de PowerShell en la consola de Administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901790"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Administrador de paquetes consola en Visual Studio)

*En este tema se describe el comando dentro de [Administrador de paquetes Console](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para obtener el comando genérico de Uninstall-Package PowerShell, consulte la referencia [de PackageManagement de PowerShell.](/powershell/module/packagemanagement)*

Quita un paquete de un proyecto y, opcionalmente, quita sus dependencias. Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.

## <a name="syntax"></a>Sintaxis

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si existen otros paquetes que dependen de este paquete, el comando fallará a menos que se especifique la opción –Force.

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Identificador | (Obligatorio) Identificador del paquete que se desinstalará. El propio modificador -Id es opcional. |
| Versión | La versión del paquete que se desinstalará, con el valor predeterminado de la versión instalada actualmente. |
| RemoveDependencies | Desinstale el paquete y sus dependencias no utilizadas. Es decir, si alguna dependencia tiene otro paquete que depende de él, se omite. |
| ProjectName | Proyecto del que se va a desinstalar el paquete, cuyo valor predeterminado es el proyecto predeterminado. |
| Force | Fuerza la desinstalación de un paquete, incluso si otros paquetes dependen de él. |
| WhatIf | Muestra lo que sucedería al ejecutar el comando sin realizar realmente la desinstalación. |

Ninguno de estos parámetros acepta caracteres comodín o entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Uninstall-Package` admite los siguientes parámetros comunes de [PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```