---
title: Referencia de PowerShell de NuGet | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: La referencia completa a los comandos de PowerShell disponibles en la consola de administrador de paquetes de NuGet en Visual Studio.
keywords: NuGet paquete consola del administrador, comandos de NuGet Powershell, referencia de NuGet Powershell
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0da5c88447784fdd49d824bbd03b11f73c22ebc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-reference"></a>Referencia de PowerShell

La consola de administrador de paquetes proporciona una interfaz de PowerShell dentro de Visual Studio en Windows para interactuar con NuGet a través de los comandos específicos que se enumeran a continuación. (La consola no está actualmente disponible en Visual Studio para Mac.) Para obtener una guía para usar la consola, consulte el [Package Manager Console](../tools/package-manager-console.md) tema.

> [!Tip]
> Todos los comandos de PowerShell se refieren sólo al consumo de paquete. Ningún comando de PowerShell se relacionan con la creación y publicación de paquetes excepto en la medida en que un paquete también puede ser un consumidor de otros paquetes.

> [!Important]
> Los comandos enumerados aquí son específicos de la consola de administrador de paquetes en Visual Studio y se diferencian el [comandos del módulo de administración de paquetes](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) que están disponibles en un entorno de PowerShell general. En concreto, cada entorno tiene comandos que no están disponibles en la otra, y comandos con el mismo nombre también pueden diferir en sus argumentos específicos. Al usar la consola de administración de paquetes en Visual Studio, se aplican los comandos y argumentos que se documentan en este tema está presente.

| Comandos comunes | Descripción | Versión de NuGet |
| --- | --- | --- |
| [Paquete de instalación](ps-ref-install-package.md) | Instala un paquete y sus dependencias en el proyecto. | Todas |
| [Paquete de actualización](ps-ref-update-package.md) | Actualiza un paquete y sus dependencias o todos los paquetes en un proyecto. | Todas |
| [Find-Package](ps-ref-find-package.md) | Busca en un origen de paquete con un identificador de paquete o palabras clave. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Recupera la lista de paquetes instalados en el repositorio local o enumera los paquetes disponibles en un origen del paquete. | Todas |

| Comandos secundarios | Descripción | Versión de NuGet |
| --- | --- | --- |
| [Agregar redirección de enlace](ps-ref-add-bindingredirect.md) | Examina todos los ensamblados de la ruta de acceso de salida para un proyecto y agrega redirecciones de enlace para el `app.config` o `web.config` cuando sea necesario. | Todas |
| [Obtener proyecto](ps-ref-get-project.md) | Muestra información sobre el valor predeterminado o el proyecto especificado. | 3.0+ |
| [Abrir página del paquete](ps-ref-open-packagepage.md) | Inicia el explorador predeterminado con el proyecto, la licencia o la dirección URL de abuso de informes para el paquete especificado. | En desuso en 3.0 + |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Registra una expansión de pestañas para los parámetros de un comando, lo que le permite crear personalizadas expansiones para los valores de parámetro usados con frecuencia. | Todas |
| [Paquete de sincronización](ps-ref-sync-package.md) | Get instalada la versión del paquete de especifica el proyecto y sincroniza la versión para el resto de proyectos de la solución. | 3.0+ |
| [Paquete de desinstalación](ps-ref-uninstall-package.md) | Quita un paquete desde un proyecto, si lo desea quitar sus dependencias. | Todas |

Para obtener ayuda detallada completa en cualquiera de estos comandos dentro de la consola, simplemente ejecute lo siguiente con el nombre de comando en cuestión:

```ps
Get-Help <command> -full
```

Todos los comandos de la consola de administrador de paquetes son compatibles con los siguientes [parámetros comunes de PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

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
