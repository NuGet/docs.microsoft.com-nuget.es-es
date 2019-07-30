---
title: Administración de paquetes NuGet con la CLI de nuget.exe
description: Instrucciones de uso de la CLI de nuget.exe para trabajar con paquetes NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9eefed6f2c1a362f27c4a5d33d07645d743379fa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317747"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="365d7-103">Administración de paquetes con la CLI de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="365d7-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="365d7-104">La herramienta CLI permite actualizar y restaurar fácilmente paquetes NuGet en proyectos y soluciones.</span><span class="sxs-lookup"><span data-stu-id="365d7-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="365d7-105">Esta herramienta ofrece todas las funcionalidades de NuGet en Windows, además de la mayoría de las características en Mac y Linux cuando se ejecutan con Mono.</span><span class="sxs-lookup"><span data-stu-id="365d7-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="365d7-106">La CLI de `nuget.exe` está diseñada para proyectos .NET Framework y para proyectos que no son de estilo SDK (por ejemplo, los destinados a bibliotecas .NET Standard).</span><span class="sxs-lookup"><span data-stu-id="365d7-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="365d7-107">Si usa un proyecto que no es de estilo SDK migrado a `PackageReference`, use la CLI de `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="365d7-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="365d7-108">La CLI de `nuget.exe` requiere un archivo [packages.config](../reference/packages-config.md) para las referencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="365d7-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="365d7-109">En la mayoría de los escenarios, recomendamos [migrar los proyectos que no son de estilo SDK](../reference/migrate-packages-config-to-package-reference.md) que usan `packages.config` a PackageReference. Después, podrá usar la CLI de `dotnet` en lugar de la CLI de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="365d7-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="365d7-110">La migración no está disponible actualmente para proyectos de C++ y ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="365d7-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="365d7-111">En este artículo se muestra el uso básico de algunos de los comandos más comunes de la CLI de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="365d7-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="365d7-112">Para la mayoría de estos comandos, la herramienta CLI busca un archivo de proyecto en el directorio actual, a menos que se especifique un archivo de proyecto en el comando.</span><span class="sxs-lookup"><span data-stu-id="365d7-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="365d7-113">Para obtener una lista completa de los comandos y los argumentos que puede usar, consulte la [Referencia de CLI de NuGet](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="365d7-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="365d7-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="365d7-114">Prerequisites</span></span>

- <span data-ttu-id="365d7-115">Instale la CLI de `nuget.exe` descargándola desde [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), guarde el archivo `.exe` en la carpeta adecuada y agregue esa carpeta a la variable de entorno PATH.</span><span class="sxs-lookup"><span data-stu-id="365d7-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="365d7-116">Instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="365d7-116">Install a package</span></span>

<span data-ttu-id="365d7-117">El comando [install](../reference/cli-reference/cli-ref-install.md) descarga e instala un paquete en un proyecto, de forma predeterminada en la carpeta actual, mediante los orígenes de paquetes especificados.</span><span class="sxs-lookup"><span data-stu-id="365d7-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="365d7-118">Instale los paquetes nuevos en la carpeta *packages* del directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="365d7-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="365d7-119">El comando `install` no modifica ningún archivo del proyecto ni *packages.config*. En este sentido se parece a `restore`, ya que solo agrega paquetes al disco, sin cambiar las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="365d7-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="365d7-120">Para agregar una dependencia, puede agregar un paquete mediante la interfaz de usuario del Administrador de paquetes o la consola en Visual Studio, o bien modificar *packages.config* y, luego, ejecutar `install` o `restore`.</span><span class="sxs-lookup"><span data-stu-id="365d7-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="365d7-121">Abra una línea de comandos y cambie al directorio que contiene el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="365d7-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="365d7-122">Use el comando siguiente para instalar un paquete NuGet en la carpeta *packages*.</span><span class="sxs-lookup"><span data-stu-id="365d7-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="365d7-123">Para instalar el paquete `Newtonsoft.json` en la carpeta *packages*, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="365d7-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="365d7-124">Como alternativa, puede usar el comando siguiente para instalar un paquete NuGet con un archivo `packages.config` existente en la carpeta *packages*.</span><span class="sxs-lookup"><span data-stu-id="365d7-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="365d7-125">Esto no agrega el paquete a las dependencias del proyecto, sino que lo instala de forma local.</span><span class="sxs-lookup"><span data-stu-id="365d7-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="365d7-126">Instalación de una versión específica de un paquete</span><span class="sxs-lookup"><span data-stu-id="365d7-126">Install a specific version of a package</span></span>

<span data-ttu-id="365d7-127">Si no se especifica la versión cuando se usa el comando [install](../reference/cli-reference/cli-ref-install.md), NuGet instala la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="365d7-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="365d7-128">También puede instalar una versión específica de un paquete NuGet:</span><span class="sxs-lookup"><span data-stu-id="365d7-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="365d7-129">Por ejemplo, para agregar la versión 12.0.1 del paquete `Newtonsoft.json`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="365d7-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="365d7-130">Para obtener más información sobre las limitaciones y el comportamiento de `install`, consulte [Instalar un paquete](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="365d7-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="365d7-131">Eliminación de un paquete</span><span class="sxs-lookup"><span data-stu-id="365d7-131">Remove a package</span></span>

<span data-ttu-id="365d7-132">Para quitar uno o varios paquetes, elimine los que ya no le interesen de la carpeta *packages*.</span><span class="sxs-lookup"><span data-stu-id="365d7-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="365d7-133">Si quiere volver a instalarlos, use el comando `restore` o `install`.</span><span class="sxs-lookup"><span data-stu-id="365d7-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="365d7-134">Enumeración de paquetes</span><span class="sxs-lookup"><span data-stu-id="365d7-134">List packages</span></span>

<span data-ttu-id="365d7-135">Puede mostrar una lista de paquetes de un origen determinado mediante el comando [list](../reference/cli-reference/cli-ref-list.md).</span><span class="sxs-lookup"><span data-stu-id="365d7-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="365d7-136">Use la opción `-Source` para restringir la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="365d7-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="365d7-137">Por ejemplo, enumere los paquetes de la carpeta *packages*.</span><span class="sxs-lookup"><span data-stu-id="365d7-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="365d7-138">Si usa un término de búsqueda, la búsqueda incluirá nombres de paquetes, etiquetas y descripciones de paquetes.</span><span class="sxs-lookup"><span data-stu-id="365d7-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="365d7-139">Actualización de un paquete individual</span><span class="sxs-lookup"><span data-stu-id="365d7-139">Update an individual package</span></span>

<span data-ttu-id="365d7-140">A menos que se especifique la versión del paquete, NuGet instala la versión más reciente del paquete cuando se usa el comando `install`.</span><span class="sxs-lookup"><span data-stu-id="365d7-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="365d7-141">Actualización de todos los paquetes</span><span class="sxs-lookup"><span data-stu-id="365d7-141">Update all packages</span></span>

<span data-ttu-id="365d7-142">Use el comando [update](../reference/cli-reference/cli-ref-update.md) para actualizar todos los paquetes.</span><span class="sxs-lookup"><span data-stu-id="365d7-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="365d7-143">Actualiza todos los paquetes de un proyecto (mediante `packages.config`) a las versiones más recientes disponibles.</span><span class="sxs-lookup"><span data-stu-id="365d7-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="365d7-144">Se recomienda ejecutar `restore` antes de `update`.</span><span class="sxs-lookup"><span data-stu-id="365d7-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="365d7-145">Restaurar paquetes</span><span class="sxs-lookup"><span data-stu-id="365d7-145">Restore packages</span></span>

<span data-ttu-id="365d7-146">Use el comando [restore](../reference/cli-reference/cli-ref-restore.md), que descarga e instala los paquetes que faltan en la carpeta *packages*.</span><span class="sxs-lookup"><span data-stu-id="365d7-146">Use the [restore](../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="365d7-147">`restore` solo agrega paquetes en el disco, pero no cambia las dependencias de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="365d7-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="365d7-148">Para restaurar las dependencias del proyecto, modifique `packages.config` y use el comando `restore`.</span><span class="sxs-lookup"><span data-stu-id="365d7-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="365d7-149">Como con los otros comandos de la CLI de `nuget.exe`, primero abra una línea de comandos y cambie al directorio que contiene el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="365d7-149">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="365d7-150">Para restaurar un paquete con `restore`:</span><span class="sxs-lookup"><span data-stu-id="365d7-150">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```