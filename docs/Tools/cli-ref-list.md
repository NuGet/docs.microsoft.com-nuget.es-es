---
title: Comando de lista de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia del comando de lista nuget.exe
keywords: paquetes de lista de referencia de la lista de NuGet, comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="list-command-nuget-cli"></a>comando de lista (NuGet CLI)

**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos

Muestra una lista de paquetes de un origen determinado. Si no se especifica ningún origen, todos los orígenes definen en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config`, se utilizan. Si `NuGet.Config` no especifica ningún origen, a continuación, `list` utiliza la fuente predeterminada (nuget.org).

## <a name="usage"></a>Uso

```cli
nuget list [search terms] [options]
```

donde los términos de búsqueda opcional filtrará la lista que aparece. Términos de búsqueda se aplican a los nombres de paquetes, etiquetas y descripciones de paquete.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| AllVersions | Enumerar todas las versiones de un paquete. De forma predeterminada, se muestra solo la versión más reciente del paquete. |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| IncludeDelisted | *(3.2 +)*  Muestra los paquetes que no figuran en. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Versión preliminar | Incluye paquetes de versión preliminar en la lista. |
| Origen | Especifica una lista de orígenes de paquetes para buscar. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
