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
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Compatibilidad con varias versiones de .NET Framework en el archivo del proyecto

Cuando cree un proyecto por primera vez, le recomendamos crear una biblioteca de clases de .NET Standard, puesto que proporciona compatibilidad con la variedad más amplia de proyectos de consumo. Al usar .NET Standard, agrega [compatibilidad multiplataforma](/dotnet/standard/library-guidance/cross-platform-targeting) a una biblioteca de .NET de manera predeterminado. Sin embargo, en algunos escenarios, es posible que también tenga que incluir código que tenga como destino un marco determinado. En este artículo se muestra cómo hacerlo para proyectos de [estilo SDK](../resources/check-project-format.md).

En el caso de los proyectos de estilo SDK, puede configurar la compatibilidad con varios marcos de destino ([TFM](/dotnet/standard/frameworks)) en el archivo del proyecto y, luego, usar `dotnet pack` o `msbuild /t:pack` para crear el paquete.

> [!NOTE]
> La CLI de nuget.exe no permite empaquetar los proyectos de estilo SDK, por lo que solo debe usar `dotnet pack` o `msbuild /t:pack`. En su lugar, se recomienda [incluir todas las propiedades](../reference/msbuild-targets.md#pack-target) que usualmente están en el archivo `.nuspec`. Para tener como destino varias versiones de .NET Framework en un proyecto que no es de estilo SDK, consulte [Compatibilidad con varias versiones de .NET Framework](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Creación de un proyecto que admite varias versiones de .NET Framework

1. Cree una biblioteca de clases .NET Standard en Visual Studio o use `dotnet new classlib`.

   Para una mayor compatibilidad, se recomienda crear una biblioteca de clases .NET Standard.

2. Edite el archivo *.csproj* para admitir los marcos de destino. Por ejemplo, cambie
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   a:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   Asegúrese de cambiar el elemento XML modificado de singular a plural (agregue "s" a las etiquetas de apertura y cierre).

3. Si tiene algún código que solo funciona en un TFM, puede usar `#if NET45` o `#if NETSTANDARD2_0` para separar el código que depende de TFM. (Para más información, consulte [Cómo lograr la compatibilidad con múltiples versiones](/dotnet/core/tutorials/libraries#how-to-multitarget)). Por ejemplo, puede usar este código:

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

4. Agregue los metadatos de NuGet que quiera a *.csproj* como propiedades de MSBuild.

   Para ver la lista de metadatos de paquetes disponibles y los nombres de las propiedades de MSBuild, consulte [pack target](../reference/msbuild-targets.md#pack-target). Consulte también [Controlar los recursos de dependencias](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Si quiere separar las propiedades relacionadas con la compilación de los metadatos de NuGet, puede usar un `PropertyGroup` distinto o poner las propiedades de NuGet en otro archivo y usar la directiva `Import` de MSBuild para incluirlo. `Directory.Build.Props` y `Directory.Build.Targets` también son compatibles a partir de MSBuild 15.0.

5. Ahora, use `dotnet pack` y el *.nupkg* resultante tendrá como destino tanto a .NET Standard 2.0 como .NET Framework 4.5.

Este es el archivo *.csproj* que se genera con los pasos anteriores y el SDK de .NET Core 2.2.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Vea también

* [Cómo especificar plataformas de destino](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Destinatarios multiplataforma](/dotnet/standard/library-guidance/cross-platform-targeting)
