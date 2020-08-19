---
title: Comando init de la CLI de NuGet
description: Referencia del comando nuget.exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623089"
---
# <a name="init-command-nuget-cli"></a>comando init (CLI de NuGet)

**Se aplica a:** versiones compatibles de creación de paquetes &bullet; **:** 3.3 +

Copia todos los paquetes de una carpeta plana en una carpeta de destino mediante un diseño jerárquico, tal como se describe en el [comando agregar](cli-ref-add.md). Es decir, el uso de `init` es equivalente al uso del `add` comando en cada paquete de la carpeta.

Al igual que con `add` , el destino debe ser una carpeta local o una ruta de acceso UNC; No se admiten repositorios de paquetes HTTP, como nuget.org o servidores privados.

## <a name="usage"></a>Uso

```cli
nuget init <source> <destination> [options]
```

donde `<source>` es la carpeta que contiene los paquetes y `<destination>` es la carpeta local o el directorio UNC en el que se copian los paquetes.

## <a name="options"></a>Opciones

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Expand`**

  Agrega todos los archivos de cada paquete que se agregan al origen del paquete. igual que `-Expand` con el `add` comando.

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
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
