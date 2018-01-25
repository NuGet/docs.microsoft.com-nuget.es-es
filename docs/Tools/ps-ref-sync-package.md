---
title: "Referencia de PowerShell de sincronización-paquete de NuGet | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referencia de comandos de PowerShell de paquete de sincronización en la consola de administrador de paquetes de NuGet en Visual Studio."
keywords: "Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, paquete de sincronización del paquete NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Paquete de sincronización (consola de administrador de paquetes en Visual Studio)

*Versión 3.0 +; disponible solo en el [NuGet Package Manager Console](Package-Manager-Console.md) en Visual Studio en Windows.*

Obtiene la versión del paquete instalado desde especificado (o predeterminado) del proyecto y sincroniza la versión para el resto de proyectos de la solución.

## <a name="syntax"></a>Sintaxis

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Id. | (Obligatorio) El identificador del paquete que se va a sincronizar. -Identificador propio modificador es opcional. |
| IgnoreDependencies | Instalar solo este paquete pero no sus dependencias. |
| NombreDelProyecto | El proyecto para sincronizar el paquete, el valor predeterminado para el proyecto predeterminado. |
| Versión | La versión del paquete para la sincronización, la versión instalada actualmente de forma predeterminada. |
| Origen | La ruta de acceso URL o una carpeta de origen del paquete para buscar. Las rutas de acceso de la carpeta local pueden ser absoluta o relativa a la carpeta actual. Si se omite, `Sync-Package` busca en el origen del paquete seleccionado. |
| IncludePrerelease | Incluye paquetes de versión preliminar de la sincronización. |
| FileConflictAction | La acción que se realizará cuando se le pregunte para sobrescribir u omitir los archivos existentes al que hace referencia el proyecto. Los valores posibles son *sobrescribir, omitir, None, OverwriteAll*, y *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La versión de los paquetes de dependencia que se va a usar, que puede ser uno de los siguientes:<br/><ul><li>*Menor* (valor predeterminado): la versión más antigua</li><li>*HighestPatch*: la versión con la revisión mínimo mayor, menor menor, más alto</li><li>*HighestMinor*: la versión con el menor principales, mayor revisión secundaria, más alto</li><li>*Mayor* (predeterminado para el paquete de actualización sin parámetros): la versión más reciente</li></ul>Puede establecer el valor predeterminado mediante la [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) en el `Nuget.Config` archivo. |
| WhatIf | Muestra qué ocurre cuando se ejecuta el comando sin realmente realizar la sincronización. |

Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Sync-Package`admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

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
