---
title: Comando de NuGet CLI spec | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: Referencia para el comando spec nuget.exe
keywords: "referencia de especificación de NuGet, especificaciones de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>comando spec (NuGet CLI)

**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** todos

Genera un `.nuspec` archivo para un nuevo paquete. Si se ejecutan en la misma carpeta que un archivo de proyecto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un con tokens `.nuspec` archivo. Para obtener más información, consulte [crear un paquete](../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```
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
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
