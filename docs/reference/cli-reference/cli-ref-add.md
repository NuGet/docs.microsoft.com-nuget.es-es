---
title: Comando Add de la CLI de NuGet
description: Referencia del comando nuget.exe Add
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622907"
---
# <a name="add-command-nuget-cli"></a>Add (comando) (CLI de NuGet)

**Se aplica a**: &bullet; **versiones compatibles**de publicación de paquetes: 3.3 +

Agrega un paquete especificado a un origen de paquete no HTTP (una carpeta o ruta de acceso UNC) en un diseño jerárquico, donde se crean las carpetas para el identificador de paquete y el número de versión. Por ejemplo:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

Al restaurar o actualizar en el origen del paquete, el diseño jerárquico proporciona un rendimiento significativamente mejor.

Para expandir todos los archivos del paquete en el origen del paquete de destino, use el `-Expand` modificador. Normalmente, esto da lugar a la aparición de subcarpetas adicionales en el destino, como `tools` y `lib` .

## <a name="usage"></a>Uso

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

donde `<packagePath>` es el directorio del paquete que se va a agregar y `<sourcePath>` especifica el origen del paquete basado en carpeta al que se agregará el paquete. No se admiten los orígenes HTTP.

## <a name="options"></a>Opciones

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Expand`**

  Agrega todos los archivos del paquete al origen del paquete.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.
Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-src|-Source`**

   Especifica el origen del paquete, que es una carpeta o un recurso compartido UNC, al que se agregará el nupkg. No se admiten los orígenes http.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
