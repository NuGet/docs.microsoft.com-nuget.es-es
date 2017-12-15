---
title: Comandos de la Ayuda de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: Referencia para el comando de ayuda nuget.exe
keywords: NuGet ayuda referencia, comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a>¿ayudar a o? comando (NuGet CLI)

**Se aplica a:** todos los &bullet; **versiones compatibles**: todos los

General muestra información de ayuda e información acerca de los comandos específicos de ayuda.

## <a name="usage"></a>Uso

```
nuget help [command] [options]
nuget ? [command] [options]
```

donde [comando] identifica un comando específico para el que se va a mostrar la Ayuda.

> [!Warning]
> Con algunos comandos, esté atento especificar *ayuda* primero, como con `nuget help install`, porque no hay un paquete denominado "help" en nuget.org. Si se ejecuta el comando `nuget install help`, no se podrá obtener ayuda sobre el comando de instalación, pero en su lugar, se instalará el paquete denominado ayuda.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| Todas | Imprimir ayuda detallada acerca de todos los comandos disponibles; se omite si no se especifica un comando específico. |
| ConfigFile | *(2.5 +)*  NuGet el archivo de configuración para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para los comandos de la Ayuda. |
| Markdown | Imprimir ayuda detallada en formato de marcado cuando se utiliza con `-All`. Tecla de método abreviado. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
