---
title: NuGet empaquetar y restaurar como MSBuild destinos
description: NuGet Pack y restore pueden funcionar directamente como MSBuild destinos con NuGet 4.0+.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067315"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet empaquetar y restaurar como MSBuild destinos

*NuGet 4.0+*

Con el [formato PackageReference,](../consume-packages/package-references-in-project-files.md) 4.0+ puede almacenar todos los metadatos de manifiesto directamente dentro de un archivo de proyecto en lugar de NuGet usar un archivo `.nuspec` independiente.

Con MSBuild 15.1+, también es un ciudadano de primera clase con los destinos NuGet y , como se describe a MSBuild `pack` `restore` continuación. Estos destinos le permiten trabajar con NuGet como lo haría con cualquier otra tarea o MSBuild destino. Para obtener instrucciones sobre NuGet cómo crear un paquete mediante , vea Crear un paquete MSBuild [ NuGet mediante MSBuild ](../create-packages/creating-a-package-msbuild.md). (Para NuGet 3.x y versiones anteriores, use los comandos [pack](../reference/cli-reference/cli-ref-pack.md) y [restore](../reference/cli-reference/cli-ref-restore.md) a través de la NuGet CLI en su lugar).

## <a name="target-build-order"></a>Orden de compilación de destinos

Dado `pack` que y son `restore`  MSBuild destinos, puede acceder a ellos para mejorar el flujo de trabajo. Por ejemplo, supongamos que desea copiar el paquete en un recurso compartido de red después de empaquetarlo. Puede hacer esto si agrega lo siguiente al archivo de proyecto:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

De forma similar, puede escribir una MSBuild tarea, escribir su propio destino y consumir NuGet propiedades en la MSBuild tarea.

> [!NOTE]
> `$(OutputPath)` es relativo y espera que ejecute el comando desde la raíz del proyecto.

## <a name="pack-target"></a>Destino de pack

En el caso de los proyectos de .NET que usan el formato , el uso de dibuja entradas del archivo de proyecto para `PackageReference` `msbuild -t:pack` usarlas en la creación de un NuGet paquete.

En la tabla siguiente se describen MSBuild las propiedades que se pueden agregar a un archivo de proyecto dentro del primer `<PropertyGroup>` nodo. Puede realizar estas modificaciones fácilmente en Visual Studio 2017 y después haciendo clic con el botón derecho en el proyecto y seleccionando **Editar {nombre_proyecto}** en el menú contextual. Para mayor comodidad, la tabla se organiza mediante la propiedad equivalente en un [ `.nuspec` archivo](../reference/nuspec.md).

> [!NOTE]
> `Owners` Las `Summary` propiedades y de no se `.nuspec` admiten con MSBuild .

| nuspecAtributo/valor | PropiedadMSBuild | Default | Notas |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | `$(AssemblyName)` de MSBuild |
| `Version` | `PackageVersion` | Versión | Esto es compatible con semver, por `1.0.0` ejemplo, `1.0.0-beta` , o `1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | vacío | Configuración `PackageVersion` sobrescritura `PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | vacío | `$(VersionSuffix)` de MSBuild . Configuración `PackageVersion` de sobrescrituras `PackageVersionSuffix` |
| `Authors` | `Authors` | Nombre del usuario actual | Lista separada por punto y coma de los autores de paquetes, que coincide con los nombres de perfil en nuget.org. Estos se muestran en la Galería en nuget.org y los mismos autores usan para hacer referencia cruzada NuGet a los paquetes. |
| `Owners` | N/D | No está presente en nuspec | |
| `Title` | `Title` | El `PackageId` | Un título fácil de usar del paquete, que se usa normalmente en las visualizaciones de la interfaz de usuario, como en nuget.org, y el Administrador de paquetes de Visual Studio. |
| `Description` | `Description` | "Descripción del paquete" | Una descripción larga del ensamblado. Si `PackageDescription` no se especifica, esta propiedad también se utiliza como la descripción del paquete. |
| `Copyright` | `Copyright` | vacío | Detalles de copyright del paquete. |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | Un valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo. |
| `license` | `PackageLicenseExpression` | vacío | Se corresponde con `<license type="expression">`. Consulte [Empaquetado de una expresión de licencia o un archivo de licencia.](#packing-a-license-expression-or-a-license-file) |
| `license` | `PackageLicenseFile` | vacío | Ruta de acceso a un archivo de licencia dentro del paquete si usa una licencia personalizada o una licencia a la que no se le ha asignado un identificador SPDX. Debe empaquetar explícitamente el archivo de licencia al que se hace referencia. Se corresponde con `<license type="file">`. Consulte [Empaquetado de una expresión de licencia o un archivo de licencia.](#packing-a-license-expression-or-a-license-file) |
| `LicenseUrl` | `PackageLicenseUrl` | vacío | `PackageLicenseUrl` está desusada. Use `PackageLicenseExpression` o `PackageLicenseFile` en su lugar. |
| `ProjectUrl` | `PackageProjectUrl` | vacío | |
| `Icon` | `PackageIcon` | vacío | Ruta de acceso a una imagen del paquete que se va a usar como icono del paquete. Debe empaquetar explícitamente el archivo de imagen de icono al que se hace referencia. Para obtener más información, vea [Empaquetado de un archivo de imagen de icono y](#packing-an-icon-image-file) [ `icon` metadatos.](./nuspec.md#icon) |
| `IconUrl` | `PackageIconUrl` | vacío | `PackageIconUrl` está en desuso en favor de `PackageIcon` . Sin embargo, para obtener la mejor experiencia de nivel inferior, debe especificar `PackageIconUrl` además de `PackageIcon` . |
| `Readme` | `PackageReadmeFile` | vacío | Debe empaquetar explícitamente el archivo Léame al que se hace referencia.|
| `Tags` | `PackageTags` | vacío | Una lista de etiquetas delimitada por punto y coma que designa el paquete. |
| `ReleaseNotes` | `PackageReleaseNotes` | vacío | Notas de la versión para el paquete. |
| `Repository/Url` | `RepositoryUrl` | vacío | Dirección URL del repositorio que se usa para clonar o recuperar el código fuente. Ejemplo: *https://github.com/ NuGet / NuGet . Client.git*. |
| `Repository/Type` | `RepositoryType` | vacío | Tipo de repositorio. Ejemplos: `git` (valor predeterminado), `tfs` . |
| `Repository/Branch` | `RepositoryBranch` | vacío | Información opcional de la rama del repositorio. `RepositoryUrl` también se debe especificar para que esta propiedad se incluya. Ejemplo: *master* ( NuGet 4.7.0+). |
| `Repository/Commit` | `RepositoryCommit` | vacío | Confirmación o conjunto de cambios opcionales de repositorio para indicar en qué origen se ha compilado el paquete. `RepositoryUrl` también se debe especificar para que esta propiedad se incluya. Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+). |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | Indica el uso previsto del paquete. Los tipos de paquete usan el mismo formato que los identificadores de paquete y están delimitados por `;` . Los tipos de paquetes pueden tener versiones anexando y `,` una [`Version`](/dotnet/api/system.version) cadena. Consulte [Establecer un tipo de NuGet paquete](../create-packages/set-package-type.md) ( NuGet 3.5.0+). |
| `Summary` | No compatible | | |

### <a name="pack-target-inputs"></a>Entradas de destino de pack

| Propiedad | Description |
| - | - |
| `IsPackable` | Un valor booleano que especifica si se puede empaquetar el proyecto. El valor predeterminado es `true`. |
| `SuppressDependenciesWhenPacking` | Establezca en `true` para suprimir las dependencias del paquete NuGet generado. |
| `PackageVersion` | Especifica la versión que tendrá el paquete resultante. Acepta todas las formas de cadena NuGet de versión. El valor predeterminado es `$(Version)`, es decir, de la propiedad `Version` del proyecto. |
| `PackageId` | Especifica el nombre para el paquete resultante. Si no se especifica, la operación `pack` usará de forma predeterminada el elemento `AssemblyName` o el nombre del directorio como el nombre del paquete. |
| `PackageDescription` | Una descripción larga del paquete para su visualización en la interfaz de usuario. |
| `Authors` | Lista separada por punto y coma de los autores de paquetes, que coincide con los nombres de perfil de nuget.org. Estos se muestran en la Galería en nuget.org y se usan para hacer referencia cruzada NuGet a paquetes de los mismos autores. |
| `Description` | Una descripción larga del ensamblado. Si `PackageDescription` no se especifica, esta propiedad también se utiliza como la descripción del paquete. |
| `Copyright` | Detalles de copyright del paquete. |
| `PackageRequireLicenseAcceptance` | Un valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo. De manera predeterminada, es `false`. |
| `DevelopmentDependency` | Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes. Con `PackageReference` ( 4.8+), esta marca también significa que los recursos en tiempo de compilación NuGet se excluyen de la compilación. Para más información, consulte [Compatibilidad de DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference). |
| `PackageLicenseExpression` | Una [expresión o identificador de licencia SPDX,](https://spdx.org/licenses/) por ejemplo, `Apache-2.0` . Para obtener más información, vea [Empaquetado de una expresión de licencia o un archivo de licencia.](#packing-a-license-expression-or-a-license-file) |
| `PackageLicenseFile` | Ruta de acceso a un archivo de licencia dentro del paquete si usa una licencia personalizada o una licencia a la que no se le ha asignado un identificador SPDX. |
| `PackageLicenseUrl` | `PackageLicenseUrl` está desusada. Use `PackageLicenseExpression` o `PackageLicenseFile` en su lugar. |
| `PackageProjectUrl` | |
| `PackageIcon` | Especifica la ruta de acceso del icono del paquete, en relación con la raíz del paquete. Para obtener más información, vea [Empaquetado de un archivo de imagen de icono.](#packing-an-icon-image-file) |
| `PackageReleaseNotes` | Notas de la versión para el paquete. |
| `PackageReadmeFile` | Léame del paquete. |
| `PackageTags` | Una lista de etiquetas delimitada por punto y coma que designa el paquete. |
| `PackageOutputPath` | Determina la ruta de acceso de salida en la que se va a quitar el paquete empaquetado. El valor predeterminado es `$(OutputPath)`. |
| `IncludeSymbols` | Este valor booleano indica si el paquete debe crear un paquete de símbolos adicionales cuando se empaqueta el proyecto. El formato del paquete de símbolos se controla mediante la propiedad `SymbolPackageFormat`. Para obtener más información, [vea IncludeSymbols](#includesymbols). |
| `IncludeSource` | Este valor booleano indica si el proceso de empaquetado debe crear un paquete de origen. El paquete de origen contiene el código fuente de la biblioteca, así como archivos PDB. Los archivos de origen se colocan en el directorio `src/ProjectName`, en el archivo de paquete resultante. Para obtener más información, [vea IncludeSource](#includesource). |
| `PackageType` | |
| `IsTool` | Especifica si se copian todos los archivos de salida en la carpeta *tools* en lugar de la carpeta *lib*. Para obtener más información, [vea IsTool](#istool). |
| `RepositoryUrl` | Dirección URL del repositorio que se usa para clonar o recuperar el código fuente. Ejemplo: *https://github.com/ NuGet / NuGet . Client.git*. |
| `RepositoryType` | Tipo de repositorio. Ejemplos: `git` (valor predeterminado), `tfs` . |
| `RepositoryBranch` | Información opcional de la rama del repositorio. `RepositoryUrl` también se debe especificar para que esta propiedad se incluya. Ejemplo: *master* ( NuGet 4.7.0+). |
| `RepositoryCommit` | Confirmación o conjunto de cambios opcionales de repositorio para indicar en qué origen se ha compilado el paquete. `RepositoryUrl` también se debe especificar para que esta propiedad se incluya. Ejemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+). |
| `SymbolPackageFormat` | Especifica el formato del paquete de símbolos. Si es "symbols.nupkg", se crea un paquete de símbolos heredado con una extensión *.symbols.nupkg* que contiene archivos PDB, DLL y otros archivos de salida. Si es "snupkg", se crea un paquete de símbolos snupkg que contiene los archivos PB portátiles. El valor predeterminado es "symbols.nupkg". |
| `NoPackageAnalysis` | Especifica que no `pack` debe ejecutar el análisis de paquetes después de compilar el paquete. |
| `MinClientVersion` | Especifica la versión mínima del cliente que puede instalar este paquete, aplicada por nuget.exe NuGet y el Visual Studio Administrador de paquetes. |
| `IncludeBuildOutput` | Este valor booleano especifica si se deben empaquetar los ensamblados de salida de la compilación en el archivo *.nupkg* o no. |
| `IncludeContentInPack` | Este valor booleano especifica si los elementos que tienen un tipo de `Content` se incluyen automáticamente en el paquete resultante. El valor predeterminado es `true`. |
| `BuildOutputTargetFolder` | Especifica la carpeta en la que se colocarán los ensamblados de salida. Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco. Para obtener más información, vea [Ensamblados de salida.](#output-assemblies) |
| `ContentTargetFolders` | Especifica la ubicación predeterminada de donde deben ir todos los archivos de contenido si `PackagePath` no se especifica para ellos. El valor predeterminado es “content;contentFiles”. Para obtener más información, consulte [Including content in a package](#including-content-in-a-package) (Incluir contenido en un paquete). |
| `NuspecFile` | Ruta de acceso relativa o absoluta al *.nuspec* archivo que se usa para el empaquetado. Si se especifica, se usa **exclusivamente** para empaquetar información y no se usa ninguna información de los proyectos. Para obtener más información, [vea Empaquetado mediante un .nuspec ](#packing-using-a-nuspec-file). |
| `NuspecBasePath` | Ruta de acceso base para el *.nuspec* archivo. Para obtener más información, [vea Empaquetado mediante un .nuspec ](#packing-using-a-nuspec-file). |
| `NuspecProperties` | Lista separada por punto y coma de pares clave=valor. Para obtener más información, [vea Empaquetado mediante .nuspec ](#packing-using-a-nuspec-file)un . |

## <a name="pack-scenarios"></a>Escenarios de pack

### <a name="suppressing-dependencies"></a>Supresión de dependencias

Para suprimir las dependencias de paquete del paquete generado, establezca en , que permitirá omitir NuGet `SuppressDependenciesWhenPacking` todas las `true` dependencias del archivo nupkg generado.

### `PackageIconUrl`

`PackageIconUrl` está en desuso en favor de la [`PackageIcon`](#packageicon) propiedad . A partir NuGet de la versión 5.3 Visual Studio 2019 16.3, genera la advertencia `pack` [NU5048](./errors-and-warnings/nu5048.md) si los metadatos del paquete solo especifican `PackageIconUrl` .

### `PackageIcon`

> [!Tip]
> Para mantener la compatibilidad con versiones anteriores con clientes y orígenes que aún no admiten `PackageIcon` , especifique `PackageIcon` y `PackageIconUrl` . Visual Studio admite `PackageIcon` paquetes procedentes de un origen basado en carpetas.

#### <a name="packing-an-icon-image-file"></a>Empaquetado de un archivo de imagen de icono

Al empaquetar un archivo de imagen de icono, use la propiedad para especificar la ruta de acceso del archivo de icono, en relación con `PackageIcon` la raíz del paquete. Además, asegúrese de que el archivo está incluido en el paquete. El tamaño del archivo de imagen está limitado a 1 MB. Entre los formatos de archivo admitidos se incluyen JPEG y PNG. Se recomienda una resolución de imagen de 128 x 128.

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

[Ejemplo de icono de paquete](https://github.com/NuGet/Samples/tree/main/PackageIconExample).

Para el nuspec equivalente, echa un vistazo a la [ nuspec referencia del icono](nuspec.md#icon).

### <a name="packagereadmefile"></a>PackageReadmeFile

*Compatible con **NuGet la versión preliminar 5.10.0 2** del SDK de  /  **.NET 5.0.300** y versiones posteriores*

Al empaquetar un archivo Léame, debe usar la propiedad para especificar la ruta de acceso del paquete, en relación con la `PackageReadmeFile` raíz del paquete. Además de esto, debe asegurarse de que el archivo está incluido en el paquete. Los formatos de archivo admitidos incluyen solo Markdown (*.md*).

Por ejemplo:

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

Para el nuspec equivalente, echa un vistazo a [ nuspec la referencia de léame](nuspec.md#readme).

### <a name="output-assemblies"></a>Ensamblados de salida

`nuget pack` copia los archivos de salida con las extensiones `.exe`, `.dll`, `.xml`, `.winmd`, `.json` y `.pri`. Los archivos de salida que se copian dependen de lo MSBuild que proporciona el `BuiltOutputProjectGroup` destino.

Hay dos propiedades que puede usar en el archivo del proyecto o en la línea de comandos MSBuild  para controlar dónde van los ensamblados de salida:

- `IncludeBuildOutput`: un valor booleano que determina si los ensamblados de salida de compilación deben incluirse en el paquete.
- `BuildOutputTargetFolder`: especifica la carpeta en la que se deben colocar los ensamblados de salida. Los ensamblados de salida (y otros archivos de salida) se copian en sus respectivas carpetas de marco.

### <a name="package-references"></a>Referencias de paquete

Vea [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Referencias entre proyectos

Las referencias de proyecto a proyecto se consideran de forma predeterminada como NuGet referencias de paquete. Por ejemplo:

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

Si desea copiar todo el contenido solo en una carpeta raíz específica (en lugar de y en ambas), puede usar la propiedad , que tiene como valor predeterminado `content` `contentFiles` MSBuild "content;contentFiles", pero se puede establecer en cualquier otro nombre de `ContentTargetFolders` carpeta. Tenga en cuenta que si solo especifica "contentFiles" en `ContentTargetFolders`, los archivos se colocan en `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` en función de `buildAction`.

`PackagePath` puede ser un conjunto de rutas de acceso de destino delimitadas por punto y coma. Especificar una ruta de acceso de paquete vacía agregaría el archivo a la raíz del paquete. Por ejemplo, en el ejemplo siguiente se agrega `libuv.txt` a `content\myfiles`, `content\samples` y la raíz del paquete:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

También hay una MSBuild propiedad , que tiene como valor predeterminado `$(IncludeContentInPack)` `true` . Si esto se establece en `false` en cualquier proyecto, el contenido de ese proyecto no se incluye en el paquete NuGet.

Otros metadatos específicos del paquete que se pueden establecer en cualquiera de los elementos anteriores incluyen y qué conjuntos y valores ```<PackageCopyToOutput>``` en la entrada de la ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` nuspec salida.

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

Cuando use una expresión de licencia, use la `PackageLicenseExpression` propiedad . Para obtener un ejemplo, vea [Ejemplo de expresión de licencia](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Para más información sobre las expresiones de licencia y las licencias aceptadas por NuGet .org, consulte metadatos [de licencia.](nuspec.md#license)

Al empaquetar un archivo de licencia, use `PackageLicenseFile` la propiedad para especificar la ruta de acceso del paquete, en relación con la raíz del paquete. Además, asegúrese de que el archivo está incluido en el paquete. Por ejemplo:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Para obtener un ejemplo, vea [Ejemplo de archivo de licencia](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).

> [!NOTE]
> Solo se `PackageLicenseExpression` puede especificar uno de , y a la `PackageLicenseFile` `PackageLicenseUrl` vez.

### <a name="packing-a-file-without-an-extension"></a>Empaquetado de un archivo sin una extensión

En algunos escenarios, como al empaquetar un archivo de licencia, es posible que quiera incluir un archivo sin una extensión.
Por motivos históricos, NuGet  &  MSBuild trate las rutas de acceso sin una extensión como directorios.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Archivo sin un ejemplo de extensión](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).

### <a name="istool"></a>IsTool

Cuando se usa `MSBuild -t:pack -p:IsTool=true`, todos los archivos de salida, como se especifica en el escenario [Ensamblados de salida](#output-assemblies), se copian en la carpeta `tools` en lugar de la carpeta `lib`. Tenga en cuenta que esto es diferente de `DotNetCliTool`, que se especifica estableciendo `PackageType` en el archivo `.csproj`.

### <a name="packing-using-a-nuspec-file"></a>Empaquetado mediante un `.nuspec` archivo

Aunque se recomienda [](../reference/msbuild-targets.md#pack-target) incluir todas las propiedades que normalmente se encuentran en el archivo en el archivo de proyecto, puede optar por usar un archivo para `.nuspec` `.nuspec` empaquetar el proyecto. Para un proyecto que no sea de estilo SDK que use , debe importar para que se pueda ejecutar la tarea de `PackageReference` `NuGet.Build.Tasks.Pack.targets` paquete. Debe restaurar el proyecto para poder empaquetar un nuspec archivo. (Un proyecto de estilo SDK incluye los destinos del paquete de forma predeterminada).

La plataforma de destino del archivo de proyecto es irrelevante y no se usa al empaquetar nuspec un . Las tres propiedades MSBuild siguientes son relevantes para el empaquetado mediante `.nuspec` :

1. `NuspecFile`: ruta de acceso relativa o absoluta al archivo `.nuspec` que se usa para el empaquetado.
1. `NuspecProperties`: lista de pares clave=valor separados por punto y coma. Debido a la forma en que funciona el análisis de la línea de comandos, se deben especificar varias propiedades como MSBuild se indica a continuación: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: ruta de acceso base para el archivo `.nuspec`.

Si se usa `dotnet.exe` para empaquetar el proyecto, use un comando similar al siguiente:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Si se usa MSBuild para empaquetar el proyecto, use un comando similar al siguiente:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Tenga en cuenta que el empaquetado de un dotnet.exe o msbuild también conduce a nuspec la creación del proyecto de forma predeterminada. Esto se puede evitar pasando la propiedad a dotnet.exe, que es el equivalente de establecer en el archivo de proyecto, junto con la configuración ```--no-build``` en el archivo del ```<NoBuild>true</NoBuild> ``` ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` proyecto.

Un ejemplo de un *archivo .csproj* para empaquetar un nuspec archivo es:

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

El `pack` destino proporciona dos puntos de extensión que se ejecutan en la compilación interna específica del marco de destino. Los puntos de extensión admiten la inclusión de ensamblados y contenido específicos de la plataforma de destino en un paquete:

- `TargetsForTfmSpecificBuildOutput` target: se usa para los archivos dentro `lib` de la carpeta o una carpeta especificada mediante `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` target: se usa para archivos fuera de `BuildOutputTargetFolder` .

#### `TargetsForTfmSpecificBuildOutput`

Escribir un destino personalizado y especificarlo como el valor de la `$(TargetsForTfmSpecificBuildOutput)` propiedad . En el caso de los archivos que necesiten entrar en (lib de forma predeterminada), el destino debe escribir esos archivos en ItemGroup y establecer los dos valores de metadatos `BuildOutputTargetFolder` `BuildOutputInPackage` siguientes:

- `FinalOutputPath`: ruta de acceso absoluta del archivo; Si no se proporciona, la identidad se usa para evaluar la ruta de acceso de origen.
- `TargetPath`: (Opcional) Se establece cuando el archivo debe ir a una subcarpeta dentro de , como los ensamblados satélite que van bajo `lib\<TargetFramework>` sus respectivas carpetas de referencia cultural. El valor predeterminado es el nombre del archivo.

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

#### `TargetsForTfmSpecificContentInPackage`

Escribir un destino personalizado y especificarlo como el valor de la `$(TargetsForTfmSpecificContentInPackage)` propiedad . Para que los archivos se incluyan en el paquete, el destino debe escribir esos archivos en ItemGroup y `TfmSpecificPackageFile` establecer los siguientes metadatos opcionales:

- `PackagePath`: ruta de acceso donde se debe generar el archivo en el paquete. NuGet emite una advertencia si se agrega más de un archivo a la misma ruta de acceso del paquete.
- `BuildAction`: la acción de compilación que se va a asignar al archivo, solo es necesaria si la ruta de acceso del paquete está en la `contentFiles` carpeta . El valor predeterminado es "None".

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
1. Pasar MSBuild datos a NuGet.Build.Tasks.dll
1. Ejecutar la restauración
1. Descarga de paquetes
1. Escribir el archivo de activos, destinos y propiedades

El `restore` destino funciona para proyectos con el formato PackageReference.
`MSBuild 16.5+` también tiene [compatibilidad de opt-in](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) con el `packages.config` formato.

> [!NOTE]
> El `restore` destino no debe [ejecutarse](#restoring-and-building-with-one-msbuild-command) en combinación con el `build` destino.

### <a name="restore-properties"></a>Restaurar las propiedades

La configuración de restauración adicional puede procede de MSBuild las propiedades del archivo del proyecto. También se pueden establecer valores desde la línea de comandos mediante el modificador `-p:` (vea los ejemplos siguientes).

| Propiedad | Description |
|--------|--------|
| `RestoreSources` | Lista delimitada por punto y coma de orígenes de paquetes. |
| `RestorePackagesPath` | Ruta de acceso de la carpeta de paquetes de usuario. |
| `RestoreDisableParallel` | Limitar las descargas a una cada vez. |
| `RestoreConfigFile` | Ruta de acceso a un archivo `Nuget.Config` que se va a aplicar. |
| `RestoreNoCache` | Si es true, evita el uso de paquetes almacenados en caché. Consulte [Administración de paquetes globales y carpetas de caché.](../consume-packages/managing-the-global-packages-and-cache-folders.md) |
| `RestoreIgnoreFailedSources` | Si es true, ignora los orígenes de paquetes que producen errores o faltan. |
| `RestoreFallbackFolders` | Carpetas de reserva, que se usan de la misma manera que se usa la carpeta de paquetes de usuario. |
| `RestoreAdditionalProjectSources` | Orígenes adicionales que se usarán durante la restauración. |
| `RestoreAdditionalProjectFallbackFolders` | Carpetas de reserva adicionales que se usarán durante la restauración. |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | Excluye las carpetas de reserva especificadas en `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | Ruta de acceso a `NuGet.Build.Tasks.dll`. |
| `RestoreGraphProjectInput` | Lista delimitada por punto y coma de proyectos para restaurar, que debe contener rutas de acceso absolutas. |
| `RestoreUseSkipNonexistentTargets`  | Cuando los proyectos se recopilan MSBuild a través de , determina si se recopilan mediante la `SkipNonexistentTargets` optimización. Cuando no se establece, el valor predeterminado es `true` . La consecuencia es un comportamiento de error rápido cuando no se pueden importar los destinos de un proyecto. |
| `MSBuildProjectExtensionsPath` | Carpeta de salida, con el valor predeterminado `BaseIntermediateOutputPath` y la `obj` carpeta . |
| `RestoreForce` | En los proyectos basados en PackageReference, fuerza que todas las dependencias se resuelvan incluso si la última restauración se ha realizado correctamente. Especificar esta marca es similar a eliminar el `project.assets.json` archivo. Esto no omite http-cache. |
| `RestorePackagesWithLockFile` | Opta por el uso de un archivo de bloqueo. |
| `RestoreLockedMode` | Ejecute la restauración en modo bloqueado. Esto significa que la restauración no volverá a evaluar las dependencias. |
| `NuGetLockFilePath` | Ubicación personalizada para el archivo de bloqueo. La ubicación predeterminada está junto al proyecto y se denomina `packages.lock.json` . |
| `RestoreForceEvaluate` | Obliga a la restauración a volver a compilar las dependencias y actualizar el archivo de bloqueo sin ninguna advertencia. |
| `RestorePackagesConfig` | Un modificador de suscripción que restaura los proyectos con packages.config. Compatibilidad solo `MSBuild -t:restore` con . |
| `RestoreUseStaticGraphEvaluation` | Un modificador opt-in para usar la evaluación de MSBuild grafos estáticos en lugar de la evaluación estándar. La evaluación de grafos estáticos es una característica experimental que es significativamente más rápida para grandes repositorios y soluciones. |

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
| `{projectName}.projectFileExtension.nuget.g.props` | Referencias a MSBuild propiedades contenidas en paquetes |
| `{projectName}.projectFileExtension.nuget.g.targets` | Referencias a MSBuild destinos contenidos en paquetes |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Restauración y creación con un MSBuild comando

Debido al hecho de que puede restaurar paquetes que desanuren destinos y propiedades, las evaluaciones de restauración y compilación se ejecutan NuGet MSBuild con diferentes propiedades globales.
Esto significa que lo siguiente tendrá un comportamiento imprevisible y, a menudo, incorrecto.

```cli
msbuild -t:restore,build
```

 En su lugar, el enfoque recomendado es:

```cli
msbuild -t:build -restore
```

La misma lógica se aplica a otros destinos similares a `build` .

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>Restaurar PackageReference y packages.config proyectos con MSBuild

Con MSBuild las versiones 16.5 y posteriores, packages.config también se admiten para `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` restore solo está disponible con `MSBuild 16.5+` y no con `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Restauración con evaluación MSBuild de grafos estáticos

> [!NOTE]
> Con MSBuild 16.6+, ha agregado una característica experimental para usar la evaluación de grafos estáticos desde la línea de comandos que mejora significativamente el tiempo de restauración para repositorios NuGet grandes.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

También puede habilitarla estableciendo la propiedad en Directory.Build.Props.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> A partir Visual Studio 2019.x y 5.x, esta característica se considera NuGet experimental y opt-in. Siga [ NuGet /Home#9803](https://github.com/NuGet/Home/issues/9803) para obtener más información sobre cuándo se habilitará esta característica de forma predeterminada.

La restauración de grafos estáticos cambia la parte de msbuild de la restauración, la lectura y evaluación del proyecto, pero no el algoritmo de restauración. El algoritmo de restauración es el mismo en todas las NuGet herramientas NuGet (.exe, MSBuild .exe, dotnet.exe y Visual Studio).

En muy pocos escenarios, la restauración de grafos estáticos puede comportarse de forma diferente a la restauración actual y es posible que falte ciertas packageReferences o ProjectReferences declaradas.

Para facilitar la mente, como una comprobación única, al migrar a la restauración de grafos estáticos, considere la posibilidad de ejecutar:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet no *debe notificar* ningún cambio. Si ve una discrepancia, envíe un problema a [ NuGet /Home.](https://github.com/nuget/home/issues/new)

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
