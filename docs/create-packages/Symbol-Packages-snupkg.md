---
title: Cómo publicar paquetes de símbolos de NuGet con el nuevo formato de paquete de símbolos ".snupkg" | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
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
ms.openlocfilehash: 5546881dbf7577eb289a28b35bc2c0e7dc5cac40
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094101"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="c442b-104">Crear paquetes de símbolos (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="c442b-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="c442b-105">Los paquetes de símbolos permiten mejorar la experiencia de depuración de los paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="c442b-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c442b-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c442b-106">Prerequisites</span></span>

<span data-ttu-id="c442b-107">[nuget.exe v4.9.0 o una versión superior](https://www.nuget.org/downloads) o [dotnet.exe v2.2.0 o una versión superior](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementan los [protocolos de NuGet](../api/nuget-protocols.md) requeridos.</span><span class="sxs-lookup"><span data-stu-id="c442b-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="c442b-108">Crear un paquete de símbolos</span><span class="sxs-lookup"><span data-stu-id="c442b-108">Creating a symbol package</span></span>

<span data-ttu-id="c442b-109">Si usa dotnet.exe o MSBuild, debe establecer las propiedades `IncludeSymbols` y `SymbolPackageFormat` para crear un archivo .snupkg además del archivo .nupkg.</span><span class="sxs-lookup"><span data-stu-id="c442b-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="c442b-110">Puede agregar las siguientes propiedades al archivo .csproj:</span><span class="sxs-lookup"><span data-stu-id="c442b-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="c442b-111">O bien especificar estas propiedades en la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="c442b-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="c442b-112">o</span><span class="sxs-lookup"><span data-stu-id="c442b-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="c442b-113">Si usa NuGet.exe, puede emplear los siguientes comandos para crear un archivo .snupkg, además del archivo .nupkg:</span><span class="sxs-lookup"><span data-stu-id="c442b-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="c442b-114">La propiedad [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) puede tener uno de estos dos valores: `symbols.nupkg` (predeterminado) o `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c442b-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="c442b-115">Si no se especifica la propiedad, se creará un paquete de símbolos heredado.</span><span class="sxs-lookup"><span data-stu-id="c442b-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="c442b-116">El formato heredado `.symbols.nupkg` todavía se admite, pero solo por motivos de compatibilidad (vea [Paquetes de símbolos heredados](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="c442b-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="c442b-117">El servidor de símbolos de NuGet.org solo acepta el nuevo formato de paquete de símbolos, `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c442b-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="c442b-118">Publicar un paquete de símbolos</span><span class="sxs-lookup"><span data-stu-id="c442b-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="c442b-119">Para su comodidad, guarde primero la clave de API con NuGet (vea [publicar un paquete](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="c442b-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="c442b-120">Después de publicar el paquete principal en nuget.org, inserte el paquete de símbolos tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="c442b-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="c442b-121">También puede insertar ambos paquetes al mismo tiempo con el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="c442b-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="c442b-122">Tanto los archivos .nupkg como .snupkg deben estar presentes en la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="c442b-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="c442b-123">NuGet publicará ambos paquetes en nuget.org. `MyPackage.nupkg` se publica en primer lugar, y luego `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c442b-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="c442b-124">Si no se publica el paquete de símbolos, compruebe que ha configurado el origen de NuGet.org como `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="c442b-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="c442b-125">La publicación de paquetes de símbolos solo es compatible con [la API de NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="c442b-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="c442b-126">Servidor de símbolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c442b-126">NuGet.org symbol server</span></span>

<span data-ttu-id="c442b-127">NuGet.org admite su propio repositorio de servidor de símbolos y solo acepta el nuevo formato de paquete de símbolos, `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c442b-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="c442b-128">Los consumidores de paquetes pueden usar los símbolos publicados en el servidor de símbolos de nuget.org agregando `https://symbols.nuget.org/download/symbols` a sus orígenes de símbolos en Visual Studio, que permite entrar en el código del paquete en el depurador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c442b-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="c442b-129">Vea [Especificar archivos de código fuente y símbolos (.pdb) en el depurador de Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md) para obtener información detallada sobre ese proceso.</span><span class="sxs-lookup"><span data-stu-id="c442b-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="c442b-130">Restricciones de paquete de símbolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c442b-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="c442b-131">NuGet.org tiene estas restricciones para los paquetes de símbolos:</span><span class="sxs-lookup"><span data-stu-id="c442b-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="c442b-132">Solo se permiten las siguientes extensiones de archivo en los paquetes de símbolos: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span><span class="sxs-lookup"><span data-stu-id="c442b-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="c442b-133">En estos momentos, solo se admiten archivos [PDB portátiles](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) en el servidor de símbolos de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c442b-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="c442b-134">Los archivos PDB y las DLL de .nupkg asociadas deben compilarse con el compilador de la versión 15.9 de Visual Studio o una superior (vea [hash criptográfico de PDB](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="c442b-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="c442b-135">Los paquetes de símbolos publicados en NuGet.org producirán un error de validación si no se cumplen estas restricciones.</span><span class="sxs-lookup"><span data-stu-id="c442b-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="c442b-136">Validación e indexación de paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="c442b-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="c442b-137">Los paquetes de símbolos publicados en [NuGet.org](https://www.nuget.org/) se someten a varias validaciones, como análisis de malware.</span><span class="sxs-lookup"><span data-stu-id="c442b-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="c442b-138">Si un paquete no supera la comprobación de validación, la página de detalles del paquete mostrará un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="c442b-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="c442b-139">Además, los propietarios del paquete recibirán un correo electrónico con instrucciones sobre cómo corregir los problemas identificados.</span><span class="sxs-lookup"><span data-stu-id="c442b-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="c442b-140">Cuando el paquete de símbolos haya superado todas las validaciones, los símbolos se indexarán mediante los servidores de símbolos de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c442b-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="c442b-141">Una vez indexado, el símbolo estará disponible para su consumo desde los servidores de símbolos de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c442b-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="c442b-142">La validación y la indexación del paquete suelen tardar menos de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="c442b-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="c442b-143">Si la publicación del paquete tarda más de lo esperado, visite [status.nuget.org](https://status.nuget.org/) para comprobar si NuGet.org está experimentando alguna interrupción.</span><span class="sxs-lookup"><span data-stu-id="c442b-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="c442b-144">Si todos los sistemas están operativos y el paquete no se ha publicado correctamente en una hora, inicie sesión en nuget.org y póngase en contacto con nosotros mediante el vínculo de contacto con el equipo de soporte técnico de la página de detalles del paquete.</span><span class="sxs-lookup"><span data-stu-id="c442b-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="c442b-145">Estructura del paquete de símbolos</span><span class="sxs-lookup"><span data-stu-id="c442b-145">Symbol package structure</span></span>

<span data-ttu-id="c442b-146">El archivo .nupkg debería ser exactamente el mismo que el de hoy, pero el archivo .snupkg debería tener las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="c442b-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="c442b-147">El archivo .snupkg debe tener el mismo id. y la misma versión que el archivo .nupkg correspondiente.</span><span class="sxs-lookup"><span data-stu-id="c442b-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="c442b-148">El archivo .snupkg debe tener la misma estructura de carpetas exacta que el archivo .nupkg para cualquier archivo DLL o EXE con distinción de que, en vez de los archivos DLL o EXE, los archivos PDB correspondientes deben estar incluidos en la misma jerarquía de carpetas.</span><span class="sxs-lookup"><span data-stu-id="c442b-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="c442b-149">El archivo .snupkg no debe incluir ningún archivos o carpetas con extensiones que no sean PDB.</span><span class="sxs-lookup"><span data-stu-id="c442b-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="c442b-150">El archivo .nuspec del archivo .snupkg también debe especificar un nuevo PackageType, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="c442b-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="c442b-151">Este debería ser el único PackageType especificado.</span><span class="sxs-lookup"><span data-stu-id="c442b-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="c442b-152">Si un autor decide usar un archivo .nuspec personalizado para compilar sus archivos .nupkg y .snupkg, estos deben tener la misma jerarquía de carpetas y archivos mostrados en el punto 2.</span><span class="sxs-lookup"><span data-stu-id="c442b-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="c442b-153">Los campos ```authors``` y ```owners``` deben excluirse del archivo .nuspec del archivo .snupkg.</span><span class="sxs-lookup"><span data-stu-id="c442b-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="c442b-154">No utilice el elemento ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="c442b-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="c442b-155">Se trata un .snupkg con la misma licencia que el .nupkg correspondiente.</span><span class="sxs-lookup"><span data-stu-id="c442b-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="c442b-156">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="c442b-156">See Also</span></span>

<span data-ttu-id="c442b-157">Considere la posibilidad de usar el vínculo de origen para habilitar la depuración de código fuente de ensamblados .NET.</span><span class="sxs-lookup"><span data-stu-id="c442b-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="c442b-158">Para obtener más información, vea la [guía de vínculos de origen](/dotnet/standard/library-guidance/sourcelink.md).</span><span class="sxs-lookup"><span data-stu-id="c442b-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink.md).</span></span>

<span data-ttu-id="c442b-159">Para obtener más información sobre los paquetes de símbolos, vea la especificación de diseño de [Mejoras de símbolos y depuración de paquetes NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements).</span><span class="sxs-lookup"><span data-stu-id="c442b-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
