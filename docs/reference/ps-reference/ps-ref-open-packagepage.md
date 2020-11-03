---
title: Referencia de PowerShell de Open-PackagePage de NuGet
description: Referencia de Open-PackagePage comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238067"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (consola del administrador de paquetes en Visual Studio)

*En desuso en 3.0 +; solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*

Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso del informe para el paquete especificado.

## <a name="syntax"></a>Sintaxis

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Identificador | IDENTIFICADOR del paquete deseado. El propio modificador-ID es opcional. |
| Versión | La versión del paquete, que tiene como valor predeterminado la versión más reciente. |
| Source | El origen del paquete, que tiene como valor predeterminado el origen seleccionado en la lista desplegable origen. |
| Licencia | Abre el explorador en la dirección URL de la licencia del paquete. Si no se especifica ninguna licencia ni-ReportAbuse, el explorador abrirá la dirección URL del proyecto del paquete. |
| ReportAbuse | Abre el explorador en la dirección URL del informe de abuso de informes. Si no se especifica ninguna licencia ni-ReportAbuse, el explorador abrirá la dirección URL del proyecto del paquete. |
| PassThru | Muestra la dirección URL; Use con-WhatIf para suprimir la apertura del explorador. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Open-PackagePage` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

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