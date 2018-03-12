---
title: "Compatibilidad con múltiples versiones de paquetes de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Descripción de los distintos métodos para fijar como destino varias versiones de .NET Framework desde un único paquete de NuGet."
keywords: "Destinos de los paquetes de NuGet, versiones de .NET Framework, NuGet y .NET, destinos de varias plataformas, creación de paquetes de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 723dbcc12ecc4e16d2ba4662559f107b9b22e2c2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="b475a-104">Compatibilidad con varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b475a-104">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="b475a-105">*Para los proyectos de .NET Core en los que se usa NuGet 4.0+, vea [pack y restore de NuGet como destinos de MSBuild](../reference/msbuild-targets.md) para obtener más información sobre la compatibilidad cruzada.*</span><span class="sxs-lookup"><span data-stu-id="b475a-105">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="b475a-106">Muchas bibliotecas tienen como destino una versión concreta de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b475a-106">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="b475a-107">Por ejemplo, podría tener una versión de la biblioteca que sea específica de UWP y otra que aproveche las ventajas de las características de la versión 4.6 de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b475a-107">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="b475a-108">Para dar cabida a esto, NuGet permite colocar varias versiones de la misma biblioteca en un único paquete cuando se usa el método de directorio de trabajo basado en convenciones, descrito en [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un paquete).</span><span class="sxs-lookup"><span data-stu-id="b475a-108">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="b475a-109">Estructura de carpetas de la versión de las plataformas</span><span class="sxs-lookup"><span data-stu-id="b475a-109">Framework version folder structure</span></span>

<span data-ttu-id="b475a-110">Al crear un paquete que solo contiene una versión de una biblioteca o que tiene como destino varias plataformas, siempre debe crear subcarpetas en `lib` usando nombres de plataforma que distingan mayúsculas de minúsculas con la siguiente convención:</span><span class="sxs-lookup"><span data-stu-id="b475a-110">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="b475a-111">Para obtener una lista completa de los nombres admitidos, vea la [referencia de las plataformas de destino](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="b475a-111">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="b475a-112">No debería tener nunca una versión de la biblioteca que no sea específica de una plataforma ni colocarla directamente en la carpeta `lib` raíz</span><span class="sxs-lookup"><span data-stu-id="b475a-112">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="b475a-113">(esta funcionalidad solo era compatible con `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="b475a-113">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="b475a-114">Si lo hiciera, haría que fuera compatible con cualquier plataforma de destino y permitiría que se instalara en cualquier lugar, algo que probablemente generaría errores inesperados en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="b475a-114">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="b475a-115">La incorporación de ensamblados en la carpeta raíz (como `lib\abc.dll`) o en subcarpetas (como `lib\abc\abc.dll`) ha quedado en desuso y se omite al usar el formato PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="b475a-115">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="b475a-116">Por ejemplo, la siguiente estructura de carpetas admite cuatro versiones de un ensamblado que son específicas de la plataforma:</span><span class="sxs-lookup"><span data-stu-id="b475a-116">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="b475a-117">Para incluir fácilmente todos estos archivos al crear el paquete, use un carácter comodín `**` recursivo en la sección `<files>` del archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="b475a-117">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="b475a-118">Carpetas específicas de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="b475a-118">Architecture-specific folders</span></span>

<span data-ttu-id="b475a-119">Si tiene ensamblados específicos de la arquitectura (es decir, ensamblados independientes que tienen como destino ARM, x86 y x64), debe colocarlos en una carpeta denominada `runtimes` dentro de subcarpetas denominadas `{platform}-{architecture}\lib\{framework}` o `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="b475a-119">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="b475a-120">Por ejemplo, la siguiente estructura de carpetas podría dar cabida a los archivos DLL nativos y administrados fijando como destino Windows 10 y la plataforma `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="b475a-120">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="b475a-121">Vea [Crear paquetes UWP](../guides/create-uwp-packages.md) para ver un ejemplo de cómo hacer referencia a estos archivos en el manifiesto de `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b475a-121">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="b475a-122">Adaptar las versiones de ensamblado y la plataforma de destino en un proyecto</span><span class="sxs-lookup"><span data-stu-id="b475a-122">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="b475a-123">Cuando NuGet instala un paquete que tiene varias versiones de ensamblado, intenta adaptar el nombre de la plataforma del ensamblado a la plataforma de destino del proyecto.</span><span class="sxs-lookup"><span data-stu-id="b475a-123">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="b475a-124">Si no se encuentra ninguna coincidencia, NuGet copia el ensamblado de la versión más reciente que sea anterior o igual a la plataforma de destino del proyecto, en caso de estar disponible.</span><span class="sxs-lookup"><span data-stu-id="b475a-124">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="b475a-125">Si no se encuentra ningún ensamblado compatible, NuGet devuelve un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="b475a-125">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="b475a-126">Por ejemplo, imagínese que tiene la siguiente estructura de carpetas en un paquete:</span><span class="sxs-lookup"><span data-stu-id="b475a-126">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="b475a-127">Al instalar este paquete en un proyecto destinado a .NET Framework 4.6, NuGet instala el ensamblado en la carpeta `net45`, ya que es la versión disponible más alta que es menor o igual a 4.6.</span><span class="sxs-lookup"><span data-stu-id="b475a-127">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="b475a-128">Por otro lado, si el proyecto tiene como destino .NET Framework 4.6.1, NuGet instalará el ensamblado en la carpeta `net461`.</span><span class="sxs-lookup"><span data-stu-id="b475a-128">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="b475a-129">Si el proyecto tiene como destino .NET Framework 4.0 o versiones anteriores, NuGet generará un mensaje de error por no haber encontrado el ensamblado compatible.</span><span class="sxs-lookup"><span data-stu-id="b475a-129">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="b475a-130">Agrupar los ensamblados por versión de la plataforma</span><span class="sxs-lookup"><span data-stu-id="b475a-130">Grouping assemblies by framework version</span></span>

<span data-ttu-id="b475a-131">NuGet copia los ensamblados de una sola carpeta de biblioteca en el paquete.</span><span class="sxs-lookup"><span data-stu-id="b475a-131">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="b475a-132">Por ejemplo, imagínese que un paquete tiene la siguiente estructura de carpetas:</span><span class="sxs-lookup"><span data-stu-id="b475a-132">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="b475a-133">Cuando se instala el paquete en un proyecto destinado a .NET Framework 4.5, `MyAssembly.dll` (v2.0) es el único ensamblado instalado.</span><span class="sxs-lookup"><span data-stu-id="b475a-133">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="b475a-134">`MyAssembly.Core.dll` (v1.0) no está instalado porque no aparece en la carpeta `net45`.</span><span class="sxs-lookup"><span data-stu-id="b475a-134">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="b475a-135">NuGet se comporta de esta manera porque es posible que `MyAssembly.Core.dll` se haya combinado en la versión 2.0 de `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="b475a-135">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="b475a-136">Si quiere que `MyAssembly.Core.dll` se instale para .NET Framework 4.5, coloque una copia en la carpeta `net45`.</span><span class="sxs-lookup"><span data-stu-id="b475a-136">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="b475a-137">Agrupar los ensamblados por perfil de la plataforma</span><span class="sxs-lookup"><span data-stu-id="b475a-137">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="b475a-138">NuGet también permite fijar como destino un perfil de plataforma específico anexando un guion y el nombre del perfil al final de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="b475a-138">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="b475a-139">Los perfiles compatibles son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="b475a-139">The supported profiles are as follows:</span></span>

- <span data-ttu-id="b475a-140">`client`: Client Profile</span><span class="sxs-lookup"><span data-stu-id="b475a-140">`client`: Client Profile</span></span>
- <span data-ttu-id="b475a-141">`full`: perfil completo</span><span class="sxs-lookup"><span data-stu-id="b475a-141">`full`: Full Profile</span></span>
- <span data-ttu-id="b475a-142">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="b475a-142">`wp`: Windows Phone</span></span>
- <span data-ttu-id="b475a-143">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="b475a-143">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="b475a-144">Determinar qué destino de NuGet se debe usar</span><span class="sxs-lookup"><span data-stu-id="b475a-144">Determining which NuGet target to use</span></span>

<span data-ttu-id="b475a-145">Al empaquetar bibliotecas que tienen como destino la biblioteca de clases portable, puede resultar difícil determinar qué destino de NuGet se debe usar en los nombres de carpeta y en el archivo `.nuspec`, sobre todo si se tiene como destino un solo subconjunto de la biblioteca de clases portable.</span><span class="sxs-lookup"><span data-stu-id="b475a-145">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="b475a-146">Los siguientes recursos externos le ayudarán con esto:</span><span class="sxs-lookup"><span data-stu-id="b475a-146">The following external resources will help you with this:</span></span>

- <span data-ttu-id="b475a-147">[Perfiles de plataforma en .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="b475a-147">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="b475a-148">[Perfiles de biblioteca de clases portable](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabla en la que se muestran los perfiles PCL y los destinos de NuGet equivalentes</span><span class="sxs-lookup"><span data-stu-id="b475a-148">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="b475a-149">[Herramienta de perfiles de la biblioteca de clases portable](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): herramienta de línea de comandos para determinar los perfiles PCL disponibles en el sistema</span><span class="sxs-lookup"><span data-stu-id="b475a-149">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="b475a-150">Archivos de contenido y scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b475a-150">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="b475a-151">Los archivos de contenido mutable y la ejecución de scripts solo están disponibles con el formato `packages.config`. Están en desuso con los demás formatos y no deben usarse con los nuevos paquetes.</span><span class="sxs-lookup"><span data-stu-id="b475a-151">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="b475a-152">Con `packages.config`, los archivos de contenido y los scripts de PowerShell se pueden agrupar por plataforma de destino usando la misma convención de carpetas dentro de las carpetas `content` y `tools`.</span><span class="sxs-lookup"><span data-stu-id="b475a-152">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="b475a-153">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b475a-153">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="b475a-154">Si se deja vacía una carpeta de plataforma, NuGet no agrega referencias de ensamblado ni archivos de contenido ni ejecuta los scripts de PowerShell para esa plataforma.</span><span class="sxs-lookup"><span data-stu-id="b475a-154">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="b475a-155">Dado que `init.ps1` se ejecuta a nivel de la solución y no depende del proyecto, debe colocarse directamente en la carpeta `tools`.</span><span class="sxs-lookup"><span data-stu-id="b475a-155">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="b475a-156">Se omite si se coloca en una carpeta de plataforma.</span><span class="sxs-lookup"><span data-stu-id="b475a-156">It's ignored if placed under a framework folder.</span></span>