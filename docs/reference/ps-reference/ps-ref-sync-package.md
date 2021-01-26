---
title: Referencia de PowerShell de Sync-Package de NuGet
description: Referencia de Sync-Package comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 4261b0a20a4fd4183f7b08096c3477e6f9d0a02d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777404"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (consola del administrador de paquetes en Visual Studio)

*Versión 3.0 +; solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*

Obtiene la versión del paquete instalado del proyecto especificado (o predeterminado) y sincroniza la versión con el resto de proyectos de la solución.

## <a name="syntax"></a>Sintaxis

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Identificador | Desee Identificador del paquete que se va a sincronizar. El propio modificador-ID es opcional. |
| IgnoreDependencies | Instale solo este paquete y no sus dependencias. |
| ProjectName | Proyecto del que se va a sincronizar el paquete, que tiene como valor predeterminado el proyecto predeterminado. |
| Versión | Versión del paquete que se va a sincronizar, que tiene como valor predeterminado la versión instalada actualmente. |
| Source | La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar. Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite, `Sync-Package` busca el origen del paquete seleccionado actualmente. |
| IncludePrerelease | Incluye paquetes de versión preliminar en la sincronización. |
| FileConflictAction | Acción que se realizará cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto. Los valores posibles son *overwrite, ignore, None, OverwriteAll* y *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:<br/><ul><li>*Más bajo* (valor predeterminado): la versión más baja</li><li>*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</li><li>*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</li><li>*Mayor* (valor predeterminado para Update-Package sin parámetros): la versión más alta</li></ul>Puede establecer el valor predeterminado mediante la [`dependencyVersion`](../nuget-config-file.md#config-section) configuración del `Nuget.Config` archivo. |
| WhatIf | Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la sincronización. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Sync-Package` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

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