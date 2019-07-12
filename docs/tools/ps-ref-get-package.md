---
title: Referencia de PowerShell Get-paquete de NuGet
description: Referencia de comandos de PowerShell Get-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842517"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Consola del Administrador de paquetes en Visual Studio)

*Este tema describe el comando dentro de la [Package Manager Console](package-manager-console.md) en Visual Studio en Windows. El comando de PowerShell Get-Package genérico, vea el [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera la lista de los paquetes instalados en el repositorio local, se enumeran los paquetes disponibles desde un origen del paquete cuando se usa con el modificador - ListAvailable o listas de actualizaciones disponibles cuando se usa con-conmutador de actualización.

## <a name="syntax"></a>Sintaxis

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Sin parámetros, `Get-Package` muestra la lista de los paquetes instalados en el proyecto predeterminado.

## <a name="parameters"></a>Parámetros

| Parámetro | DESCRIPCIÓN |
| --- | --- |
| source | La ruta de acceso URL o carpeta para el paquete. Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual. Si se omite, `Get-Package` busca el origen del paquete seleccionado actualmente. Cuando se usa con - ListAvailable, valor predeterminado es en nuget.org. |
| ListAvailable | Enumera los paquetes disponibles desde un origen del paquete, de forma predeterminada en nuget.org. Muestra el valor predeterminado es 50 paquetes a menos que se especifica PageSize - o - primero. |
| Actualizaciones | Enumera los paquetes que tienen una actualización disponible desde el origen del paquete. |
| NombreDelProyecto | El proyecto desde el que se va a obtener los paquetes instalados. Si se omite, devuelve instala los proyectos de toda la solución. |
| Filtro | Una cadena de filtro utilizada para restringir la lista de paquetes aplicando el Id. de paquete, descripción y etiquetas. |
| Primero | El número de paquetes que se devolverán desde el principio de la lista. Si no se especifica, valor predeterminado es 50. |
| Skip | Omite la primera &lt;int&gt; paquetes en la lista mostrada.  |
| AllVersions | Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente. |
| IncludePrerelease | Incluye paquetes de versión preliminar en los resultados. |
| PageSize | *(3.0 +)*  Cuando se usa con - ListAvailable (obligatorio), el número de paquetes para mostrar antes de dar un símbolo del sistema para continuar. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Get-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

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
