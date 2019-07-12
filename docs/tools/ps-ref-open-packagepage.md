---
title: Referencia de PowerShell de NuGet abierto-PackagePage
description: Referencia de comandos de PowerShell abierto PackagePage en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842266"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Consola del Administrador de paquetes en Visual Studio)

*En desuso en 3.0 + solo está disponible en el [Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*

Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso de informes para el paquete especificado.

## <a name="syntax"></a>Sintaxis

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | DESCRIPCIÓN |
| --- | --- |
| Id | El identificador del paquete del paquete deseado. -Identificador propio conmutador es opcional. |
| `Version` | La versión del paquete, la versión más reciente de forma predeterminada. |
| source | El origen del paquete, el valor predeterminado el origen seleccionado en el origen de la lista desplegable. |
| Licencia | Se abre el explorador a la dirección URL de licencia del paquete. Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete. |
| ReportAbuse | Se abre el explorador para la dirección URL de abuso de informes del paquete. Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete. |
| PassThru | Muestra la dirección URL; Utilícelo con - WhatIf para suprimir la apertura del explorador. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Open-PackagePage` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```