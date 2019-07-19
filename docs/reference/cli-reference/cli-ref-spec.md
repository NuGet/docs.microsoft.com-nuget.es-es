---
title: Comando de especificación de la CLI de NuGet
description: Referencia del comando de especificación de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327572"
---
# <a name="spec-command-nuget-cli"></a>Spec (comando de la CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** la creación de paquetes: todos

Genera un `.nuspec` archivo para un nuevo paquete. Si se ejecuta en la misma carpeta que un archivo de`.csproj`proyecto `.vbproj`( `.fsproj`,, `spec` ), crea un `.nuspec` archivo con tokens. Para obtener más información, consulte [crear un paquete](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```cli
nuget spec [<packageID>] [options]
```

donde `<packageID>` es un identificador de paquete opcional que se va a `.nuspec` guardar en el archivo.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| AssemblyPath | Especifica la ruta de acceso al ensamblado que se va a usar para los metadatos. |
| Aplica | Sobrescribe cualquier archivo existente `.nuspec` . |
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
