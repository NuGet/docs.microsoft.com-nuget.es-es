---
title: Tutorial de restauración de paquetes NuGet con Team Foundation Build
description: Tutorial sobre cómo restaurar paquetes de NuGet con Team Foundation Build (TFS y Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0e69491525fce03e504d9d455bee2718510c83c2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549890"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="2d78e-103">Configurar la restauración de paquetes con Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="2d78e-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="2d78e-104">En este artículo se ofrece un tutorial detallado sobre cómo restaurar los paquetes como parte de [Team Services Build](/vsts/build-release/index), tanto para Git como para Control de versiones de Team Services.</span><span class="sxs-lookup"><span data-stu-id="2d78e-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="2d78e-105">Aunque este tutorial es específico para el escenario de uso de Visual Studio Team Services, los conceptos también se aplican a otros sistemas de control de versiones y de compilación.</span><span class="sxs-lookup"><span data-stu-id="2d78e-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="2d78e-106">Se aplica a:</span><span class="sxs-lookup"><span data-stu-id="2d78e-106">Applies To:</span></span>

- <span data-ttu-id="2d78e-107">Proyectos de MSBuild personalizados que se ejecutan con cualquier versión de TFS</span><span class="sxs-lookup"><span data-stu-id="2d78e-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="2d78e-108">Team Foundation Server 2012 o versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="2d78e-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="2d78e-109">Plantillas personalizadas del proceso de compilación de Team Foundation migradas a TFS 2013 o a una versión posterior</span><span class="sxs-lookup"><span data-stu-id="2d78e-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="2d78e-110">Se quitaron las plantillas del proceso de compilación que tenían la funcionalidad de restauración de Nuget</span><span class="sxs-lookup"><span data-stu-id="2d78e-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="2d78e-111">Si usa Visual Studio Team Services o Team Foundation Server 2013 con sus plantillas de proceso de compilación, la restauración automática de paquetes tiene lugar como parte del proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="2d78e-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="2d78e-112">Enfoque general</span><span class="sxs-lookup"><span data-stu-id="2d78e-112">The general approach</span></span>

<span data-ttu-id="2d78e-113">Una ventaja a la hora de usar NuGet es que puede usarlo para evitar el registro de archivos binarios en el sistema de control de versiones.</span><span class="sxs-lookup"><span data-stu-id="2d78e-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="2d78e-114">Esto resulta muy interesante si usa un [sistema de control de versiones distribuido](http://en.wikipedia.org/wiki/Distributed_revision_control) como Git, porque los desarrolladores necesitan clonar la totalidad del repositorio, incluido el historial completo, antes de poder empezar a trabajar de forma local.</span><span class="sxs-lookup"><span data-stu-id="2d78e-114">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="2d78e-115">El registro de archivos binarios puede causar un importante sobredimensionamiento de repositorios, ya que estos archivos se suelen almacenar sin compresión delta.</span><span class="sxs-lookup"><span data-stu-id="2d78e-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="2d78e-116">NuGet lleva admitiendo desde hace tiempo la [restauración de paquetes](../consume-packages/package-restore.md) como parte de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2d78e-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="2d78e-117">La implementación anterior tuvo el dilema del huevo y la gallina en cuanto a los paquetes que querían ampliar el proceso de compilación porque NuGet restauró los paquetes al crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2d78e-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="2d78e-118">Pero MSBuild no permite extender la compilación durante el proceso. Alguien podría decir que se trata de un problema de MSBuild, pero yo diría que se trata de un problema inherente.</span><span class="sxs-lookup"><span data-stu-id="2d78e-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="2d78e-119">En función del aspecto que necesite ampliar, puede que ya sea demasiado tarde para registrarlo en el momento en que se restaure el paquete.</span><span class="sxs-lookup"><span data-stu-id="2d78e-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="2d78e-120">El remedio a este problema consiste en asegurarse de que los paquetes se restauran como primer paso del proceso de compilación:</span><span class="sxs-lookup"><span data-stu-id="2d78e-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="2d78e-121">Cuando el proceso de compilación restaura paquetes antes de compilar el código, no es necesario registrar los archivos `.targets`.</span><span class="sxs-lookup"><span data-stu-id="2d78e-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="2d78e-122">Se deben crear paquetes para permitir su carga en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d78e-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="2d78e-123">En caso contrario, puede que aún le interese registrar archivos `.targets` para que otros desarrolladores puedan abrir la solución sin tener que restaurar primero los paquetes.</span><span class="sxs-lookup"><span data-stu-id="2d78e-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="2d78e-124">En el siguiente proyecto de demostración se muestra cómo configurar la compilación de tal manera que las carpetas `packages` y los archivos `.targets` no tengan que registrarse.</span><span class="sxs-lookup"><span data-stu-id="2d78e-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="2d78e-125">También se muestra cómo configurar una compilación automatizada en Team Foundation Service para este proyecto de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2d78e-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="2d78e-126">Estructura del repositorio</span><span class="sxs-lookup"><span data-stu-id="2d78e-126">Repository structure</span></span>

<span data-ttu-id="2d78e-127">Nuestro proyecto de demostración es una simple herramienta de línea de comandos que usa el argumento de la línea de comandos para efectuar consultas en Bing.</span><span class="sxs-lookup"><span data-stu-id="2d78e-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="2d78e-128">Tiene como destino .NET Framework 4 y usa muchos de los [paquetes BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) y [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="2d78e-128">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="2d78e-129">La estructura del repositorio tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="2d78e-129">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="2d78e-130">Puede ver que no hemos registrado la carpeta `packages` ni ningún archivo `.targets`.</span><span class="sxs-lookup"><span data-stu-id="2d78e-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="2d78e-131">Pero sí hemos registrado el archivo `nuget.exe`, ya que es necesario durante la compilación.</span><span class="sxs-lookup"><span data-stu-id="2d78e-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="2d78e-132">Siguiendo unas convenciones de uso extendido, lo hemos registrado en una carpeta `tools` compartida.</span><span class="sxs-lookup"><span data-stu-id="2d78e-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="2d78e-133">El código fuente está en la carpeta `src`.</span><span class="sxs-lookup"><span data-stu-id="2d78e-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="2d78e-134">Aunque en nuestra demostración solo se usa una solución, es fácil imaginar que esta carpeta contiene más de una solución.</span><span class="sxs-lookup"><span data-stu-id="2d78e-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="2d78e-135">Omitir archivos</span><span class="sxs-lookup"><span data-stu-id="2d78e-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="2d78e-136">Actualmente hay un [problema conocido en el cliente de NuGet](https://nuget.codeplex.com/workitem/4072) que hace que el cliente siga agregando la carpeta `packages` al control de versiones.</span><span class="sxs-lookup"><span data-stu-id="2d78e-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="2d78e-137">Una solución consiste en deshabilitar la integración del control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="2d78e-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="2d78e-138">Para ello, necesitará un archivo `Nuget.Config ` en la carpeta `.nuget` que sea paralelo a la solución.</span><span class="sxs-lookup"><span data-stu-id="2d78e-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="2d78e-139">Si esta carpeta aún no existe, tendrá que crearla.</span><span class="sxs-lookup"><span data-stu-id="2d78e-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="2d78e-140">En [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), agregue el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="2d78e-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="2d78e-141">Con el fin de comunicar al control de versiones que no pretendemos insertar las carpetas **packages** en el repositorio, también hemos agregado archivos de omisión para el control de versiones de Git (`.gitignore`) y de TF (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="2d78e-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="2d78e-142">En estos archivos se describen los patrones de archivos que no quiere insertar en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="2d78e-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="2d78e-143">El archivo `.gitignore` tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="2d78e-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="2d78e-144">El archivo `.gitignore` es [bastante eficaz](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="2d78e-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="2d78e-145">Por ejemplo, si por lo general no quiere insertar en el repositorio el contenido de la carpeta `packages` sino que quiere optar por las instrucciones anteriores para insertar los archivos `.targets`, podría aplicar esta regla:</span><span class="sxs-lookup"><span data-stu-id="2d78e-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="2d78e-146">Se excluirán todas las carpetas `packages`, pero se volverán a incluir todos los archivos `.targets` incluidos.</span><span class="sxs-lookup"><span data-stu-id="2d78e-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="2d78e-147">Por cierto, [aquí](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore) encontrará una plantilla para archivos `.gitignore` diseñada específicamente para las necesidades de los desarrolladores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d78e-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="2d78e-148">El control de versiones de TF admite un mecanismo muy parecido mediante el archivo [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control).</span><span class="sxs-lookup"><span data-stu-id="2d78e-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="2d78e-149">La sintaxis es prácticamente la misma:</span><span class="sxs-lookup"><span data-stu-id="2d78e-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="2d78e-150">build.proj</span><span class="sxs-lookup"><span data-stu-id="2d78e-150">build.proj</span></span>

<span data-ttu-id="2d78e-151">Para nuestra demostración, el proceso de compilación es bastante sencillo.</span><span class="sxs-lookup"><span data-stu-id="2d78e-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="2d78e-152">Vamos a crear un proyecto de MSBuild que compile todas las soluciones y nos aseguraremos de que los paquetes se restauren antes de compilar las soluciones.</span><span class="sxs-lookup"><span data-stu-id="2d78e-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="2d78e-153">Este proyecto tendrá los tres destinos convencionales `Clean`, `Build` y `Rebuild`, así como el nuevo destino `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="2d78e-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="2d78e-154">Los destinos `Build` y `Rebuild` dependen de `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="2d78e-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="2d78e-155">Así se garantiza que puede ejecutar `Build` y `Rebuild` y que puede confiar en los paquetes que se están restaurando.</span><span class="sxs-lookup"><span data-stu-id="2d78e-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="2d78e-156">`Clean`, `Build` y `Rebuild` invocan el destino de MSBuild correspondiente en todos los archivos de la solución.</span><span class="sxs-lookup"><span data-stu-id="2d78e-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="2d78e-157">El destino `RestorePackages` invoca a `nuget.exe` para cada archivo de la solución.</span><span class="sxs-lookup"><span data-stu-id="2d78e-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="2d78e-158">Esto se hace usando la [funcionalidad de procesamiento por lotes de MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="2d78e-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="2d78e-159">El resultado es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="2d78e-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="2d78e-160">Configurar Team Build</span><span class="sxs-lookup"><span data-stu-id="2d78e-160">Configuring Team Build</span></span>

<span data-ttu-id="2d78e-161">Team Build ofrece varias plantillas de proceso.</span><span class="sxs-lookup"><span data-stu-id="2d78e-161">Team Build offers various process templates.</span></span> <span data-ttu-id="2d78e-162">Para esta demostración usaremos Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="2d78e-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="2d78e-163">Las instalaciones locales de TFS serán muy parecidas.</span><span class="sxs-lookup"><span data-stu-id="2d78e-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="2d78e-164">El control de versiones de Git y TF tiene diferentes plantillas de Team Build, por lo que los pasos siguientes variarán en función del sistema de control de versiones que use.</span><span class="sxs-lookup"><span data-stu-id="2d78e-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="2d78e-165">En ambos casos, lo único que tiene que hacer es seleccionar build.proj como el proyecto que va a crear.</span><span class="sxs-lookup"><span data-stu-id="2d78e-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="2d78e-166">En primer lugar, echemos un vistazo a la plantilla de proceso de Git.</span><span class="sxs-lookup"><span data-stu-id="2d78e-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="2d78e-167">En la plantilla basada en Git, la compilación se selecciona a través de la propiedad `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="2d78e-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Proceso de compilación para Git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="2d78e-169">Tenga en cuenta que esta propiedad es una ubicación del repositorio.</span><span class="sxs-lookup"><span data-stu-id="2d78e-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="2d78e-170">Puesto que el archivo `build.proj` está en la raíz, hemos usado `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="2d78e-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="2d78e-171">Si coloca el archivo de compilación en una carpeta denominada `tools`, el valor sería `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="2d78e-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="2d78e-172">En la plantilla de control de versiones de TF, el proyecto se selecciona a través de la propiedad `Projects`:</span><span class="sxs-lookup"><span data-stu-id="2d78e-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Proceso de compilación para TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="2d78e-174">A diferencia de la plantilla basada en Git, el control de versiones de TF admite los selectores (el botón situado en el lado derecho con los tres puntos).</span><span class="sxs-lookup"><span data-stu-id="2d78e-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="2d78e-175">Por eso, para evitar errores de escritura, le recomendamos que los use para seleccionar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2d78e-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
