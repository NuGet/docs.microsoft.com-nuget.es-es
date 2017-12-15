---
title: Comando de NuGet CLI setapikey | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: Referencia para el comando de setapikey nuget.exe
keywords: referencia de setapikey de NuGet, comando setapikey
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a>comando setapikey (NuGet CLI)

**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos

Guarda una clave de API para una dirección URL de servidor determinado en `NuGet.Config` para que no es necesario especificar para los comandos siguientes.

## <a name="usage"></a>Uso

```
nuget setapikey <key> -Source <url> [options]
```

donde `<source>` identifica el servidor y `<key>` es la clave o contraseña para guardar. Si `<source>` es se omite, se presupone nuget.org.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet el archivo de configuración para modificar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
