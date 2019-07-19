---
title: Referencia de PowerShell para buscar paquetes de NuGet
description: Referencia del comando de PowerShell Find-Package en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327392"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Consola del Administrador de paquetes en Visual Studio)

*Versión 3.0 +; en este tema se describe el comando en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows. Para el comando de búsqueda-paquete de PowerShell genérico, vea la [referencia de PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Obtiene el conjunto de paquetes remotos con el identificador o las palabras clave especificados del origen del paquete.

## <a name="syntax"></a>Sintaxis

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | DESCRIPCIÓN |
| --- | --- |
| Palabras &lt;clave de ID.&gt; | Desee Palabras clave que se deben usar al buscar en el origen del paquete. Use-ExactMatch para devolver solo los paquetes cuyo identificador de paquete coincida con las palabras clave. Si no se proporciona ninguna palabra `Find-Package` clave, devuelve una lista de los 20 primeros paquetes por descargas o el número especificado por-First. Tenga en cuenta que-ID es opcional y no es operativo. |
| source | La dirección URL o la ruta de acceso de la carpeta del origen del paquete que se va a buscar. Las rutas de acceso de la carpeta local pueden ser absolutas o relativas a la carpeta actual. Si se omite `Find-Package` , busca el origen del paquete seleccionado actualmente. |
| AllVersions | Muestra todas las versiones disponibles de cada paquete en lugar de la versión más reciente. |
| Primero | Número de paquetes que se van a devolver desde el principio de la lista; el valor predeterminado es 20. |
| Skip | Omite los primeros &lt;paquetes int&gt; de la lista mostrada.  |
| IncludePrerelease | Incluye paquetes de versiones preliminares en los resultados. |
| ExactMatch | Se especifica para &lt;usar&gt; palabras clave como un identificador de paquete que distingue entre mayúsculas y minúsculas. |
| StartWith | Devuelve paquetes cuyo identificador de paquete comienza &lt;con&gt;palabras clave. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Find-Package`admite los siguientes [parámetros de PowerShell comunes](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

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
