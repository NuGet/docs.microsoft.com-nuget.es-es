---
title: Comando de instalación de CLI de NuGet
description: Referencia de la nuget.exe comando de extracción
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 54a09361173ae10040433b05fcfae7304e39452e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779188"
---
# <a name="push-command-nuget-cli"></a>comando de extracción (CLI de NuGet)

**Se aplica a:** &bullet; **versiones admitidas** de publicación de paquetes: ALL; 4.1.0 + requerido para Nuget.org

> [!Important]
> Para enviar paquetes a nuget.org, debe usar nuget.exe v 4.1.0 +, que implementa los protocolos de [Nuget](../../api/nuget-protocols.md)necesarios.

Envía un paquete a un origen de paquete y lo publica.

La configuración predeterminada de NuGet se obtiene mediante la carga de `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), la carga `Nuget.Config` de los archivos o a partir de la `.nuget\Nuget.Config` raíz de la unidad y la finalización en el directorio actual (consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md)).

## <a name="usage"></a>Uso

```cli
nuget push <packagePath> [options]
```

donde `<packagePath>` identifica el paquete que se va a enviar al servidor.

## <a name="options"></a>Opciones

- **`-ApiKey`**

  La clave de API para el repositorio de destino. Si no está presente, se utiliza el especificado en el archivo de configuración.

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DisableBuffering`**

  Deshabilita el almacenamiento en búfer al insertar en un servidor HTTP (s) para reducir los usos de memoria. PRECAUCIÓN: cuando se usa esta opción, es posible que la autenticación integrada de Windows no funcione.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-NoServiceEndpoint`**

  No se anexa `api/v2/packages` a la dirección URL de origen.

- **`-NoSymbols`**

  *(3.5 +)* Si existe un paquete de símbolos, no se insertará en un servidor de símbolos.

- **`-src|-Source`**

  Especifica la dirección URL del servidor. NuGet identifica un origen de carpeta local o UNC y simplemente copia el archivo allí, en lugar de insertarlo mediante HTTP.  Además, a partir de NuGet 3.4.2, se trata de un parámetro obligatorio, a menos que el `NuGet.Config` archivo especifique un valor de *DefaultPushSource* (consulte [configuración del comportamiento de NuGet](../../consume-packages/configuring-nuget-behavior.md)).

- **`-SkipDuplicate`**

  *(5.1 +)* Si ya existe un paquete y una versión, omítalo y continúe con el siguiente paquete de la extracción, si existe.

- **`-SymbolSource`**

  *(3.5 +)* Especifica la dirección URL del servidor de símbolos; nuget.smbsrc.net se usa al insertar en nuget.org

- **`-SymbolApiKey`**

  *(3.5 +)* Especifica la clave de API de la dirección URL especificada en `-SymbolSource` .

- **`-Timeout`**

  Especifica el tiempo de espera, en segundos, para insertar en un servidor.  El valor predeterminado es 300 segundos (5 minutos).

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .


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
