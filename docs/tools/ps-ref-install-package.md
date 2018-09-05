---
title: Referencia de PowerShell de NuGet Install-Package
description: Referencia de comandos de PowerShell de Install-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546031"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Consola del Administrador de paquetes en Visual Studio)

*Este tema describe el comando dentro de la [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows. El comando de PowerShell, Install-Package genérico, vea el [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Instala un paquete y sus dependencias en un proyecto.

## <a name="syntax"></a>Sintaxis

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

En NuGet 2.8 y versiones posteriores, `Install-Package` puede degradar un paquete existente en el proyecto. Por ejemplo, si tiene 5.1.0-rc1 Microsoft.AspNet.MVC instalado, el siguiente comando de la degradación a 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Id. | (Obligatorio) El identificador del paquete para instalar. (*3.0 +*) el identificador puede ser una ruta de acceso o dirección URL de un `packages.config` archivo o un `.nupkg` archivo. -Identificador propio conmutador es opcional. |
| IgnoreDependencies | Instalar solo este paquete y no a sus dependencias. |
| NombreDelProyecto | El proyecto en el que se va a instalar el paquete, de forma predeterminada el proyecto predeterminado. |
| Origen | La ruta de acceso URL o carpeta para buscar el origen del paquete. Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual. Si se omite, `Install-Package` busca el origen del paquete seleccionado actualmente. |
| Versión | La versión del paquete para instalar, la versión más reciente de forma predeterminada. |
| IncludePrerelease | Considera que los paquetes de versión preliminar para la instalación. Si se omite, se consideran solo los paquetes estables. |
| FileConflictAction | La acción que se realizará cuando se le pida sobrescribir u omitir los archivos existentes que se hace referencia el proyecto. Los valores posibles son *sobrescribir, omitir, None, OverwriteAll*, y *(3.0 y versiones posteriores)* *IgnoreAll*. |
| DependencyVersion | La versión de los paquetes de dependencia para usar, que puede ser uno de los siguientes:<br/><ul><li>*Menor* (valor predeterminado): la versión más antigua</li><li>*HighestPatch*: la versión con la revisión menor principal, secundaria menor, más alta</li><li>*HighestMinor*: la versión con el menor principales, revisiones secundarias y de mayor más alto</li><li>*Mayor* (predeterminado para el paquete de actualización sin parámetros): la versión más alta</li></ul>Puede establecer el valor predeterminado con el [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) en el `Nuget.Config` archivo. |
| WhatIf | Muestra lo que sucedería cuando ejecute el comando sin tener que realizar la instalación. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Install-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
