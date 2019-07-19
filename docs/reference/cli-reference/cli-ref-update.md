---
title: Comando de actualización de la CLI de NuGet
description: Referencia del comando de actualización de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327512"
---
# <a name="update-command-nuget-cli"></a>Comando update (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: todas

Actualiza todos los paquetes de un proyecto (mediante `packages.config`) a las versiones más recientes disponibles. Se recomienda ejecutar [' restore '](cli-ref-restore.md) antes de ejecutar el `update`. (Para actualizar un paquete individual, use [`nuget install`](cli-ref-install.md) sin especificar un número de versión, en cuyo caso NuGet instala la versión más reciente).

Nota: `update` no funciona con la CLI que se ejecuta en mono (Mac OSX o Linux) o cuando se usa el formato PackageReference.

El `update` comando también actualiza las referencias de ensamblado en el archivo de proyecto, siempre que dichas referencias ya existan. Si un paquete actualizado tiene un ensamblado agregado, *no* se agregará una nueva referencia. Las dependencias de paquetes nuevas tampoco tienen agregadas las referencias de ensamblado. Para incluir estas operaciones como parte de una actualización, actualice el paquete en Visual Studio mediante la interfaz de usuario del administrador de paquetes o la consola del administrador de paquetes.

Este comando también se puede usar para actualizar el propio Nuget. exe mediante la marca *-Self* .

## <a name="usage"></a>Uso

```cli
nuget update <configPath> [options]
```

donde `<configPath>` identifica un `packages.config` archivo de solución o que muestra las dependencias del proyecto.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| FileConflictAction | Especifica la acción que se llevará a cabo cuando se le pida que sobrescriba u omita los archivos existentes a los que hace referencia el proyecto. Los valores son *sobrescribir, omitir, ninguno*. |
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| Id | Especifica una lista de los identificadores de paquete que se van a actualizar. |
| MSBuildPath | *(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el `-MSBuildVersion`comando, que tiene prioridad sobre. |
| MSBuildVersion | *(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando. Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Versión preliminar | Permite la actualización a versiones preliminares. Esta marca no es necesaria cuando se actualizan los paquetes de versión preliminar que ya están instalados. |
| RepositoryPath | Especifica la carpeta local en la que se instalan los paquetes. |
| Segura | Especifica que solo se instalarán las actualizaciones con la versión más alta disponible dentro de la misma versión principal y secundaria que el paquete instalado. |
| Mismo | Actualiza Nuget. exe a la versión más reciente; el resto de los argumentos se omiten. |
| source | Especifica la lista de orígenes de paquetes (como direcciones URL) que se usarán para las actualizaciones. Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, vea [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |
| `Version` | Cuando se usa con un identificador de paquete, especifica la versión del paquete que se va a actualizar. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
