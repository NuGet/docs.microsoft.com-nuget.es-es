---
title: Comando de NuGet CLI spec | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia para el comando spec nuget.exe
keywords: "referencia de especificación de NuGet, especificaciones de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
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
