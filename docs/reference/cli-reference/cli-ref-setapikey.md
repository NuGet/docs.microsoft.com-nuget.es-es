---
title: Comando setapikey de la CLI de NuGet
description: Referencia del comando setapikey de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231232"
---
# <a name="setapikey-command-nuget-cli"></a>comando setapikey (CLI de NuGet)

**Se aplica a: consumo de** paquetes, publicación &bullet; **versiones admitidas:** todos

Guarda una clave de API para una dirección URL de servidor determinada en `NuGet.Config` para que no sea necesario especificarla para los comandos posteriores.

## <a name="usage"></a>Uso

```cli
nuget setapikey <key> -Source <url> [options]
```

donde `<source>` identifica el servidor y `<key>` es la clave que se va a guardar. Si se omite `<source>`, se supone que es nuget.org. 

> [!NOTE]
> La clave de API no se utiliza para la autenticación con la fuente privada. Consulte [`nuget sources` comando](../cli-reference/cli-ref-sources.md) para administrar las credenciales para la autenticación con el origen.
> Las claves de API se pueden obtener de los servidores de NuGet individuales. Para crear y administrar APIKeys para nuget.org, consulte [Publish-API-Key](../../quickstart/includes/publish-api-key.md) .

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, se usa `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
