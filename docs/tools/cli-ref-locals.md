---
title: Comando de CLI de NuGet locals
description: Referencia para el comando locals de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545033"
---
# <a name="locals-command-nuget-cli"></a>Comando locals (CLI de NuGet)

**Se aplica a:** consumo de paquetes &bullet; **versiones compatibles:** 3.3 +

Borra o enumera recursos locales de NuGet, como el *http-cache*, *global-packages* carpeta y la carpeta temporal. El `locals` también se puede usar el comando para mostrar una lista de esas ubicaciones. Para obtener más información, consulte [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Uso

```cli
nuget locals <folder> [options]
```

donde `<folder>` es uno de `all`, `http-cache`, `packages-cache` *(3.5 y anteriores)*, `global-packages`, `temp` *(3.4 y versiones posteriores)*, y `plugins-cache` *(4.8)*.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| Clear | Borra la carpeta especificada. |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| Lista | Muestra la ubicación de la carpeta especificada, o las ubicaciones de todas las carpetas cuando se usa con *todas*. |
| No interactivo | Suprime los mensajes para confirmaciones o intervención del usuario. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Para obtener ejemplos adicionales, consulte [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).
