---
title: Comando de variables locales de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: Referencia del comando de variables locales nuget.exe
keywords: referencia de variables locales de NuGet, comandos de variables locales
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a>comando de variables locales (NuGet CLI)

**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** 3.3 +

Borra o listas de recursos locales de NuGet, como la memoria caché de la solicitud http y caché de paquetes, la carpeta paquetes global de todo el equipo. El `locals` comando también se puede usar para mostrar una lista de esas ubicaciones. Para obtener más información, consulte [administrar la memoria NuGet caché](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Uso

```
nuget locals <cache> [options]
```

donde `<cache>` es uno de los `all`, `http-cache`, `packages-cache`, `global-packages`, y `temp` *(3.4 +)*.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| Clear | Borra la memoria caché especificada. |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| Lista | Muestra la ubicación de la memoria caché especificada o las ubicaciones de todas las memorias caché cuando se usa con *todos los*. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget locals all -list
nuget locals http-cache -clear
```
