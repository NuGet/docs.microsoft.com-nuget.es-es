---
title: "Referencia de la interfaz de línea de comandos (CLI) de NuGet | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Índice de la referencia de línea de comandos para la nuget.exe CLI"
keywords: "índice de referencia NuGet.exe, interfaz de línea de comandos nuget.exe, nuget.exe CLI, comando de nuget"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8b1ee17702f5a54a77dc2cd663e13729a9b4a39f
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-cli-reference"></a>Referencia de NuGet CLI

La interfaz de línea de comandos de NuGet (CLI), `nuget.exe`, proporciona el alcance total de la funcionalidad de NuGet para instalar, crear, publicar y administrar los paquetes sin realizar ningún cambio en los archivos de proyecto.

Para utilizar cualquier comando, abra una ventana de comandos o el shell de bash y luego ejecutar `nuget` seguido por el comando y opciones adecuadas, como `nuget help pack` (para ver la ayuda sobre el comando pack).

Esta documentación refleja la versión más reciente de NuGet CLI. Para obtener detalles exactos para cualquier versión concreta que esté usando, ejecute `nuget help` para el comando deseado.

## <a name="installing-nugetexe"></a>Instalar nuget.exe

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Tip]
> Para disponer de la CLI de NuGet dentro de la consola de administrador de paquetes en Visual Studio, vea [mediante la CLI nuget.exe en la consola de](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilidad

Vea [disponibilidad de las funciones](../install-nuget-client-tools.md#feature-availability) para obtener detalles exactos.

- Todos los comandos están disponibles en Windows.
- Todos los comandos funcionan con nuget.exe quedando Mono excepto cuando se indique para `pack`, `restore`, y `update`.
- El `pack`, `restore`, `delete`, `locals`, y `push` comandos también están disponibles en Mac y Linux a través de la CLI de dotnet.

## <a name="commands-and-applicability"></a>Comandos y aplicabilidad

Comandos disponibles y aplicabilidad a la creación del paquete, el consumo de paquete o publicar un paquete a un host:

| Comandos comunes | Roles aplicables | Versión de NuGet | Descripción |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Creación | 2.7+ | Crea un paquete de NuGet desde un `.nuspec` o un archivo de proyecto. Cuando se ejecuta en Mono, no se admite la creación de un paquete desde un archivo de proyecto. |
| [push](cli-ref-push.md) | Publicación | Todas | Publica un paquete a un origen de paquete. |
| [config](cli-ref-config.md) | Todas | Todas | Obtiene o establece los valores de configuración de NuGet. |
| [help or ?](cli-ref-help.md) | Todas | Todas | Muestra la Ayuda información o ayuda para un comando. |
| [locals](cli-ref-locals.md) | Consumo | 3.3+ | Borra o enumera los paquetes en varias memorias caché o en la carpeta de paquetes global o identifica esas carpetas. |
| [restore](cli-ref-restore.md) | Consumo | 2.7+ | Restaura todos los paquetes al que hace referencia el formato de referencia de paquete en uso. Cuando se ejecuta en Mono, no se admite la restauración de paquetes con el formato PackageReference. |
| [setapikey](cli-ref-setapikey.md) | Publicación de consumo | Todas | Guarda una clave de API para un determinado paquete de origen cuando ese origen del paquete requiere una clave de acceso. |
| [spec](cli-ref-spec.md) | Creación | Todas | Genera un `.nuspec` archivo, utilizando tokens si genera el archivo desde un proyecto de Visual Studio. |

| Comandos secundarios | Roles aplicables | Versión de NuGet | Descripción |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publicación | 3.3+ | Agrega un paquete a un origen de paquete no HTTP con formato jerárquico. Para los orígenes HTTP, utilice *inserción*. |
| [delete](cli-ref-delete.md) | Publicación | Todas | Quita o unlists un paquete desde un origen del paquete. |
| [init](cli-ref-init.md) | Creación | 3.3+ | Agrega paquetes desde una carpeta a un origen de paquete con formato jerárquico. |
| [install](cli-ref-install.md) | Consumo | Todas | Instala un paquete en el actual proyecto pero no modificar proyectos o hacen referencia a archivos. |
| [list](cli-ref-list.md) | Consumo, es posible publicar | Todas | Muestra los paquetes de un origen determinado. |
| [mirror](cli-ref-mirror.md) | Publicación | En desuso en 3.2 + | Refleja un paquete y sus dependencias de un origen en un repositorio de destino. |
| [sources](cli-ref-sources.md) | Consumo, publicar | Todas | Administra los orígenes de paquetes en archivos de configuración. |
| [update](cli-ref-update.md) | Consumo | Todas | Actualiza los paquetes del proyecto para las últimas versiones disponibles. No se admite cuando se ejecuta en Mono. |

Asegúrese de comandos diferentes que el uso de varios [variables de entorno](cli-ref-environment-variables.md).

Comandos de CLI de NuGet roles aplicables:

| Rol | Comandos |
| --- | --- |
| Consumo | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Creación | `config`, `help`, `init`, `pack`, `spec` |
| Publicación | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Los programadores preocupados solo con el consumo de paquetes, por ejemplo, solo necesitan comprender ese subconjunto de comandos de NuGet.

> [!Note]
> Los nombres de opción de comando distinguen mayúsculas de minúsculas. No se incluyen opciones que están en desuso en esta referencia, como `NoPrompt` (reemplazado por `NonInteractive`) y `Verbose` (reemplazado por `Verbosity`).
