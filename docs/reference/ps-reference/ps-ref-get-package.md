---
title: Referencia de PowerShell de Get-Package de NuGet
description: Referencia de Get-Package comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1576e3f20eba1ecdd099b1e7c23aef6b1a1a0a4f
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237236"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (consola del administrador de paquetes en Visual Studio)

*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando genérico de Get-Package de PowerShell, consulte la [referencia de PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera la lista de paquetes instalados en el repositorio local, enumera los paquetes disponibles en un origen del paquete cuando se usa con el modificador-ListAvailable o enumera las actualizaciones disponibles cuando se usa con el modificador-Update.

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
| Source | La dirección URL o la ruta de acceso de la carpeta para el paquete. Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite, `Get-Package` busca el origen del paquete seleccionado actualmente. Cuando se usa con-ListAvailable, el valor predeterminado es nuget.org. |
| ListAvailable | Enumera los paquetes disponibles en el origen de un paquete, con el valor predeterminado nuget.org. Muestra un valor predeterminado de 50 paquetes, a menos que se especifiquen-PageSize y/o-First. |
| Actualizaciones | Enumera los paquetes que tienen una actualización disponible desde el origen del paquete. |
| ProjectName | Proyecto desde el que se van a obtener los paquetes instalados. Si se omite, devuelve los proyectos instalados para toda la solución. |
| Filter | Cadena de filtro que se usa para restringir la lista de paquetes aplicándolos al identificador, la descripción y las etiquetas del paquete. |
| First | Número de paquetes que se van a devolver desde el principio de la lista. Si no se especifica, el valor predeterminado es 50. |
| Omitir | Omite los primeros &lt; paquetes int &gt; de la lista mostrada.  |
| AllVersions | Muestra todas las versiones disponibles de cada paquete en lugar de la versión más reciente. |
| IncludePrerelease | Incluye paquetes de versiones preliminares en los resultados. |
| PageSize | *(3.0 +)* Cuando se usa con-ListAvailable (obligatorio), el número de paquetes que se deben enumerar antes de dar un mensaje para continuar. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Get-Package` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

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