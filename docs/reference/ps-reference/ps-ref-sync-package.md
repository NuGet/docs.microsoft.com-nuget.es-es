---
title: 'Sincronización de NuGet: referencia de PowerShell de paquetes'
description: Referencia del comando PowerShell de paquete de sincronización en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384908"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Consola del Administrador de paquetes en Visual Studio)

*Versión 3.0 +; solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*

Obtiene la versión del paquete instalado del proyecto especificado (o predeterminado) y sincroniza la versión con el resto de proyectos de la solución.

## <a name="syntax"></a>Sintaxis

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Parámetro | Descripción |
| --- | --- |
| Id. | Desee Identificador del paquete que se va a sincronizar. El propio modificador-ID es opcional. |
| IgnoreDependencies | Instale solo este paquete y no sus dependencias. |
| NombreDelProyecto | Proyecto del que se va a sincronizar el paquete, que tiene como valor predeterminado el proyecto predeterminado. |
| Version | Versión del paquete que se va a sincronizar, que tiene como valor predeterminado la versión instalada actualmente. |
| Origen | La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar. Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite, `Sync-Package` busca en el origen del paquete seleccionado actualmente. |
| IncludePrerelease | Incluye paquetes de versión preliminar en la sincronización. |
| FileConflictAction | Acción que se realizará cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto. Los valores posibles son *overwrite, ignore, None, OverwriteAll*y *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:<br/><ul><li>*Más bajo* (valor predeterminado): la versión más baja</li><li>*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</li><li>*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</li><li>*Más alto* (valor predeterminado para Update-package sin parámetros): la versión más alta</li></ul>Puede establecer el valor predeterminado mediante la opción [`dependencyVersion`](../nuget-config-file.md#config-section) del archivo de `Nuget.Config`. |
| WhatIf | Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la sincronización. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Sync-Package` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

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
