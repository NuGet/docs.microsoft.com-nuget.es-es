---
title: Referencia de PowerShell Register-TabExpansion de NuGet
description: Referencia de comandos de PowerShell Register-TabExpansion en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 98171c598bd4a3468bd23e2d6060e267c38021b4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546610"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (consola de administrador de paquetes en Visual Studio)

*Solo está disponible en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*

Registra una expansión de pestañas para los parámetros del comando especificado, de modo que cuando se usa la pestaña al escribir un comando, los valores expandidos aparecen como opciones disponibles para el parámetro en cuestión. Se sobrescriben cualquier expansiones del comando anteriores.

## <a name="syntax"></a>Sintaxis

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| nombre | (Obligatorio) El comando que se va a registrar las expansiones. -Nombre propio conmutador es opcional. |
| de esquema JSON | (Obligatorio) Un objeto que describe el argumento en la sintaxis `@{'<parameter>' = {'<value1>', '<value2>', ...}}` donde `<parameter>` es el nombre del parámetro para modificar y cada `<value>` proporciona una expansión específica. Se aceptan las comillas simples y dobles. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Register-TabExpansion` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

Considere la posibilidad de una solución que contiene tres nombres de los proyectos EventManager, utilidades y SpecialParser. El programador usa con frecuencia el `Update-Package` comando en momentos diferentes con cada uno de esos proyectos. Busca conveniente tener el `Update-Package` comandos proporcionan las expansiones de finalización automática para el `-ProjectName` argumento, así que no necesita escribir un nombre de proyecto cada vez. 

El siguiente comando y, a continuación, registra esos nombres de tres proyectos como una expansión para el `-ProjectName` parámetro:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

A continuación, puede escribir el desarrollador `Update-Package -ProjectName `, presione la tecla Tab y vea las expansiones ofrecidas como opciones de Autocompletar:

![Ejemplo del uso de Register-TabExpansion](media/Register-TabExpansion-Example.png)
