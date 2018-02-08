---
title: Contenido del archivo project.json de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Se han quitado fragmentos de información diversa del contenido de project.json en otras áreas de la documentación de NuGet."
keywords: Archivo project.json de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 42a40c6c637839c13effc9e476ac5702a92cfd2a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="748ba-104">archivo project.json</span><span class="sxs-lookup"><span data-stu-id="748ba-104">project.json archive</span></span>

<span data-ttu-id="748ba-105">El formato de referencia `project.json` se presentó con NuGet 3.x y se ha usado con ciertos tipos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="748ba-105">The `project.json` reference format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="748ba-106">Ha quedado en desuso con la presentación del formato PackageReference, en el que las dependencias se muestran directamente en un archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="748ba-106">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="748ba-107">Vea también:</span><span class="sxs-lookup"><span data-stu-id="748ba-107">Also see:</span></span>

- [<span data-ttu-id="748ba-108">esquema project.json</span><span class="sxs-lookup"><span data-stu-id="748ba-108">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="748ba-109">impacto de project.json en los autores de paquetes</span><span class="sxs-lookup"><span data-stu-id="748ba-109">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="748ba-110">project.json y UWP</span><span class="sxs-lookup"><span data-stu-id="748ba-110">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-reference-format"></a><span data-ttu-id="748ba-111">formato de referencia project.json</span><span class="sxs-lookup"><span data-stu-id="748ba-111">project.json reference format</span></span>

<span data-ttu-id="748ba-112">*Originalmente en [Restauración de paquetes](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="748ba-112">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="748ba-113">En la lista de formatos de referencia:</span><span class="sxs-lookup"><span data-stu-id="748ba-113">In the list of reference formats:</span></span>

- <span data-ttu-id="748ba-114">[`project.json`](project-json.md): *(en desuso)* Archivo JSON que mantiene la lista de las dependencias del proyecto con un gráfico general del paquete en un archivo asociado, `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-114">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="748ba-115">Este formato ha quedado en desuso en beneficio de PackageReference.</span><span class="sxs-lookup"><span data-stu-id="748ba-115">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="748ba-116">nuget restore en Mono</span><span class="sxs-lookup"><span data-stu-id="748ba-116">nuget restore on Mono</span></span>

<span data-ttu-id="748ba-117">*Originalmente en [Instalación de las herramientas del cliente NuGet](../install-nuget-client-tools.md)*</span><span class="sxs-lookup"><span data-stu-id="748ba-117">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="748ba-118">Funciona con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-118">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="748ba-119">Restricción de versiones de paquetes con la restauración</span><span class="sxs-lookup"><span data-stu-id="748ba-119">Constraining package versions with restore</span></span>

<span data-ttu-id="748ba-120">*Originalmente en [Restauración de paquetes](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="748ba-120">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="748ba-121">`project.json`: especifique un intervalo de versiones directamente con el número de versión de la dependencia.</span><span class="sxs-lookup"><span data-stu-id="748ba-121">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="748ba-122">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="748ba-122">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="748ba-123">Comandos de la CLI de NuGet</span><span class="sxs-lookup"><span data-stu-id="748ba-123">NuGet CLI commands</span></span>

- <span data-ttu-id="748ba-124">`nuget install` no funciona con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-124">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="748ba-125">`nuget restore`: con proyectos que usan `project.json`, genera un archivo `project.lock.json` y, si es necesario, un archivo `<project>.nuget.props`.</span><span class="sxs-lookup"><span data-stu-id="748ba-125">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="748ba-126">(Ambos archivos pueden omitirse del control de código fuente). El argumento `<projectPath>` puede apuntar a un archivo `project.json` y tiene el mismo comportamiento que apuntar a un archivo `packages.config` o de proyecto.</span><span class="sxs-lookup"><span data-stu-id="748ba-126">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="748ba-127">En el orden de prioridad de las carpetas de paquete, se busca primero `%userprofile%\.nuget\packages` cuando se usa `project.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-127">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="748ba-128">`nuget update`: En Mono, este comando no funciona con proyectos que usen `project.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-128">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="748ba-129">Resolución de dependencias con PackageReference</span><span class="sxs-lookup"><span data-stu-id="748ba-129">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="748ba-130">*Originalmente en [Resolución de dependencias](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="748ba-130">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="748ba-131">El comportamiento de PackageReference se aplica también a `project.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-131">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="748ba-132">La restauración de NuGet escribe el gráfico de dependencias en un archivo denominado `project.lock.json` junto a `project.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-132">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="748ba-133">Administración de recursos de dependencia</span><span class="sxs-lookup"><span data-stu-id="748ba-133">Managing dependency assets</span></span>

<span data-ttu-id="748ba-134">*Originalmente en [Resolución de dependencias](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="748ba-134">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="748ba-135">Cuando se usa el formato `project.json`, se puede controlar qué activos de dependencias fluyen al proyecto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="748ba-135">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="748ba-136">Para obtener más información, vea [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="748ba-136">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="748ba-137">Exclusión de referencias</span><span class="sxs-lookup"><span data-stu-id="748ba-137">Excluding references</span></span>

<span data-ttu-id="748ba-138">*Originalmente en [Resolución de dependencias](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="748ba-138">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="748ba-139">`project.json`: agregue `"exclude" : "all"` en la dependencia para PackageC:</span><span class="sxs-lookup"><span data-stu-id="748ba-139">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="748ba-140">Resolución de errores de paquetes incompatibles</span><span class="sxs-lookup"><span data-stu-id="748ba-140">Resolving incompatible package errors</span></span>

<span data-ttu-id="748ba-141">*Originalmente en [Resolución de dependencias](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="748ba-141">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="748ba-142">Otro medio de resolución de errores:</span><span class="sxs-lookup"><span data-stu-id="748ba-142">An added means of resolving errors:</span></span>

- <span data-ttu-id="748ba-143">**No se recomienda**: como solución temporal mientras trabaja con el autor del paquete, los proyectos destinados a `netcore`, `netstandard` y `netcoreapp` pueden indicar otras plataformas como compatibles, lo que permite que se usen los paquetes destinados a esas otras plataformas.</span><span class="sxs-lookup"><span data-stu-id="748ba-143">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="748ba-144">Vea [Importaciones de project.json](project-json.md#imports) y [Destino de restauración de MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="748ba-144">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="748ba-145">Esto puede provocar comportamientos inesperados, por lo que de nuevo, es mejor resolver las incompatibilidades del paquete trabajando con el autor del paquete en una actualización.</span><span class="sxs-lookup"><span data-stu-id="748ba-145">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="748ba-146">Versiones de .NET Framework de destino</span><span class="sxs-lookup"><span data-stu-id="748ba-146">Target frameworks</span></span>

<span data-ttu-id="748ba-147">*Originalmente en [Versiones de .NET Framework de destino](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="748ba-147">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="748ba-148">[project.json](project-json.md): el nodo `frameworks` especifica las versiones de plataforma con las que se puede compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="748ba-148">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="748ba-149">Creación de un paquete</span><span class="sxs-lookup"><span data-stu-id="748ba-149">Creating a package</span></span>

<span data-ttu-id="748ba-150">*Originalmente en [Creación de un paquete](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="748ba-150">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="748ba-151">Establecimiento de un tipo de paquete</span><span class="sxs-lookup"><span data-stu-id="748ba-151">Setting a package type</span></span>

<span data-ttu-id="748ba-152">With .NET Core 1.x, cuando se instala un paquete DotnetCliTool, Visual Studio lo coloca en el nodo `project.json` `tools` en lugar del nodo `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="748ba-152">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="748ba-153">Los tipos de paquetes se establecen en `project.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-153">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="748ba-154">`project.json`: indicar el tipo de paquete dentro de una propiedad `packOptions.packageType` de json:</span><span class="sxs-lookup"><span data-stu-id="748ba-154">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="748ba-155">Agregar propiedades y destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="748ba-155">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="748ba-156">*Originalmente en [Crear paquetes NuGet de .NET Standard con Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="748ba-156">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="748ba-157">Cuando se usa `project.json`, los destinos no se agregan al proyecto, pero se ponen a disposición de este a través de `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-157">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="748ba-158">Control de versiones de paquetes</span><span class="sxs-lookup"><span data-stu-id="748ba-158">Package versioning</span></span>

<span data-ttu-id="748ba-159">*Originalmente en [Control de versiones de paquetes](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="748ba-159">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="748ba-160">Cuando se usa el formato `project.json`, NuGet admite también el uso de una notación de caracteres comodín, \*, en las partes de sufijo de versión principal, secundaria, de revisión y preliminar del número.</span><span class="sxs-lookup"><span data-stu-id="748ba-160">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="748ba-161">Referencia de NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="748ba-161">NuGet.Config reference</span></span>

<span data-ttu-id="748ba-162">*Originalmente en [Referencia de NuGet.Config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="748ba-162">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="748ba-163">`globalPackagesFolder` solo se aplica a `project.json`.</span><span class="sxs-lookup"><span data-stu-id="748ba-163">`globalPackagesFolder` applies only to `project.json`.</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="748ba-164">referencia de archivo nuspec</span><span class="sxs-lookup"><span data-stu-id="748ba-164">nuspec file reference</span></span>

<span data-ttu-id="748ba-165">*Originalmente en [Referencia de .nuspec](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="748ba-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="748ba-166">Con `project.json`, se usa el elemento `<contentFiles>` en lugar de `<files>`.</span><span class="sxs-lookup"><span data-stu-id="748ba-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="748ba-167">Control de opciones del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="748ba-167">Package manager options control</span></span>

<span data-ttu-id="748ba-168">*Originalmente en [Referencia de la interfaz de usuario del Administrador de paquetes](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="748ba-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="748ba-169">Los proyectos con el formato de referencia `project.json` solo muestran la opción **Mostrar ventana de vista previa**.</span><span class="sxs-lookup"><span data-stu-id="748ba-169">Projects using `project.json` reference format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="748ba-170">Plantillas de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="748ba-170">Visual Studio Templates</span></span>

<span data-ttu-id="748ba-171">*Originalmente en [Paquetes NuGet en plantillas de Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="748ba-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="748ba-172">Procedimientos recomendados: las plantillas no incluyen un archivo `project.json` ni referencias o contenido que se pudieran agregar al instalar los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="748ba-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>