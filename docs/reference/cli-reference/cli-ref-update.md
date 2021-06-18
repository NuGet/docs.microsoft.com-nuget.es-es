---
title: Comando de actualización de la CLI de NuGet
description: Referencia del comando nuget.exe update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323653"
---
# <a name="update-command-nuget-cli"></a>Comando update (CLI de NuGet)

**Se aplica a: consumo de** &bullet; **paquetes Versiones admitidas:** todas

Actualiza todos los paquetes de un proyecto (mediante `packages.config`) a las versiones más recientes disponibles. Se recomienda ejecutar ["restore"](cli-ref-restore.md) antes de ejecutar `update` . (Para actualizar un paquete individual, use sin especificar un número de versión, en cuyo caso [`nuget install`](cli-ref-install.md) NuGet instala la versión más reciente).

Nota: no funciona con la CLI que se ejecuta `update` en Mono (Mac OSX o Linux) ni cuando se usa el formato PackageReference.

El `update` comando también actualiza las referencias de ensamblado en el archivo de proyecto, siempre que esas referencias ya existan. Si un paquete actualizado tiene un ensamblado agregado, no se agrega *una* nueva referencia. Las nuevas dependencias de paquete tampoco tienen sus referencias de ensamblado agregadas. Para incluir estas operaciones como parte de una actualización, actualice el paquete en Visual Studio mediante la interfaz Administrador de paquetes usuario o la Administrador de paquetes consola.

Este comando también se puede usar para actualizar nuget.exe mediante la *marca -self.*

## <a name="usage"></a>Uso

```cli
nuget update <configPath> [options]
```

donde `<configPath>` identifica un archivo de solución o que enumera las `packages.config` dependencias del proyecto.

## <a name="options"></a>Opciones

- **`-ConfigFile`**

  Archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) `~/.nuget/NuGet/NuGet.Config` o o `~/.config/NuGet/NuGet.Config` (Mac/Linux).
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  Especifica la versión de los paquetes de dependencia que se usarán, que puede ser una de las siguientes:<br/><ul><li>*Más* bajo (valor predeterminado): la versión más baja</li><li>*HighestPatch:* la versión con la revisión principal, secundaria más baja y más alta</li><li>*HighestMinor:* la versión con la revisión más baja principal, secundaria más alta y más alta</li><li>*Más* alto: la versión más alta</li><li>*Omitir:* no se usarán paquetes de dependencia</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Especifica la acción predeterminada cuando ya existe un archivo de un paquete en el proyecto de destino. Establezca en `Overwrite` para sobrescribir siempre los archivos. Establezca en `Ignore` para omitir archivos.

  La acción, el valor predeterminado, solicitará cada archivo en conflicto a menos que se especifique o , que se `PromptUser` aplicará a todos los archivos `OverwriteAll` `IgnoreAll` restantes.

- **`-ForceEnglishOutput`**

  *(3.5+)* Fuerza nuget.exe ejecutar mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-Id`**

  Especifica una lista de los iDs de paquete que se actualizarán.

- **`-MSBuildPath`**

  *(4.0+)* Especifica la ruta de acceso de MSBuild que se usará con el comando , teniendo prioridad sobre `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2+)* Especifica la versión de MSBuild que se usará con este comando. Los valores admitidos son 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. De forma predeterminada, se selecciona MSBuild en la ruta de acceso; de lo contrario, el valor predeterminado es la versión instalada más alta de MSBuild.

- **`-NonInteractive`**

  Suprime las solicitudes de confirmación o entrada del usuario.

- **`-PreRelease`**

  Permite actualizar a versiones preliminares. Esta marca no es necesaria al actualizar los paquetes de versión preliminar que ya están instalados.

- **`-RepositoryPath`**

  Especifica la carpeta local donde se instalan los paquetes.

- **`-Safe`**

  Especifica que solo se instalarán las actualizaciones con la versión más alta disponible dentro de la misma versión principal y secundaria que el paquete instalado.

- **`-Self`**

  Actualizaciones `nuget.exe` a la versión más reciente. `-Source` se puede usar, pero se omiten todos los demás argumentos. Si no se proporciona ningún origen, comprueba `nuget.org` si hay actualizaciones independientemente de la `NuGet.Config` configuración.

- **`-Source`**

  Especifica la lista de orígenes de paquetes (como direcciones URL) que se usarán para las actualizaciones. Si se omite, el comando usa los orígenes proporcionados en los archivos de configuración; vea [Configuraciones comunes de NuGet.](../../consume-packages/configuring-nuget-behavior.md)

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalles que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

- **`-Version`**

  Cuando se usa con un identificador de paquete, especifica la versión del paquete que se actualizará.

Consulte también Variables [de entorno.](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
