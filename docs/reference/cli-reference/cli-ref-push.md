---
title: Comando de instalación de CLI de NuGet
description: Referencia del comando de instalación de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327632"
---
# <a name="push-command-nuget-cli"></a>comando de extracción (CLI de NuGet)

**Se aplica a:** versiones &bullet; admitidas de publicación de paquetes **:** All; 4.1.0 + requerido para Nuget.org

> [!Important]
> Para enviar paquetes a nuget.org, debe usar Nuget. exe v 4.1.0 +, que implementa los protocolos de [Nuget](../../api/nuget-protocols.md)necesarios.

Envía un paquete a un origen de paquete y lo publica.

La configuración predeterminada de NuGet se obtiene mediante `%AppData%\NuGet\NuGet.Config` la carga de ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux), `Nuget.Config` la `.nuget\Nuget.Config` carga de los archivos o a partir de la raíz de la unidad y la finalización en el directorio actual (consulte [NuGet común). configuraciones](../../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Uso

```cli
nuget push <packagePath> [options]
```

donde `<packagePath>` identifica el paquete que se va a enviar al servidor.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| ApiKey | La clave de API para el repositorio de destino. Si no está presente, se utiliza el especificado en el archivo de configuración. |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| DisableBuffering | Deshabilita el almacenamiento en búfer al insertar en un servidor HTTP (s) para reducir los usos de memoria. PRECAUCIÓN: cuando se usa esta opción, es posible que la autenticación integrada de Windows no funcione. |
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Nosymbols | *(3.5 +)* Si existe un paquete de símbolos, no se insertará en un servidor de símbolos. |
| source | Especifica la dirección URL del servidor. NuGet identifica un origen de carpeta local o UNC y simplemente copia el archivo allí en lugar de insertarlo mediante HTTP.  Además, a partir de NuGet 3.4.2, se trata de un parámetro obligatorio `NuGet.Config` , a menos que el archivo especifique un valor de *DefaultPushSource* (consulte [configuración del comportamiento de NuGet](../../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | *(5.1 +)* Si ya existe un paquete y una versión, omítalo y continúe con el siguiente paquete de la extracción, si existe. |
| SymbolSource | *(3.5 +)* Especifica la dirección URL del servidor de símbolos; nuget.smbsrc.net se usa al insertar en nuget.org |
| SymbolApiKey | *(3.5 +)* Especifica la clave de API de la dirección URL `-SymbolSource`especificada en. |
| Tiempo de espera | Especifica el tiempo de espera, en segundos, para insertar en un servidor. El valor predeterminado es 300 segundos (5 minutos). |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
