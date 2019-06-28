---
title: Comando de eliminación de la CLI de NuGet
description: Referencia del comando de eliminación de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426105"
---
# <a name="delete-command-nuget-cli"></a>eliminar comandos (CLI de NuGet)

**Se aplica a:** publicación del paquete &bullet; **versiones compatibles:** todas

Elimina o quita un paquete desde un origen del paquete de la lista. Para nuget.org, el comando delete [quita el paquete de la lista](../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Uso

```cli
nuget delete <packageID> <packageVersion> [options]
```

donde `<packageID>` y `<packageVersion>` identificar el paquete exacto para eliminar o quitar de la lista. El comportamiento exacto depende del origen. Para las carpetas locales, por ejemplo, se elimina el paquete; para nuget.org, el paquete se da de baja.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ApiKey | La clave de API para el repositorio de destino. Si no está presente, se utiliza el especificado en el archivo de configuración. |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes para confirmaciones o intervención del usuario. |
| Source | Especifica la dirección URL del servidor. La dirección URL de nuget.org es `https://api.nuget.org/v3/index.json`. Para fuentes privadas, sustituya el nombre de host, por ejemplo, *%hostname%/api/v3*. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
