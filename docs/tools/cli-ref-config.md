---
title: Comando de CLI de NuGet config
description: Referencia para el comando config de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426070"
---
# <a name="config-command-nuget-cli"></a>comando config (CLI de NuGet)

**Se aplica a:** todas &bullet; **versiones compatibles de**: todas

Obtiene o establece los valores de configuración de NuGet. Para el uso adicional, consulte [configuraciones comunes NuGet](../consume-packages/configuring-nuget-behavior.md). Para más información sobre los nombres de clave permitidos, consulte el [referencia del archivo de configuración de NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

donde `<name>` y `<value>` especificar un par de clave y valor debe establecerse en la configuración. Puede especificar tantos pares según sea necesario. Para quitar un valor, especifique el nombre y la `=` inicio de sesión, pero ningún valor.

Para los nombres de clave permitidos, consulte el [referencia del archivo de configuración de NuGet](../reference/nuget-config-file.md).

En NuGet 3.4 y versiones posteriores, `<value>` puede usar [variables de entorno](cli-ref-environment-variables.md).

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| AsPath | Devuelve el valor de la configuración como una ruta de acceso, se omite cuando `-Set` se utiliza. |
| ConfigFile | El archivo de configuración para modificar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes para confirmaciones o intervención del usuario. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

### <a name="examples"></a>Ejemplos

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
