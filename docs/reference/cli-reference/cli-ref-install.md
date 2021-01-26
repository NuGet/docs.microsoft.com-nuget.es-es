---
title: Comando de instalación de la CLI de NuGet
description: Referencia del comando de instalación de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779259"
---
# <a name="install-command-nuget-cli"></a>comando de instalación (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: todas

Descarga e instala un paquete en un proyecto, de forma predeterminada en la carpeta actual, con los orígenes de paquete especificados.

> [!Tip]
> Para descargar un paquete directamente fuera del contexto de un proyecto, visite la página del paquete en [Nuget.org](https://www.nuget.org) y seleccione el vínculo de **descarga** .

Si no se especifican orígenes, se usan los que aparecen en el archivo de configuración global, `%appdata%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux). Consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md) para obtener más detalles.

Si no se especifica ningún paquete específico, `install` instala todos los paquetes enumerados en el `packages.config` archivo del proyecto, lo que hace que sea similar a [`restore`](cli-ref-restore.md) .

El `install` comando no modifica un archivo de proyecto o `packages.config` ; de esta manera es similar a `restore` en que solo agrega paquetes al disco, pero no cambia las dependencias de un proyecto.

Para agregar una dependencia, agregue un paquete a través de la interfaz de usuario del administrador de paquetes o la consola en Visual Studio, o bien modifique `packages.config` y, a continuación, ejecute `install` o `restore` .

## <a name="usage"></a>Uso

```cli
nuget install <packageID | configFilePath> [options]
```

donde `<packageID>` nombra el paquete que se va a instalar (con la versión más reciente) o `<configFilePath>` identifica el `packages.config` archivo que muestra los paquetes que se van a instalar. Puede indicar una versión específica con la `-Version` opción.

## <a name="options"></a>Opciones

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DependencyVersion`**

  *(4.4 +)* La versión de los paquetes de dependencia que se va a usar, que puede ser una de las siguientes:<br/><ul><li>*Más bajo* (valor predeterminado): la versión más baja</li><li>*HighestPatch*: la versión con la revisión principal más baja, menor menor y más alta.</li><li>*HighestMinor*: la versión con el reenvío más bajo principal, más alto, más alto</li><li>*Más alto*: la versión más alta</li><li>*Omitir*: no se usarán paquetes de dependencia</li></ul>

- **`-DirectDownload`**

  Descargar directamente sin llenar ninguna caché con metadatos o binarios.

- **`-DisableParallelProcessing`**

  Deshabilita la instalación de varios paquetes en paralelo.

- **`-x|-ExcludeVersion`**

  Instala el paquete en una carpeta denominada con solo el nombre del paquete y no el número de versión.

- **`-FallbackSource`**

  *(3,2 +)* Una lista de orígenes de paquetes que se usarán como reserva en caso de que el paquete no se encuentre en el origen principal o en el predeterminado.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-Framework`**

  *(4.4 +)* Plataforma de destino que se usa para seleccionar las dependencias. Si no se especifica, el valor predeterminado es "any".

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-NoCache`**

  Impide que NuGet use paquetes almacenados en caché. Consulte [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-OutputDirectory`**

  Especifica la carpeta en la que se instalan los paquetes. Si no se especifica ninguna carpeta, se usa la carpeta actual.

- **`-PackageSaveMode`**

  Especifica los tipos de archivos que se van a guardar después de la instalación del paquete: uno de `nuspec` , `nupkg` o `nuspec;nupkg` .

- **`-PreRelease`**

  Permite que se instalen paquetes de versión preliminar. Esta marca no es necesaria al restaurar paquetes con `packages.config` .

- **`-RequireConsent`**

  Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes. Para obtener más información, vea [restauración de paquetes](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Especifica la carpeta raíz de la solución para la que se van a restaurar los paquetes.

- **`-Source`**

   Especifica la lista de orígenes de paquetes (como direcciones URL) que se va a usar. Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración, vea [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

- **`-Version`**

  Permite especificar la versión del paquete que se instalará.

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
