---
title: Comando variables locales de la CLI de NuGet
description: Referencia del comando de variables locales de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327812"
---
# <a name="locals-command-nuget-cli"></a>Comando locals (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 3.3+

Borra o muestra los recursos de NuGet locales, como la carpeta *http-cache*, *global-Packages* y la carpeta Temp. El `locals` comando también se puede usar para mostrar una lista de esas ubicaciones. Para obtener más información, vea [administrar paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Uso

```cli
nuget locals <folder> [options]
```

donde `<folder>` es uno de `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 y anteriores)* ,, *(3.4 +)* y *(4.8 +)* .

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| Clear | Borra la carpeta especificada. |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| Enumerar | Muestra la ubicación de la carpeta especificada o las ubicaciones de todas las carpetas cuando se usa con *todos*. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Para obtener más ejemplos, consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
