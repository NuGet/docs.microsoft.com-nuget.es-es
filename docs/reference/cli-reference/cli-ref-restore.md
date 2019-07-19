---
title: Comando de restauración de la CLI de NuGet
description: Referencia del comando de restauración de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 82113d460f7f5ff467b0a0552cc49283de95de25
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327642"
---
# <a name="restore-command-nuget-cli"></a>comando restore (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 2.7+

Descarga e instala los paquetes que faltan en `packages` la carpeta. Cuando se usa con NuGet 4.0 + y el formato PackageReference, genera `<project>.nuget.props` un archivo, si es necesario, `obj` en la carpeta. (El archivo se puede omitir del control de código fuente).

En Mac OSX y Linux con la CLI en mono, la restauración de paquetes no es compatible con PackageReference.

## <a name="usage"></a>Uso

```cli
nuget restore <projectPath> [options]
```

donde `<projectPath>` especifica la ubicación de una solución o un `packages.config` archivo. Vea la [sección Comentarios](#remarks) a continuación para obtener información sobre el comportamiento.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| DirectDownload | *(4.0 +)* Descarga paquetes directamente sin rellenar memorias caché con los archivos binarios o metadatos. |
| DisableParallelProcessing | Deshabilita la restauración de varios paquetes en paralelo. |
| FallbackSource | *(3,2 +)* Una lista de orígenes de paquetes que se usarán como reserva en caso de que el paquete no se encuentre en el origen principal o en el predeterminado. |
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| MSBuildPath | *(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el `-MSBuildVersion`comando, que tiene prioridad sobre. |
| MSBuildVersion | *(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando. Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild. |
| NoCache | Impide que NuGet use paquetes almacenados en caché. Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| OutputDirectory | Especifica la carpeta en la que se instalan los paquetes. Si no se especifica ninguna carpeta, se usa la carpeta actual. Obligatorio al restaurar con un `packages.config` archivo a menos que `SolutionDirectory` `PackagesDirectory` se use o.|
| PackageSaveMode | Especifica los tipos de archivos que se van a guardar después de la `nuspec`instalación `nupkg`del paquete `nuspec;nupkg`: uno de, o. |
| PackagesDirectory | Igual a `OutputDirectory`. Obligatorio al restaurar con un `packages.config` archivo a menos que `SolutionDirectory` `OutputDirectory` se use o. |
| Project2ProjectTimeOut | Tiempo de espera en segundos para resolver las referencias entre proyectos. |
| Recursiva | *(4.0 +)* Restaura todos los proyectos de referencias para los proyectos de UWP y .NET Core. No se aplica a los proyectos `packages.config`que usan. |
| RequireConsent | Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes. Para obtener más información, vea [restauración de paquetes](../../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica la carpeta de la solución. No es válido al restaurar los paquetes de una solución. Obligatorio al restaurar con un `packages.config` archivo a menos que `OutputDirectory` `PackagesDirectory` se use o. |
| source | Especifica la lista de orígenes de paquetes (como direcciones URL) que se va a usar para la restauración. Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, consulte [configuración del comportamiento de NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="remarks"></a>Comentarios

El comando restore realiza los pasos siguientes:

1. Determine el modo de operación del comando restore.

   | tipo de archivo projectPath | Comportamiento |
   | --- | --- |
   | Solución (carpeta) | NuGet busca un `.sln` archivo y lo utiliza si se encuentra; de lo contrario, produce un error. `(SolutionDir)\.nuget`se utiliza como carpeta de inicio. |
   | `.sln`filesystem | Restaure los paquetes identificados por la solución; proporciona un error si `-SolutionDirectory` se usa. `$(SolutionDir)\.nuget`se utiliza como carpeta de inicio. |
   | `packages.config`o archivo de proyecto | Restaure los paquetes enumerados en el archivo, resolviendo e instalando las dependencias. |
   | Otro tipo de archivo | Se supone que el archivo es `.sln` un archivo como el anterior; si no es una solución, NuGet genera un error. |
   | (no se ha especificado projectPath) | <ul><li>NuGet busca archivos de solución en la carpeta actual. Si se encuentra un solo archivo, se utilizará uno para restaurar los paquetes; Si se encuentran varias soluciones, NuGet genera un error.</li><li>Si no hay ningún archivo de solución, NuGet busca `packages.config` y lo usa para restaurar los paquetes.</li><li>Si no se encuentra `packages.config` ninguna solución o archivo, NuGet genera un error.</ul> |

2. Determine la carpeta Packages con el siguiente orden de prioridad (NuGet genera un error si no se encuentra ninguna de estas carpetas):

    - La carpeta especificada con `-PackagesDirectory`.
    - El `repositoryPath` valor de`Nuget.Config`
    - La carpeta especificada con`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Al restaurar paquetes para una solución, NuGet hace lo siguiente:
    - Carga el archivo de solución.
    - Restaura los paquetes de nivel de solución que `$(SolutionDir)\.nuget\packages.config` aparecen en `packages` la carpeta.
    - Restaure los paquetes `$(ProjectDir)\packages.config` que aparecen `packages` en la carpeta. Para cada paquete especificado, restaure el paquete en paralelo `-DisableParallelProcessing` , a menos que se especifique.

## <a name="examples"></a>Ejemplos

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
