---
title: Comando de NuGet CLI reflejado
description: Referencia del comando de reflejado nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4cec854f05fcd207bb15a50ea4ebdc201fdb3ac6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818157"
---
# <a name="mirror-command-nuget-cli"></a>Comando mirror (CLI de NuGet)

**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** en desuso en 3.2 +

Refleja un paquete y sus dependencias de los repositorios de origen especificada en el repositorio de destino.

> [!NOTE]
> Para habilitar este comando para las versiones de NuGet antes 3.2, vaya a [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), seleccione la versión estable más reciente, descargue `NuGet.ServerExtensions.dll` y `Nuget-Signed.exe` en el disco local y el cambio de nombre `Nuget-Signed.exe` a `nuget.exe`.

## <a name="usage"></a>Uso

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

donde `<packageID>` es el paquete para reflejar, o `<configFilePath>` identifica el `packages.config` archivo que enumera los paquetes que se va a reflejar.

El `<listUrlTarget>` especifica el repositorio de origen, y `<publishUrlTarget>` especifica el repositorio de destino.

Si el repositorio de destino está en `https://machine/repo` que se esté ejecutando [NuGet.Server](../hosting-packages/nuget-server.md), las direcciones URL lista e inserte será `https://machine/repo/nuget` y `https://machine/repo/api/v2/package`, respectivamente.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| apiKey | La clave de API para el repositorio de destino. Si no está presente, se especificó en el archivo de configuración se usa (`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux)). |
| Ayuda | Muestra información de ayuda para el comando. |
| NoCache | Impide que NuGet use paquetes almacenados en caché. Vea [administrar los paquetes globales y las carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Registra qué están a cargo pero no lleva a cabo las acciones; se da por supuesto se realizó correctamente para las operaciones de inserción. |
| Versión preliminar | Incluye paquetes de versión preliminar de la operación de creación de reflejo. |
| Origen | Una lista de orígenes de paquetes para crear el reflejo. Si no se especifica ningún origen de los definen en el archivo de configuración (vea ApiKey anterior) se usan, volverá al valor predeterminado nuget.org si no se especifica ninguno. |
| Timeout | Especifica el tiempo de espera, en segundos, para insertar a un servidor. El valor predeterminado es 300 segundos (5 minutos). |
| Versión | La versión del paquete para instalar. Si no se especifica, se refleja la versión más reciente. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
