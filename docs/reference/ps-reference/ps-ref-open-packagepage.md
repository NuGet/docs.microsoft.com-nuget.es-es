---
title: Referencia de PowerShell Open-PackagePage de NuGet
description: Referencia del comando de PowerShell Open-PackagePage en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384433"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Consola del Administrador de paquetes en Visual Studio)

*En desuso en 3.0 +; solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*

Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso del informe para el paquete especificado.

## <a name="syntax"></a>Sintaxis

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Parámetro | Descripción |
| --- | --- |
| Id. | IDENTIFICADOR del paquete deseado. El propio modificador-ID es opcional. |
| Version | La versión del paquete, que tiene como valor predeterminado la versión más reciente. |
| Origen | El origen del paquete, que tiene como valor predeterminado el origen seleccionado en la lista desplegable origen. |
| Licencia | Abre el explorador en la dirección URL de la licencia del paquete. Si no se especifica ninguna licencia ni-ReportAbuse, el explorador abrirá la dirección URL del proyecto del paquete. |
| ReportAbuse | Abre el explorador en la dirección URL del informe de abuso de informes. Si no se especifica ninguna licencia ni-ReportAbuse, el explorador abrirá la dirección URL del proyecto del paquete. |
| PassThru | Muestra la dirección URL; Use con-WhatIf para suprimir la apertura del explorador. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Open-PackagePage` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

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