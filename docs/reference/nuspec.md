---
title: Referencia del archivo. nuspec para NuGet
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 5b9be55b593890127d8fe0ad1a9357b89527a09a
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433372"
---
# <a name="nuspec-reference"></a>Referencia de .nuspec

Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete. Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores. El manifiesto siempre se incluye en un paquete.

En este tema:

- [Esquema y forma general](#general-form-and-schema)
- [Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)
- [Dependencias](#dependencies)
- [Referencias de ensamblado explícitas](#explicit-assembly-references)
- [Referencias de ensamblado de plataforma](#framework-assembly-references)
- [Incluir archivos de ensamblado](#including-assembly-files)
- [Incluir archivos de contenido](#including-content-files)
- [Archivos nuspec de ejemplo](#example-nuspec-files)

## <a name="project-type-compatibility"></a>Compatibilidad de tipos de proyecto

- Use `.nuspec` `packages.config`con `nuget.exe pack` para proyectos que no son de estilo SDK que usan.

- No `.nuspec` es necesario que un archivo cree paquetes para los [proyectos de estilo SDK](../resources/check-project-format.md) (normalmente, los proyectos de .net Core y .net Standard que usan el [atributo SDK](/dotnet/core/tools/csproj#additions)). (Tenga en cuenta `.nuspec` que se genera cuando se crea el paquete).

   Si va a crear un paquete mediante `dotnet.exe pack` o `msbuild pack target`, le recomendamos que incluya en su lugar [todas las propiedades](../reference/msbuild-targets.md#pack-target) que suelen `.nuspec` estar en el archivo en el archivo del proyecto. Sin embargo, en su lugar, puede elegir [usar `.nuspec` un archivo para empaquetar `msbuild pack target`con `dotnet.exe` o ](../reference/msbuild-targets.md#packing-using-a-nuspec).

- En el caso de los `packages.config` proyectos migrados de `.nuspec` a [PackageReference](../consume-packages/package-references-in-project-files.md), no es necesario un archivo para crear el paquete. En su lugar, use [msbuild-t:Pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

## <a name="general-form-and-schema"></a>Esquema y forma general

El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

En este esquema, los archivos `.nuspec` tienen el siguiente formato general:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**. Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**. En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>Elementos de metadatos necesarios

Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete. 

Estos elementos deben aparecer dentro de un elemento `<metadata>`.

#### <a name="id"></a>id 
El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete. Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET. Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones.
#### <a name="version"></a>version
La versión del paquete, siguiendo el patrón *mayor.menor.revisión*. Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../reference/package-versioning.md#pre-release-versions). 
#### <a name="description"></a>description
Una descripción larga del paquete para su visualización en la interfaz de usuario. 
#### <a name="authors"></a>authors
Una lista separada por comas de los autores de los paquetes, que coinciden con los nombres de perfil de nuget.org. Estos se muestran en la galería de NuGet, en nuget.org, y se usan para hacer referencias cruzadas a paquetes de los mismos autores. 

### <a name="optional-metadata-elements"></a>Elementos de metadatos opcionales

#### <a name="owners"></a>owners
Lista separada por comas de los creadores del paquete usando nombres de perfil en nuget.org. Suele ser la misma lista que en `authors` y se ignora al cargar el paquete en nuget.org. Vea [Administrar los propietarios de paquetes en nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg). 

#### <a name="projecturl"></a>projectUrl
Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org. 

#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl está en desuso. Use la licencia en su lugar.

Una dirección URL para la licencia del paquete, que a menudo se muestra en ius como nuget.org.

#### <a name="license"></a>Sin
Una expresión de licencia de SPDX o una ruta de acceso a un archivo de licencia dentro del paquete, que a menudo se muestra en ius como nuget.org. Si tiene licencia para el paquete con una licencia común, como MIT o la cláusula BSD-2, use el identificador de [licencia de SPDX](https://spdx.org/licenses/)asociado. Por ejemplo:

`<license type="expression">MIT</license>`

> [!Note]
> NuGet.org solo acepta expresiones de licencia aprobadas por la iniciativa de código abierto o la Fundación gratuita de software.

Si el paquete tiene licencia con varias licencias comunes, puede especificar una licencia compuesta mediante la [Sintaxis de expresión SPDX versión 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60). Por ejemplo:

`<license type="expression">BSD-2-Clause OR MIT</license>`

Si usa una licencia personalizada que no es compatible con las expresiones de licencia, puede empaquetar `.md` un `.txt` archivo o con el texto de la licencia. Por ejemplo:

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

En el caso del equivalente de MSBuild, eche un vistazo a [empaquetar una expresión de licencia o un archivo de licencia](msbuild-targets.md#packing-a-license-expression-or-a-license-file).

A continuación se describe la sintaxis exacta de las expresiones de licencia de NuGet en [ABNF](https://tools.ietf.org/html/rfc5234).
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl
Dirección URL para una imagen de 64 x 64 con fondo transparente para usarla como icono para el paquete en la visualización de la interfaz de usuario. Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen. Por ejemplo, para usar una imagen de GitHub, use la dirección URL de archivo <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>sin formato como. 

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo.

#### <a name="developmentdependency"></a>developmentDependency
*(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes. Con PackageReference (NuGet 4.8 +), esta marca también significa que excluirá los recursos en tiempo de compilación de la compilación. Consulte [compatibilidad con DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)

#### <a name="summary"></a>resumen
Descripción breve del paquete para su visualización en la interfaz de usuario. Si se omite, se usará una versión truncada de `description`.

#### <a name="releasenotes"></a>releaseNotes
*(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete.

#### <a name="copyright"></a>copyright
*(1.5+)* Información de copyright del paquete.

#### <a name="language"></a>language
Identificador de configuración regional del paquete. Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md).

#### <a name="tags"></a>tags
Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados. 

#### <a name="serviceable"></a>reparables por 
*(3.3+)* Solo para uso interno de NuGet.

#### <a name="repository"></a>repository
Metadatos del repositorio, que constan de cuatro `type` atributos `url` opcionales: y *(4.0 +)* , y `branch` y `commit` *(4.6 +)* . Estos atributos permiten asignar el `.nupkg` al repositorio que lo compiló, con la posibilidad de obtener el valor que se obtiene como el nombre de la rama individual o el hash de SHA-1 de confirmación que compiló el paquete. Debe ser una dirección URL disponible públicamente que un software de control de versiones pueda invocar directamente. No debe ser una página HTML, ya que está destinada al equipo. Para vincular a la página del proyecto `projectUrl` , use el campo en su lugar.

Por ejemplo:
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="minclientversion"></a>minClientVersion
Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio. Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet. Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`. Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3". Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`.

#### <a name="title"></a>title
Título descriptivo del paquete que se puede usar en algunas pantallas de la interfaz de usuario. (nuget.org y el administrador de paquetes en Visual Studio no muestran el título)

#### <a name="collection-elements"></a>Elementos de colección

#### <a name="packagetypes"></a>Elemento packagetypes
*(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional. Cada tipo de paquete tiene atributos de *name* y *version*. Vea [Establecimiento de un tipo de paquete](../create-packages/set-package-type.md).
#### <a name="dependencies"></a>dependencias
Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete. Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+). Vea [Dependencias](#dependencies-element) a continuación.
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete. Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*. Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación. |
#### <a name="references"></a>referencias
*(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto. Cada referencia tiene un atributo *file*. `<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`. Si se omite, se incluyen todas las referencias de `lib`. Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación.
#### <a name="contentfiles"></a>contentFiles
*(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo. Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto. Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación.
#### <a name="files"></a>files 
El `<package>` nodo puede contener un `<files>` `<metadata>`nodo como un elemento relacionado y un `<contentFiles>` elemento secundario en `<metadata>`, para especificar qué archivos de ensamblado y de contenido se van a incluir en el paquete. Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.

## <a name="replacement-tokens"></a>Tokens de reemplazo

Al crear un paquete, el [comando `nuget pack`](../reference/cli-reference/cli-ref-pack.md) reemplaza los tokens delimitados por $ en el nodo `<metadata>` del archivo `.nuspec` por valores procedentes de un archivo de proyecto o del conmutador `-properties` del comando `pack`.

En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`. Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).

Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`. Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:

```ps
nuget pack MyProject.csproj
```

Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares. Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`. Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.

Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.

| Token | Origen del valor | Valor
| --- | --- | ---
| **$id$** | Archivo del proyecto | AssemblyName (title) del archivo de proyecto |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Archivo DLL del ensamblado | Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar. Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos. |

Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files). Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual. Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Elemento Dependencies

El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior. Los atributos de cada `<dependency>` son los siguientes:

| Atributo | DESCRIPCIÓN |
| --- | --- |
| `id` | (Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete. |
| `version` | (Obligatorio) Intervalo de versiones aceptable como dependencia. Vea [Control de versiones de paquetes](../reference/package-versioning.md#version-ranges-and-wildcards) para consultar la sintaxis exacta. |
| include | Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final. El valor predeterminado es `all`. |
| exclude | Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final. El valor predeterminado es `build,analyzers` que se puede sobrescribir. Pero `content/ ContentFiles` también se excluyen implícitamente en el paquete final que no se puede sobrescribir. Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`. Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`. |

| Etiqueta Include o Exclude | Carpetas afectadas del destino |
| --- | --- |
| contentFiles | Contenido |
| motor en tiempo de ejecución | Runtime, Resources y FrameworkAssemblies |
| compile | lib |
| compilación | build (propiedades y destinos de MSBuild) |
| nativas | nativas |
| ninguna | Sin carpetas |
| todo | Todas las carpetas |

Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Nota: Al crear un `.nuspec` a partir de un `nuget spec`proyecto mediante, las dependencias que existen en ese proyecto se incluyen automáticamente `.nuspec` en el archivo resultante.

### <a name="dependency-groups"></a>Grupos de dependencia

*Versión 2.0+*

Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.

Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`. Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.

El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias. Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.

> [!Important]
> El formato del grupo no se puede combinar con una lista plana.

En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Referencias de ensamblado explícitas

`<references>` Los`packages.config` proyectos utilizan el elemento para especificar explícitamente los ensamblados a los que debe hacer referencia el proyecto de destino al utilizar el paquete. Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño. Para obtener más información, vea la página de selección de ensamblados a los [que se hace referencia en proyectos](../create-packages/select-assemblies-referenced-by-projects.md) .

Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a>Grupos de referencias

Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.

Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`. Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.

El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias. Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.

> [!Important]
> El formato del grupo no se puede combinar con una lista plana.

En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Referencias de ensamblado de plataforma

Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo. Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias. Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.

El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:

| Atributo | DESCRIPCIÓN |
| --- | --- |
| **assemblyName** | (Obligatorio) Nombre completo del ensamblado. |
| **targetFramework** | (Opcional) Especifica la plataforma de destino a la que se aplica esta referencia. Si se omite, indica que la referencia se aplica a todas las plataformas. Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos. |

En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Incluir archivos de ensamblado

Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`. El comando `nuget pack` selecciona automáticamente los archivos necesarios.

> [!Important]
> Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados. Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.

Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente. Por ejemplo:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete. Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar. Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.

### <a name="file-element-attributes"></a>Atributos del elemento File

Cada elemento `<file>` especifica los siguientes atributos:

| Atributo | DESCRIPCIÓN |
| --- | --- |
| **src** | Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`. La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta. El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva. |
| **target** | La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`. Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones). |
| **exclude** | Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`. El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva. |

### <a name="examples"></a>Ejemplos

**Ensamblado único**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Ensamblado único específico para una plataforma de destino**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Conjunto de archivos DLL que usan un carácter comodín**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**Archivos DLL para distintas plataformas**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Archivos de exclusión**

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>Incluir archivos de contenido

Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto. Como son inmutables, no se prevé que el proyecto de consumo los modifique. Entre los archivos de contenido se encuentran los siguientes:

- Imágenes que se insertan como recursos
- Archivos de código fuente que ya están compilados
- Scripts que se deben incluir con la salida de la compilación del proyecto
- Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto

Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`. Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.

Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.

### <a name="using-the-files-element-for-content-files"></a>Usar el elemento files para los archivos de contenido

En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.

**Archivos de contenido básicos**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Archivos de contenido con estructura de directorios**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**Archivo de contenido específico para una plataforma de destino**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Archivo de contenido copiado en una carpeta con un punto en el nombre**

En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Archivos de contenido sin extensión**

Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Archivos de contenido con una ruta de acceso y un destino profundos**

En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Cambiar el nombre de un archivo de contenido del paquete**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Archivos de exclusión**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Usar el elemento contentFiles para los archivos de contenido

*NuGet 4.0 + con PackageReference*

De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados. En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.

Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.

Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:

| Atributo | DESCRIPCIÓN |
| --- | --- |
| **include** | (Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`. La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta. El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva. |
| **exclude** | Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`. El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva. |
| **buildAction** | Acción de compilación que se debe asignar al elemento de contenido para MSBuild, como `Content`, `None`, `Embedded Resource`, `Compile`, etc. El valor predeterminado es `Compile`. |
| **copyToOutput** | Un valor booleano que indica si se deben copiar los elementos de contenido en la carpeta de salida de compilación (o publicación). El valor predeterminado es false. |
| **flatten** | Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false). Esta marca solo funciona cuando la marca copyToOutput está establecida en true. El valor predeterminado es false. |

Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo. Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas. La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.

#### <a name="package-folder-structure"></a>Estructura de carpetas de los paquetes

El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.
- `TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).
- Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.

Por ejemplo:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Sección contentFiles de ejemplo

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a>Archivos nuspec de ejemplo

**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**Un archivo `.nuspec` con dependencias**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**Un archivo `.nuspec` con archivos**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**Un archivo `.nuspec` con ensamblados de plataforma**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:

- .NET4 -> `System.Web`, `System.Net`
- .NET4 Client Profile -> `System.Net`
- Silverlight 3 -> `System.Json`
- Windows Phone -> `Microsoft.Devices.Sensors`
