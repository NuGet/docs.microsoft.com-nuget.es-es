---
title: "Referencia de página del paquete NuGet abrir PowerShell | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referencia de comandos de PowerShell de página del paquete abierto en la consola de administrador de paquetes de NuGet en Visual Studio."
keywords: "Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, Abrir página del paquete del paquete NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cc645d9a2779fd6b1b329e9aac4777d50f75d16
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Abrir página del paquete (consola de administrador de paquetes en Visual Studio)

*En desuso en 3.0 +; disponible solo en el [NuGet Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*

Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso de informes para el paquete especificado.

## <a name="syntax"></a>Sintaxis

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Id. | El identificador del paquete del paquete adecuado. -Identificador propio modificador es opcional. |
| Versión | La versión del paquete, la versión más reciente de forma predeterminada. |
| Origen | El origen del paquete, el valor predeterminado para el origen seleccionado en el origen de la lista desplegable. |
| Licencia | Se abre el explorador a la dirección URL de licencia del paquete. Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete. |
| ReportAbuse | Se abre el explorador para la dirección URL de abuso de informes del paquete. Si se especifica - licencia ni - ReportAbuse, el explorador abre la dirección URL del proyecto del paquete. |
| PassThru | Muestra la dirección URL; Utilícelo con - WhatIf para suprimir abrir el explorador. |

Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Open-PackagePage` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

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