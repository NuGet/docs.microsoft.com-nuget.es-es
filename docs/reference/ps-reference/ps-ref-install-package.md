---
title: 'Instalación de NuGet: referencia de PowerShell de paquetes'
description: Referencia del comando de PowerShell Install-Package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: a65ba63ed070f40e82c43d12e5fad12d86f28112
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384446"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Consola del Administrador de paquetes en Visual Studio)

*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando genérico Install-Package de PowerShell, consulte la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Instala un paquete y sus dependencias en un proyecto.

## <a name="syntax"></a>Sintaxis

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

En NuGet 2.8 +, `Install-Package` puede degradar un paquete existente en el proyecto. Por ejemplo, si tiene instalado Microsoft. AspNet. MVC 5.1.0-RC1, el siguiente comando lo degradará a 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parameters

| Parámetro | Descripción |
| --- | --- |
| Id. | Desee Identificador del paquete que se va a instalar. (*3.0 +* ) El identificador puede ser una ruta de acceso o dirección URL de un archivo `packages.config` o un archivo `.nupkg`. El propio modificador-ID es opcional. |
| IgnoreDependencies | Instale solo este paquete y no sus dependencias. |
| NombreDelProyecto | El proyecto en el que se va a instalar el paquete, que tiene como valor predeterminado el proyecto predeterminado. |
| Origen | La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar. Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite, `Install-Package` busca en el origen del paquete seleccionado actualmente. |
| Version | Versión del paquete que se va a instalar. el valor predeterminado es la versión más reciente. |
| IncludePrerelease | Tiene en cuenta los paquetes de versión preliminar para la instalación. Si se omite, solo se considerarán los paquetes estables. |
| FileConflictAction | Acción que se realizará cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto. Los valores posibles son *overwrite, ignore, None, OverwriteAll*y *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:<br/><ul><li>*Más bajo* (valor predeterminado): la versión más baja</li><li>*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</li><li>*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</li><li>*Más alto* (valor predeterminado para Update-package sin parámetros): la versión más alta</li></ul>Puede establecer el valor predeterminado mediante la opción [`dependencyVersion`](../nuget-config-file.md#config-section) del archivo de `Nuget.Config`. |
| WhatIf | Muestra lo que ocurre cuando se ejecuta el comando sin realizar realmente la instalación. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Install-Package` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
