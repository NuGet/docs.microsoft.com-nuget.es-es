---
title: pack y restore de NuGet como destinos de MSBuild
description: pack y restore de NuGet pueden trabajar directamente como destinos de MSBuild con NuGet 4.0 y versiones posteriores.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235703"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>pack y restore de NuGet como destinos de MSBuild

*NuGet 4.0 y versiones posteriores*

Con el formato [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + puede almacenar todos los metadatos del manifiesto directamente dentro de un archivo de proyecto en lugar de usar un `.nuspec` archivo independiente.

Con MSBuild 15.1 y versiones posteriores, NuGet es también un ciudadano de MSBuild de primera clase con los destinos `pack` y `restore` como se describe a continuación. Estos destinos permiten trabajar con NuGet como lo haría con cualquier otra tarea o destino de MSBuild. Para obtener instrucciones sobre cómo crear un paquete NuGet con MSBuild, consulte [crear un paquete Nuget con MSBuild](../create-packages/creating-a-package-msbuild.md). (Para NuGet 3.x y versiones anteriores, los comandos [pack](../reference/cli-reference/cli-ref-pack.md) y [restore](../reference/cli-reference/cli-ref-restore.md) se usan a través de la CLI de NuGet en su lugar).

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

> [!NOTE]
> `$(OutputPath)` es relativo y espera que se ejecute el comando desde la raíz del proyecto.

## <a name="pack-target"></a>Destino de pack

En el caso de los proyectos de .NET Standard con el formato PackageReference, el uso de `msbuild -t:pack` dibuja entradas del archivo de proyecto para usarlas en la creación de un paquete NuGet.

En la tabla siguiente se describen las propiedades de MSBuild que se pueden agregar a un archivo de proyecto en el primer nodo `<PropertyGroup>`. Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual. Para mayor comodidad, la tabla está organizada por la propiedad equivalente en un [ `.nuspec` archivo](../reference/nuspec.md).

Tenga en cuenta que las propiedades `Owners` y `Summary` de `.nuspec` no son compatibles con MSBuild.

| Valor de atributo/NuSpec | Propiedad de MSBuild | Valor predeterminado | Notas |
|--------|--------|--------|--------|
| Identificador | PackageId | AssemblyName | $(NombreDeEnsamblado) de MSBuild |
| Versión | PackageVersion | Versión | Esto es compatible con semver, por ejemplo, "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | Al establecer PackageVersion se sobrescribe PackageVersionPrefix. |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) de MSBuild. Al establecer PackageVersion se sobrescribe PackageVersionSuffix. |
| Authors | Authors | Nombre del usuario actual | |
| Propietarios | N/A | No está presente en el archivo NuSpec | |
| Título | Título | El identificador de paquete| |
| Descripción | Descripción | "Descripción del paquete" | |
| Copyright | Copyright | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| license | PackageLicenseExpression | empty | Se corresponde con `<license type="expression">` |
| license | PackageLicenseFile | empty | Se corresponde con `<license type="file">`. Debe empaquetar explícitamente el archivo de licencia al que se hace referencia. |
| LicenseUrl | PackageLicenseUrl | empty | `PackageLicenseUrl` está en desuso, use la propiedad PackageLicenseExpression o PackageLicenseFile |
| ProjectUrl | PackageProjectUrl | empty | |
| Iconos | PackageIcon | empty | Debe empaquetar explícitamente el archivo de imagen de icono al que se hace referencia.|
| IconUrl | PackageIconUrl | empty | Para la mejor experiencia de nivel inferior, `PackageIconUrl` debe especificarse además de `PackageIcon` . A largo plazo, estará en `PackageIconUrl` desuso. |
| Etiquetas | PackageTags | empty | Las etiquetas están delimitadas mediante punto y coma. |
| ReleaseNotes | PackageReleaseNotes | empty | |
| Repositorio/dirección URL | RepositoryUrl | empty | Dirección URL del repositorio usada para clonar o recuperar el código fuente. Ejemplo *https://github.com/NuGet/NuGet.Client.git* |
| Repositorio/tipo | RepositoryType | empty | Tipo de repositorio. Ejemplos: *git*, *TFS*. |
| Repositorio/rama | RepositoryBranch | empty | Información opcional de la rama del repositorio. También se debe especificar *RepositoryUrl* para que se incluya esta propiedad. Ejemplo: *maestra* (NuGet 4.7.0 +) |
| Repositorio/confirmar | RepositoryCommit | empty | Confirmación o conjunto de cambios opcionales de repositorio para indicar en qué origen se ha compilado el paquete. También se debe especificar *RepositoryUrl* para que se incluya esta propiedad. Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Resumen | No compatible | | |

### <a name="pack-target-inputs"></a>Entradas de destino de pack

- IsPackable
- SuppressDependenciesWhenPacking
- PackageVersion
- PackageId
- Authors
- Descripción
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
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

### <a name="suppress-dependencies"></a>Suprimir dependencias

Para suprimir las dependencias de paquete del paquete NuGet generado, establezca `SuppressDependenciesWhenPacking` en, `true` lo que permitirá omitir todas las dependencias del archivo nupkg generado.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl` quedará en desuso en favor de la nueva [`PackageIcon`](#packageicon) propiedad.

A partir de NuGet 5,3 & Visual Studio 2019 versión 16,3, `pack` se generará una advertencia [NU5048](./errors-and-warnings/nu5048.md) si los metadatos del paquete solo especifican `PackageIconUrl` .

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> Debe especificar `PackageIcon` y `PackageIconUrl` para mantener la compatibilidad con versiones anteriores de clientes y orígenes que aún no admiten `PackageIcon` . Visual Studio será compatible con los `PackageIcon` paquetes procedentes de un origen basado en carpetas en una versión futura.

#### <a name="packing-an-icon-image-file"></a>Empaquetar un archivo de imagen de icono

Al empaquetar un archivo de imagen de icono, debe usar `PackageIcon` la propiedad para especificar la ruta de acceso del paquete, relativa a la raíz del paquete. Además, debe asegurarse de que el archivo está incluido en el paquete. El tamaño del archivo de imagen está limitado a 1 MB. Entre los formatos de archivo admitidos se incluyen JPEG y PNG. Se recomienda una resolución de imagen de 128x128.

Por ejemplo:

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[Ejemplo de icono de paquete](https://github.com/NuGet/Samples/tree/master/PackageIconExample).

En el caso del equivalente de nuspec, eche un vistazo a la [referencia de nuspec para el icono](nuspec.md#icon).

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

Cuando se usa `MSBuild -t:pack -p:IncludeSymbols=true`, se copian los archivos `.pdb` correspondientes junto con otros archivos de salida (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Tenga en cuenta que al establecer `IncludeSymbols=true` se crea un paquete estándar *y* un paquete de símbolos.

### <a name="includesource"></a>IncludeSource

Esto equivale a `IncludeSymbols`, salvo que también copia los archivos de código fuente junto con los archivos `.pdb`. Todos los archivos de tipo `Compile` se copian en `src\<ProjectName>\` conservando la estructura de carpetas de ruta de acceso relativa en el paquete resultante. Lo mismo sucede para los archivos de código fuente de cualquier `ProjectReference` en la que `TreatAsPackageReference` se establece en `false`.

Si un archivo de tipo Compile está fuera de la carpeta de proyecto, simplemente se agrega a `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Empaquetado de una expresión de licencia o un archivo de licencia

Cuando se usa una expresión de licencia, se debe usar la propiedad PackageLicenseExpression. 
[Ejemplo de expresión de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[Obtenga más información sobre las expresiones de licencia y las licencias que acepta NuGet.org](nuspec.md#license).

Al empaquetar un archivo de licencia, debe usar la propiedad PackageLicenseFile para especificar la ruta de acceso del paquete, relativa a la raíz del paquete. Además, debe asegurarse de que el archivo está incluido en el paquete. Por ejemplo:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

[Ejemplo de archivo de licencia](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="packing-a-file-without-an-extension"></a>Empaquetado de un archivo sin extensión

En algunos escenarios, como cuando se empaqueta un archivo de licencia, puede que desee incluir un archivo sin una extensión.
Por motivos históricos, NuGet & MSBuild tratan las rutas de acceso sin una extensión como directorios.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Archivo sin un ejemplo de extensión](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).
### <a name="istool"></a>IsTool

Cuando se usa `MSBuild -t:pack -p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`. Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.

### <a name="packing-using-a-nuspec"></a>Empaquetado mediante un archivo .nuspec

Aunque se recomienda [incluir todas las propiedades](../reference/msbuild-targets.md#pack-target) que suelen estar en el archivo `.nuspec` en el archivo del proyecto, puede optar por usar un `.nuspec` archivo para empaquetar el proyecto. Para un proyecto que no sea de estilo SDK que use `PackageReference` , debe importar `NuGet.Build.Tasks.Pack.targets` para que se pueda ejecutar la tarea del paquete. Todavía es necesario restaurar el proyecto para poder empaquetar un archivo nuspec. (Un proyecto de estilo SDK incluye los destinos Pack de forma predeterminada).

El marco de trabajo de destino del archivo de proyecto es irrelevante y no se usa cuando se empaqueta un archivo nuspec. Las tres propiedades de MSBuild siguientes son relevantes para el empaquetado mediante un archivo `.nuspec`:

1. `NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.
1. `NuspecProperties`: lista de pares clave=valor separados por punto y coma. Debido al funcionamiento del análisis de línea de comandos de MSBuild, se deben especificar varias propiedades como se indica a continuación: `-p:NuspecProperties="key1=value1;key2=value2"`.  
1. `NuspecBasePath`: ruta de acceso base para el archivo `.nuspec`.

Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Tenga en cuenta que al empaquetar un nuspec mediante dotnet.exe o MSBuild también se genera el proyecto de forma predeterminada. Esto se puede evitar pasando ```--no-build``` Property a dotnet.exe, que es el equivalente de la configuración ```<NoBuild>true</NoBuild> ``` en el archivo de proyecto, junto con ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` el valor en el archivo de proyecto.

Un ejemplo de un archivo *. csproj* para empaquetar un archivo nuspec es el siguiente:

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

### <a name="advanced-extension-points-to-create-customized-package"></a>Puntos de extensión avanzados para crear un paquete personalizado

El `pack` destino proporciona dos puntos de extensión que se ejecutan en la compilación interna específica de la plataforma de destino. Los puntos de extensión admiten, incluidos los ensamblados y el contenido específico de la plataforma de destino en un paquete:

- `TargetsForTfmSpecificBuildOutput` destino: se usa para los archivos dentro de la `lib` carpeta o en una carpeta especificada mediante `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` destino: se usa para archivos fuera de `BuildOutputTargetFolder` .

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificBuildOutput)` propiedad. En el caso de los archivos que necesiten entrar en `BuildOutputTargetFolder` (de forma predeterminada, lib), el destino debe escribir esos archivos en el ItemGroup `BuildOutputInPackage` y establecer los dos valores de metadatos siguientes:

- `FinalOutputPath`: Ruta de acceso absoluta del archivo; Si no se proporciona, la identidad se utiliza para evaluar la ruta de acceso de origen.
- `TargetPath`: (Opcional) se establece cuando el archivo debe ir a una subcarpeta dentro de `lib\<TargetFramework>` , como los ensamblados satélite que se encuentran bajo sus respectivas carpetas de referencia cultural. Tiene como valor predeterminado el nombre del archivo.

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

Escriba un destino personalizado y especifíquelo como el valor de la `$(TargetsForTfmSpecificContentInPackage)` propiedad. En el caso de los archivos que se van a incluir en el paquete, el destino debe escribir esos archivos en el ItemGroup `TfmSpecificPackageFile` y establecer los metadatos opcionales siguientes:

- `PackagePath`: Ruta de acceso en la que el archivo debe generarse en el paquete. NuGet emite una advertencia si se agrega más de un archivo a la misma ruta de acceso del paquete.
- `BuildAction`: Acción de compilación que se va a asignar al archivo, que solo es necesario si la ruta de acceso del paquete está en la `contentFiles` carpeta. El valor predeterminado es "none".

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

`MSBuild -t:restore` (que `nuget restore` y `dotnet restore` usan con proyectos de .NET Core), restaura los paquetes a los que se hace referencia en el archivo de proyecto como se indica a continuación:

1. Leer todas las referencias entre proyectos
1. Leer las propiedades del proyecto para buscar las carpetas y plataformas de destino intermedias
1. Pasar datos de MSBuild a NuGet.Build.Tasks.dll
1. Ejecutar la restauración
1. Descarga de paquetes
1. Escribir el archivo de activos, destinos y propiedades

El `restore` destino funciona con los proyectos que usan el formato PackageReference.
`MSBuild 16.5+` también tiene [compatibilidad con](#restoring-packagereference-and-packagesconfig-with-msbuild) el `packages.config` formato.

> [!NOTE]
> El `restore` destino [no debe ejecutarse](#restoring-and-building-with-one-msbuild-command) en combinación con el `build` destino.

### <a name="restore-properties"></a>Restaurar las propiedades

Otra configuración de restauración puede proceder de propiedades de MSBuild en el archivo de proyecto. También se pueden establecer valores desde la línea de comandos mediante el modificador `-p:` (vea los ejemplos siguientes).

| Propiedad | Descripción |
|--------|--------|
| RestoreSources | Lista delimitada por punto y coma de orígenes de paquetes. |
| RestorePackagesPath | Ruta de acceso de la carpeta de paquetes de usuario. |
| RestoreDisableParallel | Limitar las descargas a una cada vez. |
| RestoreConfigFile | Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar. |
| RestoreNoCache | Si es true, evita el uso de paquetes almacenados en caché. Consulte [Administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Si es true, ignora los orígenes de paquetes que producen errores o faltan. |
| RestoreFallbackFolders | Carpetas de reserva que se usan de la misma manera que se usa la carpeta de paquetes de usuario. |
| RestoreAdditionalProjectSources | Fuentes adicionales para usar durante la restauración. |
| RestoreAdditionalProjectFallbackFolders | Carpetas de reserva adicionales para usar durante la restauración. |
| RestoreAdditionalProjectFallbackFoldersExcludes | Excluye las carpetas de reserva especificadas en `RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Ruta de acceso a `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas. |
| RestoreUseSkipNonexistentTargets  | Cuando los proyectos se recopilan a través de MSBuild, determina si se recopilan con la `SkipNonexistentTargets` optimización. Cuando no se establece, el valor predeterminado es `true` . La consecuencia es un comportamiento de error rápido cuando no se pueden importar los destinos de un proyecto. |
| MSBuildProjectExtensionsPath | Carpeta de salida, que tiene como valor predeterminado `BaseIntermediateOutputPath` y la `obj` carpeta. |
| RestoreForce | En los proyectos basados en PackageReference, fuerza la resolución de todas las dependencias, incluso si la última restauración se realizó correctamente. Especificar esta marca es similar a eliminar el `project.assets.json` archivo. Esto no omite la memoria caché http. |
| RestorePackagesWithLockFile | Opta por el uso de un archivo de bloqueo. |
| RestoreLockedMode | Ejecutar restauración en modo bloqueado. Esto significa que la restauración no volverá a evaluar las dependencias. |
| NuGetLockFilePath | Una ubicación personalizada para el archivo de bloqueo. La ubicación predeterminada es junto al proyecto y se denomina `packages.lock.json` . |
| RestoreForceEvaluate | Fuerza la restauración para volver a calcular las dependencias y actualizar el archivo de bloqueo sin ninguna advertencia. |
| RestorePackagesConfig | Un modificador opcional, que restaura los proyectos con packages.config. Compatibilidad con `MSBuild -t:restore` solo. |
| RestoreUseStaticGraphEvaluation | Un modificador opcional para usar la evaluación de MSBuild de gráficos estáticos en lugar de la evaluación estándar. La evaluación de gráficos estáticos es una característica experimental que es significativamente más rápida para soluciones y repositorioss de gran tamaño. |

#### <a name="examples"></a>Ejemplos

Línea de comandos:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
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

### <a name="restoring-and-building-with-one-msbuild-command"></a>Restaurar y compilar con un comando de MSBuild

Debido al hecho de que NuGet puede restaurar paquetes que desactivan los destinos y las propiedades de MSBuild, las evaluaciones de la restauración y de la compilación se ejecutan con propiedades globales diferentes.
Esto significa que el siguiente tendrá un comportamiento imprevisible y a menudo incorrecto.

```cli
msbuild -t:restore,build
```

 En su lugar, el enfoque recomendado es:

```cli
msbuild -t:build -restore
```

La misma lógica se aplica a otros destinos similares a `build` .

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a>Restaurar PackageReference y packages.config con MSBuild

Con MSBuild 16,5 +, packages.config también se admiten para `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` restore solo está disponible con `MSBuild 16.5+` , y no con `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Restaurar con la evaluación de gráficos estáticos de MSBuild

> [!NOTE]
> Con MSBuild 16.6 +, NuGet ha agregado una característica experimental para usar la evaluación de gráficos estáticos desde la línea de comandos que mejora significativamente el tiempo de restauración de repositorios grandes.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

También puede habilitarlo estableciendo la propiedad en un directorio. Build. props.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> A partir de Visual Studio 2019. x y NuGet 5. x, esta característica se considera experimental y opcional. Siga [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) para más información sobre cuándo se habilitará esta característica de forma predeterminada.

La restauración de gráficos estáticos cambia la parte de MSBuild de restore, la lectura y evaluación del proyecto, pero no el algoritmo de restauración. El algoritmo restore es el mismo en todas las herramientas de NuGet (NuGet.exe, MSBuild.exe, dotnet.exe y Visual Studio).

En muy pocos escenarios, la restauración de gráficos estáticos puede comportarse de forma diferente a la restauración actual y es posible que falten ciertos PackageReferences declarados o referencias.

Para que le resulte más fácil, como una única comprobación, al migrar a la restauración de gráficos estáticos, considere la posibilidad de ejecutar:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet *no* debe notificar ningún cambio. Si ve una discrepancia, registre un problema en [NuGet/Home](https://github.com/nuget/home/issues/new).

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
