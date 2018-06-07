---
title: Comando spec NuGet CLI
description: Referencia para el comando spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817091"
---
# <a name="spec-command-nuget-cli"></a>comando spec (NuGet CLI)

**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** todos

Genera un `.nuspec` archivo para un nuevo paquete. Si se ejecutan en la misma carpeta que un archivo de proyecto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un con tokens `.nuspec` archivo. Para obtener más información, consulte [crear un paquete](../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```cli
nuget spec [<packageID>] [options]
```

donde `<packageID>` es un identificador de paquete opcional para guardar en el `.nuspec` archivo.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| AssemblyPath | Especifica la ruta de acceso al ensamblado que se va a usar para los metadatos. |
| Force | Sobrescribe cualquier existente `.nuspec` archivo. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
