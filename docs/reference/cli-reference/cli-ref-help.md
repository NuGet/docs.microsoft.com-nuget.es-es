---
title: Comando de ayuda de la CLI de NuGet
description: Referencia del comando ayuda de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779350"
---
# <a name="help-or--command-nuget-cli"></a>help o ? comando (CLI de NuGet)

**Se aplica a:** todas &bullet; **las versiones compatibles**: todas

Muestra información de ayuda general e información de ayuda acerca de comandos específicos.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

donde [comando] identifica un comando específico para el que se va a mostrar ayuda.

> [!Warning]
> Con algunos comandos, asegúrese de especificar la *ayuda* primero, como con `nuget help install` , ya que hay un paquete denominado "help" en Nuget.org. Si proporciona el comando `nuget install help` , no obtendrá ayuda sobre el comando de instalación pero, en su lugar, instalará el paquete denominado help.

## <a name="options"></a>Opciones

- **`-All`**

  Imprimir ayuda detallada para todos los comandos disponibles; se omite si se especifica un comando específico.

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-Markdown`**

  Imprima la ayuda detallada en formato Markdown cuando se use con `-All` . Se omite en caso contrario.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
