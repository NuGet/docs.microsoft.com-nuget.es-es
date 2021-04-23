---
title: Referencia de NuGet Install-Package PowerShell
description: Referencia de Install-Package comando de PowerShell en la consola de Administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901699"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Administrador de paquetes consola en Visual Studio)

*En este tema se describe el comando dentro de [Administrador de paquetes Console](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para obtener el comando genérico de Install-Package PowerShell, consulte la referencia [de PackageManagement de PowerShell.](/powershell/module/packagemanagement)*

Instala un paquete y sus dependencias en un proyecto.

## <a name="syntax"></a>Sintaxis

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

En NuGet 2.8+, puede cambiar a una versión anterior `Install-Package` un paquete existente en el proyecto. Por ejemplo, si tiene instalado Microsoft.AspNet.MVC 5.1.0-rc1, el siguiente comando lo degradaría a 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Identificador | (Obligatorio) Identificador del paquete que se instalará. (*3.0+*) El identificador puede ser una ruta de acceso o una dirección URL de `packages.config` un archivo o un `.nupkg` archivo. El propio modificador -Id es opcional. |
| IgnoreDependencies | Instale solo este paquete y no sus dependencias. |
| ProjectName | Proyecto en el que se va a instalar el paquete, cuyo valor predeterminado es el proyecto predeterminado. |
| Source | Dirección URL o ruta de acceso de carpeta para el origen del paquete que se buscará. Las rutas de acceso de carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite, `Install-Package` busca en el origen del paquete seleccionado actualmente. |
| Versión | La versión del paquete que se instalará, con el valor predeterminado de la versión más reciente. |
| IncludePrerelease | Tiene en cuenta los paquetes de versión preliminar para la instalación. Si se omite, solo se considerarán los paquetes estables. |
| FileConflictAction | Acción que se debe realizar cuando se le pida que sobrescriba o ignore los archivos existentes a los que hace referencia el proyecto. Los valores *posibles son Overwrite, Ignore, None, OverwriteAll* y *(3.0+)* *IgnoreAll.* |
| DependencyVersion | La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:<br/><ul><li>*Más* bajo (valor predeterminado): la versión más baja</li><li>*HighestPatch:* la versión con la revisión más baja principal, menor menor y más alta.</li><li>*HighestMinor:* la versión con la revisión más baja principal, secundaria más alta y más alta.</li><li>*Más* alto (valor predeterminado para Update-Package sin parámetros): la versión más alta</li></ul>Puede establecer el valor predeterminado mediante la [`dependencyVersion`](../nuget-config-file.md#config-section) configuración del `Nuget.Config` archivo . |
| WhatIf | Muestra lo que sucedería al ejecutar el comando sin realizar realmente la instalación. |

Ninguno de estos parámetros acepta caracteres comodín o entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Install-Package` admite los siguientes parámetros comunes de [PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.

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