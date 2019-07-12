---
title: NuGet BindingRedirect-Agregar referencia de PowerShell
description: Referencia de comandos de PowerShell Add-BindingRedirect en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842540"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Consola del Administrador de paquetes en Visual Studio)

*Solo está disponible en el [Package Manager Console](package-manager-console.md) en Visual Studio en Windows.*

Examina todos los ensamblados en la ruta de acceso de salida para un proyecto y agregar redirecciones de enlaces al archivo de configuración de aplicación o web donde sea necesario. Este comando se ejecuta automáticamente al instalar un paquete.

Para obtener más información sobre cómo enlazar redirecciones y por qué se usan, vea [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación. NET.

## <a name="syntax"></a>Sintaxis

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | DESCRIPCIÓN |
| --- | --- |
| NombreDelProyecto | (Obligatorio) El proyecto que se va a agregar redirecciones de enlace. El propio conmutador - nombreproyecto es opcional. |

Ninguno de estos parámetros aceptan caracteres comodín o de entrada de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Add-BindingRedirect` admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuración, acción del Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```