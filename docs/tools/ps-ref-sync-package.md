---
title: Referencia de PowerShell de sincronización-paquete de NuGet
description: Referencia de comandos de PowerShell de sincronización de paquete en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842246"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Consola del Administrador de paquetes en Visual Studio)

*Versión 3.0 o superior; solo está disponible en el [Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*

Obtiene la versión del paquete instalado desde especificado (o predeterminada) del proyecto y sincroniza la versión para el resto de los proyectos de la solución.

## <a name="syntax"></a>Sintaxis

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | DESCRIPCIÓN |
| --- | --- |
| Id | (Obligatorio) El identificador del paquete para sincronizar. -Identificador propio conmutador es opcional. |
| IgnoreDependencies | Instalar solo este paquete y no a sus dependencias. |
| NombreDelProyecto | El proyecto para sincronizar el paquete, de forma predeterminada el proyecto predeterminado. |
| `Version` | La versión del paquete para la sincronización, la versión actualmente instalada de forma predeterminada. |
| source | La ruta de acceso URL o carpeta para buscar el origen del paquete. Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual. Si se omite, `Sync-Package` busca el origen del paquete seleccionado actualmente. |
| IncludePrerelease | Incluye paquetes de versión preliminar de la sincronización. |
| FileConflictAction | La acción que se realizará cuando se le pida sobrescribir u omitir los archivos existentes que se hace referencia el proyecto. Los valores posibles son *sobrescribir, omitir, None, OverwriteAll*, y *(3.0 y versiones posteriores)* *IgnoreAll*. |
| DependencyVersion | La versión de los paquetes de dependencia para usar, que puede ser uno de los siguientes:<br/><ul><li>*Menor* (valor predeterminado): la versión más antigua</li><li>*HighestPatch*: la versión con la revisión menor principal, secundaria menor, más alta</li><li>*HighestMinor*: la versión con el menor principales, revisiones secundarias y de mayor más alto</li><li>*Mayor* (predeterminado para el paquete de actualización sin parámetros): la versión más alta</li></ul>Puede establecer el valor predeterminado con el [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) en el `Nuget.Config` archivo. |
| WhatIf | Muestra lo que sucedería cuando ejecute el comando sin tener que realizar la sincronización. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Sync-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
