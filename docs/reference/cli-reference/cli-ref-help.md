---
title: Comando de ayuda de la CLI de NuGet
description: Referencia del comando de ayuda de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327802"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Comando (NuGet CLI)

**Se aplica a:** todas &bullet; **las versiones compatibles**: todas

Muestra información de ayuda general e información de ayuda acerca de comandos específicos.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

donde [comando] identifica un comando específico para el que se va a mostrar ayuda.

> [!Warning]
> Con algunos comandos, asegúrese de especificar la *ayuda* primero, como con `nuget help install`, ya que hay un paquete denominado "Help" en Nuget.org. Si proporciona el comando `nuget install help`, no obtendrá ayuda sobre el comando de instalación pero, en su lugar, instalará el paquete denominado help.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| Todo | Imprimir ayuda detallada para todos los comandos disponibles; se omite si se especifica un comando específico. |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el propio comando de ayuda. |
| Markdown | Imprima la ayuda detallada en formato Markdown cuando se `-All`use con. Se omite en caso contrario. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
