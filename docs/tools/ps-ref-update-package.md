---
title: Referencia de PowerShell Update-paquete de NuGet
description: Referencia de comandos de PowerShell Update-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d47e1978ab7d827e0b8b97cd4e7237019185b50f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546081"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Consola del Administrador de paquetes en Visual Studio)

*Solo está disponible en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*

Actualiza un paquete y sus dependencias o todos los paquetes en un proyecto, a una versión más reciente.

## <a name="syntax"></a>Sintaxis

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

En NuGet 2.8 y versiones posteriores, `Update-Package` puede usarse para degradar un paquete existente en el proyecto. Por ejemplo, si tiene 5.1.0-rc1 Microsoft.AspNet.MVC instalado, el siguiente comando de la degradación a 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parámetros

|  Parámetro | Descripción |
| --- | --- |
| Id. | El identificador del paquete para actualizar. Si se omite, se actualiza todos los paquetes. -Identificador propio conmutador es opcional. |
| IgnoreDependencies | Omite la actualización de las dependencias del paquete. |
| NombreDelProyecto | El nombre del proyecto que contiene los paquetes que se va a actualizar, de forma predeterminada a todos los proyectos. |
| Versión | La versión que se usará para la actualización, la versión más reciente de forma predeterminada. En NuGet 3.0 +, el valor de versión debe ser uno de *mínima, máxima, HighestMinor*, o *HighestPatch* (equivalente a - Safe). |
| Safe | Restringe las actualizaciones a las versiones sola con la misma versión principal y secundaria, como el paquete instalado actualmente. |
| Origen | La ruta de acceso URL o carpeta para buscar el origen del paquete. Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual. Si se omite, `Update-Package` busca el origen del paquete seleccionado actualmente. |
| IncludePrerelease | Incluye paquetes de versión preliminar para las actualizaciones. |
| Reinstalación | Paquetes de Resintalls con sus versiones instaladas actualmente. Vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | La acción que se realizará cuando se le pida sobrescribir u omitir los archivos existentes que se hace referencia el proyecto. Los valores posibles son *sobrescribir, omitir, None, OverwriteAll*, y *IgnoreAll* (3.0 y versiones posteriores). |
| DependencyVersion | La versión de los paquetes de dependencia para usar, que puede ser uno de los siguientes:<br/><ul><li>*Menor* (valor predeterminado): la versión más antigua</li><li>*HighestPatch*: la versión con la revisión menor principal, secundaria menor, más alta</li><li>*HighestMinor*: la versión con el menor principales, revisiones secundarias y de mayor más alto</li><li>*Mayor* (predeterminado para el paquete de actualización sin parámetros): la versión más alta</li></ul>Puede establecer el valor predeterminado con el [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) en el `Nuget.Config` archivo. |
| ToHighestPatch | Restringe las actualizaciones a solo las versiones con la misma versión menor que el paquete instalado actualmente. |
| ToHighestMinor | Restringe las actualizaciones a solo las versiones con la misma versión principal que el paquete instalado actualmente. |
| WhatIf | Muestra lo que sucedería cuando ejecute el comando sin tener que realizar la actualización. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

### <a name="common-parameters"></a>Parámetros comunes

`Update-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.

### <a name="examples"></a>Ejemplos

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
