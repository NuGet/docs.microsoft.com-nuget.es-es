---
title: Comando setapikey de la CLI de NuGet
description: Referencia del comando nuget.exe setapikey
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780013"
---
# <a name="setapikey-command-nuget-cli"></a>comando setapikey (CLI de NuGet)

**Se aplica a: consumo de** paquetes, publicación de &bullet; **versiones admitidas:** todos

Guarda una clave de API para una dirección URL de servidor determinada en `NuGet.Config` para que no sea necesario especificarla para los comandos subsiguientes.

## <a name="usage"></a>Uso

```cli
nuget setapikey <key> -Source <url> [options]
```

donde `<source>` identifica el servidor y `<key>` es la clave que se va a guardar. Si `<source>` se omite, se supone que es Nuget.org. 

> [!NOTE]
> La clave de API no se utiliza para la autenticación con la fuente privada. Consulte el [comando `nuget sources` ](../cli-reference/cli-ref-sources.md) a fin de administrar las credenciales para la autenticación con el origen.
> Las claves de API se pueden obtener de los servidores de NuGet individuales. Para crear y administrar APIKeys para nuget.org, consulte [adquisición-a-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) .

## <a name="options"></a>Opciones

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-src|-Source`**

  Dirección URL del servidor donde la clave de API es válida.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
