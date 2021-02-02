---
title: Cómo publicar paquetes de símbolos de NuGet con el nuevo formato de paquete de símbolos ".snupkg" | Microsoft Docs
author: JonDouglas
ms.author: jodou
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Cómo crear paquetes de símbolos de NuGet (snupkg).
keywords: Paquetes de símbolos de NuGet, depuración de paquetes de NuGet, compatibilidad con la depuración de NuGet, símbolos de paquetes, convenciones de paquetes de símbolos
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 001637348fdd435e4ffd3a5a55e8128d1eab453c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774571"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="c0025-104">Crear paquetes de símbolos (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="c0025-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="c0025-105">Una buena experiencia de depuración se basa en la presencia de símbolos de depuración, ya que proporcionan información crítica, como la asociación entre el código de origen y el compilado, los nombres de variables locales, los seguimientos de la pila, etc.</span><span class="sxs-lookup"><span data-stu-id="c0025-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="c0025-106">Puede usar paquetes de símbolos (.snupkg) para distribuir estos símbolos y mejorar la experiencia de depuración de los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="c0025-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

> <span data-ttu-id="c0025-107">Tenga en cuenta que el paquete de símbolos no es la única estrategia para poner los símbolos de depuración a disposición de los consumidores de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="c0025-107">Note that symbol package isn't the only strategy to make the debug symbols available to the consumers of your library.</span></span> <span data-ttu-id="c0025-108">También es [posible `embed`](https://docs.microsoft.com/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) en `dll` o `exe` con la siguiente propiedad de proyecto: `<DebugType>embedded</DebugType>`</span><span class="sxs-lookup"><span data-stu-id="c0025-108">It's also [possible to `embed`](https://docs.microsoft.com/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) them in the `dll` or `exe` with the following project property: `<DebugType>embedded</DebugType>`</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0025-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c0025-109">Prerequisites</span></span>

<span data-ttu-id="c0025-110">[nuget.exe 4.9.0 o una versión superior](https://www.nuget.org/downloads) o [la CLI de dotnet 2.2.0 o una versión superior](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementan los [protocolos de NuGet](../api/nuget-protocols.md) requeridos.</span><span class="sxs-lookup"><span data-stu-id="c0025-110">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="c0025-111">Crear un paquete de símbolos</span><span class="sxs-lookup"><span data-stu-id="c0025-111">Creating a symbol package</span></span>

<span data-ttu-id="c0025-112">Si usa la CLI de dotnet o MSBuild, debe establecer las propiedades `IncludeSymbols` y `SymbolPackageFormat` para crear un archivo .snupkg además del archivo .nupkg.</span><span class="sxs-lookup"><span data-stu-id="c0025-112">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="c0025-113">Puede agregar las siguientes propiedades al archivo .csproj:</span><span class="sxs-lookup"><span data-stu-id="c0025-113">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="c0025-114">O bien especificar estas propiedades en la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="c0025-114">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="c0025-115">or</span><span class="sxs-lookup"><span data-stu-id="c0025-115">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="c0025-116">Si usa NuGet.exe, puede emplear los siguientes comandos para crear un archivo .snupkg, además del archivo .nupkg:</span><span class="sxs-lookup"><span data-stu-id="c0025-116">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="c0025-117">La propiedad [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) puede tener uno de estos dos valores: `symbols.nupkg` (predeterminado) o `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c0025-117">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="c0025-118">Si no se especifica la propiedad, se creará un paquete de símbolos heredado.</span><span class="sxs-lookup"><span data-stu-id="c0025-118">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="c0025-119">El formato heredado `.symbols.nupkg` todavía se admite, pero solo por motivos de compatibilidad como los paquetes nativos (vea [Paquetes de símbolos heredados](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="c0025-119">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons like native packages (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="c0025-120">El servidor de símbolos de NuGet.org solo acepta el nuevo formato de paquete de símbolos, `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c0025-120">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="c0025-121">Publicar un paquete de símbolos</span><span class="sxs-lookup"><span data-stu-id="c0025-121">Publishing a symbol package</span></span>

1. <span data-ttu-id="c0025-122">Para su comodidad, guarde primero la clave de API con NuGet (vea [publicar un paquete](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="c0025-122">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="c0025-123">Después de publicar el paquete principal en nuget.org, inserte el paquete de símbolos tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="c0025-123">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="c0025-124">También puede insertar ambos paquetes al mismo tiempo con el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="c0025-124">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="c0025-125">Tanto los archivos .nupkg como .snupkg deben estar presentes en la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="c0025-125">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="c0025-126">NuGet publicará ambos paquetes en nuget.org. `MyPackage.nupkg` se publica en primer lugar, y luego `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c0025-126">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="c0025-127">Si no se publica el paquete de símbolos, compruebe que ha configurado el origen de NuGet.org como `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="c0025-127">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="c0025-128">La publicación de paquetes de símbolos solo es compatible con [la API de NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="c0025-128">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="c0025-129">Servidor de símbolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c0025-129">NuGet.org symbol server</span></span>

<span data-ttu-id="c0025-130">NuGet.org admite su propio repositorio de servidor de símbolos y solo acepta el nuevo formato de paquete de símbolos, `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c0025-130">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="c0025-131">Los consumidores de paquetes pueden usar los símbolos publicados en el servidor de símbolos de nuget.org agregando `https://symbols.nuget.org/download/symbols` a sus orígenes de símbolos en Visual Studio, que permite entrar en el código del paquete en el depurador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0025-131">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="c0025-132">Vea [Especificar archivos de código fuente y símbolos (.pdb) en el depurador de Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obtener información detallada sobre ese proceso.</span><span class="sxs-lookup"><span data-stu-id="c0025-132">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="c0025-133">Restricciones de paquete de símbolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c0025-133">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="c0025-134">NuGet.org tiene estas restricciones para los paquetes de símbolos:</span><span class="sxs-lookup"><span data-stu-id="c0025-134">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="c0025-135">Solo se permiten las siguientes extensiones de archivo en los paquetes de símbolos: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span><span class="sxs-lookup"><span data-stu-id="c0025-135">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="c0025-136">En estos momentos, solo se admiten archivos [PDB portátiles](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) en el servidor de símbolos de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c0025-136">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="c0025-137">Los archivos PDB y las DLL de .nupkg asociadas deben compilarse con el compilador de la versión 15.9 de Visual Studio o una superior (vea [hash criptográfico de PDB](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="c0025-137">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="c0025-138">Los paquetes de símbolos publicados en NuGet.org producirán un error de validación si no se cumplen estas restricciones.</span><span class="sxs-lookup"><span data-stu-id="c0025-138">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

> [!NOTE]
> <span data-ttu-id="c0025-139">Los proyectos nativos, como los de C++, generan archivos PDB de Windows en lugar de archivos PDB portátiles.</span><span class="sxs-lookup"><span data-stu-id="c0025-139">Native projects, such as C++ projects, produce Windows PDBs instead of Portable PDBs.</span></span> <span data-ttu-id="c0025-140">Estos no son compatibles con el servidor de símbolos de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c0025-140">These are not supported by NuGet.org's symbol server.</span></span> <span data-ttu-id="c0025-141">En su lugar, use [paquetes de símbolos heredados](Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="c0025-141">Please use [Legacy Symbol Packages](Symbol-Packages.md) instead.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="c0025-142">Validación e indexación de paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="c0025-142">Symbol package validation and indexing</span></span>

<span data-ttu-id="c0025-143">Los paquetes de símbolos publicados en [NuGet.org](https://www.nuget.org/) se someten a varias validaciones, como análisis de malware.</span><span class="sxs-lookup"><span data-stu-id="c0025-143">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="c0025-144">Si un paquete no supera la comprobación de validación, la página de detalles del paquete mostrará un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="c0025-144">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="c0025-145">Además, los propietarios del paquete recibirán un correo electrónico con instrucciones sobre cómo corregir los problemas identificados.</span><span class="sxs-lookup"><span data-stu-id="c0025-145">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="c0025-146">Cuando el paquete de símbolos haya superado todas las validaciones, los símbolos se indexarán mediante los servidores de símbolos de NuGet.org y estarán listos para su consumo.</span><span class="sxs-lookup"><span data-stu-id="c0025-146">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="c0025-147">La validación y la indexación del paquete suelen tardar menos de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="c0025-147">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="c0025-148">Si la publicación del paquete tarda más de lo esperado, visite [status.nuget.org](https://status.nuget.org/) para comprobar si NuGet.org está experimentando alguna interrupción.</span><span class="sxs-lookup"><span data-stu-id="c0025-148">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="c0025-149">Si todos los sistemas están operativos y el paquete no se ha publicado correctamente en una hora, inicie sesión en nuget.org y póngase en contacto con nosotros mediante el vínculo de contacto con el equipo de soporte técnico de la página de detalles del paquete.</span><span class="sxs-lookup"><span data-stu-id="c0025-149">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="c0025-150">Estructura del paquete de símbolos</span><span class="sxs-lookup"><span data-stu-id="c0025-150">Symbol package structure</span></span>

<span data-ttu-id="c0025-151">El paquete de símbolos (.snupkg) tiene las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="c0025-151">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="c0025-152">El .snupkg tiene el mismo identificador y la misma versión que el paquete NuGet correspondiente (.nupkg).</span><span class="sxs-lookup"><span data-stu-id="c0025-152">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="c0025-153">El archivo .snupkg tiene la misma estructura de carpetas que el archivo .nupkg correspondiente para cualquier archivo DLL o EXE con la diferencia de que, en vez de los archivos DLL o EXE, los archivos PDB correspondientes deben estar incluidos en la misma jerarquía de carpetas.</span><span class="sxs-lookup"><span data-stu-id="c0025-153">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="c0025-154">El archivo .snupkg no debe incluir ningún archivos o carpetas con extensiones que no sean PDB.</span><span class="sxs-lookup"><span data-stu-id="c0025-154">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="c0025-155">El archivo .nuspec del paquete de símbolos tiene el tipo de paquete `SymbolsPackage`:</span><span class="sxs-lookup"><span data-stu-id="c0025-155">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="c0025-156">Si un autor decide usar un archivo .nuspec personalizado para compilar sus archivos .nupkg y .snupkg, estos deben tener la misma jerarquía de carpetas y archivos mostrados en el punto 2.</span><span class="sxs-lookup"><span data-stu-id="c0025-156">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="c0025-157">Los siguientes campos se excluirán del archivo .nuspec del archivo .snupkg: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl``` y ```icon```.</span><span class="sxs-lookup"><span data-stu-id="c0025-157">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="c0025-158">No utilice el elemento ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="c0025-158">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="c0025-159">Se trata un .snupkg con la misma licencia que el .nupkg correspondiente.</span><span class="sxs-lookup"><span data-stu-id="c0025-159">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="c0025-160">Consulta también</span><span class="sxs-lookup"><span data-stu-id="c0025-160">See also</span></span>

<span data-ttu-id="c0025-161">Considere la posibilidad de usar el vínculo de origen para habilitar la depuración de código fuente de ensamblados .NET.</span><span class="sxs-lookup"><span data-stu-id="c0025-161">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="c0025-162">Para obtener más información, vea la [guía de vínculos de origen](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="c0025-162">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="c0025-163">Para obtener más información sobre los paquetes de símbolos, vea la especificación de diseño de [Mejoras de símbolos y depuración de paquetes NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements).</span><span class="sxs-lookup"><span data-stu-id="c0025-163">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
