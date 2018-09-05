---
title: CLI de NuGet Agregar comando
description: Referencia de nuget.exe Agregar comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545839"
---
# <a name="add-command-nuget-cli"></a>Comando add (CLI de NuGet)

**Se aplica a**: publicación del paquete &bullet; **versiones compatibles de**: 3.3 +

Agrega un paquete específico a un origen de paquete que no sean HTTP (una carpeta o ruta de acceso UNC) en formato jerárquico, en la que se crean las carpetas para el número de identificador y la versión del paquete. Por ejemplo:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Al restaurar o actualizar en el origen del paquete, formato jerárquico proporciona un rendimiento significativamente mejor.

Para expandir todos los archivos en el paquete al origen del paquete de destino, use el `-Expand` cambie. Esto normalmente da como resultado de las subcarpetas adicionales que aparecen en el destino, como `tools` y `lib`.

## <a name="usage"></a>Uso

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

donde `<packagePath>` es la ruta de acceso al paquete para agregar, y `<sourcePath>` especifica el origen del paquete basada en la carpeta a la que se agregará el paquete. No se admiten orígenes de HTTP.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| Expand | Agrega todos los archivos en el paquete en el origen del paquete. |
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para confirmaciones o intervención del usuario. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
