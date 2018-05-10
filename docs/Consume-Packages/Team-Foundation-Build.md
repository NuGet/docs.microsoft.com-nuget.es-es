---
title: Tutorial de restauración de paquetes NuGet con Team Foundation Build
description: Tutorial sobre cómo restaurar paquetes de NuGet con Team Foundation Build (TFS y Visual Studio Team Services).
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 5eb8e68b800f623ef41a164f18efff2281e7c7cc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Configurar la restauración de paquetes con Team Foundation Build

En este artículo se ofrece un tutorial detallado sobre cómo restaurar los paquetes como parte de [Team Services Build](/vsts/build-release/index), tanto para Git como para Control de versiones de Team Services.

Aunque este tutorial es específico para el escenario de uso de Visual Studio Team Services, los conceptos también se aplican a otros sistemas de control de versiones y de compilación.

Se aplica a:

- Proyectos de MSBuild personalizados que se ejecutan con cualquier versión de TFS
- Team Foundation Server 2012 o versiones anteriores
- Plantillas personalizadas del proceso de compilación de Team Foundation migradas a TFS 2013 o a una versión posterior
- Se quitaron las plantillas del proceso de compilación que tenían la funcionalidad de restauración de Nuget

Si usa Visual Studio Team Services o Team Foundation Server 2013 con sus plantillas de proceso de compilación, la restauración automática de paquetes tiene lugar como parte del proceso de compilación.

## <a name="the-general-approach"></a>Enfoque general

Una ventaja a la hora de usar NuGet es que puede usarlo para evitar el registro de archivos binarios en el sistema de control de versiones.

Esto resulta muy interesante si usa un [sistema de control de versiones distribuido](http://en.wikipedia.org/wiki/Distributed_revision_control) como Git, porque los desarrolladores necesitan clonar la totalidad del repositorio, incluido el historial completo, antes de poder empezar a trabajar de forma local. El registro de archivos binarios puede causar un importante sobredimensionamiento de repositorios, ya que estos archivos se suelen almacenar sin compresión delta.

NuGet lleva admitiendo desde hace tiempo la [restauración de paquetes](../consume-packages/package-restore.md) como parte de la compilación. La implementación anterior tuvo el dilema del huevo y la gallina en cuanto a los paquetes que querían ampliar el proceso de compilación porque NuGet restauró los paquetes al crear el proyecto. Pero MSBuild no permite extender la compilación durante el proceso. Alguien podría decir que se trata de un problema de MSBuild, pero yo diría que se trata de un problema inherente. En función del aspecto que necesite ampliar, puede que ya sea demasiado tarde para registrarlo en el momento en que se restaure el paquete.

El remedio a este problema consiste en asegurarse de que los paquetes se restauran como primer paso del proceso de compilación:

```cli
nuget restore path\to\solution.sln
```

Cuando el proceso de compilación restaura paquetes antes de compilar el código, no es necesario registrar los archivos `.targets`.

> [!Note]
> Se deben crear paquetes para permitir su carga en Visual Studio. En caso contrario, puede que aún le interese registrar archivos `.targets` para que otros desarrolladores puedan abrir la solución sin tener que restaurar primero los paquetes.

En el siguiente proyecto de demostración se muestra cómo configurar la compilación de tal manera que las carpetas `packages` y los archivos `.targets` no tengan que registrarse. También se muestra cómo configurar una compilación automatizada en Team Foundation Service para este proyecto de ejemplo.

## <a name="repository-structure"></a>Estructura del repositorio

Nuestro proyecto de demostración es una simple herramienta de línea de comandos que usa el argumento de la línea de comandos para efectuar consultas en Bing. Tiene como destino .NET Framework 4 y usa muchos de los [paquetes BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) y [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

La estructura del repositorio tiene el siguiente aspecto:

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

Puede ver que no hemos registrado la carpeta `packages` ni ningún archivo `.targets`.

Pero sí hemos registrado el archivo `nuget.exe`, ya que es necesario durante la compilación. Siguiendo unas convenciones de uso extendido, lo hemos registrado en una carpeta `tools` compartida.

El código fuente está en la carpeta `src`. Aunque en nuestra demostración solo se usa una solución, es fácil imaginar que esta carpeta contiene más de una solución.

### <a name="ignore-files"></a>Omitir archivos

> [!Note]
> Actualmente hay un [problema conocido en el cliente de NuGet](https://nuget.codeplex.com/workitem/4072) que hace que el cliente siga agregando la carpeta `packages` al control de versiones. Una solución consiste en deshabilitar la integración del control de código fuente. Para ello, necesitará un archivo `Nuget.Config ` en la carpeta `.nuget` que sea paralelo a la solución. Si esta carpeta aún no existe, tendrá que crearla. En [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), agregue el siguiente contenido:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Con el fin de comunicar al control de versiones que no pretendemos insertar las carpetas **packages** en el repositorio, también hemos agregado archivos de omisión para el control de versiones de Git (`.gitignore`) y de TF (`.tfignore`). En estos archivos se describen los patrones de archivos que no quiere insertar en el repositorio.

El archivo `.gitignore` tiene el siguiente aspecto:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

El archivo `.gitignore` es [bastante eficaz](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Por ejemplo, si por lo general no quiere insertar en el repositorio el contenido de la carpeta `packages` sino que quiere optar por las instrucciones anteriores para insertar los archivos `.targets`, podría aplicar esta regla:

    packages
    !packages/**/*.targets

Se excluirán todas las carpetas `packages`, pero se volverán a incluir todos los archivos `.targets` incluidos. Por cierto, [aquí](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore) encontrará una plantilla para archivos `.gitignore` diseñada específicamente para las necesidades de los desarrolladores de Visual Studio.

El control de versiones de TF admite un mecanismo muy parecido mediante el archivo [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control). La sintaxis es prácticamente la misma:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

Para nuestra demostración, el proceso de compilación es bastante sencillo. Vamos a crear un proyecto de MSBuild que compile todas las soluciones y nos aseguraremos de que los paquetes se restauren antes de compilar las soluciones.

Este proyecto tendrá los tres destinos convencionales `Clean`, `Build` y `Rebuild`, así como el nuevo destino `RestorePackages`.

- Los destinos `Build` y `Rebuild` dependen de `RestorePackages`. Así se garantiza que puede ejecutar `Build` y `Rebuild` y que puede confiar en los paquetes que se están restaurando.
- `Clean`, `Build` y `Rebuild` invocan el destino de MSBuild correspondiente en todos los archivos de la solución.
- El destino `RestorePackages` invoca a `nuget.exe` para cada archivo de la solución. Esto se hace usando la [funcionalidad de procesamiento por lotes de MSBuild](/visualstudio/msbuild/msbuild-batching).

El resultado es el siguiente:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>Configurar Team Build

Team Build ofrece varias plantillas de proceso. Para esta demostración usaremos Team Foundation Service. Las instalaciones locales de TFS serán muy parecidas.

El control de versiones de Git y TF tiene diferentes plantillas de Team Build, por lo que los pasos siguientes variarán en función del sistema de control de versiones que use. En ambos casos, lo único que tiene que hacer es seleccionar build.proj como el proyecto que va a crear.

En primer lugar, echemos un vistazo a la plantilla de proceso de Git. En la plantilla basada en Git, la compilación se selecciona a través de la propiedad `Solution to build`:

![Proceso de compilación para Git](media/PackageRestoreTeamBuildGit.png)

Tenga en cuenta que esta propiedad es una ubicación del repositorio. Puesto que el archivo `build.proj` está en la raíz, hemos usado `build.proj`. Si coloca el archivo de compilación en una carpeta denominada `tools`, el valor sería `tools\build.proj`.

En la plantilla de control de versiones de TF, el proyecto se selecciona a través de la propiedad `Projects`:

![Proceso de compilación para TFVC](media/PackageRestoreTeamBuildTFVC.png)

A diferencia de la plantilla basada en Git, el control de versiones de TF admite los selectores (el botón situado en el lado derecho con los tres puntos). Por eso, para evitar errores de escritura, le recomendamos que los use para seleccionar el proyecto.
