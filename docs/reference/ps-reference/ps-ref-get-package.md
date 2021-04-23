---
title: Referencia de NuGet Get-Package PowerShell
description: Referencia de Get-Package comando de PowerShell en la consola de Administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901738"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Administrador de paquetes console en Visual Studio)

*En este tema se describe el comando dentro de Administrador de paquetes [Console](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para obtener el comando Get-Package de PowerShell genérico, vea la referencia [de PackageManagement de PowerShell.](/powershell/module/packagemanagement)*

Recupera la lista de paquetes instalados en el repositorio local, enumera los paquetes disponibles desde un origen de paquete cuando se usan con el modificador -ListAvailable o enumera las actualizaciones disponibles cuando se usan con el modificador -Update.

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
| Source | Dirección URL o ruta de acceso de carpeta para el paquete . Las rutas de acceso de carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite, `Get-Package` busca en el origen del paquete seleccionado actualmente. Cuando se usa con -ListAvailable, el valor predeterminado es nuget.org. |
| ListAvailable | Enumera los paquetes disponibles desde un origen de paquete, con el valor predeterminado nuget.org. Muestra un valor predeterminado de 50 paquetes a menos que se especifique -PageSize o -First. |
| Actualizaciones | Enumera los paquetes que tienen una actualización disponible desde el origen del paquete. |
| ProjectName | Proyecto desde el que se obtienen los paquetes instalados. Si se omite, devuelve los proyectos instalados para toda la solución. |
| Filtrar | Cadena de filtro que se usa para restringir la lista de paquetes al aplicarla al identificador, la descripción y las etiquetas del paquete. |
| First | Número de paquetes que se devolverán desde el principio de la lista. Si no se especifica, el valor predeterminado es 50. |
| Omitir | Omite los primeros paquetes &lt; int de la lista &gt; mostrada.  |
| AllVersions | Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente. |
| IncludePrerelease | Incluye paquetes de versión preliminar en los resultados. |
| PageSize | *(3.0+)* Cuando se usa con -ListAvailable (obligatorio), el número de paquetes que se enumerarán antes de dar una solicitud para continuar. |

Ninguno de estos parámetros acepta caracteres comodín o entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Get-Package` admite los siguientes parámetros comunes de [PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.

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