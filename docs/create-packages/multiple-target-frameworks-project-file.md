---
title: Compatibilidad con múltiples versiones de paquetes NuGet en el archivo del proyecto
description: Descripción de los distintos métodos para fijar como destino varias versiones de .NET Framework desde un único paquete de NuGet en el archivo del proyecto.
author: JonDouglas
ms.author: jodou
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: a05d053340bb2fe795991dfa5a2b95d8625dfd44
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774384"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="64b89-103">Compatibilidad con varias versiones de .NET Framework en el archivo del proyecto</span><span class="sxs-lookup"><span data-stu-id="64b89-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="64b89-104">Cuando cree un proyecto por primera vez, le recomendamos crear una biblioteca de clases de .NET Standard, puesto que proporciona compatibilidad con la variedad más amplia de proyectos de consumo.</span><span class="sxs-lookup"><span data-stu-id="64b89-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="64b89-105">Al usar .NET Standard, agrega [compatibilidad multiplataforma](/dotnet/standard/library-guidance/cross-platform-targeting) a una biblioteca de .NET de manera predeterminado.</span><span class="sxs-lookup"><span data-stu-id="64b89-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="64b89-106">Sin embargo, en algunos escenarios, es posible que también tenga que incluir código que tenga como destino un marco determinado.</span><span class="sxs-lookup"><span data-stu-id="64b89-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="64b89-107">En este artículo se muestra cómo hacerlo para proyectos de [estilo SDK](../resources/check-project-format.md).</span><span class="sxs-lookup"><span data-stu-id="64b89-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="64b89-108">En el caso de los proyectos de estilo SDK, puede configurar la compatibilidad con varios marcos de destino ([TFM](/dotnet/standard/frameworks)) en el archivo del proyecto y, luego, usar `dotnet pack` o `msbuild /t:pack` para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="64b89-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="64b89-109">La CLI de nuget.exe no permite empaquetar los proyectos de estilo SDK, por lo que solo debe usar `dotnet pack` o `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="64b89-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="64b89-110">En su lugar, se recomienda [incluir todas las propiedades](../reference/msbuild-targets.md#pack-target) que usualmente están en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="64b89-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="64b89-111">Para tener como destino varias versiones de .NET Framework en un proyecto que no es de estilo SDK, consulte [Compatibilidad con varias versiones de .NET Framework](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="64b89-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="64b89-112">Creación de un proyecto que admite varias versiones de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="64b89-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="64b89-113">Cree una biblioteca de clases .NET Standard en Visual Studio o use `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="64b89-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="64b89-114">Para una mayor compatibilidad, se recomienda crear una biblioteca de clases .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="64b89-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="64b89-115">Edite el archivo *.csproj* para admitir los marcos de destino.</span><span class="sxs-lookup"><span data-stu-id="64b89-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="64b89-116">Por ejemplo, cambie</span><span class="sxs-lookup"><span data-stu-id="64b89-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="64b89-117">a:</span><span class="sxs-lookup"><span data-stu-id="64b89-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="64b89-118">Asegúrese de cambiar el elemento XML modificado de singular a plural (agregue "s" a las etiquetas de apertura y cierre).</span><span class="sxs-lookup"><span data-stu-id="64b89-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="64b89-119">Si tiene algún código que solo funciona en un TFM, puede usar `#if NET45` o `#if NETSTANDARD2_0` para separar el código que depende de TFM.</span><span class="sxs-lookup"><span data-stu-id="64b89-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="64b89-120">(Para más información, consulte [Cómo lograr la compatibilidad con múltiples versiones](/dotnet/core/tutorials/libraries#how-to-multitarget)). Por ejemplo, puede usar este código:</span><span class="sxs-lookup"><span data-stu-id="64b89-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

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

4. <span data-ttu-id="64b89-121">Agregue los metadatos de NuGet que quiera a *.csproj* como propiedades de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="64b89-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="64b89-122">Para ver la lista de metadatos de paquetes disponibles y los nombres de las propiedades de MSBuild, consulte [pack target](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="64b89-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="64b89-123">Consulte también [Controlar los recursos de dependencias](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="64b89-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="64b89-124">Si quiere separar las propiedades relacionadas con la compilación de los metadatos de NuGet, puede usar un `PropertyGroup` distinto o poner las propiedades de NuGet en otro archivo y usar la directiva `Import` de MSBuild para incluirlo.</span><span class="sxs-lookup"><span data-stu-id="64b89-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="64b89-125">`Directory.Build.Props` y `Directory.Build.Targets` también son compatibles a partir de MSBuild 15.0.</span><span class="sxs-lookup"><span data-stu-id="64b89-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="64b89-126">Ahora, use `dotnet pack` y el *.nupkg* resultante tendrá como destino tanto a .NET Standard 2.0 como .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="64b89-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="64b89-127">Este es el archivo *.csproj* que se genera con los pasos anteriores y el SDK de .NET Core 2.2.</span><span class="sxs-lookup"><span data-stu-id="64b89-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="64b89-128">Vea también</span><span class="sxs-lookup"><span data-stu-id="64b89-128">See also</span></span>

* [<span data-ttu-id="64b89-129">Cómo especificar plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="64b89-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="64b89-130">Destinatarios multiplataforma</span><span class="sxs-lookup"><span data-stu-id="64b89-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
