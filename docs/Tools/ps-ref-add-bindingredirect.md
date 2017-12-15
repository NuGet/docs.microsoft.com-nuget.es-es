---
title: "Referencia de PowerShell de NuGet agregar redirección de enlace | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Referencia de comandos de PowerShell agregar redirección de enlace en la consola de administrador de paquetes de NuGet en Visual Studio."
keywords: "Consola de administrador, comandos de NuGet Powershell, referencia de NuGet Powershell, agregar redirección de enlace de paquete de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bf8cdb938195f4747932b38ef0d5bb6c34b9137
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Agregar redirección de enlace (consola de administrador de paquetes en Visual Studio)

*Disponible solo en el [consola del Administrador de paquetes de NuGet](Package-Manager-Console.md) en Visual Studio en Windows.*

Examina todos los ensamblados de la ruta de acceso de salida para un proyecto y agrega redirecciones de enlace al archivo de configuración de aplicación o web cuando sea necesario. Este comando se ejecuta automáticamente al instalar un paquete.

Para obtener más información sobre cómo enlazar redirecciones y por qué se usan, vea [redirigir versiones de ensamblado](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) en la documentación. NET.

## <a name="syntax"></a>Sintaxis

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
| --- | --- |
| NombreDelProyecto | (Obligatorio) El proyecto que se va a agregar redirecciones de enlace. El propio modificador - NombreDeProyecto es opcional. |

Ninguno de estos parámetros aceptan caracteres de entrada o el carácter comodín de canalización.

## <a name="common-parameters"></a>Parámetros comunes

`Add-BindingRedirect`admite las siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuración, acción de Error, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detallado, WarningAction y WarningVariable.

## <a name="examples"></a>Ejemplos

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```