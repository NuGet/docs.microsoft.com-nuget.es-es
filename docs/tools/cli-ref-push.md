---
title: Comando de inserción de NuGet CLI
description: Referencia del comando de inserción nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817196"
---
# <a name="push-command-nuget-cli"></a>comando de inserción (NuGet CLI)

**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** todos; 4.1.0+ necesarios para nuget.org

> [!Important]
> Para insertar los paquetes en nuget.org debe usar nuget.exe v4.1.0 +, que implementa los necesarios [protocolos de NuGet](../api/nuget-protocols.md).

Inserta un paquete a un origen de paquete y lo publica.

Configuración predeterminada de NuGet se obtiene mediante la carga de `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux), a continuación, cargar cualquier `Nuget.Config` o `.nuget\Nuget.Config` archivos a partir de la raíz de unidad y termina en el directorio actual (vea [configuración Comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Uso

```cli
nuget push <packagePath> [options]
```

donde `<packagePath>` identifica el paquete para insertar en el servidor.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| apiKey | La clave de API para el repositorio de destino. Si no está presente, se utiliza el especificado en el archivo de configuración. |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.|
| DisableBuffering | Deshabilita el almacenamiento en búfer cuando se insertan en un servidor HTTP (s) para reducir los usos de la memoria. Precaución: cuando se utiliza esta opción, la autenticación integrada de Windows podría no funcionar. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| NoSymbols | *(3.5 +)*  Si existe un paquete de símbolos, no se enviarán a un servidor de símbolos. |
| Origen | Especifica la dirección URL del servidor. NuGet identifica un origen de la carpeta local o UNC y simplemente copia el archivo no existe en lugar de insertar mediante HTTP.  Además, a partir de NuGet 3.4.2, esto es un parámetro obligatorio a menos que la `NuGet.Config` archivo especifica un *DefaultPushSource* valor (vea [NuGet configurar comportamiento](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  Especifica la URL del servidor de símbolos; nuget.smbsrc.net se utiliza cuando se realiza la inserción en nuget.org |
| SymbolApiKey | *(3.5 +)*  Especifica la clave de API de la dirección URL especificada en `-SymbolSource`. |
| Timeout | Especifica el tiempo de espera, en segundos, para insertar a un servidor. El valor predeterminado es 300 segundos (5 minutos). |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

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

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
