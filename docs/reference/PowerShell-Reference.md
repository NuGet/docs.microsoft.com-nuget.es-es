---
title: Referencia de PowerShell de NuGet
description: La referencia completa a los comandos de PowerShell disponibles en la consola del administrador de paquetes NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 4f8b42847cbc155393fe6d2afbe2e0857b619da3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236885"
---
# <a name="powershell-reference"></a>Referencia de PowerShell

La consola del administrador de paquetes proporciona una interfaz de PowerShell en Visual Studio en Windows para interactuar con NuGet a través de los comandos específicos que se enumeran a continuación. (La consola no está actualmente disponible en Visual Studio para Mac). Para obtener una guía sobre el uso de la consola de, consulte el tema [instalar y administrar paquetes mediante la consola del administrador de paquetes](../consume-packages/install-use-packages-powershell.md) .

> [!Tip]
> Todos los comandos de PowerShell solo se relacionan con el consumo de paquetes. No hay comandos de PowerShell relacionados con la creación y publicación de paquetes, excepto en la medida en que un paquete también puede ser un consumidor de otros paquetes.

> [!Important]
> Los comandos enumerados aquí son específicos de la consola del administrador de paquetes en Visual Studio y difieren de los [comandos del módulo Administración de paquetes](/powershell/module/packagemanagement/?view=powershell-6) que están disponibles en un entorno de PowerShell general. En concreto, cada entorno tiene comandos que no están disponibles en el otro, y los comandos con el mismo nombre también pueden diferir en sus argumentos específicos. Al usar la consola de Administración de paquetes en Visual Studio, se aplican los comandos y los argumentos que se documentan en este tema presente.

| Comandos comunes | Descripción | Versión de NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Permite instalar un paquete y sus dependencias en el proyecto. | Todo |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Actualiza un paquete y sus dependencias, o todos los paquetes de un proyecto. | Todo |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Busca un origen de paquete mediante un identificador de paquete o palabras clave. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Recupera la lista de paquetes instalados en el repositorio local o enumera los paquetes disponibles en el origen de un paquete. | Todo |

| Comandos secundarios | Descripción | Versión de NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Examina todos los ensamblados de la ruta de acceso de salida de un proyecto y agrega redirecciones de enlace al `app.config` o `web.config` cuando es necesario. | Todo |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Muestra información sobre el proyecto predeterminado o el especificado. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso del informe para el paquete especificado. | En desuso en 3.0 + |
| [Register-Tabexpansion controla](ps-reference/ps-ref-register-tabexpansion.md) | Registra una expansión de pestaña para los parámetros de un comando, lo que permite crear expansiones personalizadas para los valores de parámetro que se usan con frecuencia. | Todo |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Obtiene la versión del paquete instalado del proyecto especificado y sincroniza la versión con el resto de proyectos de la solución. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Quita un paquete de un proyecto y, opcionalmente, quita sus dependencias. | Todo |

Para obtener ayuda completa y detallada sobre cualquiera de estos comandos en la consola de, solo tiene que ejecutar lo siguiente con el nombre de comando en cuestión:

```ps
Get-Help <command> -full
```

Todos los comandos de la consola del administrador de paquetes admiten los siguientes [parámetros de PowerShell comunes](/powershell/module/microsoft.powershell.core/about/about_commonparameters):

- Depurar
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Verbose
- WarningAction
- WarningVariable

Para obtener más información, consulte [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) en la documentación de PowerShell.