---
title: Establecimiento de un tipo de paquete NuGet
description: En este artículo se describen los tipos de paquetes para indicar el uso previsto de un paquete.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067288"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="35991-103">Establecimiento de un tipo de paquete NuGet</span><span class="sxs-lookup"><span data-stu-id="35991-103">Set a NuGet package type</span></span>

<span data-ttu-id="35991-104">Los paquetes se pueden marcar con uno más *tipos de paquetes* para indicar su uso previsto.</span><span class="sxs-lookup"><span data-stu-id="35991-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="35991-105">Tipos de paquete conocidos</span><span class="sxs-lookup"><span data-stu-id="35991-105">Known package types</span></span>

- <span data-ttu-id="35991-106">Los paquetes de tipo `Dependency` agregan activos de tiempo de compilación o ejecución a las aplicaciones y bibliotecas, y se pueden instalar en cualquier tipo de proyecto (suponiendo que sean compatibles).</span><span class="sxs-lookup"><span data-stu-id="35991-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="35991-107">Los paquetes de tipo `DotnetTool` son herramientas de .NET que se pueden instalar mediante la [CLI de dotnet](/dotnet/articles/core/tools/index).</span><span class="sxs-lookup"><span data-stu-id="35991-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="35991-108">Los paquetes de tipo `Template` proporcionan [plantillas personalizadas](/dotnet/core/tools/custom-templates) que se pueden usar para crear archivos o proyectos como una aplicación, un servicio, una herramienta o una biblioteca de clases.</span><span class="sxs-lookup"><span data-stu-id="35991-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="35991-109">Los paquetes que no se marcan con un tipo, incluidos todos los creados con versiones anteriores de NuGet, tienen el tipo `Dependency` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="35991-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="35991-110">Se agregó compatibilidad con tipos de paquete en NuGet 3.5.</span><span class="sxs-lookup"><span data-stu-id="35991-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="35991-111">Si no necesita un tipo de paquete personalizado, es mejor *no* establecer explícitamente el tipo de paquete.</span><span class="sxs-lookup"><span data-stu-id="35991-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="35991-112">El tipo predeterminado de NuGet es `Dependency` cuando no se especifica ningún tipo.</span><span class="sxs-lookup"><span data-stu-id="35991-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="35991-113">Tipos de paquetes personalizados</span><span class="sxs-lookup"><span data-stu-id="35991-113">Custom package types</span></span>

<span data-ttu-id="35991-114">Puede marcar el paquete con uno o varios tipos de paquetes personalizados si su uso no se ajusta a los [tipos de paquete conocidos](#known-package-types).</span><span class="sxs-lookup"><span data-stu-id="35991-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="35991-115">Por ejemplo, imagine que los clientes de la aplicación `Contoso` pueden instalar extensiones.</span><span class="sxs-lookup"><span data-stu-id="35991-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="35991-116">La aplicación podría requerir que los autores de extensiones usen el tipo de paquete personalizado `ContosoExtension` para identificar sus paquetes como extensiones adecuadas que sigan las convenciones necesarias.</span><span class="sxs-lookup"><span data-stu-id="35991-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="35991-117">Visual Studio o nuget.exe no pueden instalar un paquete con un tipo de paquete personalizado.</span><span class="sxs-lookup"><span data-stu-id="35991-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="35991-118">Consulte [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) para más información.</span><span class="sxs-lookup"><span data-stu-id="35991-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="35991-119">Uso de la CLI de dotnet</span><span class="sxs-lookup"><span data-stu-id="35991-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="35991-120">Los tipos de paquete se pueden establecer en el archivo de proyecto (`.csproj`):</span><span class="sxs-lookup"><span data-stu-id="35991-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="35991-121">Los paquetes con varios usos previstos se pueden marcar con varios tipos de paquete mediante el delimitador `;`:</span><span class="sxs-lookup"><span data-stu-id="35991-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="35991-122">Se pueden crear versiones de los tipos de paquete mediante un delimitador `,` entre el tipo de paquete y su cadena [`Version`](/dotnet/api/system.version):</span><span class="sxs-lookup"><span data-stu-id="35991-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="35991-123">Uso de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="35991-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="35991-124">Los tipos de paquete se establecen en el archivo `.nuspec` dentro de un nodo `packageTypes\packageType` en el elemento `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="35991-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="35991-125">Los paquetes con varios usos previstos se pueden marcar con varios tipos de paquete:</span><span class="sxs-lookup"><span data-stu-id="35991-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="35991-126">Se pueden crear versiones de los tipos de paquete mediante una cadena [`Version`](/dotnet/api/system.version):</span><span class="sxs-lookup"><span data-stu-id="35991-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

<span data-ttu-id="35991-127">El formato de una cadena de tipo paquete es exactamente igual al de un identificador de paquete.</span><span class="sxs-lookup"><span data-stu-id="35991-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="35991-128">Es decir, un tipo de paquete es una cadena que no distingue mayúsculas de minúsculas que coincide con la expresión regular `^\w+([_.-]\w+)*$` que tiene al menos un carácter y como máximo 100 caracteres.</span><span class="sxs-lookup"><span data-stu-id="35991-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="35991-129">Si se proporciona, la versión del tipo de paquete es una cadena [`Version`](/dotnet/api/system.version).</span><span class="sxs-lookup"><span data-stu-id="35991-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="35991-130">La versión del tipo de paquete es opcional y el valor predeterminado es `0.0`.</span><span class="sxs-lookup"><span data-stu-id="35991-130">The package type version is optional and defaults to `0.0`.</span></span>
