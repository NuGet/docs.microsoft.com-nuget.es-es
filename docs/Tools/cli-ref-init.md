---
title: Comando de NuGet CLI init | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: Referencia del comando de init nuget.exe
keywords: referencia de NuGet init, comando init
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a>comando init (NuGet CLI)

**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** 3.3 +

Copia todos los paquetes de una carpeta sin formato en una carpeta de destino mediante un formato jerárquico como se describe en el [Agregar comando](#add) anteriormente. Es decir, usando `init` equivale a utilizar el `add` comando en cada paquete en la carpeta.

Al igual que con `add`, el destino debe ser una carpeta local o una ruta de acceso UNC; No se admiten los repositorios de paquete HTTP, como nuget.org %s) privada.

## <a name="usage"></a>Uso

```
nuget init <source> <destination> [options]
```

donde `<source>` es la carpeta que contiene paquetes y `<destination>` es la carpeta local o una ruta de acceso UNC a la que se copiarán los paquetes.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Expand | Agrega todos los archivos de cada paquete que se agrega al origen del paquete; igual que `-Expand` con el `add` comando. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
