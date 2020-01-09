---
title: Referencia de PowerShell para obtener paquetes de NuGet
description: Referencia del comando de PowerShell Get-Package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1c39fea2131b8f4b8a91314347a19366d5a582c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385198"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Consola del Administrador de paquetes en Visual Studio)

*En este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando genérico Get-Package de PowerShell, consulte la [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera la lista de paquetes instalados en el repositorio local, enumera los paquetes disponibles en un origen del paquete cuando se usa con el modificador-ListAvailable o enumera las actualizaciones disponibles cuando se usa con el modificador-Update.

## <a name="syntax"></a>Sintaxis

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Sin parámetros, `Get-Package` muestra la lista de paquetes instalados en el proyecto predeterminado.

## <a name="parameters"></a>Parameters

| Parámetro | Descripción |
| --- | --- |
| Origen | La dirección URL o la ruta de acceso de la carpeta para el paquete. Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite, `Get-Package` busca en el origen del paquete seleccionado actualmente. Cuando se usa con-ListAvailable, el valor predeterminado es nuget.org. |
| ListAvailable | Enumera los paquetes disponibles en el origen de un paquete, con el valor predeterminado nuget.org. Muestra un valor predeterminado de 50 paquetes, a menos que se especifiquen-PageSize y/o-First. |
| Actualizaciones | Enumera los paquetes que tienen una actualización disponible desde el origen del paquete. |
| NombreDelProyecto | Proyecto desde el que se van a obtener los paquetes instalados. Si se omite, devuelve los proyectos instalados para toda la solución. |
| Filtro | Cadena de filtro que se usa para restringir la lista de paquetes aplicándolos al identificador, la descripción y las etiquetas del paquete. |
| First | Número de paquetes que se van a devolver desde el principio de la lista. Si no se especifica, el valor predeterminado es 50. |
| Skip | Omite la primera &lt;int&gt; paquetes de la lista mostrada.  |
| AllVersions | Muestra todas las versiones disponibles de cada paquete en lugar de la versión más reciente. |
| IncludePrerelease | Incluye paquetes de versiones preliminares en los resultados. |
| PageSize | *(3.0 +)* Cuando se usa con-ListAvailable (obligatorio), el número de paquetes que se deben enumerar antes de dar un mensaje para continuar. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Get-Package` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

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
