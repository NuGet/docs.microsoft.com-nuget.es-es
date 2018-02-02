---
title: Referencia del archivo project.json para NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/27/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: En algunos tipos de proyecto, project.json mantiene la lista de paquetes NuGet que se usan en el proyecto.
keywords: project.json de NuGet, referencias de paquetes NuGet, dependencias de NuGet, project.lock.json
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2e2c521b18dd67e49942cc20eafef0be7f91573a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="projectjson-reference"></a><span data-ttu-id="f8e46-104">referencia de project.json</span><span class="sxs-lookup"><span data-stu-id="f8e46-104">project.json reference</span></span>

<span data-ttu-id="f8e46-105">*NuGet 3.x y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="f8e46-105">*NuGet 3.x+*</span></span>

<span data-ttu-id="f8e46-106">El archivo `project.json` mantiene una lista de los paquetes que se usan en un proyecto, conocida como formato de referencia de paquete.</span><span class="sxs-lookup"><span data-stu-id="f8e46-106">The `project.json` file maintains a list of packages used in a project, known as a package reference format.</span></span> <span data-ttu-id="f8e46-107">Sustituye a `packages.config` pero, a su vez, se sustituye por [PackageReference](../consume-packages/package-references-in-project-files.md) con NuGet 4.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="f8e46-107">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="f8e46-108">El archivo [`project.lock.json`](#projectlockjson) (descrito a continuación) también se usa en los proyectos que emplean `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-108">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="f8e46-109">`project.json` tiene la siguiente estructura básica, donde cada uno de los cuatro objetos de nivel superior puede tener cualquier número de objetos secundarios:</span><span class="sxs-lookup"><span data-stu-id="f8e46-109">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="f8e46-110">Dependencias</span><span class="sxs-lookup"><span data-stu-id="f8e46-110">Dependencies</span></span>

<span data-ttu-id="f8e46-111">Enumera las dependencias de paquetes NuGet del proyecto en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8e46-111">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="f8e46-112">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8e46-112">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="f8e46-113">En la sección `dependencies`, el cuadro de diálogo Administrador de paquetes NuGet agrega las dependencias de paquetes al proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8e46-113">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="f8e46-114">El identificador del paquete se corresponde con el identificador del paquete en nuget.org, el mismo que se usa en la consola del Administrador de paquetes: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-114">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="f8e46-115">Al restaurar paquetes, la restricción de versión de `"5.0.0"` implica `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-115">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="f8e46-116">Es decir, si 5.0.0 no está disponible en el servidor pero 5.0.1 sí lo está, NuGet instala 5.0.1 y le advierte de la actualización.</span><span class="sxs-lookup"><span data-stu-id="f8e46-116">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="f8e46-117">En caso contrario, NuGet elige la versión más baja posible en el servidor que coincida con la restricción.</span><span class="sxs-lookup"><span data-stu-id="f8e46-117">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="f8e46-118">Vea [Resolución de dependencias](../consume-packages/dependency-resolution.md) para obtener más detalles sobre las reglas de resolución.</span><span class="sxs-lookup"><span data-stu-id="f8e46-118">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="f8e46-119">Administración de recursos de dependencia</span><span class="sxs-lookup"><span data-stu-id="f8e46-119">Managing dependency assets</span></span>

<span data-ttu-id="f8e46-120">Los activos que fluyen desde las dependencias al proyecto de nivel superior se controlan mediante la especificación de un conjunto delimitado por comas de etiquetas en las propiedades `include` y `exclude` de la referencia de dependencia.</span><span class="sxs-lookup"><span data-stu-id="f8e46-120">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="f8e46-121">Las etiquetas se muestran en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8e46-121">The tags are listed the table below:</span></span>

| <span data-ttu-id="f8e46-122">Etiqueta Include o Exclude</span><span class="sxs-lookup"><span data-stu-id="f8e46-122">Include/Exclude tag</span></span> | <span data-ttu-id="f8e46-123">Carpetas afectadas del destino</span><span class="sxs-lookup"><span data-stu-id="f8e46-123">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="f8e46-124">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f8e46-124">contentFiles</span></span> | <span data-ttu-id="f8e46-125">Contenido</span><span class="sxs-lookup"><span data-stu-id="f8e46-125">Content</span></span>  |
| <span data-ttu-id="f8e46-126">motor en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="f8e46-126">runtime</span></span> | <span data-ttu-id="f8e46-127">Runtime, Resources y FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="f8e46-127">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="f8e46-128">compile</span><span class="sxs-lookup"><span data-stu-id="f8e46-128">compile</span></span> | <span data-ttu-id="f8e46-129">lib</span><span class="sxs-lookup"><span data-stu-id="f8e46-129">lib</span></span> |
| <span data-ttu-id="f8e46-130">compilación</span><span class="sxs-lookup"><span data-stu-id="f8e46-130">build</span></span> | <span data-ttu-id="f8e46-131">build (propiedades y destinos de MSBuild)</span><span class="sxs-lookup"><span data-stu-id="f8e46-131">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="f8e46-132">nativas</span><span class="sxs-lookup"><span data-stu-id="f8e46-132">native</span></span> | <span data-ttu-id="f8e46-133">nativas</span><span class="sxs-lookup"><span data-stu-id="f8e46-133">native</span></span> |
| <span data-ttu-id="f8e46-134">ninguna</span><span class="sxs-lookup"><span data-stu-id="f8e46-134">none</span></span> | <span data-ttu-id="f8e46-135">Sin carpetas</span><span class="sxs-lookup"><span data-stu-id="f8e46-135">No folders</span></span> |
| <span data-ttu-id="f8e46-136">todo</span><span class="sxs-lookup"><span data-stu-id="f8e46-136">all</span></span> | <span data-ttu-id="f8e46-137">Todas las carpetas</span><span class="sxs-lookup"><span data-stu-id="f8e46-137">All folders</span></span> |

<span data-ttu-id="f8e46-138">Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-138">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="f8e46-139">Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-139">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="f8e46-140">Por ejemplo, para incluir las carpetas `build` y `native` de una dependencia, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8e46-140">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="f8e46-141">Para excluir las carpetas `content` y `build` de una dependencia, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8e46-141">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="f8e46-142">Marcos de trabajo</span><span class="sxs-lookup"><span data-stu-id="f8e46-142">Frameworks</span></span>

<span data-ttu-id="f8e46-143">Enumera las plataformas en las que se ejecuta el proyecto, como `net45`, `netcoreapp` o `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-143">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="f8e46-144">En la sección `frameworks` solo se permite una entrada.</span><span class="sxs-lookup"><span data-stu-id="f8e46-144">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="f8e46-145">(Una excepción son los archivos `project.json` para los proyectos ASP.NET que se compilan con la cadena de herramientas DNX en desuso, lo que permite varios destinos).</span><span class="sxs-lookup"><span data-stu-id="f8e46-145">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX toolchain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="f8e46-146">Runtimes</span><span class="sxs-lookup"><span data-stu-id="f8e46-146">Runtimes</span></span>

<span data-ttu-id="f8e46-147">Enumera los sistemas operativos y arquitecturas en los que se ejecuta la aplicación, como `win10-arm`, `win8-x64` o `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-147">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="f8e46-148">Un paquete con una PCL que se puede ejecutar en cualquier runtime no tiene que especificar un runtime.</span><span class="sxs-lookup"><span data-stu-id="f8e46-148">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="f8e46-149">Esto también se aplica a todas las dependencias; en caso contrario, se deben especificar runtimes.</span><span class="sxs-lookup"><span data-stu-id="f8e46-149">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="f8e46-150">Supports</span><span class="sxs-lookup"><span data-stu-id="f8e46-150">Supports</span></span>

<span data-ttu-id="f8e46-151">Define un conjunto de comprobaciones de dependencias de paquete.</span><span class="sxs-lookup"><span data-stu-id="f8e46-151">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="f8e46-152">Puede definir dónde se espera que se ejecute la PCL o aplicación.</span><span class="sxs-lookup"><span data-stu-id="f8e46-152">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="f8e46-153">Las definiciones no son restrictivas, dado que es posible que el código se ejecute en otro lugar.</span><span class="sxs-lookup"><span data-stu-id="f8e46-153">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="f8e46-154">Pero, al especificar estas comprobaciones, NuGet debe comprobar que se cumplan todas las dependencias en los TxM indicados.</span><span class="sxs-lookup"><span data-stu-id="f8e46-154">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="f8e46-155">Ejemplos de los valores para esto son: `net46.app`, `uwp.10.0.app`, etc.</span><span class="sxs-lookup"><span data-stu-id="f8e46-155">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="f8e46-156">Esta sección se debería rellenar automáticamente al seleccionar una entrada en el cuadro de diálogo de destinos Biblioteca de clases portable.</span><span class="sxs-lookup"><span data-stu-id="f8e46-156">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="f8e46-157">Importaciones</span><span class="sxs-lookup"><span data-stu-id="f8e46-157">Imports</span></span>

<span data-ttu-id="f8e46-158">Las importaciones están diseñadas para permitir que los paquetes que usan el TxM `dotnet` funcionen con paquetes que no declaran un TxM de dotnet.</span><span class="sxs-lookup"><span data-stu-id="f8e46-158">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="f8e46-159">Si en el proyecto se usa el TxM `dotnet`, todos los paquetes de los que depende también deben tener un TxM `dotnet`, a menos que agregue lo siguiente a `project.json` para permitir que las plataformas que no sean de `dotnet` sean compatibles con `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="f8e46-159">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="f8e46-160">Si se usa el TxM `dotnet`, el sistema de proyecto de PCL agrega la instrucción `imports` adecuada según los destinos admitidos.</span><span class="sxs-lookup"><span data-stu-id="f8e46-160">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="f8e46-161">Diferencias respecto a aplicaciones portátiles y proyectos web</span><span class="sxs-lookup"><span data-stu-id="f8e46-161">Differences from portable apps and web projects</span></span>

<span data-ttu-id="f8e46-162">El archivo `project.json` que usa NuGet es un subconjunto del que se encuentra en proyectos de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f8e46-162">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="f8e46-163">En ASP.NET Core se usa `project.json` para metadatos del proyecto, información de compilación y dependencias.</span><span class="sxs-lookup"><span data-stu-id="f8e46-163">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="f8e46-164">Cuando se usa en otros sistemas de proyecto, esos tres elementos se dividen en archivos independientes y `project.json` contiene menos información.</span><span class="sxs-lookup"><span data-stu-id="f8e46-164">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="f8e46-165">Las diferencias principales incluyen:</span><span class="sxs-lookup"><span data-stu-id="f8e46-165">Notable differences include:</span></span>

- <span data-ttu-id="f8e46-166">Solo puede haber una plataforma en la sección `frameworks`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-166">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="f8e46-167">El archivo no puede contener las dependencias, opciones de compilación, etc., que se ven en archivos `project.json` de DNX.</span><span class="sxs-lookup"><span data-stu-id="f8e46-167">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="f8e46-168">Dado que solo puede haber una plataforma, no tiene sentido especificar dependencias específicas de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="f8e46-168">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="f8e46-169">La compilación se controla mediante MSBuild, por lo que las opciones de compilación, definiciones del preprocesador, etc., todas forman parte del archivo de proyecto de MSBuild y no de `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-169">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="f8e46-170">En NuGet 3 y versiones posteriores, no se espera que los desarrolladores modifiquen manualmente el archivo `project.json`, dado que el contenido se manipula en la interfaz de usuario del Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8e46-170">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="f8e46-171">Es decir, por supuesto se puede modificar el archivo, pero se debe compilar el proyecto para iniciar una restauración del paquete o invocar la restauración de otro modo.</span><span class="sxs-lookup"><span data-stu-id="f8e46-171">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="f8e46-172">Vea [Restauración de paquetes](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="f8e46-172">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="f8e46-173">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="f8e46-173">project.lock.json</span></span>

<span data-ttu-id="f8e46-174">El archivo `project.lock.json` se genera en el proceso de restauración de los paquetes NuGet en proyectos que usan `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f8e46-174">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="f8e46-175">Contiene una instantánea de toda la información que se genera mientras NuGet recorre el gráfico de los paquetes e incluye la versión, contenido y dependencias de todos los paquetes del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8e46-175">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="f8e46-176">El sistema de compilación usa esto para elegir los paquetes desde una ubicación global que son pertinentes al compilar el proyecto en lugar de depender de una carpeta de paquetes local en el propio proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8e46-176">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="f8e46-177">Esto supone un mayor rendimiento de compilación porque solo es necesario leer `project.lock.json` en lugar de muchos archivos `.nuspec` independientes.</span><span class="sxs-lookup"><span data-stu-id="f8e46-177">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="f8e46-178">`project.lock.json` se genera automáticamente al restaurar el paquete, por lo que se puede omitir en el control de código fuente agregándolo a los archivos `.gitignore` y `.tfignore` (vea [Paquetes y control de código fuente](../consume-packages/packages-and-source-control.md)).</span><span class="sxs-lookup"><span data-stu-id="f8e46-178">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="f8e46-179">Pero si se incluye en el control de código fuente, el historial de cambios muestra los cambios en las dependencias resueltos en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="f8e46-179">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
