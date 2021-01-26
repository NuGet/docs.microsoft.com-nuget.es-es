---
title: Comando de especificación de la CLI de NuGet
description: Referencia del comando nuget.exe Spec
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779148"
---
# <a name="spec-command-nuget-cli"></a>Spec (comando de la CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** la creación de paquetes: todos

Genera un `.nuspec` archivo para un nuevo paquete. Si se ejecuta en la misma carpeta que un archivo de proyecto ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` crea un archivo con tokens `.nuspec` . Para obtener más información, consulte [crear un paquete](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```cli
nuget spec [<packageID>] [options]
```

donde `<packageID>` es un identificador de paquete opcional que se va a guardar en el `.nuspec` archivo.

## <a name="options"></a>Opciones

- **`-AssemblyPath`**

  Especifica la ruta de acceso al ensamblado que se va a usar para los metadatos.

- **`-Force`**

  Sobrescribe cualquier `.nuspec` archivo existente.


- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
