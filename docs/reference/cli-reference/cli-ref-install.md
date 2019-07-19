---
title: Comando de instalación de la CLI de NuGet
description: Referencia del comando de instalación de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327792"
---
# <a name="install-command-nuget-cli"></a>Comando install (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: todas

Descarga e instala un paquete en un proyecto, de forma predeterminada en la carpeta actual, con los orígenes de paquete especificados.

> [!Tip]
> Para descargar un paquete directamente fuera del contexto de un proyecto, visite la página del paquete en [Nuget.org](https://www.nuget.org) y seleccione el vínculo de **descarga** .

Si no se especifican orígenes, se usan los que aparecen en el `%appdata%\NuGet\NuGet.Config` archivo de configuración global `~/.nuget/NuGet/NuGet.Config` , (Windows) o (Mac/Linux). Consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md) para obtener más detalles.

Si no se especifica ningún paquete específico `install` , instala todos los paquetes enumerados en el `packages.config` archivo del proyecto, lo que [`restore`](cli-ref-restore.md)hace que sea similar a.

El `install` comando no modifica un archivo de proyecto o `packages.config`; de esta manera es similar a `restore` en que solo agrega paquetes al disco, pero no cambia las dependencias de un proyecto.

Para agregar una dependencia, agregue un paquete a través de la interfaz de usuario del administrador de paquetes o la consola `packages.config` en Visual Studio, `install` o `restore`bien modifique y, a continuación, ejecute o.

## <a name="usage"></a>Uso

```cli
nuget install <packageID | configFilePath> [options]
```

donde `<packageID>` nombra el paquete que se va a instalar (con la versión más `<configFilePath>` reciente) `packages.config` o identifica el archivo que muestra los paquetes que se van a instalar. Puede indicar una versión específica con la `-Version` opción.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| DependencyVersion | *(4.4 +)* La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:<br/><ul><li>*Más bajo* (valor predeterminado): la versión más baja</li><li>*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</li><li>*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</li><li>*Más alto*: la versión más alta</li></ul> |
| DisableParallelProcessing | Deshabilita la instalación de varios paquetes en paralelo. |
| ExcludeVersion | Instala el paquete en una carpeta denominada con solo el nombre del paquete y no el número de versión. |
| FallbackSource | *(3,2 +)* Una lista de orígenes de paquetes que se usarán como reserva en caso de que el paquete no se encuentre en el origen principal o en el predeterminado. |
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Framework | *(4.4 +)* Plataforma de destino que se usa para seleccionar las dependencias. Si no se especifica, el valor predeterminado es "any". |
| Help | Muestra información de ayuda para el comando. |
| NoCache | Impide que NuGet use paquetes almacenados en caché. Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| OutputDirectory | Especifica la carpeta en la que se instalan los paquetes. Si no se especifica ninguna carpeta, se usa la carpeta actual. |
| PackageSaveMode | Especifica los tipos de archivos que se van a guardar después de la `nuspec`instalación `nupkg`del paquete `nuspec;nupkg`: uno de, o. |
| Versión preliminar | Permite la instalación de paquetes de versión preliminar. Esta marca no es necesaria al restaurar paquetes con `packages.config`. |
| RequireConsent | Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes. Para obtener más información, vea [restauración de paquetes](../../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica la carpeta raíz de la solución para la que se van a restaurar los paquetes. |
| source | Especifica la lista de orígenes de paquetes (como direcciones URL) que se va a usar. Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, vea [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |
| `Version` | Especifica la versión del paquete que se va a instalar. |

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
