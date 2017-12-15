---
title: "Comando de inserción de NuGet CLI | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Referencia del comando de inserción nuget.exe"
keywords: "referencia de inserción de NuGet, el comando de inserción"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a>comando de inserción (NuGet CLI)

**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** todos; 4.1.0+ necesarios para nuget.org

> [!Important]
> Para insertar los paquetes en nuget.org debe usar nuget.exe v4.1.0 +, que implementa los necesarios [protocolos de NuGet](../api/nuget-protocols.md).

Inserta un paquete a un origen de paquete y lo publica.

Configuración predeterminada de NuGet se obtiene mediante la carga de `%AppData%\NuGet\NuGet.Config`, a continuación, cargar alguna `Nuget.Config` o `.nuget\Nuget.Config` archivos a partir de la raíz de unidad y termina en el directorio actual (vea [configuración de comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Uso

```
nuget push <packagePath> [options]
```

donde `<packagePath>` identifica el paquete para insertar en el servidor.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| apiKey | La clave de API para el repositorio de destino. Si no está presente, el especificado en *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ConfigFile | *(2.5 +)*  NuGet el archivo de configuración para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| DisableBuffering | Deshabilita el almacenamiento en búfer cuando se insertan en un servidor HTTP (s) para reducir los usos de la memoria. Precaución: cuando se utiliza esta opción, la autenticación integrada de Windows podría no funcionar. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| NoSymbols | *(3.5 +)*  Si existe un paquete de símbolos, no se enviarán a un servidor de símbolos. |
| Origen | Especifica la dirección URL del servidor. Con NuGet 2.5 +, NuGet identificará un origen de la carpeta local o UNC y simplemente copie el archivo no existe en lugar de insertar mediante HTTP.  Además, a partir de NuGet 3.4.2, esto es un parámetro obligatorio a menos que la `NuGet.Config` archivo especifica un *DefaultPushSource* valor (vea [NuGet configurar comportamiento](../Consume-Packages/Configuring-NuGet-Behavior.md)). |
| SymbolSource | *(3.5 +)*  Especifica la URL del servidor de símbolos; nuget.smbsrc.net se utiliza cuando se realiza la inserción en nuget.org |
| SymbolApiKey | *(3.5 +)*  Especifica la clave de API de la dirección URL especificada en `-SymbolSource`. |
| Timeout | Especifica el tiempo de espera, en segundos, para insertar a un servidor. El valor predeterminado es 300 segundos (5 minutos). |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
