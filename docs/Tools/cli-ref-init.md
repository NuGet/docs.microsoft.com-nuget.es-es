---
title: Comando de NuGet CLI init | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia del comando de init nuget.exe
keywords: referencia de NuGet init, comando init
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="init-command-nuget-cli"></a>comando init (NuGet CLI)

**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** 3.3 +

Copia todos los paquetes de una carpeta sin formato en una carpeta de destino mediante un formato jerárquico como se describe en el [Agregar comando](cli-ref-add.md). Es decir, usando `init` equivale a utilizar el `add` comando en cada paquete en la carpeta.

Al igual que con `add`, el destino debe ser una carpeta local o una ruta de acceso UNC; No se admiten los repositorios de paquete HTTP, como nuget.org %s) privada.

## <a name="usage"></a>Uso

```cli
nuget init <source> <destination> [options]
```

donde `<source>` es la carpeta que contiene paquetes y `<destination>` es la carpeta local o una ruta de acceso UNC a la que se copian los paquetes.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Expand | Agrega todos los archivos de cada paquete que se agrega al origen del paquete; igual que `-Expand` con el `add` comando. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
