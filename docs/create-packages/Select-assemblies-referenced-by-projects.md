---
title: Selección de ensamblados a los que hacen referencia proyectos
description: Haga que un subconjunto de ensamblados del paquete esté disponible para el compilador, mientras todos los ensamblados están disponibles en tiempo de ejecución.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427480"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="c57b5-103">Selección de ensamblados a los que hacen referencia proyectos</span><span class="sxs-lookup"><span data-stu-id="c57b5-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="c57b5-104">Las referencias de ensamblado explícitas permiten usar un subconjunto de ensamblados para IntelliSense y la compilación, mientras todos los ensamblados están disponibles en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c57b5-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="c57b5-105">`PackageReference` y `packages.config` funcionan de manera diferente y, por lo tanto, los autores de paquetes deben tener cuidado al crear el paquete para que sea compatible con ambos tipos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="c57b5-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="c57b5-106">Las referencias de ensamblado explícitas están relacionadas con ensamblados .NET.</span><span class="sxs-lookup"><span data-stu-id="c57b5-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="c57b5-107">No son un método para distribuir ensamblados nativos invocados por un ensamblado administrado mediante P/Invoke.</span><span class="sxs-lookup"><span data-stu-id="c57b5-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="c57b5-108">Compatibilidad con `PackageReference`</span><span class="sxs-lookup"><span data-stu-id="c57b5-108">`PackageReference` support</span></span>

<span data-ttu-id="c57b5-109">Cuando un proyecto usa un paquete con `PackageReference` y dicho paquete contiene un directorio `ref\<tfm>\`, NuGet clasifica estos ensamblados como recursos en tiempo de compilación, mientras que los ensamblados `lib\<tfm>\` se clasifican como recursos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c57b5-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="c57b5-110">Los ensamblados de `ref\<tfm>\` no se usan en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c57b5-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="c57b5-111">Esto significa que todos los ensamblados de `ref\<tfm>\` deben tener un ensamblado coincidente en el directorio `lib\<tfm>\` o en un directorio `runtime\` pertinente. En caso contrario, probablemente se producirán errores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c57b5-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="c57b5-112">Dado que los ensamblados de `ref\<tfm>\` no se usan en tiempo de ejecución, podrían ser [ensamblados de solo metadatos](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) para reducir el tamaño del paquete.</span><span class="sxs-lookup"><span data-stu-id="c57b5-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="c57b5-113">Si un paquete contiene el elemento `<references>` nuspec (usado por `packages.config`, como verá más abajo) y no incluye ensamblados en `ref\<tfm>\`, NuGet anunciará los ensamblados que aparecen en el elemento `<references>` nuspec como recursos en tiempo de compilación y ejecución.</span><span class="sxs-lookup"><span data-stu-id="c57b5-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="c57b5-114">Esto significa que habrá excepciones en tiempo de ejecución cuando los ensamblados a los que se hace referencia necesiten cargar otro ensamblado en el directorio `lib\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="c57b5-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="c57b5-115">Si el paquete contiene un directorio `runtime\`, NuGet podría no usar los recursos del directorio `lib\`.</span><span class="sxs-lookup"><span data-stu-id="c57b5-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="c57b5-116">Compatibilidad con `packages.config`</span><span class="sxs-lookup"><span data-stu-id="c57b5-116">`packages.config` support</span></span>

<span data-ttu-id="c57b5-117">Los proyectos que usan `packages.config` para administrar paquetes NuGet suelen agregar referencias a todos los ensamblados del directorio `lib\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="c57b5-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="c57b5-118">El directorio `ref\` se ha agregado para admitir `PackageReference`, por lo que no se tiene en cuenta al usar `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="c57b5-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="c57b5-119">Para establecer explícitamente a qué ensamblados se hace referencia para los proyectos que usan `packages.config`, el paquete debe emplear el elemento [`<references>` en el archivo nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="c57b5-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="c57b5-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c57b5-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="c57b5-121">El proyecto `packages.config` usa un proceso denominado [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) para copiar los ensamblados en el directorio de salida `bin\<configuration>\`.</span><span class="sxs-lookup"><span data-stu-id="c57b5-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="c57b5-122">Se copia el ensamblado del proyecto y, luego, el sistema de compilación examina el manifiesto del ensamblado en busca de los ensamblados a los que se hace referencia. Después, copia esos ensamblados y repite el proceso de forma recursiva para todos los ensamblados.</span><span class="sxs-lookup"><span data-stu-id="c57b5-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="c57b5-123">Esto significa que si alguno de los ensamblados del directorio `lib\<tfm>\` no se muestra en el manifiesto de otro ensamblado como una dependencia (si el ensamblado se carga en tiempo de ejecución mediante `Assembly.Load`, MEF u otro marco de inserción de dependencias), puede que no se copie en el directorio de salida `bin\<configuration>\` del proyecto, a pesar de estar en `bin\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="c57b5-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="c57b5-124">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c57b5-124">Example</span></span>

<span data-ttu-id="c57b5-125">Mi paquete contendrá tres ensamblados (`MyLib.dll`, `MyHelpers.dll` y `MyUtilities.dll`), que están destinados a .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="c57b5-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="c57b5-126">`MyUtilities.dll` contiene clases diseñadas para que las usen únicamente los otros dos ensamblados, por lo que no quiero que esas clases estén disponibles en IntelliSense o en tiempo de compilación para los proyectos que usen mi paquete.</span><span class="sxs-lookup"><span data-stu-id="c57b5-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="c57b5-127">Mi archivo `nuspec` debe contener los siguientes elementos XML:</span><span class="sxs-lookup"><span data-stu-id="c57b5-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="c57b5-128">Los archivos del paquete serán los siguientes:</span><span class="sxs-lookup"><span data-stu-id="c57b5-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
