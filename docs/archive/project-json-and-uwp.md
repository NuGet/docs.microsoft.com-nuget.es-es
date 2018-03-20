---
title: Archivo project.json de NuGet con proyectos de UWP | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Descripción de cómo se usa el archivo project.json para realizar el seguimiento de las dependencias de NuGet en proyectos de Plataforma universal de Windows (UWP)."
keywords: Dependencias de NuGet, NuGet y UWP, UWP y project.json, archivo project.json de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3ef3703b2be92f84d37866bce9934ebcfed3a9f7
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="2f23e-104">project.json y UWP</span><span class="sxs-lookup"><span data-stu-id="2f23e-104">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="2f23e-105">Este contenido ha quedado en desuso.</span><span class="sxs-lookup"><span data-stu-id="2f23e-105">This content is deprecated.</span></span> <span data-ttu-id="2f23e-106">Los proyectos deben usar los formatos `packages.config` o PackageReference.</span><span class="sxs-lookup"><span data-stu-id="2f23e-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="2f23e-107">En este documento se describe la estructura de paquetes en la que se usan características de NuGet 3+ (Visual Studio 2015 y versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="2f23e-107">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="2f23e-108">Se puede usar la propiedad `minClientVersion` de `.nuspec` para indicar que se requieren las características descritas aquí si se establece en 3.1.</span><span class="sxs-lookup"><span data-stu-id="2f23e-108">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="2f23e-109">Agregar compatibilidad con UWP a un paquete existente</span><span class="sxs-lookup"><span data-stu-id="2f23e-109">Adding UWP support to an existing package</span></span>

<span data-ttu-id="2f23e-110">Si tiene un paquete existente y quiere agregar compatibilidad para las aplicaciones para UWP, no es necesario adoptar el formato de empaquetado descrito aquí.</span><span class="sxs-lookup"><span data-stu-id="2f23e-110">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="2f23e-111">Solo debe adoptar este formato si necesita las características que se describen y está dispuesto a trabajar únicamente con los clientes que han actualizado a la versión 3+ del cliente NuGet.</span><span class="sxs-lookup"><span data-stu-id="2f23e-111">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="2f23e-112">Ya uso netcore45 como destino</span><span class="sxs-lookup"><span data-stu-id="2f23e-112">I already target netcore45</span></span>

<span data-ttu-id="2f23e-113">Si ya usa `netcore45` como destino y no necesita aprovechar estas características, no es necesario realizar ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="2f23e-113">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="2f23e-114">Las aplicaciones para UWP pueden consumir paquetes de `netcore45`.</span><span class="sxs-lookup"><span data-stu-id="2f23e-114">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="2f23e-115">Quiero aprovechar las ventajas de las API específicas de Windows 10</span><span class="sxs-lookup"><span data-stu-id="2f23e-115">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="2f23e-116">En este caso es necesario agregar el moniker de la plataforma de destino `uap10.0` (TFM o TxM) al paquete.</span><span class="sxs-lookup"><span data-stu-id="2f23e-116">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="2f23e-117">Cree una carpeta en el paquete y agregue el ensamblado que se haya compilado para trabajar con Windows 10 a esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="2f23e-117">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="2f23e-118">No necesito las API específicas de Windows 10, pero quiero las características nuevas de .NET o todavía no dispongo de netcore45</span><span class="sxs-lookup"><span data-stu-id="2f23e-118">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="2f23e-119">En este caso agregaría el TxM `dotnet` al paquete.</span><span class="sxs-lookup"><span data-stu-id="2f23e-119">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="2f23e-120">A diferencia de otros TxM, `dotnet` no implica una plataforma o área expuesta.</span><span class="sxs-lookup"><span data-stu-id="2f23e-120">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="2f23e-121">Indica que el paquete funciona en cualquier plataforma en la que funcionen las dependencias.</span><span class="sxs-lookup"><span data-stu-id="2f23e-121">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="2f23e-122">Cuando se crea un paquete con el TxM `dotnet`, es probable que tenga muchas más dependencias específicas del TxM en `.nuspec`, según sea necesario definir los paquetes BCL de los que depende, por ejemplo, `System.Text`, `System.Xml`, etc. Las ubicaciones en las que funcionan esas dependencias definen dónde funciona el paquete.</span><span class="sxs-lookup"><span data-stu-id="2f23e-122">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="2f23e-123">Cómo buscar las dependencias</span><span class="sxs-lookup"><span data-stu-id="2f23e-123">How do I find out my dependencies</span></span>

<span data-ttu-id="2f23e-124">Hay dos formas de averiguar qué dependencias se muestran:</span><span class="sxs-lookup"><span data-stu-id="2f23e-124">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="2f23e-125">Use la herramienta [Generador de dependencias de NuSpec](https://github.com/onovotny/ReferenceGenerator) **de terceros**.</span><span class="sxs-lookup"><span data-stu-id="2f23e-125">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="2f23e-126">La herramienta automatiza el proceso y actualiza el archivo `.nuspec` con los paquetes dependientes en la compilación.</span><span class="sxs-lookup"><span data-stu-id="2f23e-126">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="2f23e-127">Está disponible a través de un paquete NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="2f23e-127">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="2f23e-128">(La forma complicada) Use `ILDasm` para comprobar el archivo `.dll` y ver qué ensamblados se necesitan realmente en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2f23e-128">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="2f23e-129">Después, determine de qué paquete NuGet proviene cada uno.</span><span class="sxs-lookup"><span data-stu-id="2f23e-129">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="2f23e-130">Vea el tema [`project.json`](project-json.md) para obtener más información sobre las características que ayudan en la creación de un paquete que sea compatible con el TxM `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="2f23e-130">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="2f23e-131">Si el paquete está diseñado para funcionar con proyectos PCL, se recomienda crear una carpeta `dotnet`, para evitar advertencias y posibles problemas de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="2f23e-131">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="2f23e-132">Estructura de directorios</span><span class="sxs-lookup"><span data-stu-id="2f23e-132">Directory structure</span></span>

<span data-ttu-id="2f23e-133">Los paquetes NuGet con este formato tienen la siguiente carpeta y comportamientos conocidos:</span><span class="sxs-lookup"><span data-stu-id="2f23e-133">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="2f23e-134">Carpeta</span><span class="sxs-lookup"><span data-stu-id="2f23e-134">Folder</span></span> | <span data-ttu-id="2f23e-135">comportamientos</span><span class="sxs-lookup"><span data-stu-id="2f23e-135">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="2f23e-136">Compilar</span><span class="sxs-lookup"><span data-stu-id="2f23e-136">Build</span></span> | <span data-ttu-id="2f23e-137">Contiene destinos de MSBuild y los archivos de propiedades de esta carpeta se integran de manera diferente en el proyecto, pero en caso contrario, no hay ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="2f23e-137">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="2f23e-138">Herramientas</span><span class="sxs-lookup"><span data-stu-id="2f23e-138">Tools</span></span> | <span data-ttu-id="2f23e-139">`install.ps1` y `uninstall.ps1` no se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="2f23e-139">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="2f23e-140">`init.ps1` funciona de la forma habitual.</span><span class="sxs-lookup"><span data-stu-id="2f23e-140">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="2f23e-141">Contenido</span><span class="sxs-lookup"><span data-stu-id="2f23e-141">Content</span></span> | <span data-ttu-id="2f23e-142">El contenido no se copia automáticamente en el proyecto del usuario.</span><span class="sxs-lookup"><span data-stu-id="2f23e-142">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="2f23e-143">La compatibilidad con la inclusión de contenido en el proyecto está planeada para una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="2f23e-143">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="2f23e-144">Lib</span><span class="sxs-lookup"><span data-stu-id="2f23e-144">Lib</span></span> | <span data-ttu-id="2f23e-145">Para muchos paquetes, `lib` funciona del mismo modo que en NuGet 2.x, pero con opciones ampliadas sobre qué nombres se pueden usar en su interior y lógica mejorada para seleccionar la subcarpeta correcta al consumir paquetes.</span><span class="sxs-lookup"><span data-stu-id="2f23e-145">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="2f23e-146">Pero cuando se usa junto con `ref`, la carpeta `lib` contiene los ensamblados que implementan el área expuesta definida por los ensamblados de la carpeta `ref`.</span><span class="sxs-lookup"><span data-stu-id="2f23e-146">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="2f23e-147">Ref</span><span class="sxs-lookup"><span data-stu-id="2f23e-147">Ref</span></span> | <span data-ttu-id="2f23e-148">`ref` es una carpeta opcional que contiene ensamblados de .NET que definen la superficie pública (métodos y tipos públicos) sobre la que se compila una aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f23e-148">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="2f23e-149">Es posible que los ensamblados de esta carpeta no tengan ninguna implementación, únicamente se usan para definir el área expuesta para el compilador.</span><span class="sxs-lookup"><span data-stu-id="2f23e-149">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="2f23e-150">Si el paquete no tiene ninguna carpeta `ref`, entonces `lib` es tanto el ensamblado de referencia como el de implementación.</span><span class="sxs-lookup"><span data-stu-id="2f23e-150">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="2f23e-151">Runtimes</span><span class="sxs-lookup"><span data-stu-id="2f23e-151">Runtimes</span></span> | <span data-ttu-id="2f23e-152">`runtimes` es una carpeta opcional que contiene código específico del sistema operativo, como la arquitectura de CPU y binarios específicos del sistema operativo o dependientes de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="2f23e-152">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="2f23e-153">Archivos de destinos y propiedades de MSBuild en paquetes</span><span class="sxs-lookup"><span data-stu-id="2f23e-153">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="2f23e-154">Los paquetes NuGet pueden contener archivos `.targets` y `.props` que se importan en cualquier proyecto de MSBuild en el que se instale el paquete.</span><span class="sxs-lookup"><span data-stu-id="2f23e-154">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="2f23e-155">En NuGet 2.x, esto se hacía insertando instrucciones `<Import>` en el archivo `.csproj`, en NuGet 3.0 no hay ninguna acción específica de "instalación en el proyecto".</span><span class="sxs-lookup"><span data-stu-id="2f23e-155">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="2f23e-156">En su lugar, el proceso de restauración de paquetes escribe dos archivos `[projectname].nuget.props` y `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="2f23e-156">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="2f23e-157">MSBuild sabe buscar estos dos archivos y los importa de manera automática cerca del principio y el final del proceso de compilación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2f23e-157">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="2f23e-158">Esto ofrece un comportamiento muy similar al de NuGet 2.x, pero con una diferencia importante: *en este caso no hay ningún orden garantizado de archivos de destino y propiedades*.</span><span class="sxs-lookup"><span data-stu-id="2f23e-158">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="2f23e-159">Pero MSBuild proporciona formas de ordenar los destinos mediante los atributos `BeforeTargets` y `AfterTargets` de la definición de `<Target>` (vea [Elemento Target (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="2f23e-159">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="2f23e-160">Lib y Ref</span><span class="sxs-lookup"><span data-stu-id="2f23e-160">Lib and Ref</span></span>

<span data-ttu-id="2f23e-161">El comportamiento de la carpeta `lib` no ha cambiado significativamente en NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="2f23e-161">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="2f23e-162">Pero todos los ensamblados deben estar en subcarpetas con el mismo nombre que un TxM y ya no se pueden colocar directamente en la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="2f23e-162">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="2f23e-163">Un TxM es el nombre de una plataforma para la que un recurso determinado de un paquete se supone que debe funcionar.</span><span class="sxs-lookup"><span data-stu-id="2f23e-163">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="2f23e-164">Lógicamente son una extensión de los Monikers de plataforma de destino (TFM), por ejemplo, `net45`, `net46`, `netcore50` y `dnxcore50` son ejemplos de TxM (vea [Plataformas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="2f23e-164">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="2f23e-165">TxM puede hacer referencia a una plataforma (TFM), así como a otras áreas expuestas específicas de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="2f23e-165">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="2f23e-166">Por ejemplo el TxM de UWP (`uap10.0`) representa el área expuesta de .NET, así como el área expuesta de Windows para aplicaciones para UWP.</span><span class="sxs-lookup"><span data-stu-id="2f23e-166">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="2f23e-167">Un ejemplo de estructura de lib:</span><span class="sxs-lookup"><span data-stu-id="2f23e-167">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="2f23e-168">La carpeta `lib` contiene ensamblados que se usan en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2f23e-168">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="2f23e-169">Para la mayoría de paquetes, solo se necesita una carpeta bajo `lib` para cada uno de los TxM de destino.</span><span class="sxs-lookup"><span data-stu-id="2f23e-169">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="2f23e-170">Ref</span><span class="sxs-lookup"><span data-stu-id="2f23e-170">Ref</span></span>

<span data-ttu-id="2f23e-171">En ocasiones, hay casos en los que se debe usar un ensamblado diferente durante la compilación (en la actualidad lo hacen los ensamblados de referencia .NET).</span><span class="sxs-lookup"><span data-stu-id="2f23e-171">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="2f23e-172">En esos casos, use una carpeta de nivel superior denominada `ref` (abreviatura de "ensamblados de referencia").</span><span class="sxs-lookup"><span data-stu-id="2f23e-172">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="2f23e-173">La mayoría de los autores de paquetes no requieren la carpeta `ref`.</span><span class="sxs-lookup"><span data-stu-id="2f23e-173">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="2f23e-174">Es útil para los paquetes que deben proporcionar un área expuesta coherente para la compilación e IntelliSense, pero después tienen una implementación diferente para los distintos TxM.</span><span class="sxs-lookup"><span data-stu-id="2f23e-174">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="2f23e-175">El caso de uso más importante de esto son los paquetes `System.*` que se generan como parte de la inclusión de .NET Core en NuGet.</span><span class="sxs-lookup"><span data-stu-id="2f23e-175">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="2f23e-176">Estos paquetes tienen varias implementaciones que se unifican mediante un conjunto coherente de ensamblados de referencia.</span><span class="sxs-lookup"><span data-stu-id="2f23e-176">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="2f23e-177">De manera mecánica, los ensamblados incluidos en la carpeta `ref` son los ensamblados de referencia que se pasan al compilador.</span><span class="sxs-lookup"><span data-stu-id="2f23e-177">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="2f23e-178">Para los que han usado csc.exe, estos son los ensamblados que se pasan al modificador [opción /reference de C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option).</span><span class="sxs-lookup"><span data-stu-id="2f23e-178">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="2f23e-179">La estructura de la carpeta `ref` es la misma que la de `lib`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2f23e-179">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

<span data-ttu-id="2f23e-180">En este ejemplo, todos los ensamblados de los directorios `ref` serían idénticos.</span><span class="sxs-lookup"><span data-stu-id="2f23e-180">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="2f23e-181">Runtimes</span><span class="sxs-lookup"><span data-stu-id="2f23e-181">Runtimes</span></span>

<span data-ttu-id="2f23e-182">La carpeta runtimes contiene ensamblados y bibliotecas nativas que se deben ejecutar en "runtimes" específicos, que generalmente se definen por el sistema operativo y la arquitectura de CPU.</span><span class="sxs-lookup"><span data-stu-id="2f23e-182">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="2f23e-183">Estos tiempos de ejecución se identifican mediante [identificadores en tiempo de ejecución (RID)](/dotnet/core/rid-catalog) como `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span><span class="sxs-lookup"><span data-stu-id="2f23e-183">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="2f23e-184">Aplicaciones auxiliares nativas para usar las API específicas de la plataforma</span><span class="sxs-lookup"><span data-stu-id="2f23e-184">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="2f23e-185">En el ejemplo siguiente se muestra un paquete que tiene una implementación estrictamente administrada para varias plataformas, pero que usa aplicaciones auxiliares nativas en Windows 8, donde puede llamar a API nativas específicas de Windows 8.</span><span class="sxs-lookup"><span data-stu-id="2f23e-185">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="2f23e-186">Dado el paquete anterior, sucede lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f23e-186">Given the above package the following things happen:</span></span>

- <span data-ttu-id="2f23e-187">Cuando no se encuentra en Windows 8, se usa el ensamblado `lib/net40/MyLibrary.dll`.</span><span class="sxs-lookup"><span data-stu-id="2f23e-187">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="2f23e-188">Cuando se encuentra en Windows 8, se usa `runtimes/win8-<architecture>/lib/MyLibrary.dll` y `native/MyNativeHelper.dll` se copia en la salida de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2f23e-188">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="2f23e-189">En el ejemplo anterior el ensamblado `lib/net40` es simplemente código administrado, mientras que los ensamblados en la carpeta runtimes se invocarán en el ensamblado auxiliar nativo para llamar a las API específicas de Windows 8.</span><span class="sxs-lookup"><span data-stu-id="2f23e-189">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="2f23e-190">Solo se selecciona una carpeta `lib`, por lo que, si hay una carpeta específica del entorno en tiempo de ejecución, se elige sobre `lib`, que no es específica del entorno en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2f23e-190">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="2f23e-191">La carpeta nativa es aditiva; si existe, se copia en la salida de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2f23e-191">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="2f23e-192">Contenedor administrado</span><span class="sxs-lookup"><span data-stu-id="2f23e-192">Managed wrapper</span></span>

<span data-ttu-id="2f23e-193">Otra manera de usar los runtimes es enviar un paquete que sea un contenedor administrado sobre un ensamblado nativo.</span><span class="sxs-lookup"><span data-stu-id="2f23e-193">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="2f23e-194">En este escenario se crea un paquete similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f23e-194">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="2f23e-195">En este caso no hay una carpeta `lib` de nivel superior como dicha carpeta, dado que no hay ninguna implementación de este paquete que no se base en el ensamblado nativo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="2f23e-195">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="2f23e-196">Si el ensamblado administrado, `MyLibrary.dll`, fuera exactamente el mismo en ambos casos, entonces se podría colocar en una carpeta `lib` de nivel superior, pero como la falta de un ensamblado nativo no produce un error de instalación en el paquete si se instaló en una plataforma que no fuera win-x86 o win-x64, se usaría la biblioteca de nivel superior, pero no se copiaría ningún ensamblado nativo.</span><span class="sxs-lookup"><span data-stu-id="2f23e-196">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="2f23e-197">Creación de paquetes para NuGet 2 y NuGet 3</span><span class="sxs-lookup"><span data-stu-id="2f23e-197">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="2f23e-198">Si quiere crear un paquete que se pueda consumir en proyectos que usen `packages.config` así como en paquetes con `project.json`, entonces se aplica lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f23e-198">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="2f23e-199">Ref y runtimes solo funcionan en NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="2f23e-199">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="2f23e-200">Ambos se ignoran en NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="2f23e-200">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="2f23e-201">No se puede confiar en que `install.ps1` o `uninstall.ps1` funcionen.</span><span class="sxs-lookup"><span data-stu-id="2f23e-201">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="2f23e-202">Estos archivos se ejecutan cuando se usa `packages.config`, pero se ignoran con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="2f23e-202">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="2f23e-203">Por tanto, el paquete debe poder usarse sin ejecutarlos.</span><span class="sxs-lookup"><span data-stu-id="2f23e-203">So your package needs to be usable without them running.</span></span> <span data-ttu-id="2f23e-204">`init.ps1` sigue ejecutándose en NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="2f23e-204">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="2f23e-205">La instalación de destinos y propiedades es diferente, por lo que debe asegurarse de que el paquete funciona en ambos clientes según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="2f23e-205">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="2f23e-206">Los subdirectorios de lib deben ser un TxM en NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="2f23e-206">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="2f23e-207">No se pueden colocar bibliotecas en la raíz de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="2f23e-207">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="2f23e-208">Con NuGet 3, el contenido no se copia de manera automática.</span><span class="sxs-lookup"><span data-stu-id="2f23e-208">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="2f23e-209">Los consumidores del paquete podrían copiar los archivos personalmente o usar una herramienta como un ejecutor de tareas para automatizar la copia de los archivos.</span><span class="sxs-lookup"><span data-stu-id="2f23e-209">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="2f23e-210">NuGet 3 no ejecuta las transformaciones de archivos de origen y configuración.</span><span class="sxs-lookup"><span data-stu-id="2f23e-210">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="2f23e-211">Si se va a admitir NuGet 2 y 3, `minClientVersion` debe ser la versión más baja del cliente de NuGet 2 en la que el paquete funciona.</span><span class="sxs-lookup"><span data-stu-id="2f23e-211">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="2f23e-212">En el caso de un paquete existente no es necesario cambiar.</span><span class="sxs-lookup"><span data-stu-id="2f23e-212">In the case of an existing package it shouldn't need to change.</span></span>
