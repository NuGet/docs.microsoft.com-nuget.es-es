---
title: Comando de instalación de la CLI de NuGet
description: Referencia del comando de instalación de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036947"
---
# <a name="install-command-nuget-cli"></a>Comando install (CLI de NuGet)

**Se aplica a: consumo de** paquetes &bullet; **versiones admitidas:** todos

Descarga e instala un paquete en un proyecto, de forma predeterminada en la carpeta actual, con los orígenes de paquete especificados.

> [!Tip]
> Para descargar un paquete directamente fuera del contexto de un proyecto, visite la página del paquete en [Nuget.org](https://www.nuget.org) y seleccione el vínculo de **descarga** .

Si no se especifica ningún origen, se usan los que aparecen en el archivo de configuración global, `%appdata%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux). Consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md) para obtener más detalles.

Si no se especifica ningún paquete específico, `install` instala todos los paquetes enumerados en el archivo de `packages.config` del proyecto, lo que hace que sea similar a [`restore`](cli-ref-restore.md).

El comando `install` no modifica un archivo de proyecto o `packages.config`; de este modo, es similar a `restore` en que solo agrega paquetes al disco, pero no cambia las dependencias de un proyecto.

Para agregar una dependencia, agregue un paquete a través de la interfaz de usuario o la consola del administrador de paquetes en Visual Studio, o bien modifique `packages.config` y, a continuación, ejecute `install` o `restore`.

## <a name="usage"></a>Uso

```cli
nuget install <packageID | configFilePath> [options]
```

donde `<packageID>` nombra el paquete que se va a instalar (con la versión más reciente) o `<configFilePath>` identifica el archivo `packages.config` que muestra los paquetes que se van a instalar. Puede indicar una versión específica con la opción `-Version`.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, se usa `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| DependencyVersion | *(4.4 +)* La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:<br/><ul><li>*Más bajo* (valor predeterminado): la versión más baja</li><li>*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</li><li>*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</li><li>*Más alto*: la versión más alta</li><li>*Omitir*: no se usarán paquetes de dependencia</li></ul> |
| DisableParallelProcessing | Deshabilita la instalación de varios paquetes en paralelo. |
| ExcludeVersion | Instala el paquete en una carpeta denominada con solo el nombre del paquete y no el número de versión. |
| FallbackSource | *(3,2 +)* Una lista de orígenes de paquetes que se usarán como reserva en caso de que el paquete no se encuentre en el origen principal o en el predeterminado. |
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| marco | *(4.4 +)* Plataforma de destino que se usa para seleccionar las dependencias. Si no se especifica, el valor predeterminado es "any". |
| Ayuda | Muestra información de ayuda para el comando. |
| NoCache | Impide que NuGet use paquetes almacenados en caché. Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| OutputDirectory | Especifica la carpeta en la que se instalan los paquetes. Si no se especifica ninguna carpeta, se usa la carpeta actual. |
| PackageSaveMode | Especifica los tipos de archivos que se van a guardar después de la instalación del paquete: uno de `nuspec`, `nupkg`o `nuspec;nupkg`. |
| PreRelease | Permite la instalación de paquetes de versión preliminar. Esta marca no es necesaria al restaurar paquetes con `packages.config`. |
| RequireConsent | Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes. Para obtener más información, vea [restauración de paquetes](../../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica la carpeta raíz de la solución para la que se van a restaurar los paquetes. |
| Source | Especifica la lista de orígenes de paquetes (como direcciones URL) que se va a usar. Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, vea [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |
| Versión | Permite especificar la versión del paquete que se instalará. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
