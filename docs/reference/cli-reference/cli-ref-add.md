---
title: Comando Add de la CLI de NuGet
description: Referencia del comando Add de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327862"
---
# <a name="add-command-nuget-cli"></a>Comando add (CLI de NuGet)

**Se aplica a**: &bullet; **versiones compatibles**de publicación de paquetes: 3.3+

Agrega un paquete especificado a un origen de paquete no HTTP (una carpeta o ruta de acceso UNC) en un diseño jerárquico, donde se crean las carpetas para el identificador de paquete y el número de versión. Por ejemplo:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Al restaurar o actualizar en el origen del paquete, el diseño jerárquico proporciona un rendimiento significativamente mejor.

Para expandir todos los archivos del paquete en el origen del paquete de destino, use `-Expand` el modificador. Normalmente, esto da lugar `tools` a la aparición de subcarpetas adicionales en el destino, como y. `lib`

## <a name="usage"></a>Uso

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

donde `<packagePath>` es el directorio del paquete que se va a agregar `<sourcePath>` y especifica el origen del paquete basado en carpeta al que se agregará el paquete. No se admiten los orígenes HTTP.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| Expand | Agrega todos los archivos del paquete al origen del paquete. |
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
