---
title: Comando de NuGet CLI variables locales
description: Referencia del comando de variables locales nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a>comando de variables locales (NuGet CLI)

**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** 3.3 +

Borra o se enumeran los recursos de NuGet locales como el *caché http*, *global paquetes* carpeta y la carpeta temporal. El `locals` comando también se puede usar para mostrar una lista de esas ubicaciones. Para obtener más información, consulte [administrar los paquetes globales y las carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Uso

```cli
nuget locals <folder> [options]
```

donde `<folder>` es uno de los `all`, `http-cache`, `packages-cache` *(3.5 y versiones anteriores)*, `global-packages`, y `temp` *(3.4 +)*.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| Clear | Borra la carpeta especificada. |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| Lista | Muestra la ubicación de la carpeta especificada o las ubicaciones de todas las carpetas cuando se usa con *todos los*. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Para obtener ejemplos adicionales, vea [administrar los paquetes globales y las carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).
