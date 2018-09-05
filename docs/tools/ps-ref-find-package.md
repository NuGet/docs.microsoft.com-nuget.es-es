---
title: Referencia de PowerShell de Find-paquete de NuGet
description: Referencia de comandos de PowerShell de Find-Package en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550983"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Consola del Administrador de paquetes en Visual Studio)

*Versión 3.0 o superior; Este tema describe el comando dentro de la [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows. El comando de PowerShell Find-Package genérico, vea el [referencia de PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Obtiene el conjunto de paquetes remotos con el identificador especificado o palabras clave del origen del paquete.

## <a name="syntax"></a>Sintaxis

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Id. de &lt;palabras clave&gt; | (Obligatorio) Palabras clave pueden usarse al buscar el origen del paquete. Utilice - ExactMatch para devolver solo los paquetes cuyo identificador de paquete coincide con las palabras clave. Si no se especifica ninguna palabra clave, `Find-Package` devuelve una lista de los primeros 20 paquetes por descarga o el número especificada por - primero. Tenga en cuenta que - Id. es opcional y una operación inefectiva. |
| Origen | La ruta de acceso URL o carpeta para buscar el origen del paquete. Las rutas de acceso de carpeta local pueden ser absoluta o relativa a la carpeta actual. Si se omite, `Find-Package` busca el origen del paquete seleccionado actualmente. |
| AllVersions | Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente. |
| First | El número de paquetes que se devolverán desde el principio de la lista. el valor predeterminado es 20. |
| Skip | Omite la primera &lt;int&gt; paquetes en la lista mostrada.  |
| IncludePrerelease | Incluye paquetes de versión preliminar en los resultados. |
| ExactMatch | Especificado para usar &lt;palabras clave&gt; como un identificador del paquete distingue mayúsculas de minúsculas. |
| StartWith | Devuelve los paquetes cuyo paquete ID comienza con &lt;palabras clave&gt;. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Find-Package` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
