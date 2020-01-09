---
title: Referencia de PowerShell Add-BindingRedirect de NuGet
description: Referencia del comando Add-BindingRedirect de PowerShell en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384989"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Consola del Administrador de paquetes en Visual Studio)

*Solo está disponible en la [consola del administrador de paquetes](../../consume-packages/install-use-packages-powershell.md) en Visual Studio en Windows.*

Examina todos los ensamblados de la ruta de acceso de salida de un proyecto y agrega redirecciones de enlace al archivo de configuración web o de aplicación cuando sea necesario. Este comando se ejecuta automáticamente al instalar un paquete.

Para obtener más información sobre las redirecciones de enlace y por qué se usan, consulte [redirección de versiones de ensamblado](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación de .net.

## <a name="syntax"></a>Sintaxis

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Parámetro | Descripción |
| --- | --- |
| NombreDelProyecto | Desee Proyecto al que se van a agregar redirecciones de enlace. El propio modificador-ProjectName es opcional. |

Ninguno de estos parámetros acepta caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Add-BindingRedirect` admite los siguientes [parámetros comunes de PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, error Action, ErrorVariable, outbuffer, outvariable, PipelineVariable, verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```