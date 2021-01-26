---
title: Comando de reflejo de la CLI de NuGet
description: Referencia del comando nuget.exe Mirror
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779174"
---
# <a name="mirror-command-nuget-cli"></a>comando Mirror (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles** de publicación de paquetes: desusados en 3,2 +

Refleja un paquete y sus dependencias de los repositorios de origen especificados en el repositorio de destino.

> [!NOTE]
> Los NuGet.ServerExtensions.dll y NuGet-Signed.exe que anteriormente admitían este comando en NuGet 2. x (cambiando el nombre de NuGet-Signed.exe a nuget.exe) ya no están disponibles para su descarga. Para usar un comando similar a este, pruebe [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).

## <a name="usage"></a>Uso

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

donde `<packageID>` es el paquete que se va a reflejar, o `<configFilePath>` identifica el `packages.config` archivo que muestra los paquetes que se van a reflejar.

`<listUrlTarget>`Especifica el repositorio de origen y `<publishUrlTarget>` especifica el repositorio de destino.

Si el repositorio de destino se encuentra en `https://machine/repo` que ejecuta [NuGet. Server](../../hosting-packages/nuget-server.md), la lista y las direcciones URL de inserciones serán `https://machine/repo/nuget` y `https://machine/repo/api/v2/package` , respectivamente.

## <a name="options"></a>Opciones

- **`-ApiKey`**

  La clave de API para el repositorio de destino. Si no está presente, se usa el especificado en el archivo de configuración ( `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).

- **`-Help`**

  Muestra información de ayuda para el comando.

- **`-NoCache`**

  Impide que NuGet use paquetes almacenados en caché. Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-Noop`**

  Registra lo que se haría pero no realiza las acciones; supone que las operaciones de inserciones se han realizado correctamente.

- **`-PreRelease`**

  Incluye paquetes de versión preliminar en la operación de creación de reflejo.

- **`-Source`**

  Una lista de orígenes de paquetes que se van a reflejar. Si no se especifican orígenes, se usan los definidos en el archivo de configuración (vea ApiKey anterior), de forma predeterminada se usa nuget.org si no se especifica ninguno.

- **`-Timeout`**

  Especifica el tiempo de espera, en segundos, para insertar en un servidor.  El valor predeterminado es 300 segundos (5 minutos).

- **`-Version`**

  Versión del paquete que se va a instalar. Si no se especifica, la versión más reciente está reflejada.

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
