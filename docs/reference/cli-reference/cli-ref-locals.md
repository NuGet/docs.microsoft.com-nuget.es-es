---
title: Comando variables locales de la CLI de NuGet
description: Referencia del comando nuget.exe variables locales
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779197"
---
# <a name="locals-command-nuget-cli"></a>comando variables locales (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 3.3 +

Borra o muestra los recursos de NuGet locales, como la carpeta *http-cache*, *global-Packages* y la carpeta Temp. El `locals` comando también se puede usar para mostrar una lista de esas ubicaciones. Para obtener más información, vea [administrar paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Uso

```cli
nuget locals <folder> [options]
```

donde `<folder>` es uno de `all` , `http-cache` , `packages-cache` *(3,5 y anteriores)*, `global-packages` , `temp` *(3.4 +)* y `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Opciones

- **`-Clear`**

  Borra la carpeta especificada.

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-List`**

  Muestra la ubicación de la carpeta especificada o las ubicaciones de todas las carpetas cuando se usa con *todos*.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Para obtener más ejemplos, consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
