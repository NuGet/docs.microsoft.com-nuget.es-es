---
title: Comando list de la CLI de NuGet
description: Referencia del comando list de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780054"
---
# <a name="list-command-nuget-cli"></a>List (comando) (CLI de NuGet)

**Se aplica a: consumo de** paquetes, publicación de &bullet; **versiones admitidas:** todos

Muestra una lista de paquetes de un origen determinado. Si no se especifica ningún origen, se usan todos los orígenes definidos en el archivo de configuración global, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` . Si `NuGet.Config` no especifica ningún origen, `list` utiliza la fuente predeterminada (Nuget.org).

## <a name="usage"></a>Uso

```cli
nuget list [search terms] [options]
```

donde los términos de búsqueda opcionales filtrarán la lista mostrada. Los [términos de búsqueda](../../consume-packages/finding-and-choosing-packages.md#search-syntax) se aplican a los nombres de los paquetes, etiquetas y descripciones de paquetes tal y como se usan en Nuget.org. 

## <a name="options"></a>Opciones

- **`-AllVersions`**

  Enumera todas las versiones de un paquete. De forma predeterminada, solo se muestra la versión más reciente del paquete.

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-IncludeDelisted`**

  *(3,2 +)* Muestra los paquetes que no aparecen en la lista.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-PreRelease`**

  Incluye paquetes de versiones preliminares en la lista.

- **`-Source`**

  Origen del paquete que se va a buscar. Puede especificar varios orígenes mediante la `-Source` opción varias veces.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

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
