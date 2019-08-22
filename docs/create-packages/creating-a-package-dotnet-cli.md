---
title: Creación de un paquete NuGet con la CLI de dotnet
description: Un guía detallada sobre el proceso de diseño y creación de un paquete NuGet, incluidos puntos de decisión clave como archivos y control de versiones.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 40a42be91d3848db3e721a674e3fec4096fccd08
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69489022"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Creación de un paquete NuGet con la CLI de dotnet

Con independencia de lo que haga el paquete o lo que contenga el código, use una de las herramientas de CLI, ya sea `nuget.exe` o `dotnet.exe`, para empaquetar esa funcionalidad en un componente que se pueda compartir y usar por parte de otros desarrolladores. En este artículo se describe cómo crear un paquete con la CLI de dotnet. Para instalar la CLI de `dotnet`, consulte [Instalación de las herramientas del cliente NuGet](../install-nuget-client-tools.md). A partir de Visual Studio 2017, la CLI de dotnet se incluye con las cargas de trabajo de .NET Core.

Con los proyectos .NET Core y .NET Standard que usan el [formato de estilo SDK](../resources/check-project-format.md) y cualquier otro proyecto de estilo SDK, NuGet usa la información del archivo de proyecto directamente para crear un paquete. Para consultar tutoriales paso a paso, vea [Creación de paquetes de .NET Standard con la CLI de dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) o [Creación de paquetes de .NET Standard con Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack` es funcionalmente equivalente a `dotnet pack`. Para compilar con MSBuild, vea [Creación de un paquete de NuGet con MSBuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> Este tema se aplica a los proyectos de [estilo SDK](../resources/check-project-format.md), por lo general proyectos de .NET Core y .NET Standard.

## <a name="set-properties"></a>Establecimiento de las propiedades

Las propiedades siguientes se requieren para crear un paquete.

- `PackageId`, el identificador de paquete, que debe ser único en la galería que hospeda el paquete. Si no se especifica, el valor predeterminado es `AssemblyName`.
- `Version`, un número de versión específico con el formato *Principal.Secundaria.Revisión[-Sufijo]* donde *-Sufijo* identifica las [versiones preliminares](prerelease-packages.md). Si no se especifica, el valor predeterminado es 1.0.0.
- El título del paquete como debe aparecer en el host (por ejemplo, nuget.org)
- `Authors`, información del autor y el propietario. Si no se especifica, el valor predeterminado es `AssemblyName`.
- `Company`, el nombre de la empresa. Si no se especifica, el valor predeterminado es `AssemblyName`.

En Visual Studio, puede establecer estos valores en las propiedades del proyecto (haga clic con el botón derecho en el proyecto en el Explorador de soluciones, elija **Propiedades** y seleccione la pestaña **Paquete**). También puede establecer estas propiedades directamente en los archivos del proyecto (`.csproj`).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Asigne al paquete un identificador que sea único en nuget.org o en el origen de paquete que esté usando.

En el ejemplo siguiente se muestra un archivo del proyecto sencillo y completo que incluye estas propiedades. (Puede crear un nuevo proyecto predeterminado mediante el comando `dotnet new classlib`).

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

También puede establecer las propiedades opcionales, como `Title`, `PackageDescription` y `PackageTags`, tal como se describe en los [destinos de paquetes de MSBuild](../reference/msbuild-targets.md#pack-target), la sección [Controlar los recursos de dependencias](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) y [Propiedades de los metadatos de NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **PackageTags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.

Para obtener más información sobre cómo declarar dependencias y especificar números de versión, vea [Referencias del paquete en archivos del proyecto](../consume-packages/package-references-in-project-files.md) y [Control de versiones de paquetes](../concepts/package-versioning.md). También es posible exponer recursos directamente desde las dependencias en el paquete mediante los atributos `<IncludeAssets>` y `<ExcludeAssets>`. Para más información, consulte [Controlar los recursos de dependencias](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Elección de un identificador de paquete único y establecimiento del número de versión

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Ejecutar el comando pack

Para compilar un paquete NuGet (un archivo `.nupkg`) desde el proyecto, ejecute el comando `dotnet pack`, que también genera el proyecto automáticamente:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

El resultado mostrará la ruta de acceso al archivo `.nupkg`.

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Generación automática del paquete en la compilación

Para ejecutar automáticamente `dotnet pack` al ejecutar `dotnet build`, agregue la siguiente línea al archivo de proyecto en `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Cuando ejecute `dotnet pack` en una solución, se empaquetarán todos los proyectos de la solución que lo permitan (la propiedad [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) se establece en `true`).

> [!NOTE]
> Cuando genera automáticamente el paquete, el tiempo de empaquetado aumenta el tiempo de compilación del proyecto.

### <a name="test-package-installation"></a>Prueba de instalación del paquete

Antes de publicar un paquete, normalmente querrá probar el proceso de instalación de un paquete en un proyecto. Las pruebas aseguran que los archivos necesarios acaban en los lugares correctos en el proyecto.

Puede probar las instalaciones de forma manual en Visual Studio o en la línea de comandos mediante los [pasos de instalación de paquetes](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normales.

> [!IMPORTANT]
> Los paquetes son inmutables. Si corrige un problema, cambie el contenido del paquete y vuelva a empaquetar. Cuando vuelva a realizar la prueba, seguirá usando la versión anterior del paquete hasta que [bote la carpeta global de paquetes](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). Esto resulta especialmente relevante cuando se prueban paquetes que no usan una etiqueta preliminar única en cada compilación.

## <a name="next-steps"></a>Pasos siguientes

Una vez haya creado un paquete, que es un archivo `.nupkg`, puede publicarlo en la galería de su elección como se describe en [Publicación de un paquete](../nuget-org/publish-a-package.md).

Es posible que también quiera ampliar las funcionalidades del paquete o admitir otros escenarios, como se describe en los temas siguientes:

- [Control de versiones del paquete](../concepts/package-versioning.md)
- [Admitir varias plataformas de destino](../create-packages/multiple-target-frameworks-project-file.md)
- [Transformaciones de archivos de origen y configuración](../create-packages/source-and-config-file-transformations.md)
- [Localización](../create-packages/creating-localized-packages.md)
- [Versiones preliminares](../create-packages/prerelease-packages.md)
- [Definición del tipo de paquete](../create-packages/set-package-type.md)
- [Creación de paquetes con ensamblados de interoperabilidad COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Por último, hay tipos de paquete adicionales que tener en cuenta:

- [Paquetes nativos](../guides/native-packages.md)
- [Paquetes de símbolos](../create-packages/symbol-packages.md)
