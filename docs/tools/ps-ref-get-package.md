---
title: Referencia de PowerShell Get-paquete de NuGet
description: Referencia de comandos de PowerShell Get-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f4b71fc44e44dcbd5d123a0e2fed63adb79964b5
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818508"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Consola del Administrador de paquetes en Visual Studio)

*Este tema describe el comando dentro de la [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows. Para el comando de PowerShell Get-Package genérico, vea la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera la lista de paquetes instalados en el repositorio local, enumera los paquetes disponibles en un origen del paquete cuando se usa con el modificador - ListAvailable o listas de actualizaciones disponibles cuando se usa con-conmutador de actualización.

## <a name="syntax"></a>Sintaxis

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Sin parámetros, `Get-Package` muestra la lista de paquetes instalados en el proyecto predeterminado.

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Origen | La ruta de acceso URL o una carpeta para el paquete. Las rutas de acceso de la carpeta local pueden ser absoluta o relativa a la carpeta actual. Si se omite, `Get-Package` busca en el origen del paquete seleccionado. Cuando se usa con - ListAvailable, el valor predeterminado es nuget.org. |
| ListAvailable | Enumera los paquetes disponibles en un origen del paquete, nuget.org de forma predeterminada. Muestra el valor predeterminado es 50 paquetes a menos que se especifique PageSize - o - primero. |
| Actualizaciones | Enumera los paquetes que tienen una actualización disponible en el origen del paquete. |
| NombreDelProyecto | El proyecto desde el que se obtendrán los paquetes instalados. Si se omite, devuelve instaladas proyectos para toda la solución. |
| Filtro | Una cadena de filtro que se usa para reducir la lista de paquetes mediante la aplicación para el Id. de paquete, la descripción y etiquetas. |
| First | El número de paquetes que se va a devolver desde el principio de la lista. Si no se especifica, valor predeterminado es 50. |
| Skip | Omite la primera &lt;int&gt; paquetes en la lista mostrada.  |
| AllVersions | Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente. |
| IncludePrerelease | Incluye paquetes de versión preliminar en los resultados. |
| PageSize | *(3.0 +)*  Cuando se usa con - ListAvailable (obligatorio), el número de paquetes para mostrar antes de entregar un mensaje para continuar. |

Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Get-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
