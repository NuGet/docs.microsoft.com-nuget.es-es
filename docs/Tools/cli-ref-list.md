---
title: Comando de lista de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: Referencia del comando de lista nuget.exe
keywords: paquetes de lista de referencia de la lista de NuGet, comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>comando de lista (NuGet CLI)

**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos

Muestra una lista de paquetes de un origen determinado. Si no se especifica ningún origen, todos los orígenes definen en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config`, se utilizan. Si `NuGet.Config` no especifica ningún origen, a continuación, `list` utiliza la fuente predeterminada (nuget.org).

## <a name="usage"></a>Uso

```
nuget list [search terms] [options]
```

donde los términos de búsqueda opcional filtrará la lista que aparece. Términos de búsqueda se aplican a los nombres de paquetes, etiquetas y descripciones de paquete.

## <a name="options"></a>Opciones
| Opción | Descripción |
| --- | --- |
| AllVersions | Enumerar todas las versiones de un paquete. De forma predeterminada, se muestra solo la versión más reciente del paquete. |
| ConfigFile | *(2.5 +)*  NuGet el archivo de configuración para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| IncludeDelisted | *(3.2 +)*  Muestra los paquetes que no figuran en. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Versión preliminar | Incluye paquetes de versión preliminar en la lista. |
| Origen | Especifica una lista de orígenes de paquetes para buscar. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
