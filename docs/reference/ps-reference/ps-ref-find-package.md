---
title: Referencia de NuGet Find-Package PowerShell
description: Referencia de Find-Package comando de PowerShell en la consola de Administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901764"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Administrador de paquetes console en Visual Studio)

*Versión 3.0+; En este tema se describe el comando dentro [de Administrador de paquetes Console](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para obtener el comando Find-Package de PowerShell genérico, vea la referencia [de PackageManagement de PowerShell.](/powershell/module/packagemanagement)*

Obtiene el conjunto de paquetes remotos con el identificador o las palabras clave especificados del origen del paquete.

## <a name="syntax"></a>Sintaxis

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Palabras &lt; clave de identificador&gt; | (Obligatorio) Palabras clave que se usarán al buscar en el origen del paquete. Use -ExactMatch para devolver solo los paquetes cuyo identificador de paquete coincida con las palabras clave. Si no se especifica ninguna palabra clave, devuelve una lista de los 20 paquetes principales por descargas o el número `Find-Package` especificado por -First. Tenga en cuenta que -Id es opcional y no-op. |
| Source | Dirección URL o ruta de acceso de carpeta para el origen del paquete que se buscará. Las rutas de acceso de carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite, `Find-Package` busca en el origen del paquete seleccionado actualmente. |
| AllVersions | Muestra todas las versiones disponibles de cada paquete en lugar de solo la versión más reciente. |
| First | Número de paquetes que se devolverán desde el principio de la lista. el valor predeterminado es 20. |
| Omitir | Omite los primeros paquetes &lt; int de la lista &gt; mostrada.  |
| IncludePrerelease | Incluye paquetes de versión preliminar en los resultados. |
| ExactMatch | Se especifica para usar palabras &lt; clave como identificador de paquete que distingue &gt; mayúsculas de minúsculas. |
| StartWith | Devuelve paquetes cuyo identificador de paquete comienza con &lt; palabras clave &gt; . |

Ninguno de estos parámetros acepta caracteres comodín o entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Find-Package` admite los siguientes parámetros comunes de [PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.

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