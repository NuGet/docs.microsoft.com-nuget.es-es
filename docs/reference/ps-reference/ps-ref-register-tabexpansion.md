---
title: Referencia de PowerShell Register-Tabexpansion controla de NuGet
description: Referencia del comando de PowerShell Register-Tabexpansion controla en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384459"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-Tabexpansion controla (consola del administrador de paquetes en Visual Studio)

*Solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*

Registra una expansión de pestaña para los parámetros del comando especificado, de modo que cuando se usa la pestaña al escribir un comando, los valores expandidos aparecen como opciones disponibles para el parámetro en cuestión. Se sobrescriben las expansiones anteriores para el comando.

## <a name="syntax"></a>Sintaxis

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Parámetro | Descripción |
| --- | --- |
| Name | Desee Comando en el que se van a registrar las expansiones. El propio modificador-name es opcional. |
| de esquema JSON | Desee Un objeto que describe el argumento en la sintaxis `@{'<parameter>' = {'<value1>', '<value2>', ...}}` donde `<parameter>` es el nombre del parámetro que se va a modificar y cada `<value>` proporciona una expansión específica. Se aceptan comillas simples y dobles. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Register-TabExpansion` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

Considere una solución que contenga tres nombres de proyecto EventManager, Utilities y SpecialParser. Con frecuencia, el desarrollador usa el comando `Update-Package` en momentos diferentes con cada uno de estos proyectos. Le resulta conveniente que el comando `Update-Package` proporcione expansiones de finalización automática para el argumento `-ProjectName` para que no tenga que escribir un nombre de proyecto cada vez. 

El siguiente comando registra los tres nombres de proyecto como una expansión para el parámetro `-ProjectName`:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

A continuación, el desarrollador puede escribir `Update-Package -ProjectName `, presionar la tecla TAB y ver las expansiones que se ofrecen como opciones de finalización automática:

![Ejemplo de uso de Register-Tabexpansion controla](media/Register-TabExpansion-Example.png)
