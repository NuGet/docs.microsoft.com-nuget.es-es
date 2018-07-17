---
title: pack y restore de NuGet como destinos de MSBuild
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0e7e0952519afdcb4b50f31d33cce2a92e3579b4
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39069705"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>pack y restore de NuGet como destinos de MSBuild

*NuGet 4.0 y versiones posteriores*

Con el formato PackageReference, NuGet 4.0 + puede almacenar los metadatos de todos los manifiestos directamente en un archivo de proyecto, en lugar de usar un archivo `.nuspec` aparte.

Con MSBuild 15.1 y versiones posteriores, NuGet es también un ciudadano de MSBuild de primera clase con los destinos `pack` y `restore` como se describe a continuación. Estos destinos permiten trabajar con NuGet como lo haría con cualquier otra tarea o destino de MSBuild. (Para NuGet 3.x y versiones anteriores, los comandos [pack](../tools/cli-ref-pack.md) y [restore](../tools/cli-ref-restore.md) se usan a través de la CLI de NuGet en su lugar).

## <a name="target-build-order"></a>Orden de compilación de destinos

Dado que `pack` y `restore` son destinos de MSBuild, puede tener acceso a ellos para mejorar el flujo de trabajo. Por ejemplo, supongamos que quiere copiar el paquete en un recurso compartido de red después de empaquetarlo. Puede hacer esto si agrega lo siguiente al archivo de proyecto:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

De forma similar, puede escribir una tarea de MSBuild, su propio destino y usar propiedades de NuGet en la tarea de MSBuild.

## <a name="pack-target"></a>Destino de pack

Para los proyectos de .NET Standard con el formato PackageReference, utilizando `msbuild /t:pack` dibuja las entradas del archivo de proyecto debe utilizar para crear un paquete de NuGet.

En la tabla siguiente se describen las propiedades de MSBuild que se pueden agregar a un archivo de proyecto en el primer nodo `<PropertyGroup>`. Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual. Para mayor comodidad, la tabla se organiza por la propiedad equivalente en un [archivo `.nuspec`](../reference/nuspec.md).

Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.

| Valor de atributo/NuSpec | Propiedad de MSBuild | Default | Notas |
|--------|--------|--------|--------|
| Id. | PackageId | AssemblyName | $(NombreDeEnsamblado) de MSBuild |
| Versión | PackageVersion | Versión | Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | vacío | Al establecer PackageVersion se sobrescribe PackageVersionPrefix. |
| VersionSuffix | PackageVersionSuffix | vacío | $(VersionSuffix) de MSBuild. Al establecer PackageVersion se sobrescribe PackageVersionSuffix. |
| Authors | Authors | Nombre del usuario actual | |
| Owners | N/D | No está presente en el archivo NuSpec | |
| Title | Title | El identificador de paquete| |
| Descripción | Descripción | "Descripción del paquete" | |
| Copyright | Copyright | vacío | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| LicenseUrl | PackageLicenseUrl | vacío | |
| ProjectUrl | PackageProjectUrl | vacío | |
| IconUrl | PackageIconUrl | vacío | |
| Etiquetas | PackageTags | vacío | Las etiquetas están delimitadas mediante punto y coma. |
| ReleaseNotes | PackageReleaseNotes | vacío | |
| Url del repositorio | RepositoryUrl | vacío | Dirección URL del repositorio utilizado para clonar o recuperar el código fuente. Ejemplo: *https://github.com/NuGet/NuGet.Client.git* |
| / Tipo de repositorio | RepositoryType | vacío | Tipo de repositorio. Ejemplos: *git*, *tfs*. |
| Rama del repositorio | RepositoryBranch | vacío | Información de rama del repositorio opcional. *RepositoryUrl* también debe especificarse para que se incluye esta propiedad. Ejemplo: *maestro* (NuGet 4.7.0+) |
| Repositorio/confirmación | RepositoryCommit | vacío | Confirmación del repositorio opcional o conjunto de cambios para indicar que el paquete de origen se compiló. *RepositoryUrl* también debe especificarse para que se incluye esta propiedad. Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Resumen | No compatibles | | |

### <a name="pack-target-inputs"></a>Entradas de destino de pack

- IsPackable
- PackageVersion
- PackageId
- Authors
- Descripción
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- RepositoryBranch
- RepositoryCommit
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>Escenarios de pack

### <a name="packageiconurl"></a>PackageIconUrl

Como parte del cambio para [NuGet problema 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` se cambiará a `PackageIconUri` y puede ser una ruta de acceso relativa a un archivo de icono que se incluirá en la raíz del paquete resultante.

### <a name="output-assemblies"></a>Ensamblados de salida

`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`. Los archivos de salida que se copian dependen de lo que proporciona MSBuild desde el destino `BuiltOutputProjectGroup`.

Hay dos propiedades de MSBuild que se pueden usar en el archivo de proyecto o la línea de comandos para controlar dónde van los ensamblados de salida:

- `IncludeBuildOutput`: un valor booleano que determina si los ensamblados de salida de compilación deben incluirse en el paquete.
- `BuildOutputTargetFolder`: especifica la carpeta en la que se deben colocar los ensamblados de salida. Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.

### <a name="package-references"></a>Referencias de paquete

Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Referencias entre proyectos

Las referencias entre proyectos se consideran de forma predeterminada como referencias de paquetes NuGet, por ejemplo:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

También puede agregar los metadatos siguientes a la referencia de proyecto:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Inclusión de contenido en un paquete

Para incluir contenido, agregue metadatos adicionales al elemento `<Content>` existente. De forma predeterminada todos los elementos de tipo "Content" se incluyen en el paquete a menos que los reemplace con entradas como la siguiente:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

De forma predeterminada, todo el contenido se agrega a la raíz de la carpeta `content` y `contentFiles\any\<target_framework>` dentro de un paquete y se conserva la estructura de carpetas relativa, a menos que se especifique una ruta de acceso de paquete:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Si quiere copiar todo el contenido a una carpeta raíz determinada (en lugar de `content` y `contentFiles`), puede usar la propiedad `ContentTargetFolders` de MSBuild, cuyo valor predeterminado es "content;contentFiles", pero que se puede establecer en cualquier otro nombre de carpeta. Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.

`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma. Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete. Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

También hay una propiedad `$(IncludeContentInPack)` de MSBuild, cuyo valor predeterminado es `true`. Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.

Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen ```<PackageCopyToOutput>``` y ```<PackageFlatten>```, que establece los valores ```CopyToOutput``` y ```Flatten``` en la entrada ```contentFiles``` del archivo nuspec de salida.

> [!Note]
> Además de los elementos Content, los metadatos `<Pack>` y `<PackagePath>` también se pueden establecer en archivos con una acción de compilación Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.
>
> Para que el comando pack anexe el nombre de archivo a la ruta de acceso del paquete cuando se usan patrones globales, la ruta de acceso del paquete debe terminar con el carácter separador de carpeta; en caso contrario, la ruta de acceso del paquete se trata como la ruta de acceso completa, incluido el nombre de archivo.

### <a name="includesymbols"></a>IncludeSymbols

Cuando se usa `MSBuild /t:pack /p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.

### <a name="includesource"></a>IncludeSource

Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`. Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante. Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.

Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.

### <a name="istool"></a>IsTool

Cuando se usa `MSBuild /t:pack /p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`. Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.

### <a name="packing-using-a-nuspec"></a>Empaquetado mediante un archivo .nuspec

Puede usar un `.nuspec` archivo para empaquetar el proyecto siempre que tenga un archivo de proyecto SDK para importar `NuGet.Build.Tasks.Pack.targets` para que se puede ejecutar la tarea de empaquetado. Deberá restaurar el proyecto antes de que puede empaquetar un archivo nuspec. La plataforma de destino del archivo del proyecto es irrelevante y no se utiliza cuando se empaqueta un nuspec. Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:

1. `NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.
1. `NuspecProperties`: lista de pares clave=valor separados por punto y coma. Debido al funcionamiento del análisis de línea de comandos de MSBuild, se deben especificar varias propiedades como se indica a continuación: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: ruta de acceso base para el archivo `.nuspec`.

Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

Tenga en cuenta que el empaquetado nuspec además utilizando dotnet.exe o msbuild conduce a compilar el proyecto de forma predeterminada. Esto puede evitarse pasando ```--no-build``` dotnet.exe, que es el equivalente del valor de propiedad ```<NoBuild>true</NoBuild> ``` en el archivo de proyecto, junto con la opción ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` en el archivo de proyecto

Un ejemplo de un archivo csproj para empaquetar un archivo nuspec es:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Avanzada de puntos de extensión para crear el paquete personalizado

El `pack` destino proporciona dos puntos de extensión que se ejecutan en la compilación interna, de específica de framework de destino. Se admiten los puntos de extensión como contenido específico de framework de destino y los ensamblados en un paquete:

- `TargetsForTfmSpecificBuildOutput` destino: uso para los archivos en el `lib` carpeta o una carpeta especificada utilizando `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` destino: uso de archivos fuera de la `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Escribir un destino personalizado y lo especifica como el valor de la `$(TargetsForTfmSpecificBuildOutput)` propiedad. Para los archivos que deben entrar en el `BuildOutputTargetFolder` (lib de forma predeterminada), el destino debe escribir esos archivos en el elemento ItemGroup `BuildOutputInPackage` y establecer los dos valores de metadatos siguientes:

- `FinalOutputPath`: La ruta de acceso absoluta del archivo; Si no se proporciona, la identidad se utiliza para evaluar la ruta de acceso de origen.
- `TargetPath`: (Opcional) establecer cuando el archivo debe ir en una subcarpeta dentro de `lib\<TargetFramework>` , como ensamblados satélite que van en sus carpetas respectivas de referencia cultural. El valor predeterminado es el nombre del archivo.

Ejemplo:

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

Escribir un destino personalizado y lo especifica como el valor de la `$(TargetsForTfmSpecificContentInPackage)` propiedad. Para que los archivos que se incluyen en el paquete, el destino debe escribir esos archivos en el elemento ItemGroup `TfmSpecificPackageFile` y establezca los siguientes metadatos opcionales:

- `PackagePath`: Ruta de acceso donde el archivo debe ser la salida en el paquete. NuGet emite una advertencia si se agrega más de un archivo a la misma ruta de acceso del paquete.
- `BuildAction`: La acción de compilación para asignar al archivo, solo es necesario si la ruta de acceso del paquete está en el `contentFiles` carpeta. El valor predeterminado es "None".

Por ejemplo:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>Destino de restore

`MSBuild /t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:

1. Leer todas las referencias entre proyectos
1. Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias
1. Pasar datos de MSBuild a NuGet.Build.Tasks.dll
1. Ejecutar la restauración
1. Descargar los paquetes
1. Escribir el archivo de activos, destinos y propiedades

El `restore` destino funciona **sólo** para proyectos con el formato PackageReference. Lo hace **no** profesional de proyectos que usan el `packages.config` dar formato; use [restauración de nuget](../tools/cli-ref-restore.md) en su lugar.

### <a name="restore-properties"></a>Restaurar las propiedades

Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto. También se pueden establecer valores desde la línea de comandos mediante el modificador `/p:` (vea los ejemplos siguientes).

| Property | Descripción |
|--------|--------|
| RestoreSources | Lista delimitada por punto y coma de orígenes de paquetes. |
| RestorePackagesPath | Ruta de acceso de la carpeta de paquetes de usuario. |
| RestoreDisableParallel | Limitar las descargas a una cada vez. |
| RestoreConfigFile | Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar. |
| RestoreNoCache | Si es true, evita el uso de paquetes almacenados en caché. Consulte [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Si es true, ignora los orígenes de paquetes que producen errores o faltan. |
| RestoreTaskAssemblyFile | Ruta de acceso a `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas. |
| RestoreOutputPath | Carpeta de salida, que de forma predeterminada es `obj`. |

#### <a name="examples"></a>Ejemplos

Línea de comandos:

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

Archivo del proyecto:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Restaurar salidas

La restauración crea los archivos siguientes en la carpeta `obj` de compilación:

| Archivo | Descripción |
|--------|--------|
| `project.assets.json` | Contiene el gráfico de dependencias de todas las referencias de paquete. |
| `{projectName}.projectFileExtension.nuget.g.props` | Referencias a propiedades de MSBuild incluidas en paquetes |
| `{projectName}.projectFileExtension.nuget.g.targets` | Referencias a destinos de MSBuild incluidos en paquetes |

### <a name="packagetargetfallback"></a>PackageTargetFallback

El elemento `PackageTargetFallback` permite especificar un conjunto de destinos compatibles que se usarán al restaurar los paquetes. Está diseñado para permitir que los paquetes que usan un [TxM](../reference/target-frameworks.md) de dotnet funcionen con paquetes compatibles que no declaran un TxM de dotnet. Es decir, si el proyecto usa el TxM de dotnet, todos los paquetes de los que depende también deben tener un TxM de dotnet, a menos que agregue `<PackageTargetFallback>` al proyecto para permitir que las plataformas que no sean de dotnet sean compatibles con dotnet.

Por ejemplo, si el proyecto usa el TxM `netstandard1.6` y un paquete dependiente solo contiene `lib/net45/a.dll` y `lib/portable-net45+win81/a.dll`, se producirá un error al compilar el proyecto. Si lo que quiere incluir es el último archivo DLL, puede agregar `PackageTargetFallback` como se indica a continuación para indicar que el archivo DLL `portable-net45+win81` es compatible:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Para declarar una reserva para todos los destinos del proyecto, excluya el atributo `Condition`. También puede extender cualquier `PackageTargetFallback` existente mediante la inclusión de `$(PackageTargetFallback)` como se muestra aquí:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Reemplazo de una biblioteca desde un gráfico de restauración

Si una restauración agrega el ensamblado equivocado, se puede excluir la opción predeterminada de ese paquete y reemplazarla por una de su propia elección. En primer lugar, con una `PackageReference` de nivel superior, excluya todos los activos:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Después, agregue su propia referencia a la copia local correspondiente del archivo DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
