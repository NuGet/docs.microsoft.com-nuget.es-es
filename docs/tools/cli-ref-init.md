---
title: Comando de CLI de NuGet init
description: Referencia del comando de init de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551415"
---
# <a name="init-command-nuget-cli"></a>Init comandos (CLI de NuGet)

**Se aplica a:** la creación del paquete &bullet; **versiones compatibles:** 3.3 +

Copia todos los paquetes de una carpeta sin formato en una carpeta de destino mediante un formato jerárquico como se describió para la [Agregar comando](cli-ref-add.md). Es decir, usando `init` equivale a usar el `add` comando en cada paquete en la carpeta.

Igual que con `add`, el destino debe ser una carpeta local o una ruta de acceso UNC; No se admiten los repositorios de paquetes HTTP como nuget.org o servidores privados.

## <a name="usage"></a>Uso

```cli
nuget init <source> <destination> [options]
```

donde `<source>` es la carpeta que contiene paquetes y `<destination>` es la carpeta local o una ruta de acceso UNC a la que se copian los paquetes.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Expand | Agrega todos los archivos de cada paquete que se agrega al origen del paquete; igual que `-Expand` con el `add` comando. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para confirmaciones o intervención del usuario. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
