---
title: Comando de la lista de la CLI de NuGet
description: Referencia del comando de la lista de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549806"
---
# <a name="list-command-nuget-cli"></a>comando de lista (CLI de NuGet)

**Se aplica a:** consumo de paquetes, publicar &bullet; **versiones compatibles:** todas

Muestra una lista de paquetes desde un origen determinado. Si no se especifica ningún origen, todos los orígenes definen en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, se usan. Si `NuGet.Config` no especifica ningún origen, a continuación, `list` utiliza la fuente predeterminada (nuget.org).

## <a name="usage"></a>Uso

```cli
nuget list [search terms] [options]
```

donde los términos de búsqueda opcional filtrarán la lista mostrada. Términos de búsqueda se aplican a los nombres de paquetes, las etiquetas y descripciones de paquetes, tal como aparecen cuando se usen en nuget.org.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| AllVersions | Enumerar todas las versiones de un paquete. De forma predeterminada, se muestra solo la versión más reciente del paquete. |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| IncludeDelisted | *(3.2 y versiones posteriores)*  Muestra los paquetes que están ocultos. |
| No interactivo | Suprime los mensajes para confirmaciones o intervención del usuario. |
| Versión preliminar | Incluye paquetes de versión preliminar en la lista. |
| Origen | Especifica una lista de los orígenes de paquetes para buscar. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
