---
title: Referencia de PowerShell de NuGet
description: Referencia completa a los comandos de PowerShell disponibles en la consola de Administrador de paquetes NuGet en Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 7bc0395a98e75fe006e048b91d84cb5c17220161
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901894"
---
# <a name="powershell-reference"></a>Referencia de PowerShell

La Administrador de paquetes proporciona una interfaz de PowerShell dentro de Visual Studio en Windows para interactuar con NuGet a través de los comandos específicos que se enumeran a continuación. (La consola no está disponible actualmente en Visual Studio para Mac). Para obtener una guía sobre el uso de la consola, consulte el tema [Instalación y administración de paquetes mediante Administrador de paquetes Consola.](../consume-packages/install-use-packages-powershell.md)

> [!Tip]
> Todos los comandos de PowerShell solo se relacionan con el consumo de paquetes. Ningún comando de PowerShell está relacionado con la creación y publicación de paquetes, excepto en la medida en que un paquete también puede ser un consumidor de otros paquetes.

> [!Important]
> Los comandos que se enumeran aquí son específicos de la consola del administrador de paquetes de Visual Studio y difieren de los [comandos del módulo de Administración de paquetes](/powershell/module/packagemanagement) que están disponibles en un entorno de PowerShell general. En concreto, cada entorno tiene comandos que no están disponibles en el otro entorno, y los comandos con el mismo nombre también pueden tener distintos argumentos específicos. Al usar la consola de Administración de paquetes en Visual Studio, se aplican los comandos y los argumentos que se documentan en este tema.

| Comandos comunes | Descripción | Versión de NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Permite instalar un paquete y sus dependencias en el proyecto. | All |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Actualiza un paquete y sus dependencias, o todos los paquetes de un proyecto. | All |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Busca un origen de paquete mediante un identificador de paquete o palabras clave. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Recupera la lista de paquetes instalados en el repositorio local o enumera los paquetes disponibles desde un origen de paquete. | All |

| Comandos secundarios | Descripción | Versión de NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Examina todos los ensamblados de la ruta de acceso de salida de un proyecto y agrega redirecciones de enlace a `app.config` o `web.config` cuando sea necesario. | All |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Muestra información sobre el proyecto predeterminado o especificado. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso del paquete especificado. | En desuso en 3.0+ |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Registra una expansión de tabulación para los parámetros de un comando, lo que le permite crear expansiones personalizadas para los valores de parámetro usados habitualmente. | All |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Obtenga la versión del paquete instalado del proyecto especificado y sincronice la versión con el resto de proyectos de la solución. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Quita un paquete de un proyecto y, opcionalmente, quita sus dependencias. | All |

Para obtener ayuda completa y detallada sobre cualquiera de estos comandos dentro de la consola, simplemente ejecute lo siguiente con el nombre del comando en cuestión:

```ps
Get-Help <command> -full
```

Todos los Administrador de paquetes console admiten los siguientes [parámetros comunes de PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)

- Depurar
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Verbose
- WarningAction
- WarningVariable

Para obtener más información, [consulte about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) en la documentación de PowerShell.