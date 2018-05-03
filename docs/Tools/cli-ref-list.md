---
title: Comando de lista de NuGet CLI
description: Referencia del comando de lista nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a>comando de lista (NuGet CLI)

**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos

Muestra una lista de paquetes de un origen determinado. Si no se especifica ningún origen, todos los orígenes definen en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, se utilizan. Si `NuGet.Config` no especifica ningún origen, a continuación, `list` utiliza la fuente predeterminada (nuget.org).

## <a name="usage"></a>Uso

```cli
nuget list [search terms] [options]
```

donde los términos de búsqueda opcional filtrará la lista que aparece. Términos de búsqueda se aplican a los nombres de paquetes, etiquetas y descripciones de paquete tal como aparecen cuando se usen en nuget.org.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| AllVersions | Enumerar todas las versiones de un paquete. De forma predeterminada, se muestra solo la versión más reciente del paquete. |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.|
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

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
