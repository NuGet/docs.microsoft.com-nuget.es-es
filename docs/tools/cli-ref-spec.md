---
title: Comando de CLI de NuGet spec
description: Referencia para el comando spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794156"
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
