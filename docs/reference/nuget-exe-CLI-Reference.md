---
title: Referencia de la interfaz de Command-Line NuGet (CLI)
description: Índice de referencia de la línea de comandos para la CLI de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a9a5fc4d3b1e0f19fa3ea249ca7759c8ebc2d12e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777700"
---
# <a name="nuget-cli-reference"></a>Referencia de la CLI de NuGet

La interfaz de la línea de comandos (CLI) de NuGet, `nuget.exe` , proporciona el alcance completo de la funcionalidad de Nuget para instalar, crear, publicar y administrar paquetes sin realizar cambios en los archivos del proyecto.

Para usar cualquier comando, abra una ventana de comandos o un shell de bash y, después, ejecute `nuget` seguido del comando y las opciones adecuadas, como `nuget help pack` (para ver la ayuda del comando Pack).

En esta documentación se refleja la versión más reciente de la CLI de NuGet. Para obtener detalles exactos de cualquier versión determinada que esté usando, ejecute `nuget help` para el comando deseado.

Para obtener información sobre cómo usar comandos básicos con la CLI de `nuget.exe`, consulte [Instalar y usar paquetes mediante la CLI de nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Instalación de nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Para que la CLI de NuGet esté disponible en la consola del administrador de paquetes en Visual Studio, consulte [uso de la CLI de nuget.exe en la consola de](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilidad

Consulte [disponibilidad de características](../install-nuget-client-tools.md#feature-availability) para obtener detalles exactos.

- Todos los comandos están disponibles en Windows.
- Todos los comandos funcionan con nuget.exe que se ejecutan en mono excepto cuando se indica para `pack` , `restore` y `update` .
- Los `pack` `restore` comandos,, `delete` , `locals` y `push` también están disponibles en Mac y Linux a través de la CLI de dotnet.

## <a name="commands-and-applicability"></a>Comandos y aplicabilidad

Comandos disponibles y aplicabilidad en la creación de paquetes, el consumo de paquetes o la publicación de un paquete en un host:

| Comandos comunes | Roles aplicables | Versión de NuGet | Descripción |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | Creación | 2.7+ | Crea un paquete de NuGet a partir de un `.nuspec` archivo de proyecto de o. Cuando se ejecuta en mono, no se admite la creación de un paquete a partir de un archivo de proyecto. |
| [push](cli-reference/cli-ref-push.md) | Publicación | All | Publica un paquete en un origen del paquete. |
| [config](cli-reference/cli-ref-config.md) | All | All | Obtiene o establece los valores de configuración de NuGet. |
| [help or ?](cli-reference/cli-ref-help.md) | All | All | Muestra información de ayuda o ayuda para un comando. |
| [locals](cli-reference/cli-ref-locals.md) | Consumo | 3.3 + | Muestra las ubicaciones de las carpetas *global-Packages*, *http-cache* y *temp* , y borra el contenido de esas carpetas. |
| [restore](cli-reference/cli-ref-restore.md) | Consumo | 2.7+ | Restaura todos los paquetes a los que hace referencia el formato de administración de paquetes en uso. Cuando se ejecuta en mono, no se admite la restauración de paquetes con el formato PackageReference. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Publicación, consumo | All | Guarda una clave de API para un origen de paquete determinado cuando el origen del paquete requiere una clave para el acceso. |
| [spec](cli-reference/cli-ref-spec.md) | Creación | All | Genera un `.nuspec` archivo mediante tokens si se genera el archivo desde un proyecto de Visual Studio. |

| Comandos secundarios | Roles aplicables | Versión de NuGet | Descripción |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Publicación | 3.3 + | Agrega un paquete a un origen de paquete no HTTP mediante el diseño jerárquico. En el caso de los orígenes HTTP, use la *inserciones*. |
| [delete](cli-reference/cli-ref-delete.md) | Publicación | All | Quita o elimina de la lista un paquete del origen del paquete. |
| [init](cli-reference/cli-ref-init.md) | Creación | 3.3 + | Agrega paquetes de una carpeta a un origen de paquete mediante el diseño jerárquico. |
| [install](cli-reference/cli-ref-install.md) | Consumo | All | Instala un paquete en el proyecto actual, pero no modifica los proyectos ni los archivos de referencia. |
| [list](cli-reference/cli-ref-list.md) | Consumo, quizás publicar | All | Muestra los paquetes de un origen determinado. |
| [mirror](cli-reference/cli-ref-mirror.md) | Publicación | En desuso en 3,2 + | Refleja un paquete y sus dependencias desde un origen a un repositorio de destino. |
| [search](cli-reference/cli-ref-search.md) | Consumo | 5,8 + | Busca un origen determinado mediante la cadena de consulta proporcionada. |
| [sources](cli-reference/cli-ref-sources.md) | Consumo, publicación | All | Administra orígenes de paquetes en archivos de configuración. |
| [update](cli-reference/cli-ref-update.md) | Consumo | All | Actualiza los paquetes de un proyecto a las versiones disponibles más recientes. No se admite cuando se ejecuta en mono. |

Los distintos comandos hacen uso de varias [variables de entorno](cli-reference/cli-ref-environment-variables.md).

Comandos de la CLI de NuGet por roles aplicables:

| Role | Comandos |
| --- | --- |
| Consumo | `config`, `help`, `install`, `list`, `locals`, `restore`, `search`, `setapikey`, `sources`, `update` |
| Creación | `config`, `help`, `init`, `pack`, `spec` |
| Publicación | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Los desarrolladores interesados solo en el consumo de paquetes, por ejemplo, necesitan comprender solo el subconjunto de comandos de NuGet.

> [!Note]
> Los nombres de las opciones de comando no distinguen mayúsculas de minúsculas. Las opciones que están en desuso no se incluyen en esta referencia, como `NoPrompt` (reemplazado por `NonInteractive` ) y `Verbose` (reemplazado por `Verbosity` ).
