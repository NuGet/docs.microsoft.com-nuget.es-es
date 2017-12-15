---
title: "Comando de instalación de NuGet CLI | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Referencia para el comando de instalación nuget.exe"
keywords: "NuGet instalar referencia, el comando de paquete de instalación"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a>Instale el comando (NuGet CLI)

**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** todos

Descarga e instala un paquete en un proyecto, de forma predeterminada en la carpeta actual, usando orígenes del paquete especificado.

> [!Tip]
> Para descargar un paquete directamente fuera del contexto de un proyecto, visite la página del paquete en [nuget.org](https://www.nuget.org) y seleccione la **descargar** vínculo. 

Si no se especifica ningún origen de los indicados en el archivo de configuración global, `%APPDATA%\NuGet\NuGet.Config`, se utilizan. Vea [configuración de comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md) para obtener más detalles.

Si no se especifica ningún paquete específico, `install` instala todos los paquetes que se muestran en el proyecto `packages.config` archivo, lo que similar a [ `restore` ](#restore). (El `install` comando no funciona con `project.json`.)

El `install` comando no modifica un archivo de proyecto o `packages.config`; de este modo es similar a `restore` ya que se solo agrega paquetes en el disco, pero no cambia las dependencias del proyecto.

Para agregar una dependencia, agregue un proyecto a través del Administrador de paquetes de interfaz de usuario o la consola en Visual Studio o modificar `packages.config` y, a continuación, ejecute cualquiera `install` o `restore`. Para los proyectos con `project.json`, puede modificar ese archivo y, a continuación, ejecutar `restore`.

## <a name="usage"></a>Uso

```
nuget install <packageID | configFilePath> [options]
```

donde `<packageID>` nombres el paquete que desea instalar (con la versión más reciente), o `<configFilePath>` identifica el `packages.config` archivo que enumera los paquetes que se va a instalar. Puede indicar una versión específica con la `-Version` opción.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet el archivo de configuración para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| DisableParallelProcessing | Deshabilita la instalación de varios paquetes en paralelo. |
| ExcludeVersion | Instala el paquete en una carpeta denominada con solo el nombre del paquete y no el número de versión. |
| FallbackSource | *(3.2 +)*  Una lista de orígenes de paquetes que se usará como de reservas en caso de que el paquete no se encuentra en el servidor principal o el origen predeterminado. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Framework | *(4.4 +)*  Utilizado para seleccionar las dependencias de .NET framework de destino. El valor predeterminado es 'Any' Si no se especifica. |
| Ayuda | Muestra información de ayuda para el comando. |
| NoCache | Impide que NuGet use paquetes de memorias caché del equipo local. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| OutputDirectory | Especifica la carpeta en la que se instalan los paquetes. Si no se especifica ninguna carpeta, se usa la carpeta actual. |
| PackageSaveMode | Especifica los tipos de archivos para guardar después de la instalación de paquete: uno de `nuspec`, `nupkg`, o `nuspec;nupkg`. |
| Versión preliminar | Permite que los paquetes de versión preliminar para instalarse. Esta marca no es necesaria al restaurar paquetes con `packages.config`. |
| RequireConsent | Comprueba que la restauración de paquetes está habilitada antes de descargar e instalar los paquetes. Para obtener más información, consulte [la restauración del paquete](../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica la carpeta raíz de la solución para el que se va a restaurar los paquetes. |
| Origen | Especifica la lista de orígenes de paquetes (como las direcciones URL) para usar. Si se omite, el comando utiliza los orígenes proporcionados en archivos de configuración, consulte [NuGet configurar comportamiento](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |
| Versión | Especifica la versión del paquete para instalar. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
