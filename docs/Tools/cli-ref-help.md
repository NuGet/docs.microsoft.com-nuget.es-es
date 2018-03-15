---
title: Comandos de la Ayuda de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia para el comando de ayuda nuget.exe
keywords: NuGet ayuda referencia, comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 281c6ccc7c58d153280441430be063d9ee89955d
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="help-or--command-nuget-cli"></a>¿ayudar a o? comando (NuGet CLI)

**Se aplica a:** todos los &bullet; **versiones compatibles**: todos los

General muestra información de ayuda e información acerca de los comandos específicos de ayuda.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

donde [comando] identifica un comando específico para el que se va a mostrar la Ayuda.

> [!Warning]
> Con algunos comandos, esté atento especificar *ayuda* primero, como con `nuget help install`, porque no hay un paquete denominado "help" en nuget.org. Si se ejecuta el comando `nuget install help`, no obtener ayuda sobre el comando de instalación, pero en su lugar, se instalará el paquete denominado ayuda.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| Todas | Imprimir ayuda detallada acerca de todos los comandos disponibles; se omite si no se especifica un comando específico. |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para los comandos de la Ayuda. |
| Markdown | Imprimir ayuda detallada en formato de marcado cuando se utiliza con `-All`. Tecla de método abreviado. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
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
