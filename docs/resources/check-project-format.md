---
title: Identificación del formato del proyecto
description: En este artículo se describe cómo identificar el formato del proyecto.
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488478"
---
# <a name="identify-the-project-format"></a>Identificación del formato del proyecto

NuGet funciona con todos los proyectos de .NET. Sin embargo, el formato de proyecto (del estilo de SDK o sin el estilo de SDK) determina algunas de las herramientas y los métodos que se deben usar para consumir y crear paquetes NuGet. Los proyectos del estilo de SDK usan el [atributo de SDK](/dotnet/core/tools/csproj#additions). Es importante identificar el tipo de proyecto, ya que los métodos y las herramientas que se usan para consumir y crear paquetes NuGet dependen del formato de proyecto. En el caso de los proyectos que no son del estilo de SDK, los métodos y las herramientas también dependen de si el proyecto se ha migrado al formato `PackageReference`.

El hecho de que el proyecto sea del estilo de SDK o no depende del método que se ha usado para crearlo. En la tabla siguiente se muestra el formato de proyecto predeterminado y la herramienta de la CLI asociada para el proyecto cuando se crea con Visual Studio 2017 y versiones posteriores.

| Proyecto&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Formato de proyecto predeterminado | Herramienta de la CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Notas |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | Estilo de SDK | [CLI de dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Los proyectos creados antes de Visual Studio 2017 no son del estilo de SDK. Use la CLI de `nuget.exe`. |
| .NET Core | Estilo de SDK | [CLI de dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Los proyectos creados antes de Visual Studio 2017 no son del estilo de SDK. Use la CLI de `nuget.exe`. |
| .NET Framework | Estilo no de SDK | [CLI de nuget.exe](../install-nuget-client-tools.md#nugetexe-cli) | Los proyectos de .NET Framework creados con otros métodos pueden ser del estilo de SDK. En su lugar, use la [CLI de dotnet](../install-nuget-client-tools.md#dotnetexe-cli) para estos. |
| Proyecto .NET [migrado](../consume-packages/migrate-packages-config-to-package-reference.md) | Estilo no de SDK| Para crear paquetes, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration). | Para crear paquetes, se recomienda `msbuild -t:pack`. También puede usar la [CLI de dotnet](../install-nuget-client-tools.md#dotnetexe-cli). Los proyectos migrados no son proyectos del estilo de SDK. |

## <a name="check-the-project-format"></a>Comprobación del formato de proyecto

Si no está seguro de si el proyecto tiene un formato del estilo de SDK o no, busque el atributo de SDK en el elemento `<Project>` del archivo de proyecto (para C#, es el archivo *. csproj). Si existe, el proyecto es del estilo de SDK.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Comprobación del formato de proyecto en Visual Studio

Si trabaja en Visual Studio, puede comprobar rápidamente el formato del proyecto con uno de los métodos siguientes:

- En el Explorador de soluciones haga clic con el botón derecho en el proyecto y seleccione **Editar myprojectname.csproj**.

   Esta opción solo está disponible a partir de Visual Studio 2017 para proyectos que usan el atributo de estilo SDK. También puede usar el otro método.

   ![Edición del archivo del proyecto](media/edit-project-file.png)

   Un proyecto del estilo de SDK muestra el [atributo de SDK](/dotnet/core/tools/csproj#additions) en el archivo del proyecto.
   
- En el menú **Proyecto**, elija **Descargar proyecto**, o bien haga clic con el botón derecho en el proyecto y elija **Descargar proyecto**.

   Este proyecto no incluirá el atributo de SDK en el archivo del proyecto. No es un proyecto del estilo de SDK.

   ![Descarga del proyecto](media/unload-project.png)

   Después, haga clic con el botón derecho en el proyecto descargado y elija **Editar myprojectname.csproj**.

## <a name="see-also"></a>Consulte también

- [Creación de paquetes de .NET Standard con la CLI de dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Creación de paquetes de .NET Standard con Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Creación y publicación de un paquete de .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [Empaquetado y restauración de NuGet como destinos de MSBuild](../reference/msbuild-targets.md)
