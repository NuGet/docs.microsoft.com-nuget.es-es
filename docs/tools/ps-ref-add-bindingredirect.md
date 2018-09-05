---
title: NuGet BindingRedirect-Agregar referencia de PowerShell
description: Referencia de comandos de PowerShell Add-BindingRedirect en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551662"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Consola del Administrador de paquetes en Visual Studio)

*Solo está disponible en el [consola del Administrador de paquetes de NuGet](package-manager-console.md) en Visual Studio en Windows.*

Examina todos los ensamblados en la ruta de acceso de salida para un proyecto y agregar redirecciones de enlaces al archivo de configuración de aplicación o web donde sea necesario. Este comando se ejecuta automáticamente al instalar un paquete.

Para obtener más información sobre cómo enlazar redirecciones y por qué se usan, vea [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación. NET.

## <a name="syntax"></a>Sintaxis

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| NombreDelProyecto | (Obligatorio) El proyecto que se va a agregar redirecciones de enlace. El propio conmutador - nombreproyecto es opcional. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Add-BindingRedirect` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```