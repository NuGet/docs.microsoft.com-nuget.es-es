---
title: Creación de un paquete NuGet con MSBuild
description: Un guía detallada sobre el proceso de diseño y creación de un paquete NuGet, incluidos puntos de decisión clave como archivos y control de versiones.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: a965a3049f46af59efcfad2ecf19e0923fda413b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488951"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Creación de un paquete NuGet con MSBuild

Cuando crea un paquete NuGet a partir del código, empaqueta la funcionalidad en un componente que se pueda compartir con otros desarrolladores, así como que estos puedan usarlo. En este artículo se describe cómo crear un paquete con MSBuild. MSBuild viene preinstalado con cada carga de trabajo de Visual Studio que incluya NuGet. Además, también puede usar MSBuild mediante la CLI de dotnet con [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild).

Con los proyectos .NET Core y .NET Standard que usan el [formato de estilo SDK](../resources/check-project-format.md) y cualquier otro proyecto de estilo SDK, NuGet usa la información del archivo de proyecto directamente para crear un paquete.  En el caso de un proyecto sin SDK que use `<PackageReference>`, NuGet también usará el archivo del proyecto para crear un paquete.

Los proyectos con SDK tienen la funcionalidad de paquetes disponible de forma predeterminada. En el caso de los proyectos PackageReference sin SDK, deberá agregar el paquete NuGet.Build.Tasks.Pack a las dependencias del proyecto. Para obtener información detallada sobre los destinos de paquete de MSBuild, vea [pack y restore de NuGet como destinos de MSBuild](../reference/msbuild-targets.md).

El comando que crea un paquete, `msbuild -t:pack`, es equivalente funcionalmente a `dotnet pack`.

> [!IMPORTANT]
> Este tema se aplica a los proyectos [con SDK](../resources/check-project-format.md), que suelen ser proyectos de .NET Core y .NET Standard, así como a los paquetes sin SDK que usan PackageReference.

## <a name="set-properties"></a>Establecimiento de las propiedades

Las propiedades siguientes se requieren para crear un paquete.

- `PackageId`, el identificador de paquete, que debe ser único en la galería que hospeda el paquete. Si no se especifica, el valor predeterminado es `AssemblyName`.
- `Version`, un número de versión específico con el formato *Principal.Secundaria.Revisión[-Sufijo]* donde *-Sufijo* identifica las [versiones preliminares](prerelease-packages.md). Si no se especifica, el valor predeterminado es 1.0.0.
- El título del paquete como debe aparecer en el host (por ejemplo, nuget.org)
- `Authors`, información del autor y el propietario. Si no se especifica, el valor predeterminado es `AssemblyName`.
- `Company`, el nombre de la empresa. Si no se especifica, el valor predeterminado es `AssemblyName`.

En Visual Studio, puede establecer estos valores en las propiedades del proyecto (haga clic con el botón derecho en el proyecto en el Explorador de soluciones, elija **Propiedades** y seleccione la pestaña **Paquete**). También puede establecer estas propiedades directamente en los archivos del proyecto ( *.csproj*).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Asigne al paquete un identificador que sea único en nuget.org o en el origen de paquete que esté usando.

En el ejemplo siguiente se muestra un archivo del proyecto sencillo y completo que incluye estas propiedades.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
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

## <a name="add-the-nugetbuildtaskspack-package"></a>Adición del paquete NuGet.Build.Tasks.Pack

Si usa MSBuild con un proyecto sin SDK y PackageReference, agregue el paquete NuGet.Build.Tasks.Pack al proyecto.

1. Abra el archivo del proyecto y agregue lo siguiente tras el elemento `<PropertyGroup>`:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Abra un símbolo del sistema para desarrolladores (en el cuadro **Búsqueda**, escriba **Símbolo del sistema para desarrolladores**).

   Normalmente, es preferible iniciar el símbolo del sistema para desarrolladores de Visual Studio en el menú **Inicio**, ya que se configurará con todas las rutas de acceso necesarias para MSBuild.

3. Cambie a la carpeta que contiene el archivo del proyecto y escriba el siguiente comando para instalar el paquete NuGet.Build.Tasks.Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Asegúrese de que la salida de MSBuild indica que la compilación se ha completado correctamente.

## <a name="run-the-msbuild--tpack-command"></a>Ejecución del comando msbuild -t:pack

Para compilar un paquete NuGet (un archivo `.nupkg`) desde el proyecto, ejecute el comando `msbuild -t:pack`, que también genera el proyecto automáticamente:

En el símbolo del sistema para desarrolladores de Visual Studio, escriba el comando siguiente:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

El resultado mostrará la ruta de acceso al archivo `.nupkg`.

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>Generación automática del paquete en la compilación

Para ejecutar automáticamente `msbuild -t:pack` al compilar o restaurar el proyecto, agregue la siguiente línea al archivo del proyecto en `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Cuando ejecuta `msbuild -t:pack` en una solución, se empaquetan todos los proyectos de la solución que se pueden empaquetar (la propiedad [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) se establece en `true`).

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

- [Empaquetado y restauración de NuGet como destinos de MSBuild](../reference/msbuild-targets.md)
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
