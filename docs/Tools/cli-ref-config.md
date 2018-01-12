---
title: Comando config de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: Referencia para el comando config de nuget.exe
keywords: "referencia de configuración de NuGet, comando config"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f49751d9747687177e3b6c1890ee9d2919be8d0e
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2018
---
# <a name="config-command-nuget-cli"></a>comando config (NuGet CLI)

**Se aplica a:** todos los &bullet; **versiones compatibles**: todos los

Obtiene o establece los valores de configuración de NuGet. Para uso adicionales, consulte [configuración de comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md). Para obtener información detallada sobre los nombres de clave permitidos, consulte la [referencia del archivo de configuración de NuGet](../Schema/nuget-config-file.md).

## <a name="usage"></a>Uso

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

donde `<name>` y `<value>` especificar un par clave-valor que se establecerán en la configuración. Puede especificar tantos pares según sea necesario. Para quitar un valor, especifique el nombre y la `=` inicio de sesión, pero ningún valor.

Para los nombres de clave permitidos, consulte la [referencia del archivo de configuración de NuGet](../Schema/nuget-config-file.md).

En NuGet 3.4 o superior, `<value>` puede usar [variables de entorno](cli-ref-environment-variables.md).

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| AsPath | Devuelve el valor de la configuración como una ruta de acceso, se omite cuando `-Set` se utiliza. |
| ConfigFile | *(2.5 +)*  NuGet el archivo de configuración para modificar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

### <a name="examples"></a>Ejemplos

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
