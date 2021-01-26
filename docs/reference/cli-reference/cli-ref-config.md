---
title: Comando de configuración de la CLI de NuGet
description: Referencia del comando nuget.exe config
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775967"
---
# <a name="config-command-nuget-cli"></a>comando config (CLI de NuGet)

**Se aplica a:** todas &bullet; **las versiones compatibles**: todas

Obtiene o establece los valores de configuración de NuGet. Para obtener más uso, consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md). Para obtener más información sobre los nombres de clave permitidos, consulte la [Referencia del archivo de configuración de NuGet](../nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

donde `<name>` y `<value>` especifican un par clave-valor que se establecerá en la configuración. Puede especificar tantos pares como desee. Para quitar un valor, especifique el nombre y el `=` signo pero no el valor.

Para ver los nombres de clave permitidos, consulte la [Referencia del archivo de configuración de NuGet](../nuget-config-file.md).

En NuGet 3.4 +, `<value>` puede usar [variables de entorno](cli-ref-environment-variables.md).

## <a name="options"></a>Opciones


- **`AsPath`**

  Devuelve el valor de configuración como una ruta de acceso, que se omite cuando `-Set` se usa.

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-Set`**

  Uno en más pares clave-valor que se establecerá en la configuración.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

Vea también [variables de entorno](cli-ref-environment-variables.md)

### <a name="examples"></a>Ejemplos

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
