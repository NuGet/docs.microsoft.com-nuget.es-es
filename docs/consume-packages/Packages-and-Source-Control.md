---
title: Paquetes NuGet y control de código fuente
description: Consideraciones sobre cómo tratar los paquetes de NuGet dentro de los sistemas de control de código fuente y de control de versiones, y cómo omitir paquetes con TFVC y Git.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9d9ea10ccd32bb65ad0d62b591f5e2cb58ea3427
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "69019988"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Omitir paquetes de NuGet en sistemas de control de código fuente

Los desarrolladores suelen ignorar los paquetes de NuGet de sus repositorios de control de código fuente y, en su lugar, se basan en la [restauración de paquetes](package-restore.md) para volver a instalar las dependencias de un proyecto antes de efectuar una compilación.

Entre los motivos por los que confiar en la restauración de paquetes están los siguientes:

1. Los sistemas de control de versiones distribuidos, como Git, incluyen copias completas de cada versión de cada archivo del repositorio. Los archivos binarios que se actualizan con frecuencia provocan un sobredimensionamiento considerable y aumenta el tiempo necesario para clonar el repositorio.
1. Cuando se incluyen paquetes en el repositorio, los desarrolladores tienden a agregar referencias directamente al contenido del paquete en el disco, en lugar de hacer referencia a los paquetes a través de NuGet, con lo que se pueden generar nombres de ruta de acceso codificados de forma rígida en el proyecto.
1. Resulta más difícil limpiar la solución de cualquier carpeta de paquete sin usar, ya que tiene que asegurarse de no eliminar ninguna carpeta de paquete que todavía esté en uso.
1. Mediante la omisión de paquetes, se mantienen limpios los límites de propiedad entre el código y los paquetes de otras personas de las que dependa. Muchos paquetes de NuGet ya se mantienen en sus propios repositorios de control de código fuente.

Aunque la restauración de paquetes es el comportamiento predeterminado en NuGet, es necesario llevar a cabo algunas tareas manuales para omitir los paquetes (es decir, la carpeta `packages` del proyecto) del control de código fuente, tal y como se describe en las secciones siguientes.

## <a name="omitting-packages-with-git"></a>Omitir paquetes con Git

Use el [archivo .gitignore](https://git-scm.com/docs/gitignore) para omitir, entre otras cosas, los paquetes NuGet (`.nupkg`) la carpeta `packages` y `project.assets.json`. Como referencia, vea el [archivo `.gitignore` de ejemplo para los proyectos de Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Las partes importantes del archivo `.gitignore` son:

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Omitir paquetes con Control de versiones de Team Foundation

> [!Note]
> Si es posible, siga estas instrucciones *antes* de agregar el proyecto al control de código fuente. De lo contrario, elimine manualmente la carpeta `packages` del repositorio y registre este cambio antes de continuar.

Para deshabilitar la integración del control de código fuente con TFVC para los archivos seleccionados:

1. Cree una carpeta denominada `.nuget` en la carpeta de la solución (donde se encuentra el archivo `.sln`).
    - Sugerencia: En Windows, para crear esta carpeta en el Explorador de Windows, use el nombre `.nuget.` *con* el punto final.

1. En esa carpeta, cree un archivo denominado `NuGet.Config` y ábralo para editarlo.

1. Agregue el siguiente texto como mínimo, donde el valor [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) indica a Visual Studio que omita todos los elementos de la carpeta `packages`:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Si usa TFS 2010 o versiones anteriores, esconda la carpeta `packages` de sus asignaciones del área de trabajo.

1. En TFS 2012 o versiones posteriores, o en Visual Studio Team Services, cree un archivo `.tfignore` tal como se describe en [Add files to the server](/vsts/tfvc/add-files-server?view=vsts#tfignore) (Agregar archivos al servidor). En ese archivo, incluya el contenido siguiente para ignorar explícitamente las modificaciones efectuadas en la carpeta `\packages` en el nivel de repositorio y en algunos otros archivos intermedios. Puede crear el archivo en el Explorador de Windows usando el nombre `.tfignore.` con el punto final, pero puede que deba deshabilitar primero la opción "Ocultar las extensiones de los tipos de archivo conocidos":

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Agregue `NuGet.Config` y `.tfignore` al control de código fuente y registre sus cambios.
