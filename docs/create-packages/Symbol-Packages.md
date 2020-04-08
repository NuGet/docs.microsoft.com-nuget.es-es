---
title: Creación de paquetes de símbolos heredados (.symbols.nupkg)
description: Cómo crear paquetes de NuGet que solo contienen símbolos para admitir la depuración de otros paquetes de NuGet en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476274"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="81fc9-103">Creación de paquetes de símbolos heredados (.symbols.nupkg)</span><span class="sxs-lookup"><span data-stu-id="81fc9-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="81fc9-104">El nuevo formato recomendado para paquetes de símbolos es .snupkg.</span><span class="sxs-lookup"><span data-stu-id="81fc9-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="81fc9-105">Vea [Crear paquetes de símbolos (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="81fc9-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="81fc9-106">.symbols.nupkg todavía se admite, pero solo por motivos de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="81fc9-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="81fc9-107">Además de crear paquetes para nuget.org u otros orígenes, NuGet también admite la creación de paquetes de símbolos asociados que se pueden publicar en servidores de símbolos.</span><span class="sxs-lookup"><span data-stu-id="81fc9-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="81fc9-108">El formato de paquete de símbolos heredado, .symbols.nupkg, se puede insertar en el repositorio SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="81fc9-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="81fc9-109">Los consumidores de paquetes pueden agregar `https://nuget.smbsrc.net` a sus orígenes de símbolos en Visual Studio, que permite entrar en el código del paquete en el depurador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81fc9-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="81fc9-110">Vea [Especificar archivos de código fuente y símbolos (.pdb) en el depurador de Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obtener información detallada sobre ese proceso.</span><span class="sxs-lookup"><span data-stu-id="81fc9-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="81fc9-111">Crear un paquete de símbolos heredado</span><span class="sxs-lookup"><span data-stu-id="81fc9-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="81fc9-112">Para crear un paquete de símbolos heredado, siga estas convenciones:</span><span class="sxs-lookup"><span data-stu-id="81fc9-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="81fc9-113">Asigne al paquete principal (con el código) el nombre `{identifier}.nupkg` e incluya todos los archivos excepto los archivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="81fc9-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="81fc9-114">Asigne al paquete de símbolos heredados el nombre `{identifier}.symbols.nupkg` e incluya los archivos DLL de ensamblado, los archivos `.pdb`, los archivos XMLDOC y los archivos de origen (vea las secciones siguientes).</span><span class="sxs-lookup"><span data-stu-id="81fc9-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="81fc9-115">Puede crear ambos paquetes con la opción `-Symbols`, ya sea desde un archivo `.nuspec` o desde un archivo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="81fc9-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="81fc9-116">Tenga en cuenta que `pack` requiere Mono 4.4.2 en Mac OS X y no funciona en los sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="81fc9-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="81fc9-117">En los equipos Mac, también debe convertir los nombres de las rutas de acceso de Windows del archivo `.nuspec` a las rutas de acceso de estilo Unix.</span><span class="sxs-lookup"><span data-stu-id="81fc9-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="81fc9-118">Estructura del paquete de símbolos heredado</span><span class="sxs-lookup"><span data-stu-id="81fc9-118">Legacy symbol package structure</span></span>

<span data-ttu-id="81fc9-119">Un paquete de símbolos heredado puede tener como destino varias plataformas de destino de la misma manera que un paquete de bibliotecas, por lo que la estructura de la carpeta `lib` debe ser exactamente igual que el paquete principal, incluyendo solo los archivos `.pdb` junto con los archivos DLL.</span><span class="sxs-lookup"><span data-stu-id="81fc9-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="81fc9-120">Por ejemplo, un paquete de símbolos heredado que tenga como destino .NET 4.0 y Silverlight 4 tendría este diseño:</span><span class="sxs-lookup"><span data-stu-id="81fc9-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="81fc9-121">Los archivos de código fuente se colocan en una carpeta especial independiente denominada `src`, que debe seguir la estructura relativa del repositorio de origen.</span><span class="sxs-lookup"><span data-stu-id="81fc9-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="81fc9-122">Esto es así porque los archivos PDB contienen rutas de acceso absolutas a los archivos de código fuente que se usan para compilar los archivos DLL correspondientes y se deben buscar durante el proceso de publicación.</span><span class="sxs-lookup"><span data-stu-id="81fc9-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="81fc9-123">Se puede quitar una ruta de acceso base (prefijo de ruta de acceso común). Por ejemplo, imagínese que tiene una biblioteca creada a partir de estos archivos:</span><span class="sxs-lookup"><span data-stu-id="81fc9-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

<span data-ttu-id="81fc9-124">Aparte de la carpeta `lib`, un paquete de símbolos heredado tendría que tener este diseño:</span><span class="sxs-lookup"><span data-stu-id="81fc9-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="81fc9-125">Hacer referencia a los archivos en el archivo nuspec</span><span class="sxs-lookup"><span data-stu-id="81fc9-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="81fc9-126">Se puede crear un paquete de símbolos heredado mediante convenciones a partir de una estructura de carpetas, tal y como se describe en la sección anterior, o especificando su contenido en la sección `files` del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="81fc9-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="81fc9-127">Por ejemplo, para crear el paquete que se muestra en la sección anterior, use lo siguiente en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="81fc9-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="81fc9-128">Publicar un paquete de símbolos heredado</span><span class="sxs-lookup"><span data-stu-id="81fc9-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="81fc9-129">Para insertar paquetes en nuget.org debe usar [la versión 4.9.1 o una versión posterior de nuget.exe](https://www.nuget.org/downloads), que implementa los [protocolos de NuGet](../api/nuget-protocols.md) necesarios.</span><span class="sxs-lookup"><span data-stu-id="81fc9-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="81fc9-130">Para mayor comodidad, guarde primero la clave de API con NuGet (vea [Publish a package](../nuget-org/publish-a-package.md) [Publicar un paquete]), que se aplicará a nuget.org y a symbolsource.org, porque symbolsource.org comprobará con nuget.org que usted es el propietario del paquete.</span><span class="sxs-lookup"><span data-stu-id="81fc9-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="81fc9-131">Una vez publicado el paquete principal en nuget.org, inserte el paquete de símbolos heredado del siguiente modo. El paquete usará automáticamente symbolsource.org como destino debido a la aparición de `.symbols` en el nombre de archivo:</span><span class="sxs-lookup"><span data-stu-id="81fc9-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="81fc9-132">Para publicar el paquete en otro repositorio de símbolos, o para insertar un paquete de símbolos heredado que no sigue la convención de nomenclatura, use la opción `-Source`:</span><span class="sxs-lookup"><span data-stu-id="81fc9-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="81fc9-133">También puede insertar el paquete principal y el paquete de símbolos en ambos repositorios a la vez usando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="81fc9-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="81fc9-134">Con la versión 4.5.0 o una versión posterior de nuget.exe, los paquetes de símbolos no se insertan automáticamente en symbolsource.org. Tendría que insertar los paquetes de símbolos por separado, tal como se describe en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="81fc9-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="81fc9-135">En este caso, NuGet publicará `MyPackage.symbols.nupkg`, si existe, en https://nuget.smbsrc.net/ (la dirección URL de inserción para symbolsource.org) después de que haya publicado el paquete principal en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="81fc9-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="81fc9-136">Vea también</span><span class="sxs-lookup"><span data-stu-id="81fc9-136">See also</span></span>

* <span data-ttu-id="81fc9-137">[Crear paquetes de símbolos (.snupkg)](Symbol-Packages-snupkg.md): el nuevo formato recomendado para paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="81fc9-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="81fc9-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (Cambio al nuevo motor SymbolSource) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="81fc9-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
