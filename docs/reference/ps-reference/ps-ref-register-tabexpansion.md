---
title: Referencia de PowerShell de Register-TabExpansion de NuGet
description: Referencia de Register-TabExpansion comando de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6ad0da0e84fc2e31499c06bde013d2a256987d9a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777458"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (consola del administrador de paquetes en Visual Studio)

*Solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*

Registra una expansión de pestaña para los parámetros del comando especificado, de modo que cuando se usa la pestaña al escribir un comando, los valores expandidos aparecen como opciones disponibles para el parámetro en cuestión. Se sobrescriben las expansiones anteriores para el comando.

## <a name="syntax"></a>Sintaxis

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| Nombre | Desee Comando en el que se van a registrar las expansiones. El propio modificador-name es opcional. |
| Definición | Desee Un objeto que describe el argumento en la sintaxis `@{'<parameter>' = {'<value1>', '<value2>', ...}}` donde `<parameter>` es el nombre del parámetro que se va a modificar y cada uno `<value>` proporciona una expansión específica. Se aceptan comillas simples y dobles. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Register-TabExpansion` admite los siguientes [parámetros comunes de PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

Considere una solución que contenga tres nombres de proyecto EventManager, Utilities y SpecialParser. Con frecuencia, el desarrollador usa el `Update-Package` comando en momentos diferentes con cada uno de estos proyectos. Es conveniente que el `Update-Package` comando proporcione expansiones de finalización automática para el `-ProjectName` argumento, por lo que no es necesario escribir un nombre de proyecto cada vez. 

El siguiente comando registra los tres nombres de proyecto como una expansión para el `-ProjectName` parámetro:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

A continuación, el desarrollador puede escribir `Update-Package -ProjectName ` , presionar Tab y ver las expansiones que se ofrecen como opciones de finalización automática:

![Ejemplo de uso de Register-TabExpansion](media/Register-TabExpansion-Example.png)