---
title: Comando de NuGet CLI reflejado | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia del comando de reflejado nuget.exe
keywords: referencia de reflejado de NuGet, comando espejo
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff5f1c1a915943e8a2eb9c6d6ab09a850968371
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="mirror-command-nuget-cli"></a>comando reflejado (NuGet CLI)

**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** en desuso en 3.2 +

Refleja un paquete y sus dependencias de los repositorios de origen especificada en el repositorio de destino.

> [!NOTE]
> Para habilitar este comando para las versiones de NuGet antes 3.2, vaya a [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), seleccione la versión estable más reciente, descargue `NuGet.ServerExtensions.dll` y `Nuget-Signed.exe` en el disco local y el nombre `Nuget-Signed.exe` a `nuget.exe`.

## <a name="usage"></a>Uso

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

donde `<packageID>` es el paquete para reflejar, o `<configFilePath>` identifica el `packages.config` archivo que enumera los paquetes que se va a reflejar.

El `<listUrlTarget>` especifica el repositorio de origen, y `<publishUrlTarget>` especifica el repositorio de destino.

Si el repositorio de destino está en `https://machine/repo` que se esté ejecutando [NuGet.Server](../hosting-packages/NuGet-Server.md), las direcciones URL lista e inserte será `https://machine/repo/nuget` y `https://machine/repo/api/v2/package`, respectivamente.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| apiKey | La clave de API para el repositorio de destino. Si no está presente, el especificado en *%AppData%\NuGet\NuGet.Config* se utiliza. |
| Ayuda | Muestra información de ayuda para el comando. |
| NoCache | Impide que NuGet use paquetes de memorias caché del equipo local. |
| NOOP | Registra qué están a cargo pero no lleva a cabo las acciones; se da por supuesto se realizó correctamente para las operaciones de inserción. |
| Versión preliminar | Incluye paquetes de versión preliminar de la operación de creación de reflejo. |
| Origen | Una lista de orígenes de paquetes para crear el reflejo. Si no se especifica ningún origen de los definen en *%AppData%\NuGet\NuGet.Config* se usan, volverá al valor predeterminado nuget.org si no se especifica ninguno. |
| Timeout | Especifica el tiempo de espera, en segundos, para insertar a un servidor. El valor predeterminado es 300 segundos (5 minutos). |
| Versión | La versión del paquete para instalar. Si no se especifica, se refleja la versión más reciente. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
