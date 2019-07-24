---
title: Referencia de la interfaz de la línea de comandos (CLI) de NuGet
description: Índice de referencia de la línea de comandos de la CLI de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 52aa2c533a8b67ae10455888a34a7ac9767fd0e3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327472"
---
# <a name="nuget-cli-reference"></a>Referencia de la CLI de NuGet

La interfaz de la línea de comandos (CLI `nuget.exe`) de Nuget,, proporciona el alcance completo de la funcionalidad de Nuget para instalar, crear, publicar y administrar paquetes sin realizar cambios en los archivos del proyecto.

Para usar cualquier comando, abra una ventana de comandos o un shell de Bash `nuget` y, después, ejecute seguido del comando y las `nuget help pack` opciones adecuadas, como (para ver la ayuda del comando Pack).

En esta documentación se refleja la versión más reciente de la CLI de NuGet. Para obtener detalles exactos de cualquier versión determinada que esté usando `nuget help` , ejecute para el comando deseado.

Para obtener información sobre cómo usar comandos básicos con la CLI de `nuget.exe`, consulte [Instalar y usar paquetes mediante la CLI de nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Instalación de Nuget. exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Para que la CLI de NuGet esté disponible en la consola del administrador de paquetes en Visual Studio, consulte [uso de la CLI de Nuget. exe en la consola de](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilidad

Consulte [disponibilidad de características](../install-nuget-client-tools.md#feature-availability) para obtener detalles exactos.

- Todos los comandos están disponibles en Windows.
- Todos los comandos funcionan con Nuget. exe, que se ejecuta en mono `pack`excepto `restore`cuando se `update`indica para, y.
- Los `pack`comandos `restore`, ,`delete` ,`locals`y también`push` están disponibles en Mac y Linux a través de la CLI de dotnet.

## <a name="commands-and-applicability"></a>Comandos y aplicabilidad

Comandos disponibles y aplicabilidad en la creación de paquetes, el consumo de paquetes o la publicación de un paquete en un host:

| Comandos comunes | Roles aplicables | Versión de NuGet | DESCRIPCIÓN |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | Creación | 2.7+ | Crea un paquete de NuGet a `.nuspec` partir de un archivo de proyecto de o. Cuando se ejecuta en mono, no se admite la creación de un paquete a partir de un archivo de proyecto. |
| [push](cli-reference/cli-ref-push.md) | Publicación | Todo | Publica un paquete en un origen del paquete. |
| [config](cli-reference/cli-ref-config.md) | Todo | Todo | Obtiene o establece los valores de configuración de NuGet. |
| [help or ?](cli-reference/cli-ref-help.md) | Todo | Todo | Muestra información de ayuda o ayuda para un comando. |
| [locals](cli-reference/cli-ref-locals.md) | Consumo | 3.3+ | Muestra las ubicaciones de las carpetas *global-Packages*, *http-cache*y *temp* , y borra el contenido de esas carpetas. |
| [restore](cli-reference/cli-ref-restore.md) | Consumo | 2.7+ | Restaura todos los paquetes a los que hace referencia el formato de administración de paquetes en uso. Cuando se ejecuta en mono, no se admite la restauración de paquetes con el formato PackageReference. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Publicación, consumo | Todo | Guarda una clave de API para un origen de paquete determinado cuando el origen del paquete requiere una clave para el acceso. |
| [spec](cli-reference/cli-ref-spec.md) | Creación | Todo | Genera un `.nuspec` archivo mediante tokens si se genera el archivo desde un proyecto de Visual Studio. |

| Comandos secundarios | Roles aplicables | Versión de NuGet | DESCRIPCIÓN |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Publicación | 3.3+ | Agrega un paquete a un origen de paquete no HTTP mediante el diseño jerárquico. En el caso de los orígenes http, use la inserciones. |
| [delete](cli-reference/cli-ref-delete.md) | Publicación | Todo | Quita o elimina de la lista un paquete del origen del paquete. |
| [init](cli-reference/cli-ref-init.md) | Creación | 3.3+ | Agrega paquetes de una carpeta a un origen de paquete mediante el diseño jerárquico. |
| [install](cli-reference/cli-ref-install.md) | Consumo | Todo | Instala un paquete en el proyecto actual, pero no modifica los proyectos ni los archivos de referencia. |
| [lista](cli-reference/cli-ref-list.md) | Consumo, quizás publicar | Todo | Muestra los paquetes de un origen determinado. |
| [mirror](cli-reference/cli-ref-mirror.md) | Publicación | En desuso en 3,2 + | Refleja un paquete y sus dependencias desde un origen a un repositorio de destino. |
| [sources](cli-reference/cli-ref-sources.md) | Consumo, publicación | Todo | Administra orígenes de paquetes en archivos de configuración. |
| [update](cli-reference/cli-ref-update.md) | Consumo | Todo | Actualiza los paquetes de un proyecto a las versiones disponibles más recientes. No se admite cuando se ejecuta en mono. |

Los distintos comandos hacen uso de varias [variables de entorno](cli-reference/cli-ref-environment-variables.md).

Comandos de la CLI de NuGet por roles aplicables:

| Rol | Comandos: |
| --- | --- |
| Consumo | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Creación | `config`, `help`, `init`, `pack`, `spec` |
| Publicación | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Los desarrolladores interesados solo en el consumo de paquetes, por ejemplo, necesitan comprender solo el subconjunto de comandos de NuGet.

> [!Note]
> Los nombres de las opciones de comando no distinguen mayúsculas de minúsculas. Las opciones que están en desuso no se incluyen en esta referencia `NoPrompt` , como (reemplazado por `NonInteractive`) `Verbose` y (reemplazado por `Verbosity`).
