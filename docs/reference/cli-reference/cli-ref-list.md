---
title: Comando list de la CLI de NuGet
description: Referencia del comando de lista Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813343"
---
# <a name="list-command-nuget-cli"></a>List (comando) (CLI de NuGet)

**Se aplica a: consumo de** paquetes, publicación &bullet; **versiones admitidas:** todos

Muestra una lista de paquetes de un origen determinado. Si no se especifica ningún origen, se usan todos los orígenes definidos en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`. Si `NuGet.Config` no especifica ningún origen, `list` utiliza la fuente predeterminada (nuget.org).

## <a name="usage"></a>Usage

```cli
nuget list [search terms] [options]
```

donde los términos de búsqueda opcionales filtrarán la lista mostrada. Los términos de búsqueda se aplican a los nombres de los paquetes, etiquetas y descripciones de paquetes tal y como se usan en nuget.org.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| AllVersions | Enumera todas las versiones de un paquete. De forma predeterminada, solo se muestra la versión más reciente del paquete. |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, se usa `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Ayuda de | Muestra información de ayuda para el comando. |
| IncludeDelisted | *(3,2 +)* Muestra los paquetes que no aparecen en la lista. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| PreRelease | Incluye paquetes de versiones preliminares en la lista. |
| Origen | Especifica una lista de los orígenes de paquetes que se van a buscar. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

Enumerar todos los paquetes de las fuentes configuradas:
```
nuget list
```
Enumere los paquetes relacionados con Azure con un nivel de detalle detallado:
```
nuget list Azure -Verbosity detailed
```
Enumerar todas las versiones de los paquetes relacionados con Azure de las fuentes configuradas:
```
nuget list Azure -AllVersions
```
Enumerar todas las versiones de los paquetes relacionados con JSON desde el origen o la fuente especificados:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Enumerar los paquetes relacionados con JSON de varios orígenes y fuentes:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

