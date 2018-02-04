---
title: pack y restore de NuGet como destinos de MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
keywords: "NuGet y MSBuild, destino del comando pack de NuGet, destino de restauración de NuGet"
ms.reviewer:
- karann-msft
ms.openlocfilehash: 6c488f49e12b014e7bd197d57041745387a4d7b4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>pack y restore de NuGet como destinos de MSBuild

*NuGet 4.0 y versiones posteriores*

Con el formato PackageReference, NuGet 4.0 + puede almacenar metadatos de todos los manifiestos directamente dentro de un archivo de proyecto, en lugar de usar una `.nuspec` archivo.

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

Cuando se usa el módulo de destino, es decir, `msbuild /t:pack`, MSBuild dibuja sus entradas del archivo de proyecto. En la tabla siguiente se describe las propiedades de MSBuild que se pueden agregar a un archivo de proyecto dentro de la primera `<PropertyGroup>` nodo. Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual. Para mayor comodidad, la tabla se organiza por la propiedad equivalente en un [archivo `.nuspec`](../reference/nuspec.md).

Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.

| Valor de atributo/NuSpec | Propiedad de MSBuild | Default | Notas |
|--------|--------|--------|--------|
| Id. | PackageId | AssemblyName | $(NombreDeEnsamblado) de MSBuild |
| Versión | PackageVersion | Versión | Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | vacío | Establecer PackageVersion sobrescribe PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | vacío | $(VersionSuffix) de MSBuild. Establecer PackageVersion sobrescribe PackageVersionSuffix |
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
| RepositoryUrl | RepositoryUrl | vacío | |
| RepositoryType | RepositoryType | vacío | |
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

Como parte del cambio para el [Problema 2582 de NuGet](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` se cambiará en última instancia por `PackageIconUri` y puede ser una ruta de acceso relativa a un archivo de icono que se incluirá en la raíz del paquete resultante.

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
> Además de elementos de contenido, el `<Pack>` y `<PackagePath>` metadatos también pueden establecerse en los archivos con una acción de compilación de compilación, EmbeddedResource, ApplicationDefinition, página, recursos, pantalla de presentación, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o ninguno.
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

Puede usar un archivo `.nuspec` para empaquetar el proyecto siempre que tenga un archivo de proyecto para importar `NuGet.Build.Tasks.Pack.targets` para que la tarea de empaquetado se pueda ejecutar. Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:

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

## <a name="restore-target"></a>Destino de restore

`MSBuild /t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:

1. Leer todas las referencias entre proyectos
1. Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias
1. Pasar datos de MSBuild a NuGet.Build.Tasks.dll
1. Ejecutar la restauración
1. Descargar los paquetes
1. Escribir el archivo de activos, destinos y propiedades

### <a name="restore-properties"></a>Restaurar las propiedades

Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto. También se pueden establecer valores desde la línea de comandos mediante el modificador `/p:` (vea los ejemplos siguientes).

| Property | Descripción |
|--------|--------|
| RestoreSources | Lista delimitada por punto y coma de orígenes de paquetes. |
| RestorePackagesPath | Ruta de acceso de la carpeta de paquetes de usuario. |
| RestoreDisableParallel | Limitar las descargas a una cada vez. |
| RestoreConfigFile | Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar. |
| RestoreNoCache | Si es true, evita el uso de la caché web. |
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
<PropertyGroup>
```

### <a name="restore-outputs"></a>Restaurar salidas

La restauración crea los archivos siguientes en la carpeta `obj` de compilación:

| Archivo | Descripción |
|--------|--------|
| `project.assets.json` | Anteriormente `project.lock.json` |
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
