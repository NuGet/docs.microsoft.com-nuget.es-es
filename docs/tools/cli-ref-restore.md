---
title: Comando de restauración de la CLI de NuGet
description: Referencia del comando de restauración de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d7a4188de4fb6f812ca19e7f9e302a5a133c58b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425971"
---
# <a name="restore-command-nuget-cli"></a>restaurar comandos (CLI de NuGet)

**Se aplica a:** consumo de paquetes &bullet; **versiones compatibles:** 2.7+

Descarga e instala los paquetes que faltan en el `packages` carpeta. Cuando se usa con NuGet 4.0 + y el formato PackageReference, genera un `<project>.nuget.props` archivo, si es necesario, en el `obj` carpeta. (Se puede omitir el archivo de control de código fuente.)

En Mac OSX y Linux con la CLI en Mono, no se admite la restauración de paquetes con PackageReference.

## <a name="usage"></a>Uso

```cli
nuget restore <projectPath> [options]
```

donde `<projectPath>` especifica la ubicación de una solución o un `packages.config` archivo. Consulte [comentarios](#remarks) a continuación para obtener detalles de comportamiento.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| DirectDownload | *(4.0 y versiones posteriores)*  Descarga los paquetes directamente sin rellenar las memorias caché con los archivos binarios o de metadatos. |
| DisableParallelProcessing | Deshabilita la restauración de varios paquetes en paralelo. |
| FallbackSource | *(3.2 y versiones posteriores)*  Una lista de orígenes de paquetes para utilizar como de reservas en caso de que el paquete no se encuentra en el servidor principal o el origen predeterminado. |
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Help | Muestra información de ayuda para el comando. |
| MSBuildPath | *(4.0 y versiones posteriores)*  Especifica la ruta de acceso de MSBuild que use con el comando, tiene prioridad sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 y versiones posteriores)*  Especifica la versión de MSBuild que se usará con este comando. Los valores admitidos son 4, 12, 14, 15.1, versión 15.3, 15.4, 15.5, versión 15.6, versión 15.7, 15,8, 15.9. De forma predeterminada que se selecciona la versión de MSBuild en su ruta de acceso, en caso contrario, el valor predeterminado es la última versión instalada de MSBuild. |
| NoCache | Impide que NuGet utilice paquetes almacenados en caché. Consulte [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime los mensajes para confirmaciones o intervención del usuario. |
| OutputDirectory | Especifica la carpeta donde se instalan los paquetes. Si se especifica ninguna carpeta, se usa la carpeta actual. Necesario cuando se restaura con un `packages.config` archivo a menos que `PackagesDirectory` o `SolutionDirectory` se utiliza.|
| PackageSaveMode | Especifica los tipos de archivos que se va a guardar tras la instalación del paquete: uno de `nuspec`, `nupkg`, o `nuspec;nupkg`. |
| PackagesDirectory | Igual a `OutputDirectory`. Necesario cuando se restaura con un `packages.config` archivo a menos que `OutputDirectory` o `SolutionDirectory` se utiliza. |
| Project2ProjectTimeOut | Tiempo de espera en segundos para resolver las referencias de proyecto a proyecto. |
| Recursiva | *(4.0 y versiones posteriores)*  Restaura todas las referencias de proyectos para proyectos de UWP y .NET Core. No se aplica a proyectos mediante `packages.config`. |
| RequireConsent | Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes. Para obtener más información, consulte [la restauración del paquete](../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica la carpeta de soluciones. No es válido al restaurar los paquetes de una solución. Necesario cuando se restaura con un `packages.config` archivo a menos que `PackagesDirectory` o `OutputDirectory` se utiliza. |
| Source | Especifica la lista de orígenes de paquetes (como las direcciones URL) para la restauración. Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, consulte [del comportamiento de configuración de NuGet](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="remarks"></a>Comentarios

El comando restore lleva a cabo los pasos siguientes:

1. Determinar el modo de operación del comando restore.

   | tipo de archivo projectPath | Comportamiento |
   | --- | --- |
   | Solución (carpeta) | NuGet busca un `.sln` archivo y utiliza ese si se encuentra; en caso contrario, produce un error. `(SolutionDir)\.nuget` se utiliza como la carpeta de inicio. |
   | `.sln` Archivo | Restauración de paquetes que se identifican por la solución; da como resultado un error si `-SolutionDirectory` se utiliza. `$(SolutionDir)\.nuget` se utiliza como la carpeta de inicio. |
   | `packages.config` o el archivo de proyecto | Restaurar los paquetes enumerados en el archivo, la resolución e instalación de dependencias. |
   | Otro tipo de archivo | Se supone que el archivo sea un `.sln` archivo anterior; si no es una solución, NuGet da un error. |
   | (projectPath no especificado) | <ul><li>NuGet busca archivos de solución en la carpeta actual. Si se encuentra un único archivo, que se usa para restaurar paquetes; Si se encuentran varias soluciones, NuGet produce un error.</li><li>Si no hay ningún archivo de solución, NuGet busca un `packages.config` y lo usa para restaurar los paquetes.</li><li>Si no hay ninguna solución o `packages.config` se encuentra el archivo, NuGet produce un error.</ul> |

2. Determinar la carpeta de paquetes mediante el siguiente orden de prioridad (NuGet produce un error si no se encuentra ninguna de estas carpetas):

    - La carpeta especificada con `-PackagesDirectory`.
    - El `repositoryPath` valor en `Nuget.Config`
    - La carpeta especificada con `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Al restaurar los paquetes de una solución, NuGet hace lo siguiente:
    - Carga el archivo de solución.
    - Restaura los paquetes de nivel de solución incluidos en `$(SolutionDir)\.nuget\packages.config` en el `packages` carpeta.
    - Restaurar los paquetes enumerados en `$(ProjectDir)\packages.config` en el `packages` carpeta. Para cada paquete especificado, la restauración del paquete en paralelo a menos `-DisableParallelProcessing` se especifica.

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
