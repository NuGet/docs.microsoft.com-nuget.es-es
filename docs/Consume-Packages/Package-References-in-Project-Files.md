---
title: PackageReference de NuGet en archivos de proyecto de Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0+ y VS2017"
keywords: Dependencias de paquetes de NuGet, referencias de paquetes, archivos de proyecto, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a>Referencias del paquete (PackageReference) en archivos de proyecto

Las referencias de paquetes, mediante el nodo `PackageReference`, le permiten administrar las dependencias de NuGet directamente dentro de los archivos de proyecto, en lugar de necesitar un archivo `packages.config` o `project.json` independiente. Este método no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.Config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en [Configuración del comportamiento de NuGet](Configuring-NuGet-Behavior.md).

> [!Important]
> Actualmente, las referencias de paquetes solo se admiten en Visual Studio 2017 para los proyectos de .NET Core, .NET Standard y UWP que tengan como destino Windows 10 Build 15063 (Creators Update).

El enfoque `PackageReference` le permite usar condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras agrupaciones. También le proporciona un control específico sobre las dependencias y el flujo de contenido. En términos de comportamiento y de [resolución de dependencias](Dependency-Resolution.md), es lo mismo que usar `project.json`.

Para más información sobre la integración de MSBuild con referencias de paquetes en los archivos de proyecto, vea [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md).

## <a name="adding-a-packagereference"></a>Agregar una PackageReference

Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Controlar la versión de una dependencia

La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config` o `project.json`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).

## <a name="floating-versions"></a>Versiones flotantes

Las [versiones flotantes](../consume-packages/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Controlar los recursos de dependencias

Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete. En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Las siguientes etiquetas de metadatos controlan los recursos de dependencia:

| Etiqueta | Description | Valor predeterminado |
| --- | --- | --- |
| IncludeAssets | Se consumirán estos recursos | todo |
| ExcludeAssets | No se consumirán estos recursos | ninguna | 
| PrivateAssets | Estos recursos se consumirán, pero no irán al proyecto principal | archivos de contenido; analizadores; compilación |


A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:

| Valor | Description |
| --- | ---
| compile | Contenido de la carpeta `lib` |
| motor en tiempo de ejecución | Contenido de la carpeta `runtime` |
| contentFiles | Contenido de la carpeta `contentfiles` |
| compilación | Propiedades y destinos de la carpeta `build` |
| analyzers | Analizadores de .NET |
| nativas | Contenido de la carpeta `native` |
| ninguna | No se usa ninguno de los anteriores. |
| todo | Todo lo anterior (excepto `none`) |

En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal. Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger. AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.

## <a name="adding-a-packagereference-condition"></a>Agregar una condición PackageReference

Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades. Pero actualmente solo se admite la variable `TargetFramework`.

Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`. En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria. Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

Un paquete creado con este proyecto mostrará que Newtonsoft.json se incluye como dependencia únicamente para un destino `net452`:

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
