---
title: Compatibilidad con múltiples versiones de paquetes NuGet en el archivo del proyecto
description: Descripción de los distintos métodos para fijar como destino varias versiones de .NET Framework desde un único paquete de NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: b7870bb6aac39f0865d88efc8c16751fdbecc3a8
ms.sourcegitcommit: cae759ad8518c049575a30ad3bf04fe5d06244fb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2019
ms.locfileid: "68616775"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="26d80-103">Compatibilidad con varias versiones de .NET Framework en el archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="26d80-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="26d80-104">Cuando cree un proyecto por primera vez, le recomendamos crear una biblioteca de clases de .NET Standard, puesto que proporciona compatibilidad con la variedad más amplia de proyectos de consumo.</span><span class="sxs-lookup"><span data-stu-id="26d80-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="26d80-105">Al usar .NET Standard, agrega [compatibilidad multiplataforma](/dotnet/standard/library-guidance/cross-platform-targeting) a una biblioteca de .NET de manera predeterminado.</span><span class="sxs-lookup"><span data-stu-id="26d80-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="26d80-106">Sin embargo, en algunos escenarios, es posible que también tenga que incluir código que tenga como destino un marco determinado.</span><span class="sxs-lookup"><span data-stu-id="26d80-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="26d80-107">En este artículo se muestra cómo hacerlo para proyectos de [estilo SDK](../resources/check-project-format.md).</span><span class="sxs-lookup"><span data-stu-id="26d80-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="26d80-108">En el caso de los proyectos de estilo SDK, puede configurar la compatibilidad con varios marcos de destino ([TFM](/dotnet/standard/frameworks)) en el archivo del proyecto y, luego, usar `dotnet pack` o `msbuild /t:pack` para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="26d80-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="26d80-109">La CLI de nuget.exe no permite empaquetar los proyectos de estilo SDK, por lo que solo debe usar `dotnet pack` o `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="26d80-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="26d80-110">En su lugar, se recomienda [incluir todas las propiedades](../reference/msbuild-targets.md#pack-target) que usualmente están en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="26d80-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="26d80-111">Para tener como destino varias versiones de .NET Framework en un proyecto que no es de estilo SDK, consulte [Compatibilidad con varias versiones de .NET Framework](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="26d80-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="26d80-112">Creación de un proyecto que admite varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="26d80-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="26d80-113">Cree una biblioteca de clases .NET Standard en Visual Studio o use `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="26d80-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="26d80-114">Para una mayor compatibilidad, se recomienda crear una biblioteca de clases .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="26d80-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="26d80-115">Edite el archivo *.csproj* para admitir los marcos de destino.</span><span class="sxs-lookup"><span data-stu-id="26d80-115">Edit the *.csproj* file to support the target frameworks.</span></span>

   <span data-ttu-id="26d80-116">Por ejemplo, cambie `<TargetFramework>netstandard2.0</TargetFramework>` a `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.</span><span class="sxs-lookup"><span data-stu-id="26d80-116">For example, change `<TargetFramework>netstandard2.0</TargetFramework>` to `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.</span></span>

   <span data-ttu-id="26d80-117">Asegúrese de cambiar el elemento XML modificado de singular a plural (agregue "s" a las etiquetas de apertura y cierre).</span><span class="sxs-lookup"><span data-stu-id="26d80-117">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="26d80-118">Si tiene algún código que solo funciona en un TFM, puede usar `#if NET45` o `#if NETSTANDARD20` para separar el código que depende de TFM.</span><span class="sxs-lookup"><span data-stu-id="26d80-118">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD20` to separate TFM-dependent code.</span></span> <span data-ttu-id="26d80-119">(Para más información, consulte [Cómo lograr la compatibilidad con múltiples versiones](/dotnet/core/tutorials/libraries#how-to-multitarget)). Por ejemplo, puede usar este código:</span><span class="sxs-lookup"><span data-stu-id="26d80-119">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. <span data-ttu-id="26d80-120">Agregue los metadatos de NuGet que quiera a *.csproj* como propiedades de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="26d80-120">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="26d80-121">Para ver la lista de metadatos de paquetes disponibles y los nombres de las propiedades de MSBuild, consulte [pack target](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="26d80-121">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="26d80-122">Consulte también [Controlar los recursos de dependencias](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="26d80-122">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="26d80-123">Si quiere separar las propiedades relacionadas con la compilación de los metadatos de NuGet, puede usar un `PropertyGroup` distinto o poner las propiedades de NuGet en otro archivo y usar la directiva `Import` de MSBuild para incluirlo.</span><span class="sxs-lookup"><span data-stu-id="26d80-123">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="26d80-124">`Directory.Build.Props` y `Directory.Build.Targets` también son compatibles a partir de MSBuild 15.0.</span><span class="sxs-lookup"><span data-stu-id="26d80-124">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="26d80-125">Ahora, use `dotnet pack` y el *.nupkg* resultante tendrá como destino tanto a .NET Standard 2.0 como .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="26d80-125">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="26d80-126">Este es el archivo *.csproj* que se genera con los pasos anteriores y el SDK de .NET Core 2.2.</span><span class="sxs-lookup"><span data-stu-id="26d80-126">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="26d80-127">Vea también</span><span class="sxs-lookup"><span data-stu-id="26d80-127">See also</span></span>

* [<span data-ttu-id="26d80-128">Cómo especificar plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="26d80-128">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="26d80-129">Destinatarios multiplataforma</span><span class="sxs-lookup"><span data-stu-id="26d80-129">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
