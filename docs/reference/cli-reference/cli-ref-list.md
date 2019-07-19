---
title: Comando list de la CLI de NuGet
description: Referencia del comando de lista Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327742"
---
# <a name="list-command-nuget-cli"></a>List (comando) (CLI de NuGet)

**Se aplica a: consumo de** paquetes &bullet; , publicación de **versiones admitidas:** todos

Muestra una lista de paquetes de un origen determinado. Si no se especifica ningún origen, se usan todos los orígenes definidos en el `%AppData%\NuGet\NuGet.Config` archivo de configuración global `~/.nuget/NuGet/NuGet.Config`, (Windows) o. Si `NuGet.Config` no especifica ningún origen `list` , utiliza la fuente predeterminada (Nuget.org).

## <a name="usage"></a>Uso

```cli
nuget list [search terms] [options]
```

donde los términos de búsqueda opcionales filtrarán la lista mostrada. Los términos de búsqueda se aplican a los nombres de los paquetes, etiquetas y descripciones de paquetes tal y como se usan en nuget.org.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| AllVersions | Enumera todas las versiones de un paquete. De forma predeterminada, solo se muestra la versión más reciente del paquete. |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| IncludeDelisted | *(3,2 +)* Muestra los paquetes que no aparecen en la lista. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Versión preliminar | Incluye paquetes de versiones preliminares en la lista. |
| source | Especifica una lista de los orígenes de paquetes que se van a buscar. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
