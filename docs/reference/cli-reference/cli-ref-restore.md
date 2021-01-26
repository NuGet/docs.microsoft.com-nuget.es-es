---
title: Comando de restauración de la CLI de NuGet
description: Referencia del comando nuget.exe restore
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780032"
---
# <a name="restore-command-nuget-cli"></a>comando restore (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 2.7 +

Descarga e instala los paquetes que faltan en la `packages` carpeta. Cuando se usa con NuGet 4.0 + y el formato PackageReference, genera un `<project>.nuget.props` archivo, si es necesario, en la `obj` carpeta. (El archivo se puede omitir del control de código fuente).

En Mac OSX y Linux con la CLI en mono, la restauración de paquetes no es compatible con PackageReference.

## <a name="usage"></a>Uso

```cli
nuget restore <projectPath> [options]
```

donde `<projectPath>` especifica la ubicación de una solución o un `packages.config` archivo. Vea la [sección Comentarios](#remarks) a continuación para obtener información sobre el comportamiento.

## <a name="options"></a>Opciones

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DirectDownload`**

  *(4.0 +)* Descarga paquetes directamente sin rellenar memorias caché con los archivos binarios o metadatos.

- **`-DisableParallelProcessing`**

   Deshabilita la restauración de varios paquetes en paralelo.

- **`-FallbackSource`**

  *(3,2 +)* Una lista de orígenes de paquetes que se usarán como reserva en caso de que el paquete no se encuentre en el origen principal o en el predeterminado. Use un punto y coma para separar las entradas de la lista.

- **`-Force`**

  En los proyectos basados en PackageReference, fuerza la resolución de todas las dependencias, incluso si la última restauración se realizó correctamente. Especificar esta marca es similar a eliminar el `project.assets.json` archivo. Esto no omite la memoria caché http.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-ForceEvaluate`**

  Fuerza la restauración para volver a evaluar todas las dependencias aunque ya exista un archivo de bloqueo.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-LockFilePath`**

  Ubicación de salida donde se escribe el archivo de bloqueo del proyecto. De forma predeterminada, es `PROJECT_ROOT\packages.lock.json`.

- **`-LockedMode`**

  No permite actualizar el archivo de bloqueo del proyecto.

- **`-MSBuildPath`**

   *(4.0 +)* Especifica la ruta de acceso de MSBuild que se va a usar con el comando, que tiene prioridad sobre `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3,2 +)* Especifica la versión de MSBuild que se va a usar con este comando. Los valores admitidos son 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión más alta instalada de MSBuild.

- **`-NoCache`**

  Impide que NuGet use paquetes almacenados en caché. Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-OutputDirectory`**

  Especifica la carpeta en la que se instalan los paquetes. Si no se especifica ninguna carpeta, se usa la carpeta actual. Obligatorio al restaurar con un `packages.config` archivo a menos `PackagesDirectory` que `SolutionDirectory` se use o.

- **`-PackageSaveMode`**

  Especifica los tipos de archivos que se van a guardar después de la instalación del paquete: uno de `nuspec` , `nupkg` o `nuspec;nupkg` .

- **`-PackagesDirectory`**

  Igual a `OutputDirectory`. Obligatorio al restaurar con un `packages.config` archivo a menos `OutputDirectory` que `SolutionDirectory` se use o.

- **`-Project2ProjectTimeOut`**

  Tiempo de espera en segundos para resolver las referencias entre proyectos.

- **`-Recursive`**

  *(4.0 +)* Restaura todos los proyectos de referencias para los proyectos de UWP y .NET Core. No se aplica a los proyectos que usan `packages.config` .

- **`-RequireConsent`**

  Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes. Para obtener más información, vea [restauración de paquetes](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Especifica la carpeta de la solución. No es válido al restaurar los paquetes de una solución. Obligatorio al restaurar con un `packages.config` archivo a menos `PackagesDirectory` que `OutputDirectory` se use o.

- **`-Source`**

  Especifica la lista de orígenes de paquetes (como direcciones URL) que se va a usar para la restauración. Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, consulte [configuración del comportamiento de NuGet](../../consume-packages/configuring-nuget-behavior.md). Use un punto y coma para separar las entradas de la lista.

- **`-UseLockFile`**

  Habilita la generación del archivo de bloqueo del proyecto y su uso con la restauración.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="remarks"></a>Observaciones

El comando restore realiza los pasos siguientes:

1. Determine el modo de operación del comando restore.

   | tipo de archivo projectPath | Comportamiento |
   | --- | --- |
   | Solución (carpeta) | NuGet busca un `.sln` archivo y lo utiliza si se encuentra; de lo contrario, produce un error. `(SolutionDir)\.nuget` se utiliza como carpeta de inicio. |
   | Archivo `.sln` | Restaure los paquetes identificados por la solución; proporciona un error si `-SolutionDirectory` se usa. `$(SolutionDir)\.nuget` se utiliza como carpeta de inicio. |
   | `packages.config` o archivo de proyecto | Restaure los paquetes enumerados en el archivo, resolviendo e instalando las dependencias. |
   | Otro tipo de archivo | Se supone que el archivo es un `.sln` archivo como el anterior; si no es una solución, NuGet genera un error. |
   | (no se ha especificado projectPath) | <ul><li>NuGet busca archivos de solución en la carpeta actual. Si se encuentra un solo archivo, se utilizará uno para restaurar los paquetes; Si se encuentran varias soluciones, NuGet genera un error.</li><li>Si no hay ningún archivo de solución, NuGet busca `packages.config` y lo usa para restaurar los paquetes.</li><li>Si no se encuentra ninguna solución o `packages.config` archivo, NuGet genera un error.</ul> |

2. Determine la carpeta Packages con el siguiente orden de prioridad (NuGet genera un error si no se encuentra ninguna de estas carpetas):

    - La carpeta especificada con `-PackagesDirectory` .
    - El `repositoryPath` valor de `Nuget.Config`
    - La carpeta especificada con `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Al restaurar paquetes para una solución, NuGet hace lo siguiente:
    - Carga el archivo de solución.
    - Restaura los paquetes de nivel de solución que aparecen en `$(SolutionDir)\.nuget\packages.config` la `packages` carpeta.
    - Restaure los paquetes `$(ProjectDir)\packages.config` que aparecen en la `packages` carpeta. Para cada paquete especificado, restaure el paquete en paralelo, a menos que `-DisableParallelProcessing` se especifique.

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
