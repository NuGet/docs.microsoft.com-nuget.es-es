---
title: "Comando de restauración de NuGet CLI | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referencia para el comando de restauración nuget.exe"
keywords: "NuGet referencia de restauración, restaurar los comandos de paquetes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 93d7b6967d9297ee822df1583351385210775173
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="restore-command-nuget-cli"></a>comando restore (NuGet CLI)

**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** 2.7 +

Descarga e instala los paquetes que faltan en la `packages` carpeta. Cuando se usa con NuGet 4.0 + y el formato PackageReference, genera un `<project>.nuget.props` de archivos, si es necesario, en el `obj` carpeta. (El archivo puede omitirse en control de código fuente.)

En Mac OSX y Linux con la CLI en Mono, no se admite la restauración de paquetes con PackageReference.

## <a name="usage"></a>Uso

```cli
nuget restore <projectPath> [options]
```

donde `<projectPath>` especifica la ubicación de una solución o un `packages.config` archivo. Vea [comentarios](#remarks) a continuación para obtener detalles de comportamientos.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| DirectDownload | *(4.0 +)*  Descarga paquetes directamente sin rellenar las memorias caché con los archivos binarios o los metadatos. |
| DisableParallelProcessing | Deshabilita la restauración de varios paquetes en paralelo. |
| FallbackSource | *(3.2 +)*  Una lista de orígenes de paquetes que se usará como de reservas en caso de que el paquete no se encuentra en el servidor principal o el origen predeterminado. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| MSBuildPath | *(4.0 +)*  Especifica la ruta de acceso de MSBuild para usar con el comando, tiene prioridad sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Especifica la versión de MSBuild que se utilizará con este comando. Valores admitidos son 4, 12, 14, 15. De forma predeterminada, se seleccionará el MSBuild en la ruta de acceso, en caso contrario, valor predeterminado es la última versión instalada de MSBuild. |
| NoCache | Impide que NuGet use paquetes de memorias caché del equipo local. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| OutputDirectory | Especifica la carpeta en la que se instalan los paquetes. Si no se especifica ninguna carpeta, se usa la carpeta actual. |
| PackageSaveMode | Especifica los tipos de archivos para guardar después de la instalación de paquete: uno de `nuspec`, `nupkg`, o `nuspec;nupkg`. |
| PackagesDirectory | Igual a `OutputDirectory`. |
| Project2ProjectTimeOut | Tiempo de espera en segundos para resolver las referencias de proyecto a proyecto. |
| Recursiva | *(4.0 +)*  Restaura todas las referencias de proyectos para proyectos de UWP y .NET Core. No se aplica a proyectos mediante `packages.config`. |
| RequireConsent | Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes. Para obtener más información, consulte [la restauración del paquete](../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica la carpeta de soluciones. No es válido cuando restaurando paquetes para una solución. |
| Origen | Especifica la lista de orígenes de paquetes (como las direcciones URL) para que utilice para la restauración. Si se omite, el comando utiliza los orígenes proporcionados en archivos de configuración, consulte [NuGet configurar comportamiento](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Nivel de detalle |> especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="remarks"></a>Comentarios

El comando restore lleva a cabo los pasos siguientes:

1. Determinar el modo de operación del comando restore.
    tipo de archivo projectPath | Comportamiento
    | --- | --- |
    Solución (carpeta) | NuGet busca un `.sln` archivo y utiliza ese si se encuentra; en caso contrario, produce un error. `(SolutionDir)\.nuget`se utiliza como la carpeta de inicio.
    `.sln`archivo | Restaurar los paquetes que se identifican por la solución; da como resultado un error si `-SolutionDirectory` se utiliza. `$(SolutionDir)\.nuget`se utiliza como la carpeta de inicio.
    `packages.config`o un archivo de proyecto | Restaurar los paquetes enumerados en el archivo, resolver e instalando dependencias.
    Otros tipos de archivos | Archivo que se supone que un `.sln` archivo anterior; si no es una solución, NuGet da un error.
    (projectPath no especificado) | -NuGet busca archivos de solución en la carpeta actual. Si se encuentra un único archivo, que se utiliza para restaurar paquetes; Si se encuentran varias soluciones, NuGet produce un error.
    |-Si no hay ningún archivo de solución, NuGet busca un `packages.config` y que se utiliza para restaurar los paquetes.
    |-Si no hay ninguna solución o `packages.config` se encuentra el archivo, NuGet produce un error.

1. Determinar la carpeta de paquetes mediante el siguiente orden de prioridad (NuGet produce un error si no se encuentra ninguna de estas carpetas):

    - La carpeta especificada con `-PackagesDirectory`.
    - El `repositoryPath` valor en`Nuget.Config`
    - La carpeta especificada con`-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. Al restaurar paquetes para una solución, NuGet hace lo siguiente:
    - Carga el archivo de solución.
    - Restaura los paquetes de nivel de solución incluidos en `$(SolutionDir)\.nuget\packages.config` en el `packages` carpeta.
    - Restaurar los paquetes enumerados en `$(ProjectDir)\packages.config` en el `packages` carpeta. Para cada paquete especificado, restaurar el paquete en paralelo, a menos que `-DisableParallelProcessing` se especifica.

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
