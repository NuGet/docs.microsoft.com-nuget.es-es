---
title: 'Actualización de NuGet: referencia de PowerShell de paquetes'
description: Referencia del comando de PowerShell Update-package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e1bff9d4b7391d8be87afa4b8f2fbd51ae922140
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384861"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Consola del Administrador de paquetes en Visual Studio)

*Solo está disponible en la [consola del administrador de paquetes NuGet](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*

Actualiza un paquete y sus dependencias, o todos los paquetes de un proyecto, a una versión más reciente.

## <a name="syntax"></a>Sintaxis

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

En NuGet 2.8 +, `Update-Package` se puede usar para degradar un paquete existente en el proyecto. Por ejemplo, si tiene instalado Microsoft. AspNet. MVC 5.1.0-RC1, el siguiente comando lo degradará a 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parameters

|  Parámetro | Descripción |
| --- | --- |
| Id. | Identificador del paquete que se va a actualizar. Si se omite, actualiza todos los paquetes. El propio modificador-ID es opcional. |
| IgnoreDependencies | Omite la actualización de las dependencias del paquete. |
| NombreDelProyecto | Nombre del proyecto que contiene los paquetes que se van a actualizar; el valor predeterminado es todos los proyectos. |
| Version | Versión que se va a usar para la actualización, que tiene como valor predeterminado la versión más reciente. En NuGet 3.0 y versiones posteriores, el valor de la versión debe ser uno de los más *bajos, HighestMinor*o *HighestPatch* (equivalente a Safe). |
| Caja fuerte | Restringe las actualizaciones solo a las versiones con la misma versión principal y secundaria que el paquete instalado actualmente. |
| Origen | La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar. Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite, `Update-Package` busca en el origen del paquete seleccionado actualmente. |
| IncludePrerelease | Incluye paquetes de versión preliminar para las actualizaciones. |
| Reinstalación | Resintalls paquetes con sus versiones instaladas actualmente. Vea [Reinstalación y actualización de paquetes](../../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Acción que se realizará cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto. Los valores posibles son *overwrite, ignore, None, OverwriteAll*y *IgnoreAll* (3.0 +). |
| DependencyVersion | La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:<br/><ul><li>*Más bajo* (valor predeterminado): la versión más baja</li><li>*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</li><li>*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</li><li>*Más alto* (valor predeterminado para Update-package sin parámetros): la versión más alta</li></ul>Puede establecer el valor predeterminado mediante la opción [`dependencyVersion`](../nuget-config-file.md#config-section) del archivo de `Nuget.Config`. |
| ToHighestPatch | equivalente a Safe. |
| ToHighestMinor | Restringe las actualizaciones a solo las versiones con la misma versión principal que el paquete instalado actualmente. |
| WhatIf | Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la actualización. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

### <a name="common-parameters"></a>Parámetros comunes

`Update-Package` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

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
