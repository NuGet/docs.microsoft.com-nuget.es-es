---
title: Comando de instalación de la CLI de NuGet
description: Referencia para el comando de instalación de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e609b01bc14083ce212f6d4d4c6d3412f0ee316b
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508327"
---
# <a name="install-command-nuget-cli"></a>Comando install (CLI de NuGet)

**Se aplica a:** consumo de paquetes &bullet; **versiones compatibles:** todas

Descarga e instala un paquete en un proyecto, de forma predeterminada a la carpeta actual, con los orígenes de paquete especificado.

> [!Tip]
> Para descargar un paquete directamente fuera del contexto de un proyecto, visite la página del paquete en [nuget.org](https://www.nuget.org) y seleccione el **descargar** vínculo.

Si no se especifica ningún origen, aquellos que aparecen en el archivo de configuración global, `%appdata%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), se usan. Consulte [del comportamiento de configuración de NuGet](../consume-packages/configuring-nuget-behavior.md) para obtener más detalles.

Si se especifica ningún paquete específico, `install` instala todos los paquetes enumerados en el proyecto `packages.config` archivo, lo que parece [ `restore` ](cli-ref-restore.md).

El `install` comando no modifica un archivo de proyecto o `packages.config`; de este modo es similar a `restore` en que solo agrega paquetes en el disco pero no cambia las dependencias de un proyecto.

Para agregar una dependencia, agregar un paquete mediante el Administrador de paquetes de interfaz de usuario o la consola en Visual Studio o modificar `packages.config` y, a continuación, ejecute cualquiera `install` o `restore`.

## <a name="usage"></a>Uso

```cli
nuget install <packageID | configFilePath> [options]
```

donde `<packageID>` nombra el paquete que desea instalar (con la versión más reciente), o `<configFilePath>` identifica el `packages.config` archivo que enumera los paquetes que se va a instalar. Puede indicar una versión específica con el `-Version` opción.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| DependencyVersion | *(4.4 +)*  La versión de los paquetes de dependencia para usar, que puede ser uno de los siguientes:<br/><ul><li>*Menor* (valor predeterminado): la versión más antigua</li><li>*HighestPatch*: la versión con la revisión menor principal, secundaria menor, más alta</li><li>*HighestMinor*: la versión con el menor principales, revisiones secundarias y de mayor más alto</li><li>*Mayor*: la versión más alta</li></ul> |
| DisableParallelProcessing | Deshabilita la instalación de varios paquetes en paralelo. |
| ExcludeVersion | Instala el paquete en una carpeta denominada con solo el nombre del paquete y no el número de versión. |
| FallbackSource | *(3.2 y versiones posteriores)*  Una lista de orígenes de paquetes para utilizar como de reservas en caso de que el paquete no se encuentra en el servidor principal o el origen predeterminado. |
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Framework | *(4.4 +)*  Se usa para seleccionar las dependencias de .NET framework de destino. El valor predeterminado es "Any" Si no se especifica. |
| Ayuda | Muestra información de ayuda para el comando. |
| NoCache | Impide que NuGet utilice paquetes almacenados en caché. Consulte [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| No interactivo | Suprime los mensajes para confirmaciones o intervención del usuario. |
| OutputDirectory | Especifica la carpeta donde se instalan los paquetes. Si se especifica ninguna carpeta, se usa la carpeta actual. |
| PackageSaveMode | Especifica los tipos de archivos que se va a guardar tras la instalación del paquete: uno de `nuspec`, `nupkg`, o `nuspec;nupkg`. |
| Versión preliminar | Permite que los paquetes preliminares instalarse. Esta marca no es necesaria al restaurar los paquetes con `packages.config`. |
| RequireConsent | Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes. Para obtener más información, consulte [la restauración del paquete](../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica la carpeta raíz de la solución para que se va a restaurar los paquetes. |
| Origen | Especifica la lista de orígenes de paquetes (como las direcciones URL) para usar. Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, consulte [del comportamiento de configuración de NuGet](../consume-packages/configuring-nuget-behavior.md). |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |
| Versión | Especifica la versión del paquete para instalar. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
