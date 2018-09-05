---
title: Comando de Ayuda de la CLI de NuGet
description: Referencia del comando de Ayuda de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546568"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Comando (NuGet CLI)

**Se aplica a:** todas &bullet; **versiones compatibles de**: todas

General muestra información de ayuda e información acerca de los comandos específicos de ayuda.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

donde [comando] identifica un comando específico para el que se va a mostrar la Ayuda.

> [!Warning]
> Con algunos comandos, esté atento especificar *ayuda* primero, como ocurre con `nuget help install`, porque no hay un paquete denominado "Ayuda" en nuget.org. Si se ejecuta el comando `nuget install help`, no obtener ayuda sobre el comando de instalación, pero en su lugar, se instalará el paquete denominado ayuda.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| Todas | Imprime la ayuda detallada de todos los comandos disponibles; se omite si no se especifica un comando específico. |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Ayuda | Muestra información de ayuda para el propio comando de ayuda. |
| Markdown | Imprimir ayuda detallada en formato de marcado cuando se usa con `-All`. Pasa por alto en caso contrario. |
| No interactivo | Suprime los mensajes para confirmaciones o intervención del usuario. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
