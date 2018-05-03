---
title: Comando de actualización de NuGet CLI
description: Referencia para el comando de actualización nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e6964d92436ce1bac9e6af85f6dae75fcf40378d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="update-command-nuget-cli"></a>comando de actualización (NuGet CLI)

**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** todos

Actualiza todos los paquetes en un proyecto (mediante `packages.config`) a sus versiones más recientes disponibles. Se recomienda ejecutar ['restore'](cli-ref-restore.md) antes de ejecutar el `update`. (Para actualizar un paquete individual, utilice [ `nuget install` ](cli-ref-install.md) sin especificar un número de versión, en el que NuGet mayúscula instala la versión más reciente.)

Nota: `update` no funciona con la CLI ejecutando bajo Mono (Mac OSX o Linux) o cuando se usa el formato PackageReference.

El `update` comando también actualiza las referencias de ensamblado en el archivo de proyecto, proporcionado por las que hace referencia ya existe. Si un paquete actualizado no tiene un ensamblado agregado, es una nueva referencia *no* agregado. También nuevas dependencias de paquete no tienen sus referencias de ensamblado agregados. Para incluir estas operaciones como parte de una actualización, actualice el paquete en Visual Studio mediante la UI del Administrador de paquetes o la consola de administrador de paquetes.

Este comando también puede utilizarse para actualizar nuget.exe propio mediante el *-self* marca.

## <a name="usage"></a>Uso

```cli
nuget update <configPath> [options]
```

donde `<configPath>` identifica ya sea un `packages.config` o un archivo de solución que enumera las dependencias del proyecto.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.|
| FileConflictAction | Especifica la acción que se realizará cuando se le pregunte para sobrescribir u omitir los archivos existentes al que hace referencia el proyecto. Los valores son *sobrescribir, omitir, ninguno*. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| Id. | Especifica una lista de identificadores para la actualización de paquete. |
| MSBuildPath | *(4.0 +)*  Especifica la ruta de acceso de MSBuild para usar con el comando, tiene prioridad sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Especifica la versión de MSBuild que se utilizará con este comando. Valores admitidos son 4, 12, 14, 15. De forma predeterminada, se seleccionará el MSBuild en la ruta de acceso, en caso contrario, valor predeterminado es la última versión instalada de MSBuild. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Versión preliminar | Permite la actualización a las versiones preliminares. Esta marca no es necesaria al actualizar paquetes de versión preliminar que ya están instalados. |
| RepositoryPath | Especifica la carpeta local donde están instalados los paquetes. |
| Seguridad de | Especifica que solo se actualiza con la versión más reciente disponible dentro de la misma versión principal y secundaria tal y como se instalará el paquete instalado. |
| En sí mismo | Nuget.exe actualizaciones a la versión más reciente; todos los demás argumentos se pasan por alto. |
| Origen | Especifica la lista de orígenes de paquetes (como las direcciones URL) para utilizar para las actualizaciones. Si se omite, el comando utiliza los orígenes proporcionados en archivos de configuración, consulte [NuGet configurar comportamiento](../consume-packages/configuring-nuget-behavior.md). |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |
| Versión | Cuando se usa con un Id. de paquete, especifica la versión del paquete para actualizar. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
