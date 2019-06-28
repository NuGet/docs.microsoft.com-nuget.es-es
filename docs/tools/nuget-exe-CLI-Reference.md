---
title: Referencia de la interfaz de línea de comandos (CLI) de NuGet
description: Índice de la referencia de línea de comandos para la CLI de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a257dbbd9d56b5989e050ed4096d096cd1036184
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426018"
---
# <a name="nuget-cli-reference"></a>Referencia de CLI de NuGet

La interfaz de línea de comandos (CLI de NuGet), `nuget.exe`, proporciona el alcance total de las funcionalidades de NuGet para instalar, crear, publicar y administrar los paquetes sin realizar cambios en los archivos de proyecto.

Para utilizar cualquier comando, abra una ventana de comandos o el shell de bash y ejecute `nuget` seguido por el comando y las opciones adecuadas, como `nuget help pack` (para ver la Ayuda en el comando pack).

Esta documentación refleja la versión más reciente de la CLI de NuGet. Para obtener información exacta para cualquier versión concreta que esté usando, ejecute `nuget help` para el comando deseado.

Para obtener información sobre cómo usar los comandos básicos con el `nuget.exe` CLI, consulte [instalar y usar paquetes mediante la CLI de nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Instalación de nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Para que la CLI de NuGet disponible dentro de la consola de administrador de paquetes en Visual Studio, consulte [mediante la CLI de nuget.exe en la consola de](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilidad

Consulte [disponibilidad de características](../install-nuget-client-tools.md#feature-availability) para ver los detalles exactos.

- Todos los comandos están disponibles en Windows.
- Todos los comandos que funcionan con nuget.exe ejecutándose en Mono, excepto cuando se indique para `pack`, `restore`, y `update`.
- El `pack`, `restore`, `delete`, `locals`, y `push` comandos también están disponibles en Mac y Linux mediante la CLI de dotnet.

## <a name="commands-and-applicability"></a>Comandos y aplicabilidad

Los comandos disponibles y aplicabilidad a creación de paquetes, consumo de paquetes o publicar un paquete a un host:

| Comandos comunes | Roles aplicables | Versión de NuGet | Descripción |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Creación de | 2.7+ | Crea un paquete de NuGet desde una `.nuspec` o archivo de proyecto. Cuando se ejecuta en Mono, no se admite la creación de un paquete desde un archivo de proyecto. |
| [push](cli-ref-push.md) | Publicación | Todas | Publica un paquete en un origen del paquete. |
| [config](cli-ref-config.md) | Todas | Todas | Obtiene o establece los valores de configuración de NuGet. |
| [help or ?](cli-ref-help.md) | Todas | Todas | Muestra la información o ayuda para un comando de ayuda. |
| [locals](cli-ref-locals.md) | Consumo | 3.3+ | Se enumeran las ubicaciones de la *global-packages*, *http-cache*, y *temp* carpetas y borra el contenido de esas carpetas. |
| [restore](cli-ref-restore.md) | Consumo | 2.7+ | Restaura todos los paquetes que se hace referencia el formato de paquete de administración en uso. Cuando se ejecuta en Mono, no se admite la restauración de paquetes con el formato PackageReference. |
| [setapikey](cli-ref-setapikey.md) | Publicación de consumo | Todas | Guarda una clave de API para un origen de paquete determinado cuando ese origen del paquete requiere una clave para el acceso. |
| [spec](cli-ref-spec.md) | Creación de | Todas | Genera un `.nuspec` de archivos, mediante los tokens si generar el archivo de un proyecto de Visual Studio. |

| Comandos secundarios | Roles aplicables | Versión de NuGet | Descripción |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publicación | 3.3+ | Agrega un paquete a un origen de paquete que no sea HTTP con formato jerárquico. Para los orígenes HTTP, utilice *inserción*. |
| [delete](cli-ref-delete.md) | Publicación | Todas | Elimina o quita un paquete desde un origen del paquete de la lista. |
| [init](cli-ref-init.md) | Creación de | 3.3+ | Agrega paquetes desde una carpeta a un origen de paquete con formato jerárquico. |
| [install](cli-ref-install.md) | Consumo | Todas | Instala un paquete en el actual del proyecto, pero no modifica los proyectos o hacen referencia a archivos. |
| [lista](cli-ref-list.md) | Consumo, quizás de publicación | Todas | Muestra los paquetes desde un origen determinado. |
| [mirror](cli-ref-mirror.md) | Publicación | En desuso en 3.2 y versiones posteriores | Refleja un paquete y sus dependencias de un origen a un repositorio de destino. |
| [sources](cli-ref-sources.md) | Consumo, publicar | Todas | Administra los orígenes de paquetes en archivos de configuración. |
| [update](cli-ref-update.md) | Consumo | Todas | Actualiza los paquetes de un proyecto a las últimas versiones disponibles. No se admite cuando se ejecuta en Mono. |

Distintos comandos hacer uso de varios [variables de entorno](cli-ref-environment-variables.md).

Comandos de CLI de NuGet por roles aplicables:

| Rol | Comandos |
| --- | --- |
| Consumo | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Creación de | `config`, `help`, `init`, `pack`, `spec` |
| Publicación | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Los desarrolladores que se trate únicamente con el consumo de paquetes, por ejemplo, sólo necesitan comprender ese subconjunto de comandos de NuGet.

> [!Note]
> Los nombres de opción de comando distinguen mayúsculas de minúsculas. No se incluyen opciones que están en desuso en esta referencia, como `NoPrompt` (reemplazado por `NonInteractive`) y `Verbose` (reemplazado por `Verbosity`).
