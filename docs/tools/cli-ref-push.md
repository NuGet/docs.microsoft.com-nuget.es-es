---
title: Comando de CLI de NuGet push
description: Referencia del comando de inserción de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bce04864224a66019a52cdfff8355f68dc424204
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975001"
---
# <a name="push-command-nuget-cli"></a>inserción de comandos (CLI de NuGet)

**Se aplica a:** publicación del paquete &bullet; **versiones compatibles:** todos; 4.1.0 necesarios para nuget.org

> [!Important]
> Para insertar paquetes en nuget.org debe usar nuget.exe 4.1.0 +, que implementa la requiere [protocolos de NuGet](../api/nuget-protocols.md).

Inserta un paquete a un origen de paquete y lo publica.

Configuración predeterminada de NuGet se obtiene mediante la carga `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), a continuación, cargar cualquier `Nuget.Config` o `.nuget\Nuget.Config` archivos a partir de la raíz de la unidad y finalizando en el directorio actual (consulte [configuración Comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Uso

```cli
nuget push <packagePath> [options]
```

donde `<packagePath>` identifica el paquete para insertar en el servidor.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ApiKey | La clave de API para el repositorio de destino. Si no está presente, se utiliza el especificado en el archivo de configuración. |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| DisableBuffering | Deshabilita el almacenamiento en búfer al insertar en un servidor HTTP (s) para disminuir los usos de la memoria. Precaución: cuando se usa esta opción, la autenticación integrada de Windows podría no funcionar. |
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes para confirmaciones o intervención del usuario. |
| NoSymbols | *(3.5 y versiones posteriores)*  Si existe un paquete de símbolos, no se podrán realizar en un servidor de símbolos. |
| Source | Especifica la dirección URL del servidor. NuGet identifica un origen de la carpeta local o UNC y simplemente copia el archivo existe en lugar de insertar mediante HTTP.  Además, a partir de NuGet 3.4.2, esto es un parámetro obligatorio a menos que el `NuGet.Config` archivo especifica un *DefaultPushSource* valor (consulte [del comportamiento de configuración de NuGet](../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | Si ya existe un paquete y versión, omitirla y continuar con el siguiente paquete en la inserción, si existe. |
| SymbolSource | *(3.5 y versiones posteriores)*  Especifica la URL del servidor de símbolos; nuget.smbsrc.net se utiliza al realizar inserciones en nuget.org |
| SymbolApiKey | *(3.5 y versiones posteriores)*  Especifica la clave de API de la dirección URL especificada en `-SymbolSource`. |
| Tiempo de espera | Especifica el tiempo de espera en segundos, para insertar en un servidor. El valor predeterminado es 300 segundos (5 minutos). |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

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
