---
title: Referencia de PowerShell de NuGet
description: La referencia completa a los comandos de PowerShell disponibles en la consola de administrador de paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 425ba736eba4609ebd6b5185ae3f1f976ab07a67
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842564"
---
# <a name="powershell-reference"></a>Referencia de PowerShell

La consola de administrador de paquetes proporciona una interfaz de PowerShell en Visual Studio en Windows para interactuar con NuGet a través de los comandos específicos que se enumeran a continuación. (La consola no está actualmente disponible en Visual Studio para Mac.) Para obtener una guía de uso de la consola, consulte [instalar y administrar paquetes mediante la consola de administrador de paquetes](../tools/package-manager-console.md) tema.

> [!Tip]
> Todos los comandos de PowerShell se relacionan con solo consumo de paquetes. No hay comandos de PowerShell están relacionados con la creación y publicación de paquetes, excepto en la medida en que un paquete también puede ser un consumidor de otros paquetes.

> [!Important]
> Los comandos enumerados aquí son específicos de la consola de administrador de paquetes en Visual Studio y diferir la [comandos del módulo de administración de paquetes](/powershell/module/packagemanagement/?view=powershell-6) que están disponibles en un entorno de PowerShell general. En concreto, cada entorno tiene comandos que no están disponibles en el otro, y comandos con el mismo nombre también pueden diferir en sus argumentos específicos. Cuando se usa la consola de administración de paquetes en Visual Studio, se aplican los comandos y argumentos que se documentan en este tema.

| Comandos comunes | DESCRIPCIÓN | Versión de NuGet |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Instalar un paquete y sus dependencias en el proyecto. | Todo |
| [Update-Package](ps-ref-update-package.md) | Actualiza un paquete y sus dependencias o todos los paquetes en un proyecto. | Todo |
| [Find-Package](ps-ref-find-package.md) | Busca un origen del paquete con un identificador de paquete o palabras clave. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Recupera la lista de los paquetes instalados en el repositorio local, o enumera los paquetes disponibles desde un origen del paquete. | Todo |

| Comandos secundarios | DESCRIPCIÓN | Versión de NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Examina todos los ensamblados en la ruta de acceso de salida para un proyecto y agregar redirecciones de enlaces para el `app.config` o `web.config` cuando sea necesario. | Todo |
| [Get-Project](ps-ref-get-project.md) | Muestra información sobre el valor predeterminado o el proyecto especificado. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso de informes para el paquete especificado. | En desuso en 3.0 + |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Registra una expansión de pestañas para los parámetros de un comando, lo que permite crear personalizadas expansiones para los valores de parámetro usados. | Todo |
| [Sync-Package](ps-ref-sync-package.md) | Get instalada la versión del paquete de especifica el proyecto y sincroniza la versión para el resto de los proyectos de la solución. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Quita un paquete desde un proyecto, quitar, opcionalmente, sus dependencias. | Todo |

Para obtener ayuda completa y detallada en cualquiera de estos comandos dentro de la consola, simplemente ejecute lo siguiente con el nombre del comando en cuestión:

```ps
Get-Help <command> -full
```

Todos los comandos de la consola de administrador de paquetes admiten lo siguiente [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

- Depuración
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Detallado
- WarningAction
- WarningVariable

Para obtener más información, consulte [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) en la documentación de PowerShell.
