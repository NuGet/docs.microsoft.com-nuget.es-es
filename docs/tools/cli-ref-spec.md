---
title: Comando de CLI de NuGet spec
description: Referencia para el comando spec nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546454"
---
# <a name="spec-command-nuget-cli"></a>especificación de comandos (CLI de NuGet)

**Se aplica a:** la creación del paquete &bullet; **versiones compatibles:** todas

Genera un `.nuspec` archivo para un nuevo paquete. Si se ejecutan en la misma carpeta que un archivo de proyecto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un con tokens `.nuspec` archivo. Para obtener más información, consulte [creación de un paquete](../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```cli
nuget spec [<packageID>] [options]
```

donde `<packageID>` es un identificador de paquete opcional para guardar en el `.nuspec` archivo.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| AssemblyPath | Especifica la ruta de acceso al ensamblado que se usará para los metadatos. |
| Force | Sobrescribe cualquier existente `.nuspec` archivo. |
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para confirmaciones o intervención del usuario. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
