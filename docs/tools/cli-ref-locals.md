---
title: Comando de NuGet CLI variables locales
description: Referencia del comando de variables locales nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818206"
---
# <a name="locals-command-nuget-cli"></a>Comando locals (CLI de NuGet)

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
